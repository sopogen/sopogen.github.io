---

- 컨테이를 생성할 때 자원 할당량을 정해주지 않으면, 제한 없이 자원을 사용하게 됨
- 컨테이너 생성시에 메모리, cpu 등의 자원할당을 미리 정해줄 수 있음

### 메모리 할당

---

- --memory : 메모리 할당
- --memory-swap : 스왑 메모리 공간 할당

```bash
docker run --memory="1g" --memory-swap="2g" $(DOCKER_IMAGE)
```

### CPU 할당

---

- --cpu-shares : CPU 사용 비율 할당. 총 cpu-shares에서 해당되는 비율 만큼의 CPU 자원 사용
- - -cpuset-cpus : 호스트에 CPU가 여러개 있을 때 특정 CPU 사용
- - -cpus : 사용 CPU 개수 지정

```bash
docker run --cpu-shares 1024 --cpuset-cpus:2 --cpus:1 $(DOCKER_IMAGE)
```

### Block I/O 할당

---

- --device-write-bps : 쓰는 작업의 속도 제한
- --device-read-bps : 읽는 작업의 속도 제한
- --device-(write / read)-isop : 쓰는 / 읽는 작업의 속도 제한을 비율로 지정

```bash
docker run --device-write-bps $(DEVICE):1mb --device-read-isop $(DEVICE):10 $(DOCKER_IMAGE)
```