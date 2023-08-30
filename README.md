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
    $ sudo vi /etc/nginx/sites-available/{레파지토리 주소}
    $ sudo ln -s /etc/nginx/sites-available/{레파지토리 주소} /etc/nginx/sites-enabled/
    $ sudo nginx -t
    $ sudo nginx -s reload
### 5. docker-compose 실행
    $ docker compose up -d

> 상태 확인

    $ docker compose ps

> 로그 확인 

    $ docker compose logs

## Docker image push
> 이미지 생성

    $ docker build -t {레파지토리 주소}/{이미지명}:{태그} {Dockerfile 위치}

> registry 로그인

    $ docker login {레파지토리 주소}

> 이미지 푸쉬

    $ docker push {레파지토리 주소}/{이미지명}:{태그}

> 레파지토리 확인

    $ curl https://{레파지토리 주소}/v2/_catalog

> 레파지토리 이미지 태그 목록 확인

    $ curl https://{레파지토리 주소}/v2/{이미지명}/tags/list

## Docker image pull
> registry 로그인

    $ docker login {레파지토리 주소}

> 이미지 풀

    $ docker pull {레파지토리 주소}/{이미지명}:{태그}

> 이미지 확인

    $ docker images


