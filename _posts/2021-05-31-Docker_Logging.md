---

- 도커의 컨테이너 로그는 보통 JSON 형태로 컨테이너 내에 저장된다. 밑의 명령어로 확인 가능.

    ```jsx
    # cat /var/lib/docker/containers/${CONTAINER_ID}/${CONTAINER_ID}-json.log
    ```

### Log driver

- 다양한 로그 드라이버를 사용할 수 있다. Default는 json

```bash
docker run --log-driver ${DRIVER_TYPE}
```

- syslog / rsyslog
    - 유닉스 OS의 오래된 표준 로그 드라이버
    - udp, tcp 둘 다 가능
    - 사용시에 컨테이너 내 /etc/rsyslog.conf 에서 udp, tcp syslog reception 부분을 활성화 해줘야 함
- fluentd
    - 각종 로그 수집 & 저장 오픈소스 툴
    - 도커 컨테이너 로그 저장 플러그인 제공
- Amazon Cloudwatch
    - AWS 내에서 로그 스트림 확인 가능