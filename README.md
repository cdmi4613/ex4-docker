# Docker Private EC2 CI/CD 실습

GitHub Actions, AWS Systems Manager(SSM), Amazon S3, Docker를 이용하여
Private EC2에 Nginx Docker 컨테이너를 자동 배포하는 실습입니다.

## 배포 구조

GitHub Actions
→ AWS Systems Manager (SSM)
→ Private EC2
→ Docker
→ Nginx Container
→ Web Page

## 배포 과정

1. main 브랜치에 소스코드 Push
2. GitHub Actions 실행
3. SSM을 통해 Private EC2에 명령 전달
4. Docker에서 `nginx:1.31.3-alpine` 이미지 실행
5. S3의 웹 파일을 Private EC2로 가져오기
6. `docker cp`를 이용해 웹 파일을 Nginx 컨테이너에 복사
7. Nginx 컨테이너에서 웹 페이지 서비스

## 프로젝트 구조

```text
ex4-docker/
├── .github/
│   └── workflows/
│       └── docker.yml
├── images/
├── index.html
└── README.md
주요 기술
GitHub Actions
AWS Systems Manager (SSM)
Amazon S3
Amazon EC2
Docker
Nginx
배포 방식

볼륨 마운트를 사용하지 않고 S3에서 웹 파일을 받은 후
docker cp를 이용하여 실행 중인 Nginx 컨테이너 내부로 복사합니다.
