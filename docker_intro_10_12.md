# Docker 입문 강의

## 슬라이드 10: Docker 네트워크

- **네트워크 타입**:
  - **Bridge**: 기본 네트워크 모드, 동일 호스트 내 컨테이너 간 통신
  - **Host**: 호스트 네트워크 직접 사용
  - **None**: 네트워크 없음
  - **Overlay**: 다중 호스트 간 컨테이너 통신 (Swarm 모드)
  
- **네트워크 명령어**:
  - `docker network ls`: 네트워크 목록 확인
  - `docker network create [네트워크명]`: 네트워크 생성
  - `docker network connect [네트워크명] [컨테이너명]`: 컨테이너를 네트워크에 연결

---

## 슬라이드 11: Docker 볼륨

- **데이터 지속성 문제**: 컨테이너 삭제 시 데이터도 삭제됨
- **볼륨 타입**:
  - **볼륨(Volumes)**: Docker가 관리하는 호스트 파일시스템의 일부
  - **바인드 마운트(Bind Mounts)**: 호스트 시스템의 임의 경로 마운트
  - **tmpfs 마운트**: 메모리에만 데이터 저장
  
- **볼륨 명령어**:
  - `docker volume create [볼륨명]`: 볼륨 생성
  - `docker volume ls`: 볼륨 목록 확인
  - `docker volume rm [볼륨명]`: 볼륨 삭제

---

## 슬라이드 12: 실전 예제 - 웹 애플리케이션 배포

- **구성 요소**:
  - 프론트엔드: React 앱
  - 백엔드: Node.js API
  - 데이터베이스: MongoDB
  
- **docker-compose.yml 예제**:
```yaml
version: '3'
services:
  frontend:
    build: ./frontend
    ports:
      - "80:80"
    depends_on:
      - backend
  backend:
    build: ./backend
    ports:
      - "3000:3000"
    environment:
      - MONGO_URI=mongodb://db:27017/myapp
    depends_on:
      - db
  db:
    image: mongo:latest
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:
```

### 윈도우/맥 사용자 노트
- **윈도우**: 볼륨 경로는 C:\\path\\to\\data와 같은 형식으로 지정
- **맥**: 볼륨 경로는 /path/to/data와 같은 형식으로 지정
- **주의**: 볼륨 권한 문제 발생 시 시스템 설정 확인 필요