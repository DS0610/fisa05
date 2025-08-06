# Linux
---
```
# 컨테이너 생성
$ docker run -d --name ubuntu -p 23:22 -it --privileged ubuntu:22.04
                                 # --privileged 특정 권한들에 접속. 예: docker 안에서 docker 실행 등
	                               # 웬만하면 안 쓰는 편이 보안상 좋음

# 컨테이너 실행
$ docker exec -it ubuntu /bin/bash

# 필수 외 패키지 모두 설치
$ unminimize

apt-get update 
apt-get install net-tools vim openssh-server ssh sudo info man-db less psmisc nano tzdata cron

# ssh 접속 허용
$ service ssh start 
```
### 리눅스란
- 오픈 소스(open source) 방식으로 개발됨
- 서버 운영체제 시장에서 유닉스를 넘어 확고한 지위를 다지고 있음
- 안드로이드도 리눅스 커널을 기초로 개발되었음

#### 커널
- 운영체제의 핵심 → 모든 작업에 우선하여 동작하는 프로그램을 의미
- 인터럽트 처리, 프로세스 관리, 메모리 관리, 파일 시스템 관리, 프로그래밍 인터페이스 제공 등 운영체제의 기본적인 기능들을 제공
- 리눅스는 커널 부분만을 의미

#### 리눅스 특징
1. 개인이 무료로 사용 가능
2. 악성 소프트웨어가 동작할 수 있는 권한이 제한적 → 안전
3. 다중 사용자용 서버 운영체제 → 다중 작업에 최적화
4. 스크립트를 통해 많은 부분을 자동화 → 운영 편리함
5. 직접 소스 코드를 보면서 구체적인 동작을 파악할 수 있음
6. 구체적인 기능에 따라 여러가지 버전을 사용할 수 있음
7. GUI와 CLI 두 가지 인터페이스를 제공
    1. CLI를 사용하면 높은 작업 효율을 얻을 수 있음
8. GNU 도구를 자유롭게 사용 가능
>>여러 시스템으로 구성된 서버 환경을 관리하는 방법이 더 중요. 값비싼 고성능 서버 하나보다 여러 시스템을 연결해서 제공하는 서비스가 경제적이며 시스템에 장애가 발생하더라도 빠르게 복구할 수 있어 안정적이므로 리눅스 서버가 활용되기 시작

###### 우분투 설치 과정은 PASS

