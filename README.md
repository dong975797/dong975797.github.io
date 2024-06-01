오픈소스sw과제
===============
목차
----
1. top
2. ps
3. jobs
4. kill

top
--
**전체적인 CPU / Memory의 사용량 및 프로세스 단위의 리소스 사용량을 확인할 수 있다.**
* shift + p : CPU 사용률 내림차순
* shit + m : 메모리 사용률 내림차순
* shift + t : 프로세스가 돌아가고 있는 시간 순
* k : kill. k 입력 후 PID 번호 작성. signal은 9
* f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
* a : 메모리 사용량에 따라 정렬
* b : Batch 모드로 작동
* 1 : CPU Core별로 사용량 보여줌
```
top -b -n 1
```
 ![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Frxlg4%2FbtqYfV2LE3L%2FSW5SbyO65ZUa5PggM3KI8K%2Fimg.png)
[설명]

* 1:15 : 1시간 15분 전에 서버가 구동
* load average : 현재 시스템이 얼마나 일을 하는지를 나타냄. 3개의 숫자는 1분, 5분, 15분 간의 평균 실행/대기 중인 프로세스의 수. CPU 코어수 보다 적으면 문제 없음
* Tasks : 프로세스 개수
* KiB Mem, Swap : 각 메모리의 사용량
* PR : 실행 우선순위
* VIRT, RES, SHR : 메모리 사용량 => 누수 check 가능
* S : 프로세스 상태(작업중, I/O 대기, 유휴 상태 등)

ps
--
**Process State의 약자로 현재 실행 중인 프로세스와 상태를 출력하는 명령어이다.**

명령어 목록
* a : 터미널과 연관된 프로세스만 출력
* x : 터미널과 연관되지 않는 프로세스만 출력
* -A : 모든 프로세스 출력 (-e와 동일)
* -e : 모든 프로세스 출력
* -a : 세션 리더와 터미널과 연관되지 않은 프로세스를 제외하고 모든 프로세스를 출력
* p : 지정한 PID 목록의 정보만 출력
* -C : 지정한 프로세스의 실행 파일 이름의 정보만 출력
* -u : 특정 사용자의 프로세스 정보를 출력
* u : 프로세스의 소유자 정보를 함께 출력
* l : BSD 형식의 긴 형식으로 출력
* e : 프로세스 정보와 함께 프로세스의 환경변수 정보도 출력
* -l : 긴 포맷으로 출력
* -o : 사용자 정의 형식 지정 가능
* f : 프로세스 계층을 텍스트 형식의 트리구조를 보여줌.
* -f : 전체 포맷으로 출력
 ![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FJzNka%2FbtsCOy6jjjO%2FcsjX2vyKt6dUuImIcXijxk%2Fimg.png)
[설명]
* F:	프로세스 플래그
* S:	프로세스 상태코드
* UID:	프로세스 소유자이름
* PID:	프로세스 고유식별자
* PPID:	부모프로세스의 PID
* C:	프로세서 사용률 %로 표기
* PRI:	프로세스의 우선순위. 높은값이 낮은 우선순위
* NI:	nice 값이며 19에서 -20값
* SZ:	프로세스 이미지가 차지하는 물리적 페이지 크기
* WCHAN:	대기중일때 커널 함수의 이름
* STIME:	프로세스가 시작한 시간
* TTY:	터미널의 종류
* TIME:	총 CPU 사용시간
* CMD:	프로세스의 실행 시 명령줄

[자주 쓰는 명령어]
```
$ ps -p 1(프로세스 번호가 1인 프로세스 출력)

$ ps -u apache(계정이 apache인 프로세스들을 )

$ ps -fp [PID] # PID를 키워드로 프로세스 정보를 확인

$ ps -u root # 특정 사용자가 돌리는 프로세스의 정보를 알고 싶을 때

$ ps -p 1222 -o comm= # PID가 1222인 프로세스의 이름을 출력

$ ps -C httpd -o pid= # 이름이 httpd인 프로세스들의 pid를 출력
```

jobs
-
**셸에서 실행중인 프로세스 목록을 확인할 수 있다.**

기본형식은 다음과 같다.
```
jobs [OPTIONS] [JOB]
```
* -l: 프로세스 ID와 함께 잡 목록을 출력
* -n: 마지막로 알림 이후 변경된 잡만 출력
* -p: 잡의 프로세스 ID만 출력
* -r: 실행 중인 잡만 출력
* -s: 중지된 잡만 출력
* -command: 지정한 명령어를 실행

[실행예시]

![alt text](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKWXTd%2FbtrcLAQP0GL%2F9PU2e4Y0lFeBB1nh4rIJQ0%2Fimg.png)
* Running: 작업이 계속 진행중임
* Done: 작업이 완료되어 0을 반환
* Done(code): 작업이 종료되었으며 0이 아닌 코드를 반환
* Stopped: 작업이 일시 중단
* Stopped(SIGTSTP): SIGTSTP 시그널이 작업을 일시 중단
* Stopped(SIGSTOP): SIGSTOP 시그널이 작업을 일시 중단
* Stopped(SIGTTIN): SIGTTIN 시그널이 작업을 일시 중단
* Stopped(SIGTTOU): SIGTTOU 시그널이 작업을 일시 중단

kill
-
**프로세스를 종료하거나 그외에도 다른 신호를 보내어 프로세스의 동장을 제어할 수 있다.**
기본형식은 다음과 같다.
```
kill [옵션] <PID>
```
여기서 <PID>는 종료할 프로세스의 식별자인 프로세스 ID를 나타낸다.

* -s <signal>: 특정 시그널(signal)을 사용하여 프로세스를 종료. 기본적으로 SIGTERM 시그널이 사용.
* -l, --list: 지원되는 시그널(signal) 목록을 출력.
* -a, --all: 현재 사용자에 속한 모든 프로세스를 종료.
* -q, --queue: 프로세스에 시그널을 보내는 대신 시그널을 대기열에 추가.

종료하는 것 외에도 다른 동작을 수행할 수 있다. 예시는 다음과 같다.
