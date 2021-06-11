

- 여러 개의 컨테이너가 하나의 어플리케이션으로 동작하는 경우, 이를 테스트하기 위해서는 매번 RUN에 옵션을 달고 여러개를 실행하기가 번거로움
- 따라서 여러개의 컨테이너를 하나의 프로젝트로 다룰 수 있도록 하는 것이 docker compose
- 컴포즈를 생성하기 위해 YAML 파일 작성 필요
- 구조:
    - 프로젝트 → 서비스 → 컨테이너
    
      

##### Commands

---

- up: docker-compose yml 파일에 따라 compose 생성
    - -f : yml 파일의 위치와 이름 지정. default는 ./docker-compose.yml
    
- scale: 기존에 있던 서비스의 컨테이너의 개수를 변경

    ```bash
    docker-compose scale <SERVICE_NAME>=<CONTAINER_COUNT>
    ```

- down: 생성된 프로젝트 삭제

- config : YAML 파일의 포맷 및 오타 적합성 검사

    

##### YAML 파일

---

- version : 버전 정의
    - 가장 상단에 명시
- services : 서비스 정의

    ```yaml
    services:
    	<SERVICE_NAME_1>:
    		image: ...
    	<SERVICE_NAME_2>:
    		image: ...
    ```

    - image : 서비스 컨테이너 생성시 사용할 이미지
    - links : 다른 서비스에 서비스명만으로 접근할 수 있도록 함. [SERVICE:ALIAS] 형식으로 작성하면 별칭으로도 접근할 수 있음
    - environment : 환경변수 지정
    - command : 컨테이너 실행시 수행할 명령어 지정
    - depends_on : 특정 컨테이너에 대한 의존 관계 지정. 지정한 컨테이너가 먼저 생성되고 이후에 실행됨.
        - cf) --no-deps : 특정 서비스의 컨테이너만 생성하되 의존성을 두고 싶지 않을 때 사용
    - ports : 컨테이너 개방 포트 지정
    - build : 컨테이너를 생성할 도커파일 지정. 이후에 도커파일이 변경되도 이미지를 새로 빌드하지는 않음
        - docker-compose up -d --build 를 사용하면 새로 빌드 가능
    - extends : 다른 YAML 파일이나 현재 YAML파일의 다른 서비스에서 서비스 속성을 상속받음

        다른 파일에서 가져올 때에는 파일 이름을 명시

        ```yaml
        services:
        	<SERVICE_NAME_1>:
        		...
        		file: <OTHER_YAMLFILE.YAML>
        		extends: <SERVICE_NAME_K>
        ```

- networks : 네트워크 정의
    - driver : 네트워크 드라이버 변경. Default는 브리지 타입 네트워크
    - ipam : subnet, ip 범위 등 설정. IPAM을 사용할 수 있는 driver 를 사용해야 함
    - external : YAML 파일을 통해 프로젝트 생성시마다 네트워크를 생성하는 것이 아닌, 기존의 네트워크를 사용하도록 설정.

        ```yaml
        networks:
        	<NETWORK_NAME>:
        		external: true
        ```

- volumes : 볼륨 정의
    - driver : 볼륨 생성시 사용할 드라이버 정의. Default는 local
    - external: YAML 파일을 통해 프로젝트 생성시마다 네트워크를 생성하는 것이 아닌, 기존의 볼륨을 사용하도록 설정

    ```yaml
    volumes:
    	<VOLUME_NAME>:
    		external: true
    ```