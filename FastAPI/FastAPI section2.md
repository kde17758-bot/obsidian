### 1. FastAPI 알아보기

>[!note] 클라이언트-서버 모델
>#### 클라이언트-서버 모델이란?
>: 서비스 구조를 사용하는 요청자와 서비스를 제공하는 제공자를 분리하여 역할과 책임을 각각 관리하는 구조
>>[!abstract] 클라이언트-서버 모델의 장점
>>- 확장 가능성  : 하나의 서버에서 다수의 클라이언트 대응 가능
>>- 관심사의 분리 : 역할을 명확하게 분리해서 성능, 보안에 대한 최적화
>>>**[예시]**
>>>-  일반적으로, 클라이언트의 컴퓨팅 능력이 낮아 무거운 연산 처리는 고사양의 서버에서 대신하여 성능에 대한 최적화 
>>>- 개인정보와 같은 보안이 중요한 데이터는 권한된 사용자만 접근이 가능하도록 만들어 안전하게 데이터를 관리
>>```mermaid
>>graph LR
>>c[클라이언트] -->|HTTP 요청| N[(네트워크)] -->|HTTP 요청| s[서버]
>>s[서버] -->|HTTP 응답| N[(네트워크)] -->|HTTP 응답| c[클라이언트]
>>```
>>> -> 이때, 클라이언트와 서버는 올바르게 데이터를 주고받기 위해 사전에 협의 된 API로 통신

---
### 2. API란?
#### Application Programming Interface 
: 서버의 기능을 클라이언트가 사용할 수 있도록 만든 인터페이스
>[!example] Interface 예시
>- **리모컨**
>>- 기능을 외부에서 사용할 수 있게 제공
>>```mermaid
>>graph LR
>>user[사용자] --> button[버튼-물리신호] --> 전기신호 --> 장비
>>```
>- **에어컨**
>>**<내부>**
>>- 실내 온도 감지
>>- 실외기 조작
>>
>> **<외부>**
>> - 전원 ON/OFF
>> - 온도 조절
>> - 바람 세기 조절
>

---
### 3. REST API (RESTful API)
: 실질적으로 API를 디자인하는 방법
-> 클라이언트와 서버가 서로 예측 가능한 방법으로 통신할 수 있음
#### Representational State Transfer
: 서버에서 관리하는 데이터의 상태가 표현되는 디자인

>[!note] REST API 특징
>- **Resource**
>: URL를 통해 고유한 리소스 표현 (서버에서 관리하고 있는 자원에 대해 표현)
>>ex> 
>>- `/api/v1/posts` :  posts라는 게시물들에 대한 데이터를 사용할 수 있음
>>- `/api/v1/posts/123/comments` : 123번 게시물들에 달린 댓글 데이터에 접근하게 됨
>
>- **Method**
>: HTTP Method 통해 API의 구체적인 동작 표현
>>ex> 
>>- `GET/api/vi/posts` : posts 조회
>>- `POST/api/v1/posts` : post 생성
>>- `PATCH/api/v1/posts/123` : post 수정
>>- `DELETE/api/v1/posts/123` : post 삭제
>
>-> REST API를 사용하면, 간결한 인터페이스로 클라이언트와 서버간의 통신을 관리할 수 있게 됨.

---
### 4. ToDo 서비스 만들기
- **GET** 
	- 전체 ToDo 조회 : `/api/v1/todos`
	- 단일 ToDo 조회 : `/api/v1/todos/<id>`
- **POST**
	- ToDo 생성 : `/api/v1/todos`
- **PATCH**
	- ToDo 수정 : `/api/v1/todos/<id>`
- **DELETE**
	- ToDo 삭제 : `/api/v1/todos/<id>`

```cmd
python -m venv todos
cd todos
Scripts\activate
```
---
### 5. FastAPI 프로젝트 세팅
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def health_check_handler():
	return {"ping": "pong"}
```