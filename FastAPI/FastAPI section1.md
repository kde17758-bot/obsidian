### 1. Python 가상 환경 구축
![[Pasted image 20260120111821.png|400]]
![[Pasted image 20260120111931.png|400]]
![[Pasted image 20260120113020.png|450]]
VScode를 사용해도 좋지만, 실습 할 때에는 pyCharm을 사용해보는 것도 좋을 것 같아서 cmd를 쓰다가 pyCharm으로 재시작하였다.
이때, 강의에서는 MacOS를 사용했기에 명령어가 많이 달랐다.
ex>세부 파일명 공개 : ls -> dir / which -> where 등 ...
>[!example] Windows 버전 Python 가상 환경 구축
>>```cmd
>>python -m venv example (가상 환경 생성)
>>cd example (example directory 이동)
>>dir
>>Scripts\activate.bat (가상 환경 활성화)
>>which python
>>python --version
>>```
>
---

### 2. Docker 설치
![[Pasted image 20260120113832.png]]
 Docker 정상적으로 설치 완료!
---
### 3. PyCharm 설치
![[Pasted image 20260120114625.png|550]]
PyCharm 설치 후 생성해둔 example 가상환경 open
-> python interpreter로 연결되어있는 지 확인 후 example 안에 main.py 생성