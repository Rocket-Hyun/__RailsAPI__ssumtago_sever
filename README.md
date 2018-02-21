# 인공지능 럽파고 어플리케이션 Restful API 서버

### 툴: Ruby on Rails 5 API
### API: 페이스북 로그인 API, RabbitMQ, JWT, FCM, 몽고DB
#### 설명: 제작 중

# RESTFUL API
### 유저 회원가입 (email 방식만)
    [POST] /users
>     {
>       "email": "ssumtago@ssumtago.com",
>       "password": "tagotago",
>       "joinType": "email",
>       "name": "Tago Man",
>       "sex": "man",
>       "age": "25"
>     }
> * email, password, joinType, name 필수
> * 회원가입 성공시 JWT 토큰값 반환


### 유저 GET (facebook은 회원가입도 여기서)
    [GET] /users
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 인증 확인시 현재 유저 정보 반환


### 유저 UPDATE
    [PATCH] /users
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
>    
>     [Body]
>     {
>       "name": "정순"
>       "fcmToken": "f3iDP3aghcc:APA91bE_n3b2IepFR5ZKk1thfaketokenafbhVCWENFJZJ12nDUZgnL6mmV5EBDvEqTNp5b"
>     }
> * 전송 성공시 success 메세지 반환


### 유저 DELETE
    [DELETE] /users
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 전송 성공시 success 메세지 반환


### 로그인 (이메일/페이스북)
    [POST] /sessions
>     {
>       "email": "ssumtago@ssumtago.com",
>       "password": "tagotago",
>       "joinType": "email"
>     }
> * email, password, joinType 필수
> * 페이스북 로그인은 password에 토큰값
> * 페이스북 로그인은 첫 로그인시엔 회원가입, 이후엔 로그인
> * 로그인 성공시 JWT 토큰값 반환


### 설문지 Create
    [POST] /surveys
>     {
>       "models": [],
>       "name": "첫번째 설문지",
>       "questions": "[]",
>       "answerCodes": "02001001",
>       "version": "1.0.0",
>       "surveyId": "23",
>       "desc": "설명"
>     }
> * 성공시 survey 값 반환


### 설문지 Read
    [GET] /surveys
> * 성공시 모든 surveys값 반환

    [GET] /surveys/:surveyId
> * 성공시 해당 survey값 반환


### 설문지 Update
    [PATCH] /surveys/:surveyId
>     {
>       "models": [],
>       "name": "첫번째 설문지",
>       "questions": "[]",
>       "answerCodes": "02001001",
>       "version": "1.0.0",
>       "surveyId": "23",
>       "desc": "설명"
>     }
> * 성공시 해당 survey값 반환


### 설문지 Delete
    [DELETE] /surveys/:surveyId
> * 성공시 해당 survey값 삭제 성공 msg 반환


### 썸 Request 보내는곳
#### 썸 CREATE
    [POST] /ssums
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
>
>     [Body]
>     {
>       "name":"정현",
>       "age":"21",
>       "sex":"male"
>     }
> * 전송 성공시 success 메세지 반환


#### 썸 READ
    [GET] ssums/:ssumId
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 전송 성공시 ssum 정보 반환


#### 썸 UPDATE
    [PATCH] /ssums/:ssumId
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
>
>     [Body]
>     {
>       "name":"정현2",
>       "age":"25",
>       "sex":"male"
>     }
> * 전송 성공시 success 메세지 반환


#### 썸지 DELETE
    [DELETE] ssums/:ssumId
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 전송 성공시 success 메세지 반환
-------------------------

### 썸지 Request 보내는곳
#### 썸지 CREATE
    [POST] ssums/:ssumId/predictReports
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
>
>     [Body]
>     {
>       "surveyId":1, //Integer
>       "modelId":1, //Integer
>       "version":"1.0.1",
>       "data": [
>         {"questionCode":"01000120001", "answerCode":"02001001"},
>         {"questionCode":"01000120002", "answerCode":"02002003"},
>         {"questionCode":"01000120003", "answerCode":"02003004"}
>       ]
>     }
> * 전송 성공시 success 메세지 반환


#### 썸지 READ
    [GET] ssums/:ssumId/predictReports/:reportId
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 전송 성공시 report 정보 반환


#### 썸지 UPDATE
    [PATCH] ssums/:ssumId/predictReports
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
>     [Body]
>     {
>       "reportId":"5945f2a90640fd12bb91fb97",
>       "data": [
>         {"questionCode":"01000120001", "answerCode":"02001001"},
>         {"questionCode":"01000120002", "answerCode":"02002003"},
>         {"questionCode":"01000120003", "answerCode":"02003004"}
>       ]
>     }
> * 전송 성공시 success 메세지 반환


#### 썸지 DELETE
    [DELETE] ssums/:ssumId/predictReports/:reportId
>     [Headers]
>     Key: jwt
>     Value: <JWT값>
> * 전송 성공시 success 메세지 반환

### 예측 결과 Request 보내는 곳
    [POST] /predictResults
>
>     [Body]
>     {
>       "userId":"593ab60c5283625315549dce",
>       "surveyId":1, //Integer
>       "predictResult": [0.86, 0.76]  //Array >> Double
>     }
> * 전송 성공시 success 메세지 반환
