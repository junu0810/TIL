Nginx를 사용하다보면 Redirect와 Rewrite로 화면을 출력해야할 경우가 온다.

오늘은 배포간 사용했던 redirect와 rewrite에 대해 정리해보고자 한다.

### 1. Redirect
```nginx
location /nginx {
  return 200 "nginx"
}
```
- String같은 정적데이터를 return하여 표시하고 싶으면 위의 방법을 사용하면 된다.
- [200]은 HTTP status를 표시해주는 방법입니다. 
- 만약 정적이 아닌 화면으로 Redirect하고 싶은경우 [200]이 아닌 [307]과 같은 30x대 HTTP_status를 작성하면 된다.

<br> 

```nginx
location /static {
  return 307 /static_Data.jpg
}
```
- static_Data.jpg는 정적파일로 nginx안에 root의 하위에 존재하는 파일이다 (EX. root /var/www/html/ ) 
- 그럼 URL에 "URL/파일명" 의 형식으로 표시되고 화면에 출력된다.
<img width="507" alt="image" src="https://user-images.githubusercontent.com/89199949/212471066-0b410121-7acc-44e0-b85a-cb54a633136e.png">


#### 여기서 생각이 들었다. 사용자가 데이터의 파일명이나 형식에대해 알게되는게 관연 정상적인 방법일까?
아래의 rewrite 방식으로 해결이 가능한 부분이다.
### 2. Rewrite
```nginx
rewrite ^/?$ /static_Data.jpg
```
- 위의 방법을 사용하면 "/"에 대한 모든 요청은 /static_Data.jpg 데이터를 불러오는 요청으로 바뀌게 된다.
- 유저에게도 파일명이 안보이고 "/"요청만 보일 뿐이다.

<br>

```nginx
rewrite ^/test/(\w+) /nginx/$1;

location /nginx {
         return 200 "Hello nginx";
}

location = /nginx/baek {
         return 200 "Hello baek";
}
```
- '/test/..' 요청이 들어올경우 nginx에서 /nginx의 location으로 분기처리됩니다.
- '/test/baek/를 호출하면 $1부분에서 값을 인식하여 '/nginx/baek'로 location을 분기처리하여 처리됩니다.
- '/test/apache/'를 호출하게 되면 $1부분이 인식은 하지만 일치되는 부분이 없기 때문에 '/nginx'로 분기처리 됩니다.
