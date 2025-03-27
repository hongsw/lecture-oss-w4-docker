# Docker 입문 강의

## 슬라이드 7: Dockerfile 작성하기

- **Dockerfile이란?**: 도커 이미지를 생성하기 위한 스크립트 파일
- **주요 지시자**:
  - `FROM`: 기본 이미지 지정
  - `WORKDIR`: 작업 디렉토리 설정
  - `COPY`/`ADD`: 파일 복사
  - `RUN`: 명령어 실행
  - `ENV`: 환경변수 설정
  - `EXPOSE`: 포트 노출
  - `CMD`/`ENTRYPOINT`: 컨테이너 실행 명령 지정

---

## 슬라이드 8: 나만의 이미지 만들기

- **Dockerfile 예제**:
```dockerfile
# Node.js 애플리케이션을 위한 Dockerfile
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

- **이미지 빌드 및 실행**:
```bash
# 이미지 빌드
docker build -t my-nodejs-app .

# 컨테이너 실행
docker run -d -p 3000:3000 my-nodejs-app
```

---

## 슬라이드 9: Docker Compose 소개

- **Docker Compose란?**: 다중 컨테이너 애플리케이션을 정의하고 실행하기 위한 도구
- **docker-compose.yml 파일 예제**:
```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db
  db:
    image: mongo:latest
    volumes:
      - mongo-data:/data/db
volumes:
  mongo-data:
```

- **실행 명령어**:
```bash
docker-compose up -d  # 백그라운드에서 실행
docker-compose down   # 컨테이너 중지 및 제거
```

### 윈도우/맥 사용자 노트
- **윈도우**: Docker Desktop에 Docker Compose 포함됨
- **맥**: Docker Desktop에 Docker Compose 포함됨
- **주의**: 볼륨 마운트 시 경로 표기법에 주의(윈도우 특히)