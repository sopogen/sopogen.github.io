- 도커 이미지들은 docker hub 에 저장됨
- docker search
    - docker hub에서 키워드에 대한 도커 이미지들을 검색  
    
      

##### 이미지 생성

---

- docker commit
  : 컨테이너로 이미지 생성

    ```bash
    docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
    ```

    - -a : 이미지 작성자 지정
  
    - -m : 커밋 메세지 지정  
  
      

##### 이미지 삭제

---

- docker rmi
- 현재 컨테이너에 사용되고 있는 이미지는 삭제할 수 없음
    - 만약 -f 옵션으로 강제 삭제하면 이미지 이름만 삭제되어 none이 되고 파일은 남아있음
    
    - 이러한 이미지를 dangling image라고 함
    
       

##### 이미지 추출 및 적용

---

- docker save
: 도커 이미지를 바이너리 파일로 추출

    ```bash
    docker save -o $(FILE_NAME) $(IMAGE_NAME)
    ```

- docker load
: 추출된 도커 이미지를 도커에 로드

    ```bash
    docker load -i $(FILE_NAME)
    ```

- import, export
: save, load와 비슷한 기능을 하지만, 컨테이너가 생성 될 때의 설정 정보는 저장되지 않음



##### 이미지 배포

---

- docker hub 에서 개인 레포 생성
- 저장소에 이미지 업로드
- docker tag
: 이미지에 이름을 추가하여 업로드 할 수 있게 함

    ```bash
    docker tag $(IMAGE_NAME) $(USER_NAME)/$(REPO_NAME)[:VERSION]
    ```

- docker login 후에 docker push