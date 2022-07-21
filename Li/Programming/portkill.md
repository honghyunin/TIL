# port 8080 already in use

> 저는 윈도우를 사용하므로 윈도우 기준에서 설명하겠습니다. 

우선 cmd를 관리자 권한으로 실행하여 ``netstat -a -o`` 명령어를 입력한다

![portkill](/images/portkill.png)

이 중에서 로컬 주소의 0.0.0.0:~~ 이후의 숫자의 __PID를 확인__ 하여

``taskkill /f /pid 포트번호`` 를 입력하시면 port가 죽게됩니다.