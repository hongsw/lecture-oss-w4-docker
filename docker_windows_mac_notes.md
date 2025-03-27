# Docker 입문 - 윈도우/맥 사용자를 위한 노트

## Windows 사용자 가이드

### 시스템 요구사항
- **Windows 10/11**: 
  - Pro, Enterprise, Education (버전 1607 이상)
  - Windows 10 Home (버전 2004 이상, 빌드 19041 이상)
- **시스템 사양**:
  - 64비트 프로세서 (Intel/AMD)
  - 4GB 이상 RAM 권장
  - BIOS 가상화 지원 (Intel VT-x 또는 AMD-V)

### WSL2 설정
1. **WSL2 활성화**:
   ```powershell
   # PowerShell 관리자 권한으로 실행
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```

2. **WSL2 Linux 커널 업데이트 패키지 설치**:
   - [Microsoft 공식 다운로드 페이지](https://docs.microsoft.com/ko-kr/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)에서 패키지 다운로드 및 설치

3. **WSL2를 기본 버전으로 설정**:
   ```powershell
   wsl --set-default-version 2
   ```

### Docker Desktop 설치
1. [Docker 공식 웹사이트](https://www.docker.com/products/docker-desktop/)에서 Docker Desktop for Windows 다운로드
2. 설치 프로그램 실행 및 "Use WSL 2 instead of Hyper-V" 옵션 선택
3. 설치 완료 후 시스템 재시작

### 자주 발생하는 문제 및 해결책
1. **"Hardware assisted virtualization and data execution protection must be enabled in the BIOS"**:
   - BIOS 설정에서 가상화 기능 (VT-x/AMD-V) 활성화 필요
   
2. **WSL2 업데이트 실패**:
   - WSL2 Linux 커널 업데이트 패키지 수동 설치 시도
   
3. **Docker Desktop이 시작되지 않는 경우**:
   ```powershell
   # Docker 서비스 재시작
   net stop com.docker.service
   net start com.docker.service
   ```
   
4. **볼륨 마운트 경로 문제**:
   - Windows 경로 사용 시: `C:\Users\username\data`
   - WSL2에서 사용 시: `/mnt/c/Users/username/data`
   - Docker Compose에서는 `/c/Users/username/data` 형식 권장

## macOS 사용자 가이드

### 시스템 요구사항
- **Apple Silicon (M1/M2)**: macOS 11.0 (Big Sur) 이상
- **Intel**: macOS 10.15 (Catalina) 이상
- **하드웨어**: 최소 4GB RAM, 권장 8GB 이상

### Docker Desktop 설치
1. [Docker 공식 웹사이트](https://www.docker.com/products/docker-desktop/)에서 맥 환경에 맞는 버전 다운로드
   - Apple Silicon: .dmg (Apple Silicon)
   - Intel: .dmg (Intel Chip)
2. .dmg 파일 열고 Docker.app을 Applications 폴더로 드래그
3. Docker 앱 실행 (최초 실행 시 권한 요청 승인 필요)

### 환경별 최적화
1. **Apple Silicon (M1/M2)**:
   - Settings > General > "Use Virtualization framework" 활성화
   - Settings > Resources > Memory 설정 (기본 4GB, 작업량에 따라 조절)
   
2. **Intel Mac**:
   - Settings > Resources > Memory 설정 (기본 2GB, 필요시 증가)
   - CPU 코어 수 최적화 (시스템 성능 고려)

### 자주 발생하는 문제 및 해결책
1. **Docker Desktop이 시작되지 않는 경우**:
   ```bash
   # Docker 데몬 재시작
   osascript -e 'quit app "Docker"'
   open -a Docker
   ```
   
2. **디스크 공간 부족 경고**:
   - Settings > Resources > Disk image size 조절
   - 미사용 이미지 및 볼륨 정리:
     ```bash
     docker system prune -a --volumes
     ```
     
3. **Apple Silicon 호환성 문제**:
   - 이미지가 arm64 아키텍처를 지원하는지 확인
   - 호환되지 않는 경우 Rosetta 에뮬레이션 활성화:
     Settings > Features in development > "Use Rosetta for x86/amd64 emulation"
   
4. **볼륨 마운트 성능 이슈**:
   - Settings > Resources > File sharing에서 필요한 디렉토리만 추가
   - 대량 파일 작업 시 Docker 볼륨 사용 권장

### 터미널에서 Docker CLI 사용
```bash
# Docker CLI 버전 확인
docker --version

# Docker Desktop 상태 확인
docker info
```

## 공통 문제해결

### 컨테이너 시작 실패
```bash
# 로그 확인
docker logs [컨테이너ID]

# 인터랙티브 쉘로 디버깅
docker exec -it [컨테이너ID] /bin/bash
# 또는
docker exec -it [컨테이너ID] /bin/sh
```

### 리소스 부족 문제
- Docker Desktop에서 할당된 CPU/메모리 리소스 증가
- 불필요한 컨테이너 및 이미지 정리:
  ```bash
  # 중지된 컨테이너 삭제
  docker container prune
  
  # 미사용 이미지 삭제
  docker image prune
  
  # 전체 Docker 시스템 정리
  docker system prune
  ```

### 네트워크 문제
```bash
# 네트워크 목록 확인
docker network ls

# 네트워크 검사
docker network inspect [네트워크ID]

# 네트워크 재생성
docker network rm [네트워크ID]
docker network create [네트워크명]
```