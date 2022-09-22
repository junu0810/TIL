```
case $1 in
    start)
        var1=$(ps -ef | grep 'java');
        echo process info :: ${var1}

        get_pid=$(echo ${var1} | cut -d " " -f2);

        if [ -n "${get_pid}" ];
        then 
            result1=$(kill -9 ${get_pid})
            echo process is Down
            nohup sudo java -jar study-definition-repository-0.0.1-SNAPSHOT.jar &
            echo running process
        fi
    ;;
esac
```

### 파일명.sh satrt 를 하면 기존서버가 꺼지고 새롭게 배포를 시행한다.
