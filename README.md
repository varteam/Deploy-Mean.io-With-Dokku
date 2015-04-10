# 사전 작업
우분투 설치 [https://github.com/varteam/Install-Ubuntu14.04]

도커 설치 [https://github.com/varteam/Install-Docker-On-Ubuntu]

도쿠 설치 [https://github.com/varteam/Install-Dokku-on-ubuntu]

# Deploy-Mean.io-With-Dokku
Mean.io 를 dokku 와 함께 관리 배포 하는 방법

## mean.io 소스 다운로드

    $ git clone https://github.com/linnovate/mean.git

## mongodb container 와 연결

    //서버에서
    // if you didn't start mongodb, you need to start mongodb first($ dokku mongodb:start)
    $ dokku mongodb:create meanio meanio
    $ dokku mongodb:link meanio meanio

## dokku 서버와 git 연결

    //git remote add dokku dokku@<IP Address>:<App Name>
    $ git remote add dokku dokku@abc.com:mean.io

그리고 config/env/ 에서 해당 mongodb 환경설정 변경경
현재는 production.js 파일을 수정 (나중에 NODE_ENV 를 통해서 변경 가능)

    'use strict';

    module.exports = {
      db: process.env.MONGO_URI,
      /**
       * Database options that will be passed directly to mongoose.connect
       * Below are some examples.
       * See http://mongodb.github.io/node-mongodb-native/driver-articles/mongoclient.html#mongoclient-connect-options
       * and http://mongoosejs.com/docs/connections.html for more information
       */
      dbOptions: {
        /*
        
        --생략--


## dokku 서버로 git push
    
    $ git push dokku master
    Counting objects: 7030, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (2996/2996), done.
    Writing objects: 100% (7030/7030), 4.00 MiB | 177.00 KiB/s, done.
    Total 7030 (delta 3556), reused 7017 (delta 3547)
    -----> Cleaning up...
    -----> Building meanio from buildstep...
    -----> Adding BUILD_ENV to build environment...
    -----> Node.js app detected
    -----> Requested node range: 0.10.x
    -----> Resolved node version: 0.10.38
    -----> Downloading and installing node
    -----> Exporting config vars to environment
    -----> Installing dependencies

--생략--

