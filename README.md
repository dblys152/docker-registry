# 개인 Private Registry 구축

### 1. Docker registry image pull
    $ docker pull registry
### 2. 사용자 인증 방식
> htpasswd를 생성하기 위한 apache2-utils 설치

    $ sudo apt-get install apache2-utils
    $ mkdir /etc/docker/registry/auth
    
> htpasswd 생성

    $ htpasswd -c /etc/docker/registry/auth/htpasswd {유저명}
    => 패스워드 입력
    
### 3. SSL 인증서 발급
### 4. Nginx 설정
    $ sudo vi /etc/nginx/sites-available/{도메인}
    $ sudo ln -s /etc/nginx/sites-available/{도메인} /etc/nginx/sites-enabled/
    $ sudo nginx -t
    $ sudo nginx -s reload
### 5. docker-compose 실행
    $ docker compose up -d

> 실행중인 컨테이너 확인

    $ docker compose ps

> 실행중인 registry 컨테이너 로그 확인 

    $ docker logs registry

## Docker image push
> 이미지 생성

    $ docker build -t {도메인}/{레파지토리명}:{태그} .

> registry 로그인

    $ docker login {도메인}

> 이미지 푸쉬

    $ docker push {도메인}/{레파지토리명}:{태그}

> 레파지토리 확인

    $ curl https://{도메인}/v2/_catalog

> 레파지토리 이미지 목록 확인

    $ curl https://{도메인}/v2/{레파지토리명}/tags/list

## Docker image pull
> registry 로그인

    $ docker login {도메인}

> 이미지 풀

    $ docker pull {도메인}/{레파지토리명}:{태그}

> 이미지 확인

    $ docker images


