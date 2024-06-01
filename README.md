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
