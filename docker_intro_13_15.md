# Docker 입문 강의

## 슬라이드 13: Docker 최적화 기법

- **경량 베이스 이미지**: Alpine 리눅스 기반 이미지 사용
  - 예: `node:16-alpine` vs `node:16`
  
- **다단계 빌드(Multi-stage builds)**: 빌드 환경과 실행 환경 분리
```dockerfile
# 빌드 단계
FROM node:16 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# 실행 단계
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
```

- **레이어 최적화**: RUN, COPY, ADD 명령 최소화

---

## 슬라이드 14: Docker 보안 고려사항

- **권한 최소화**:
  - 루트가 아닌 사용자로 실행
  - `USER` 지시자 사용
  
- **이미지 보안 스캔**:
  - Docker Scout 활용
  - 취약점 정기 점검
  
- **시크릿 관리**:
  - 환경 변수 또는 Docker Secrets 사용
  - Dockerfile에 민감한 정보 포함하지 않기

---

## 슬라이드 15: Docker 생태계와 다음 단계

- **관련 기술**:
  - **Kubernetes**: 컨테이너 오케스트레이션
  - **Docker Swarm**: Docker 내장 오케스트레이션
  - **Docker Registry**: 이미지 저장소
  
- **학습 자원**:
  - 공식 문서: [docs.docker.com](https://docs.docker.com)
  - Docker Hub: [hub.docker.com](https://hub.docker.com)
  - Play with Docker: [labs.play-with-docker.com](https://labs.play-with-docker.com)

- **실습 권장 사항**:
  - 간단한 애플리케이션 컨테이너화
  - Docker Compose로 다중 서비스 애플리케이션 배포
  - CI/CD 파이프라인에 Docker 통합

### 윈도우/맥 사용자 노트
- **윈도우**: Docker Desktop 리소스 사용량 조절 가능 (Settings > Resources)
- **맥**: Docker Desktop 리소스 사용량 조절 가능 (Preferences > Resources)
- **주의**: 시스템 부하 고려하여 적절한 리소스 할당 필요