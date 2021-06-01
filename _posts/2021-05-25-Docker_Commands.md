---

- docker run
  : 컨테이너를 만들고 실행하는 명령어

    - -i  (= -interactive) : STDIN(표준 입력)을 받을 수 있게 해준다.
    - -t (= -tty) : Psuedo-tty를 배정해준다.
        - Psuedo-tty: 네트워크를 통해 시스템에 원격접속 했을 때 열리는 터미널
        - 따라서 -it를 같이 사용하면 표준입력을 받을 수 있는 원격 터미널을 컨테이너 안에서 사용할 수 있다.
    - -p : 컨테이너 포트를 설정한다.

        ```shell
        docker run -p ${HOST_PORT} : ${CONTAINER_PORT} ubuntu:14.04
        ```

    - -d (= -detach) : 컨테이너를 detach하여 백그라운드에 돌아가는 프로그램으로 실행한다.
      
        - 만약 컨테이너 내에 포어그라운드로 돌아갈 프로그램이 설정되어 있지 않다면 -d 로 docker run을 한 순간 컨테이너가 종료된다.
    - -e (= --env) : 컨테이너의 환경변수를 설정한다.
    - -v (= --volume) : 볼륨 컨테이너 설정
      : 컨테이너의 데이터베이스 등을 백업해놓을 수 있도록 함
        - 호스트 볼륨을 도커 볼륨에 마운트

        ```shell
        docker volume -v ${HOST_DIRECTORY} : ${CONTAINER_DIRECTORY} ubuntu:14.04
        ```

        - 도커 볼륨 생성

        ```shell
        docker volume -v ${VOLUME_NAME} : ${CONTAINER_DIRECTORY} ubuntu:14.04
        ```

    - --log-opt : 로그 옵션 설정 가능
        - max-size
        - max-file

- docker logs
  : 컨테이너의 모든 표준출력과 에러 로그를 확인 가능한 명령어
    - 컨테이너 로그는 보통 JSON 형태로 컨테이너 내에 저장된다. 밑의 명령어로 확인 가능.

        ```shell
        cat /var/lib/docker/containers/${CONTAINER_ID}/${CONTAINER_ID}-json.log
        ```

    - --tail : 뒤의 몇 줄만 출력 가능

        ```shell
        docker logs --tail 2 ${CONTAINER_NAME}
        ```

    - --since : 특정 유닉스 시간 이후의 로그만 출력 가능

        ```shell
        docker logs --since 147454594 ${CONTAINER_NAME}
        ```

    - -t : 로그에  타임스탬프 출력 가능
    - -f : 로그를 스트림으로 확인
      
        - ctrl + c로 탈출 가능

- docker stop
: 실행중인 컨테이너를 정지하는 명령어

    ```shell
    docker stop ${CONTAINER_NAME}
    ```

- docker rm
  : 컨테이너를 삭제하는 명령어. 보통 정지된 컨테이너만 삭제 가능

    - -f (= --force) : 강제 삭제. 실행중인 컨테이너도 삭제 가능

- docker ps
  : 실행중인 컨테이너 목록을 불러오는 명령어

    - -a : 정지 중인 컨테이너까지 모든 컨테이너 목록을 불러옴
    - -q : 컨테이너의 아이디만 반환

- docker network
: 컨테이너용 네트워크를 핸들링
    - create : 네트워크 생성
        - --driver : 드라이버 타입 설정
        - --subnet : 서브넷 설정
        - --ip-range : IP 할당 범위 설정
        - --gateway : 게이트웨이 설정