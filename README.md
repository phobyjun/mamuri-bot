![node-17.9.0](https://img.shields.io/badge/Node-17.9.0-green?logo=nodedotjs)
![express-4.18.1](https://img.shields.io/badge/Express-4.18.1-green?logo=express)
![sequelize-6.20.0](https://img.shields.io/badge/Sequelize-6.20.0-green?logo=Sequelize)

![go-1.17.3](https://img.shields.io/badge/Go-1.17.3-blue?logo=go)
![goecho-4.7.2](https://img.shields.io/badge/Echo-4.7.2-blue)
![python-latest](https://img.shields.io/badge/Python-latest-blue?logo=python)
![fastapi-0.77.1](https://img.shields.io/badge/Fastapi-0.77.1-blue?logo=fastapi)

![mysql-5.7](https://img.shields.io/badge/Mysql-5.7-yellowgreen?logo=mysql)
![ngrok-v3](https://img.shields.io/badge/ngrok-v3-yellowgreen?logo=ngrok)

<div align="center"><img src="./img/readme_logo.png" width="20%" height="20%"></div>
<div align="center">경희대학교 오픈소스SW개발 강의 2022-1 팀프로젝트</div>

# 매무리 봇 (Mamuri-bot)

사용자에게 입력받은 키워드를 통해 3곳의 중고매물 사이트(중고나라, 당근마켓, 번개장터)에 매물을 감지, 알림을 전송하는 봇입니다.

## About The Project

- 봇을 사용해 키워드를 입력 받습니다.
- 주기적 크롤링을 통해 새로운 매물을 감지해 알림을 전송합니다.
- 다음의 QR코드를 통해 챗봇 서비스 사용이 가능합니다.

<div align="center"><img src="./img/qrcode.png" width="20%" height="20%"></div>

### Overview

![mockup_1x](./img/mockup_1x.png)

### Project Architecture

![project_structure](./img/project_structure.png)

### Built With

- [Node.js](https://nodejs.org/ko/)
- [Express](https://expressjs.com/ko/)
- [Go](https://go.dev/)
- [Echo](https://echo.labstack.com)
- [Python](https://python.org)
- [FastAPI](https://fastapi.tiangolo.com/)
- [MySQL](https://www.mysql.com)
- [ngrok](https://ngrok.com)

## Getting Started

### Prerequisites

Need to installation docker and docker-compose
- [Docker](https://www.docker.com/get-started/)
- [Docker-compose](https://docs.docker.com/compose/install/)

Need to write secret
- `mamuri-bot/database/mysql_init/.env`
   ```dotenv
   # Database Configuration
   TZ=Asia/Seoul
   MYSQL_HOST={YOUR_MYSQL_HOST}
   MYSQL_PORT={YOUR_MYSQL_PORT}
   MYSQL_ROOT_PASSWORD={YOUR_MYSQL_ROOT_PASSWORD}
   ```

- `mamuri-bot/joongna/config/.env`
   ```dotenv
   # Secret Configuration
   SECRET.CLIENTID={NAVER_API_CLIENT_ID}
   SECRET.CLIENTSECRET={NAVER_API_CLIENT_SECRET}
   # Header Configuration
   HEADER.COOKIE=NID_SES={YOUR_COOKIE}
   HEADER.USERAGENT={YOUR_SYSTEM_USER_AGENT}
   ```

- `mamuri-bot/ngrok/ngrok.yml`
   ```yaml
   authtoken: { YOUR_NGROK_AUTH_TOKEN }
   version: 2
   tunnels:
     mamuri:
       proto: http
       addr: mamuri-server:8080
   ```

- `mamuri-bot/server/config/.env`
   ```dotenv
   channelAccessToken: {YOUR_LINE_CHANNEL_ACCESS_TOKEN}
   channelId: {YOUR_LINE_CHANNEL_ID}
   channelSecret: {YOUR_LINE_CHANNEL_SECRET}
   ```

### Installation

1. Clone the repository
   ```shell
   $ git clone http://khuhub.khu.ac.kr/2018102211/mamuri-bot
   ```

2. Put your secret files that you create in prerequisite to
   ```shell
   mamuri-bot/database/mysql_init/.env
   mamuri-bot/joongna/config/.env
   mamuri-bot/ngrok/ngrok.yml
   mamuri-bot/server/config/.env
   ```
   
3. Executing `deploy.sh` for deployment with docker-compose. This script will `build` all images automatically and `docker-compose up` on your system
   ```shell
   #!/usr/bin/env bash
   docker build -t daangn-api-server ./daangn/
   docker build -t joongna-api-server ./joongna/
   docker build -t bunjang-api-server ./bunjang/
   docker build -t mamuri-db ./database/
   docker build -t mamuri-server ./server/
   docker build -t mamuri-ngrok ./ngrok/
   docker-compose up -d
   ```
   ```shell
   $ ./deploy.sh
   ```

4. Check your ngrok public URL
   ```shell
   $ docker logs mamuri-ngrok
   ```
   ![ngrok_deployment_1](http://khuhub.khu.ac.kr/2018102211/mamuri-bot/uploads/4ccdc73c9efc4c3dc58147f17b992cc6/그림1.png)

5. Set your public URL to Line chatbot configuration for webhook
   ![ngrok_deployment_2](http://khuhub.khu.ac.kr/2018102211/mamuri-bot/uploads/5dd076f66629948dd1682fc4054ff459/그림2.png)

## Contributing

프로젝트에 기여하고 싶으신 분들은 아래 절차를 따라주시기 바랍니다.

1. 프로젝트 fork
2. feature branch 생성 (git checkout -b feature/name)
3. commit (git commit -m "Add feature)
4. push (git push origin feature/name)
5. pull request 생성

## License

MIT 라이센스 아래 사용 가능합니다. LICENSE.txt를 통해 자세한 정보를 확인하세요.

## Contact

- 유명현: mhlew0106@khu.ac.kr
- 윤준석: phobyjun@khu.ac.kr
