FROM 

Docker 이미지는 base 이미지부터 시작해서 기존 이미지 위에 새로운 이미지를 중첩해서 여러 단계의 이미지 층을 쌓아가며 만들어진다.

- base이미지를 지정

WORKDIR

- 쉘의 cd 명령문처럼 컨테이너 상에서 작업 디렉토리로 전환을 위해 사용된다.

RUN

- 쉘에서 커맨드를 실행하는 것 처럼 이미지 빌드 과정에서 필요한 커맨드를 실행하기 위해 사용된다.

ENTRYPOINT

- 이미지 실행 시 항상 실행되어야 하는 커맨드

CMD

- 해당 이미지를 컨테이너로 띄울 때 디폴트로 실행할 커맨나, ENTRYPOINT 명령문으로 지정돈 커맨드에 디폴트로 넘길 파라미터를 지정할 때 사용된다.
    
    ```bash
    ENTRYPOINT ["node"]
    CMD ["index.js"]
    
    $ dockerr run test //node index.js 실행
    $ docker run test main.js //node main.js 실행  
    ```
    
    RUN → 이미지 빌드 시 항상 실행되며 도커파일에 여러개의 명령문을 선언할 수 있다.
    
    CMD → 이미지를 컨테이너로 띄울 때 딱 한번 실행 되며, docker run 커맨드에 인자를 넘길 경우 실행되지 않는다. 
    

COPY

- 호스트 컴퓨터에 있는 디렉터리나 파일을 DOCKER 이미지의 파일 시스템으로 복사

```docker
FROM node:alpine // alpine linux를 사용하는 것이 용량이 적다 

WORKDIR /src/app // 하위 동작들을 할 Dir 설정
#ENV PATH /app/node_modules/.bin:$PATH

COPY package.json .
RUN npm install -g npm@8.11.0
# RUN npm install react-scripts@2.1.3 -g --silent

COPY ./ ./

EXPOSE 8080
CMD ["npm","start"]
```

docker build 명령어 

<aside>
💡 docker build -t sally-test:0.1 ./

- t 옵션 : 빌드할 이미지의 이름 지정
- build:0.0 : 이미지의 이름과 버전
- ./ : dockerfile이 위치한 디렉토리
</aside>

docker run 명령어 

<aside>
💡 docker run -it -p 3300:3100 <컨테이너 이름>

</aside>

docker continer 접속 명령어 

<aside>
💡 docker exec -it <컨테이너 이름> /bin/sh  
#bash가 없음

</aside>
