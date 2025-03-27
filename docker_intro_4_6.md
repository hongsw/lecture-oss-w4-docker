# Docker 입문 강의

## 슬라이드 4: Docker 설치하기

- **요구사항**: 
  - 윈도우: Windows 10 Pro, Enterprise, Education (64bit) 이상
  - 맥: macOS 10.14 이상, Apple Silicon/Intel 모두 지원
  - 리눅스: Ubuntu, Debian, Fedora, CentOS 등 다양한 배포판 지원

- **설치 방법**:
  - 공식 웹사이트에서 Docker Desktop 다운로드: https://www.docker.com/products/docker-desktop/
  - 설치 마법사 실행 및 설정 진행

---

## 슬라이드 5: Docker 기본 명령어

- **이미지 관련**:
  - `docker images`: 로컬에 있는 이미지 목록 확인
  - `docker pull [이미지명:태그]`: 이미지 다운로드
  - `docker rmi [이미지ID]`: 이미지 삭제

- **컨테이너 관련**:
  - `docker ps`: 실행 중인 컨테이너 목록
  - `docker ps -a`: 모든 컨테이너 목록
  - `docker run [이미지명]`: 컨테이너 실행
  - `docker stop [컨테이너ID]`: 컨테이너 중지
  - `docker rm [컨테이너ID]`: 컨테이너 삭제

---

## 슬라이드 6: Docker 실행 예제

```bash
# Nginx 웹 서버 실행하기
docker run -d -p 8080:80 --name my-nginx nginx

# 실행중인 컨테이너 확인
docker ps

# 웹 브라우저에서 확인: http://localhost:8080

# 컨테이너 중지 및 삭제
docker stop my-nginx
docker rm my-nginx
```

### 윈도우/맥 사용자 노트
- **윈도우**: PowerShell이나 명령 프롬프트에서 명령어 실행
- **맥**: 터미널 앱에서 명령어 실행
- **주의**: 윈도우에서 경로 지정 시 백슬래시(\) 대신 슬래시(/) 사용 권장