### 커널, 셸, 터미널
![Architecture of OS Linux](https://paperdoll.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fd1a988f4-e527-4f37-84f2-5cf57ae3d75a%2Fd7dac6a3-e415-4462-a334-dae8b0c6b403%2FUntitled.png?table=block&id=18eefd73-3489-81de-a26b-e9d0aa864f6c&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=690&userId=&cache=v2)
![Linux kernel](https://paperdoll.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fd1a988f4-e527-4f37-84f2-5cf57ae3d75a%2Fe9bd86f8-2e2d-41b2-a188-a7c7c18996fe%2FUntitled.png?table=block&id=18eefd73-3489-81ab-a86e-f3b2c45a8846&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=520&userId=&cache=v2)
- Shell(셸):  CLI환경을 통해 명령어를 입력하고 실행하는 부분 → 커널의 인터페이스
    - sh라는 표준 셸을 바탕으로 대화형 조작에 필요한 기능을 갖춘 **bash**(history, alias, ...)
    - bash위에 다양한 기능을 추가한 **zsh**
- 터미널(Terminal): 컴퓨터의 입출력만을 담당하는 전용 하드웨어
    - 현재 리눅스를 다룰 때, 소프트웨어로 구현한 터미널 에뮬레이터(리눅스, 윈도, 맥 등에서 애플리케이션으로 동작)가 사용됨

##### 커맨드 라인 사용법
- 자동완성: `tab`
- `Ctrl`+방향을 의미하는 단어의 앞글자로 커서를 이동
    - `b`는 backward,  `f`는 forward의 약자, `a`는 ahead, `e`는 end
    - `p` : 바로 전 명령으로 이동 (위쪽 방향 화살표 키와 같음)
    - `n` : 다음 명령으로 이동 (아래쪽 방향 화살표 키와 같음)
- `Ctrl` + `C` : 강제종료 후 새로운 커맨드라인 시작
- `Ctrl` + `r` : 명령이력 검색. 문자를 하나 입력할 때마다 증분하여 이력을 검색

#### 슈퍼 사용자와 일반 사용자
- 슈퍼 사용자: 관리자 권한을 가지는 특별한 사용자
    - root라는 사용자 이름을 가져서 루트 사용자라고도 불림
    - 시스템 설정 파일을 바꾸거나 새로운 애플리케이션을 설치할 수 있고, 파일에 설정된 퍼미션을 무시하고 모든 파일을 읽고 수정하고 삭제할 수 있음

- 일반 사용자: 슈퍼 사용자가 아닌 사용자
```
리눅스는 되돌리기가 어려운만큼 평소에는 일반 사용자($)로 조작하다가 반드시 필요한 상황에서만 슈퍼 사용자(#)로 조작하는 편을 권장
```

#### 사용자 전환
`su`명령어
- 일시적으로 다른 사용자로 전환할 수 있는 명령어
- 로그아웃하지 않고 다른 사용자가 될 수 있음
- 주로 슈퍼 사용자로 전환하기 위해 사용
- 일반 사용자로 먼저 로그인한 뒤에 su 명령어로 슈퍼 사용자로 전환하여 작업
- su 명령어로 슈퍼 사용자가 될 수 없음
```
프롬프트가 $에서 #으로 바뀐 상태에서 작업
```

#### 슈퍼 사용자 권한 잠시 빌려오기
`sudo` 명령어 사용
```
명령어 앞에 sudo 명령어를 사용하면 슈퍼사용자의 비밀번호를 몰라도 슈퍼 사용자의 권한을 가진 사용자임을 확인하고 빌려와 일반 사용자로도 작업할 수 있음

$ sudo cat /etc/shadow
```

### 리눅스의 파일과 디렉터리
![디렉터리란](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F54fead8e-e263-40cb-8306-ce7f95a1d6a3%2FUntitled.png?table=block&id=18eefd73-3489-8166-a1eb-e28fb03faade&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=480&userId=&cache=v2)

- 리눅스는 파일로 구성됨
- 정보(데이터)(문서, 이미지, 영상, 프로그램 등)이 파일로 보존
- 시스템을 구성하는 장치조차도 파일로 다룸
- 리눅스 커널도 파일이고 시스템 설정도 파일에 기록
- 리눅스에서는 모든 것을 파일로 다루기 때문에 파일 조작 방법을 익히는 것이 중요
- 리눅스에서는 언제나 시스템 전체에 단 하나의 트리만 가지게 됨(마운트)

### 각 디렉터리 역할
**/bin**
- 일반 사용자 및 관리자가 사용하는 명령어의 실행 파일이 배치되어 있는 디렉터리
- /bin는 특히 시스템과 관련된 중요도가 높은 명령어를 포함하고 있음

**/dev**
- 디바이스 파일이 배치되어 있는 디렉터리
- 디바이스 파일이란 디스크나 키보드 등 하드웨어를 다루기 위한 특수 파일

**/etc**
- 리눅스에서 돌아가는 다양한 애플리케이션의 설정 파일이 etc 아래에 배치됨
- 애플리케이션뿐만 아니라 리눅스 자체의 설정 파일도 이곳에 있음
- 리눅스를 운영하고 관리할 때 무척 중요한 디렉터리

**/home**
- 사용자별로 할당되는 홈 디렉터리가 배치되는 디렉터리
- 홈 디렉터리란 사용자별로 할당되는 개인용 디렉터리를 말함
- 사용자 이름이 디렉터리 이름으로 사용됨
- 예를 들어 사용자 이름이 yj라면 사용자의 홈 디렉터리는 /home/yj가 됨
- 사용자는 홈 디렉터리 안에서 자유롭게 파일이나 디렉터리를 작성해 작업할 수 있음

**/sbin**
- /bin와 비슷하게 실행 파일을 포함하는 디렉터리
- 이 디렉터리에는 관리자용 명령어가 포함되어 있음
- 예를 들어 시스템을 종료시키는 shutdown 명령어 등

**/usr**
- 설치한 애플리케이션의 실행 파일, 문서, 라이브러리 등이 이 디렉터리에 포함
- /usr 아래에는 bin, sbin, etc 등이 있어 루트 디렉터리와 구조가 비슷함

**/var**
- 변화하는(variable) 데이터를 저장하기 위한 디렉터리
- 애플리케이션 실행 중에 만들어진 데이터나 로그, 메일 등이 이곳에 저장
- /var에는 많은 파일이 기록되므로 용량이 부족해질 수도 있으니 시스템을 관리할 때 주의해야 함

### 리눅스 기본 명령어
1. 명령어 찾기
    1. `whatis` : 가장 간략, 완전히 키워드가 일치해야 가능
    2. `info` : U는 한단계 위로, Q는 Info 화면 종료
    3. `man` : 가장 상세하게 알려줌
```
$ whatis ls

$ info ls

명령어 --help

$ man ls

```
2. `ls`(목록): 현재 디렉토리의 파일과 디렉토리를 나열
```
$ ls
$ ls /usrv
```
- 인자로 여러 경로를 지정할 수 있으며 모든 경로에 대해 ls 명령어가 실행
- 경로 확장: **와일드카드 확장** 혹은 **파일 이름 글로브(glob)**
###### 명령어에 옵션 붙여서 사용
- 옵션: 명령의 행동에 영향을 미치는 행동
```
명령 [옵션] [인수1] [인수2]
$ ls -l /boot
$ ls -l /boot /usr
$ ls -a # 숨겨진 파일도 함께 출력
$ ls -F # 파일 종류 의미하는 기호 추가해 출력

# 두 개 이상 지정 시
$ ls -a -F 
$ ls -aF

# 명령어의 인자도 지정하고 옵션도 지정하는 경우
$ ls -a -F /boot
```
- `-l` 옵션:  파일 이름뿐만 아니라 파일의 속성과 상세 정보까지 함께 출력
![커맨드 라인 옵션](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F5b041248-306e-43d9-a3cf-fb91cccb99a2%2FUntitled.png?table=block&id=18eefd73-3489-8149-b640-cee725c51c0a&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=1140&userId=&cache=v2)

3. `pwd`(작업디토터리 출력): 현재 디렉터리 표시
    1. 절대 경로: 루트 디렉토리부터 해당 파일에 이르는 경로를 표시하는 것
    2. 상대 경로: 현재 디렉토리 안에 있는 file-2는 간단히 file-2로 지정(ex> ./file-2)
4. `cd`(디렉토리 변경): 현재 디렉토리 변경
5. `mkdir`(디렉토리 생성): 새 디렉토리를 생성 
    - 중간 경로의 디렉터리가 존재하지 않으면 에러가 발생
    - `-p` 옵션 사용
```
$ mkdir hello # 새 디렉토리 생성
$ cd ~/hello # 현재 디렉토리 변경
$ pwd # 현재 작업디렉토리 출력
$ cd /hello
$ pwd
```
6. `cat`(연결): 파일의 내용을 표시하거나 여러 파일을 연결
```
$ cat file.txt

$ echo hello1 >> file1.txt # hello1을 file1.txt에 append

$ cat -n file1.txt file2.txt > combined.txt (행번호 함께 출력)
```
7. `cp`(복사): 파일 또는 디렉토리를 복사
```
$ cp file1.txt file3.txt  # 원본 복사본
$ cp -r dir1 dir2
```
8. `mv`(이동): 파일 또는 디렉토리를 이동하거나 이름을 변경
```
$ mv file.txt file3.txt
$ mv file3.txt dir3/
```
- 파일 이동 시 원래 있던 곳에는 더 이상 존재하지 않음
- `-i` 옵션을 지정하면 덮어쓰기 전에 정말로 덮어쓸지 확인
9. `rm`(제거): 파일 또는 디렉토리를 삭제
```
$ rm file.txt (파일 제거)
$ rm file.txt file1.txt  (파일 여러개 제거)
$ rm *.txt
$ rm -r directory (디렉토리와 그 내용 제거)
$ rm -i *.txt
$ rm [f,h]* # 또는 rm f* h*  
# 정규식: rm [fh]* 하면 f-h 사이 모든 문자열 삭제
```
10. `rmdir`(디렉토리 제거): **비어있는 디렉토리**를 제거 
```
$ rmdir empty_directory
```
11. `touch`(터치): 새로운 빈 파일을 생성하거나 기존 파일의 타임스탬프를 업데이트
```
$ touch new_file.txt
$ touch file{1..100}
```
- 단순히 빈 파일을 만드는 용도로도 많이 사용
- 이미 존재하는 파일을 지정해도 내용이 지워지거나 하지는 않고 **시간만 변경**
12. `which`(프로그램 경로 확인)
```
$ which crontab
```
13. `whereis`(프로그램 관련 파일들 함께 확인)
```
$ whereis crontab
```
14. `less`(스크롤 표시): 파일을 스크롤과 함께 출력
```
less /etc/bash.bashrc
```
15. `grep` (글로벌 정규 표현식 출력): 파일 또는 출력에서 특정 패턴을 검색
- `|` (파이프)를 통해 앞의 명령어에서 전달된 결과물을 다음 명령어에 넘겨주고 특정 문자열을 조회해서 사용할 때 많이 사용하는 명령어
```
$ grep "search_term" file.txt
```
16. `echo` (에코): 텍스트 줄을 표시
```
$ echo "Hello, World!"
```
17. `df` (디스크 여유 공간): 디스크 공간 사용량을 표시
```
$ df -h
```
18. `du` (디스크 사용량): 파일 및 디렉토리의 디스크 사용량을 표시
```
$ du -sh /home/user/
```
19. `ps` (프로세스 상태): 현재 실행 중인 프로세스를 나열
```
$ ps aux
$ ps -ef | grep init # 실행 중인 프로세스를 모두 나열한 후 init 문자열을 담은 줄만 출력
```
20. `kill`(종료): 프로세스를 종료
```
$ kill 12345
```
21. `ln`: 링크 만들기
- 파일에 별명을 붙이는 것
- 하드링크와 소프트링크
    - **하드링크**
    1. 디스크에서 원본 파일과 **동일한 물리적 위치**를 가리키는 새 디렉토리 항목(inode)을 생성
    2. 다른 파일 시스템이나 파티션에 걸쳐 있을 수 없음
    3. 디렉토리에 대해 생성할 수 없으며 **파일에 대해서만 생성**
    4. 파일을 삭제해도 파일에 대한 **모든 하드링크가 삭제될 때까지** 디스크에서 **실제 데이터가 제거되지 않음**
    - **소프트링크**
    1. **다른 파일이나 디렉토리의 경로**를 가리키는 특수한 유형의 파일
    2. 파일과 디렉터리 모두에 대해 만들 수 있음
    3. 소프트링크된 파일을 삭제하면 실제 데이터가 아닌 **링크만 제거**
    4. 원본 파일이 삭제되면 소프트링크는 존재하지 않는 파일을 가리키는 **깨진 링크**가 됨
    5. 상대 경로를 사용하면 디렉토리를 이동하거나 이름을 바꿀 때 링크가 끊어질 수 있으므로 소스 파일 또는 디렉토리의 **절대 경로**를 사용
```
$ ln source_file hardlink # 하드링크를 생성하려면 -s 플래그 없이 ln 명령을 사용

$ ln -s source_file_or_directory softlink # 소프트링크 생성시 -s 플래그 사용
```
22. `find`: 특정 파일 혹은 특정 문자열을 포함한 파일을 출력
`tree`: 파일의 구조를 함께 출력
```
find / | grep log
tree / | grep log | less
```
23. `nano`, `vi`, `vim`, `emacs`(텍스트 편집기): 텍스트 편집기 열기
```
$ nano file.txt
$ vi file.txt
$ vim file.txt
```
24. `awk`: 파일이나 입력된 데이터 스트림에서 데이터를 처리하고 분석하는 데 매우 유용한 도구. 주로 텍스트 파일에서 특정 패턴을 찾고, 해당 패턴이 일치하는 줄을 출력하거나 수정하는 데 사용
```
$ awk '{ print $2 }' sample.txt # 특정 열을 출력
$ awk '$3 == 25 { print $0 }' sample.txt # 특정 패턴을 만족하는 행 출력
$ awk '{ sum += $3; count++ } END { print "Average age:", sum/count }' sample.txt
#  모든 사람의 평균 나이를 계산
awk 'BEGIN { print "Processing the file..." } { print $0 }' sample.txt
```
25. `visudo`: **특정 사용자**에게 **sudo 명령어**를 **허용**하는 방법

#### 셸 변수
1. 로컬변수: 선언된 셸 안에서만 사용 가능(지역적)
2. 지역변수: 현재 셸에 의해서 실행된 서브셸, 다른 프로그램 등에게까지 전달됨
```
변수명=값
$변수명
export 변수명 -- 환경변수에 등록 

echo $변수명
```

- `env`: 환경변수 보여줌
- `set`: 로컬변수, 환경변수, 함수 보여줌
- `unset 변수명`: 변수 삭제

#### Bash 설정
1. `alias`: 명령어에 별칭 붙임
```
$ alias ls="ls -F"
```
- 셸 종료시마다 사라짐

```
# 서버가 실행되면 .bashrc의 스크립트를 실행하므로 
# 여기에 적어두면 매번 시작될때마다 해당 명령어가 실행됩니다.
$ vi ~/.bashrc

# 최초 로그인시 한번만 할 개인 사용자에 대한 설정은
$ vi ~/.profile 

# 시스템 전체의 로그인 셸 사용자에게 적용되는 초기화 스크립트입니다.
$ vi /etc/profile

# 바뀐 내용을 현재에 적용
$ source ~/.bashrc
$ source /etc/profile

$ login 유저아이디  로 확인
```
2. `history`

##### 셸에서 사용되는 특수문자들
1. `*`: 와일드카드
2. `?`: 한글자 대체
3. `[]`: 대괄호 안에 있는 여러 문자 중 하나
4. `;`: 여러개 명령어를 한줄의 커맨드라인에 입력하여 순서대로 알아서 실행

#### 입/출력
1. `>`: 출력 리다이렉션. 기존 파일의 내용에 덮어씀
2. `>>`: 출력 리다이렉션. 파일에 내용 추가
3. `2>`: 에러 리다이렉션. 터미널 대신 파일에 저장해서 특정 결과 보낼 때 사용

#### Vim, Vi 에디터
![Vim, Vi 에디터](https://paperdoll.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fd1a988f4-e527-4f37-84f2-5cf57ae3d75a%2Fd04cdbcf-3f95-45c5-9414-6234c6a4a14f%2FUntitled.png?table=block&id=18eefd73-3489-814a-8233-fae7b359cf18&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=1010&userId=&cache=v2)

#### 셔뱅
- `!/bin/bash`
    - 특별한 형태의 주석 (#!)으로 아래 코드의 해석에 sh를 사용하겠다는 의미
    - 셸의 실행 명령을 전달받은 리눅스 커널은 먼저 파일의 첫 부분을 확인하고 #!가 있으면 그 뒤에 적힌 명령어를 실행
- `exit 0`: 명령어가 다 실행된 후 종료 코드를 반환하는 명령어

#### 조건문
1. if문
```
# 형식
# if [ 조건 ] # [ 조건 ] 안에서는 각 단어마다 공백을 넣어주어야 합니다.
# then
#   참일 경우 실행
# elif [ 조건2 ]
# then
#  echo "비슷한 두번째 조건을 만족합니다"	
# else
#  거짓인 경우 실행
# fi
```
![산술비교](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Ff10e104a-0e27-4ea6-8b77-054ece0578cf%2FUntitled.png?table=block&id=18eefd73-3489-8138-b7db-e6c70ea781ec&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=400&userId=&cache=v2)
![문자열 비교](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F3756602a-3c98-4831-8480-d007c46e2fc7%2FUntitled.png?table=block&id=18eefd73-3489-8103-89cd-d0b71f5a1dee&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=400&userId=&cache=v2)
![파일 조건](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F9b0f1111-e0c8-4ad9-a7d8-d20a78e54e62%2FUntitled.png?table=block&id=18eefd73-3489-8105-8eae-f01c24e6a656&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=400&userId=&cache=v2)

2. case ~ esac문
```
#!/bin/sh

echo "리눅스가 재미있나요? (yes / no)"
read answer

case $answer in
    yes | y | Y | Yes | YES)  # case1
       echo "다행입니다."
       echo "야호";; ## case문 안에서는 세미콜론을 두개 찍어서 케이스 종료를 구분합니다.
    [nN]*) #case2 - n이나 N으로 시작하는 모든단어
       echo "안타깝네요.";;
    *) # case3 - 나머지 모든 경우
       echo "어차피 도구일 뿐..."
       exit 1;;
esac
exit 0
```
#### 반복문
```
# while.sh
# true, false 
#!/bin/sh
echo "무한반복 입력을 시작합니다(b: break, c: continue, e: exit)"
while [ 1 ] ; do
 read input
 case $input in
 	b | B )
 		break ;;
 	c | C )
 		echo "continue를 누르면 while의 조건으로 돌아감"
 		continue ;;
	 	e | E )
 		echo "exit를 누르면 프로그램(함수)를 완전히 종료함"
 		exit 1 ;;
 esac;
 done
 echo "break를 누르면 while을 빠져나와 지금 이 문장이 출력됨."
 exit 0
```
```
#for.sh

#!/bin/sh

for fname in $(ls *.sh)
do
    echo "--------$fname-------"
    head -3 $fname
done
exit 0
# 현재 디렉터리에 있는 셸 스크립트 파일(*.sh)의 파일명과 앞 3줄을 출력하는 프로그램
```

#### crontab
- `cron`: 주기적이고 반복적 작업을 하기 위한 프로그램
    - OS를 시작할 때 함께 실행
    - /etc/crontab 파일을 읽어서 설정한 시작에 해당 명령어를 실행
```
ps  -ef  | grep  cron
service --status-all | grep + # 크론이 실행중인지 확인

crontab -l # 확인
crontab -e # edit -> 에디터 선택(2)
crontab -r # 삭제

* * * * * df -u > /tmp/test.log # minute hour day(month) month day(week)
```

### 파일시스템
- 파일 종류
    1. 일반 파일: 텍스트 파일, 실행파일, 이미지 파일 등 주로 데이터 저장
    2. 디렉토리
    ![디렉토리 계층구조](data:image/png;base64,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)
    - 리눅스에선 디렉토리도 파일로 취급

    3. 심볼릭 링크(소프트 링크)
    - 원본 파일 → 다른 파일명으로 지정한 것
    4. 장치파일
    - 하드디스크, 키보드 같은 장치

#### 리눅스 계정 추가
- 리눅스 계정은 루트유저/일반유저/System유저(관리자)로 구분
- 0번 uid가 root, 1000부터가 일반(1~999 사이는 시스템이 사용하는 계정에게 할당되는 번호)

1. 사용자 추가하기
- `useradd`: 단순 추가, `adduser`: 인터랙티브 모드로 추가

2. 사용자 그룹 만들기
- GROUP을 먼저 생성 후 user 넣기
```
# 그룹 생성
$ groupadd  lastday

# 그룹 삭제
$ groupdel lastday
```
### 파일 소유자
1. 파일 및 디렉토리의 권한 변경
![파일 소유자](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdna%2FlCFFd%2FbtrxwzpDJWZ%2FAAAAAAAAAAAAAAAAAAAAACd-__6EuIdidA0yuWWuPGcp2nD4gAA5qPaJKHLUjlgf%2Fimg.png%3Fcredential%3DyqXZFxpELC7KVnFOS48ylbz2pIh7yKj8%26expires%3D1756652399%26allow_ip%3D%26allow_referer%3D%26signature%3D4YyQsqutvoV9USyRLnU2XS84jpg%253D)

2. `chown`(소유자 변경): 파일 또는 디렉토리의 소유자 및 그룹 변경
```
$ chown new_owner:new_group file.txt


$ ll
$ sudo chown root test1 # 소유자 변경
$ ll
$ sudo chown -R user01 test1/ # 디렉토리의 경우
$ sudo chgrp team2 test1 # 그룹 변경
$ sudo chown user03.team2 test1 # 소유자와 그룹 모두 변경
```

3. 수치 모드
![수치 모드](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fdbb76d9f-2d6b-41da-8ceb-a7f567155849%2FUntitled.png?table=block&id=18eefd73-3489-8147-9ded-e333342f36e3&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=720&userId=&cache=v2)
![퍼미션 수치](https://paperdoll.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fc2df8d4f-cb48-4304-b4e8-c06dd9787f48%2FUntitled.png?table=block&id=18eefd73-3489-8141-8776-d5da3a9d600c&spaceId=d1a988f4-e527-4f37-84f2-5cf57ae3d75a&width=840&userId=&cache=v2)

#### 소프트웨어 및 파일 관리
1. `dkpg`
```
$ dpkg  -l # 시스템에 설치된 모든 명령어 확인

$ dpkg  -l | grep net-to # 특정 단어를 가진 패키지 조회
```

2. `apt`
    1. `apt-get`: 패키지 설치, 제거, 업데이트 등 패키지를 관리하는 데 사용되는 명령어
    2. `apt-cache`: 패키지 정보 조회와 검색에 사용되는 명령어
```
# apt-get
- 패키지 설치: `sudo apt-get install vim`
- 패키지 제거: `sudo apt-get remove vim`
- 패키지 목록 업데이트: `sudo apt-get update`

# apt-cache
- 패키지 검색: `apt-cache search editor`
- 패키지 정보 조회: `apt-cache show vim`
- 패키지 의존성 확인: `apt-cache depends vim`
- 캐시 디렉토리 용량 조회: `du -sh /var/cache/apt/archives/`
```
##### 캐시 삭제 명령어
1. `apt-get clean`: 디렉토리의 모든 패키지 캐시 파일(.deb)을 삭제하여 디스크 공간을 확보
```
sudo apt-get clean
```
2. `apt-get autoclean`: 더 이상 다운로드할 수 없는 오래된 패키지 파일만 삭제
```
sudo apt-get autoclean
```

#### 우분투에서의 파일 관리
1. tar
```
$ tar -cf test.tar *
```
- 묶어주는 것일 뿐, 압축의 개념은 아니므로 **용량**이 줄어들지는 않음

|아카이브 생성| -cvf |copy, verbose, file|
|:---:|:---:|:---:|
|아카이브 확인| -tvf |table of contents, verbose, file|
|아카이브 해제| -xvf |extract, verbose, file|

2. tgz
- tar로 묶고 gzip으로 압축
```
gzip 2day.txt # 압축을 하면 2day.txt는 사라지고 압축된 파일만 생깁니다.
gzip -d 2day.txt.gz # -d : decompress
gzip -k 2day.txt # 원본파일은 남겨두고 압축
```

### 다른 서버에서의 접속, 파일 주고받기
1. SSH(Secure SHell): 네트워크 상의 **다른 컴퓨터**에 로그인하거나 원격 시스템에서 **명령을 실행**하고 다른 시스템으로 **파일을 복사**할 수 있도록 해주는 응용 프로그램 또는 그 프로토콜

2. SCP(Secure Copy) 
- 원격지에 있는 파일과 디렉터리를  보내거나 가져올 때 사용하는 파일 전송 프로토콜