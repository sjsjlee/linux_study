# 리눅스 기본 

shutdown 명령

- shutdown -P : 전원끄기
- shutdown -r : 재부팅
- shutdown -c : 취소
- shutdown -k : 메세지 전송(실제종료x)
- shutdown -h :
- shutdown -s-t 60 : 1분후 꺼짐
- shutdown -s-t 600 : 10분후 꺼짐

### 자동완성과 히스토리

- 자동완성과 도스키 기능
    - 터미널에서 방향키 위아래 누르면 이전에 실행했던 명령 나옴
    - history : 기존에 사용했던 명령 보기
    - hitory -c : 저장되었던 명령 모두 삭제
    - tab : 자동완성키
    

### 리눅스에서 자주 사용되는 에디터

- gedit
    - 한영전환 : shift+space
- vi
    - :q - 종료
        - 이렇게 작동하는 것을 ex 모드, 라인명령모드라고 부름
    - I, A : insert 모드
    - ESC : escape
    - 저장(w), 종료(q), 취소(i)
    - !(무시하고 종료)
    - U : undo 기능(돌아가기)
    - .swp : 비정상종료된 파일명
    
    
    ### 리눅스 기본 명령어
    
    - ls
        - list 약자, windows 'dir'과 같은 역할
        - 해당 디렉터리에 있는 파일의 목록 나열
        - ls -a
            - 현재 디렉터리의 목록(숨김파일 포함, .txt 파일 보려면)
        - ls -l
            - 현재 디렉터리의 목록
        - ls *.cfg
            - 확장자명 cfg인 목록
        - ls -l /etc/sysconfig/a*
            - ~디렉터리에 있는 목록중 앞글자 a인 것
        - ls -ald D*
            - D로 시작하는 모든 파일 들어가지 않고 목록만 보여줌
        - ls D?
            - D로 시작하고 문자 하나만 붙어있는 것
        - ls . : 현재 디렉터리
        - ls .. : 부모 디렉터리
        - ls ../.. : 루트 디렉터리
    - cd
        - change directory, 디렉터리를 이동
        - ~ : 홈디렉터리
        - .. : 부모디렉터리
        - cd ../etc/sysconfig : 현재디렉토리의 상위 디렉토리로 이동한 후 /etc/sysconfig로 이동
    - pwd
        - 현재 디렉터리의 전체 경로 출력
    - rm
        - 파일, 디렉터리 삭제 - 권한있어야함
        - rm -i abc.txt : 정말 삭제할지 확인 메시지
        - -f : 삭제시 확인하지 않고 바로 삭제
        - -r : 해당디렉터리 삭제
        - -rf : 해당디렉터리 확인하지 않고 강제 삭제
    - cp
        - cp abc.txt cba.txt
            - abc.txt를 cba.txt라는 이름으로 바꿔서 복사
        - -r : 디렉터리 복사
    - touch
        - 크기가 0인 새파일 생성
        - 이미 파일존재한다면  최종수정시간 현재시간으로 변경
        - 시간 없는 파일에 시간 추가 가능
    - mv
        - 파일 디렉터리 이름 변경하거나 다른디렉터리로 옮길 때
    - mkdir
        - 새로운 디렉터리 생성
        - mkdir abc
            - 현재 디렉터리 아래에 /abc 디렉터리 생성
        - mkdir -p /def/fgh
            - 부모디렉터리 없으면 자동생성, parents의 약자
    - cat
        - 파일 내용 화면에 보여줌
        - cat test.txt test2.txt test3.txt > alltest.txt
            - 한파일로 합쳐서 파일 보여줌
    - head, tail
        - 파일의 앞 10행, 마지막 10행 출력
        - head -3 : 앞 3행 출력
        - tail -5 : 마지막 5행 출력
    - more
        - 텍스트 파일 페이지 단위로 화면 출력
        - space bar 누르면 다음 페이지 이동, B누르면 앞페이지, Q누르면 종료
        - more +10 test.txt
            - 10행부터 보여줌
        - more alltest.txt = cat alltest.txt | more
    - less
        - more과 비슷하지만 기능확장
        - more 키도 사용가능하며, pageup&pagedown 사용 가능
    - file
        - 해당 파일이 어떤 종류의 파일인지 표시
        - dvd장치 - block special
        - 텍스트 파일 - 아스키파일
    
    ## 사용자관리와 파일 속성
    
    ### 사용자와 그룹
    
    - 리눅스는 다중 사용자 시스템
    - vi /etc/passwd
        - 사용자이름:암호:사용자ID:사용자소속그룹ID:전체이름:홈디렉터리:기본셀
        - 암호는 x로 표시
            - /etc/shadow 파일에 비밀번호 지정되어 있음
    - vi /etc/group
        - 사용자이름:암호:그룹id:그룹에속한사용자이름
            - 그룹에 속한 사용자이름은 참조로 사용된다, 아무것도 써있지 않다고 해서 그룹에 소속된 사용자가 반드시 없다는 뜻 아님
    
    ### 사용자와 그룹 관련 명령어
    
    - useradd
        - 새로운 사용자 추가
        - /etc/passwd, /etc/group, /etc/shadow에 새로운 행 추가
        - -u : 사용자 id 지정
        - -g : 그룹 지정
        - -d : 홈디렉터리 지정
        - -s : 기본 셸 지정
    - passwd
        - 사용자 비밀번호 지정하거나 변경
    - usermod
        - 사용자 속성 변경
        - -g : 그룹변경
    - userdel
        - 사용자 삭제
        - -r : 홈디렉터리까지 삭제
    - chage
        - 사용자 암호 주기적으로 변경
        - -l : 설정된 사항 확인
        - -m : 사용해야하는 최소 일자
        - -M : 사용할 수 있는 최대 일자
        - -E : 만료날자
        - -W : 경고기간
    - groups
        - 사용자가 소속된 그룹 보여줌
    - groupadd
        - 새로운 그룹 생성
        - -g : 그룹id 지정
    - groupmod
        - 그룹 속성 변경(바람직하지 않음)
        - -n : 이름변경
    - groupdel
        - 그룹 삭제
    - gpasswd
        - 그룹 암호 설정하거나 그룹 관리를 수행
        - -A :  관리자 지정
        - -a : 사용자로 추가
        - -d : 사용자 제거
        - !! : 암호지정되어있지 않다는 표시임

## 파일압축과 묶기

### 파일 압축

- 리눅스 압축파일 확장명 : xz, bz2, gz, zip, Z 등
- 예전에는 주로 gz 사용, 최근에는 압축률이 더좋은 bz2, xz 사용
- xz : 확장명 xz로 압축하거나 풀어줌
    - xz 파일이름
        - 파일이름.xz인 압축파일로 만들어줌
    - xz -d 파일이름.xz
        - decompress(압축해제)
        - 파일이름.xz 압축파일을 일반파일 파일이름으로 만들어줌
    - xz -l *.xz
        - list
        - *.xz 압축파일의 파일목록과 압축률 등 표시
    - xz -k *.xz
        - keep
        - 압축후 기존파일 삭제하지 않고 그대로 둠
- bzip2 : bz2 압축하거나 풀어줌
    - bzip2 파일이름
    - bzip2 -d 파일이름.bz2
- bunzip2 : bz2 압축풀어줌
    - bzip2 -d와 동일
- gzip : 확장명 gz로
- gunzip : 확장명 gz의 압축 풀어줌
    - gzip -d 파일이름.gz 와 동일
- zip : 윈도우즈와 호환되는 확장명 zip 압축하거나 풀어줌
    - zip 생성할파일이름.zip 압축할파일이름
        - 압축할 파일이름 '생성할파일이름.zip'으로 만듦
- unzip : zip 압축 풀어줌
    - unzip 압축파일.zip

### 파일묶기

- windows 압축프로그램이 '파일압축'과 '파일묶기' 한꺼번에 해줌
    - aaa+bbb= ccc.zip
- 리눅스는 파일압축과 파일묶기 원칙적으로 별개의 프로그램으로 실행
- 명령어는 tar, 묶인 파일의 확장명도 tar
- tar
    - 확장명 tar로 묶음 파일 만들거나 묶음을 풀어줌
    - 동작
        - c : 새로운 묶음 만듦
        - x : 묶인 파일 풀어줌
        - t :경로확인
        - C : 지정된 디렉터리에 압축풀어줌, 지정하지 않으면 묶을 때와 동일한 디렉터리에 묶음 풀림
    - 옵션
        - f(필수) : 묶음파일이름 지정, 테이프 장치 백업 기본
        - v : visual의 의미 파일 묶이거나 풀리는 과정 보여줌(생략가능)
        - J : tar+xz
        - z : tar+gzip
        - j : tar+bzip2
    - 사용예
        - tar cvf my.tar /etc/sysconfig → 묶기,과정, 필수
        - tar cvfJ my.tar.xz /etc/sysconfig → 묶기, 과정, 필수, xz파일
        - tar cvfz my.tar.gz
        - tar cvfj my.tar.bz2
        - tar tvf my.tar → 파일확인
        - tar xvf my.tar →파일확인하면서 풀기(현재디렉토리에 풀림)
        - tar Cxvf newdir my.tar → newdir에 tar  풀기
        - tar xfJ my.tar.xz → xz 압축해제+tar 풀기
        - tar xfz my.tar.xz → gzip 압축해제+tar풀기
        - tar xfj my.tar.bz2 → bzip2 압축해제+tar 풀기

### 파일위치검색

- find 경로 옵션 조건 action
    - 옵션
        - -name, -user(소유자), -newer(전,후), -perm(허가권), -size(크기)
    - action
        - -print(기본값), -exec(외부 명령 실행)
            - exec → 발견하자마자 수행
    - 기본 사용 예
        - find /etc -name "*.conf" → /etc 디렉터리 하위에 확장명이 *.conf인 파일 검색
        - find /home -user centos → /home 디렉터리 하위에 소유자가 centos인 파일 검색
        - find ~ -perm 644 →현재 사용자 홈디렉터리 하위에 허가권 644인 파일 검색
        - find /usr/bin -size +10k -size -10k → 디렉터리 하위에 파일크기가 10kb~100kb 파일 검색
    - 고급사용예
        - find ~ -size 0k -exec ls -l { } \;
            - 현재 사용자 홈디렉터리 하위에 파일크기 0인 파일 목록 상세 출력
        - find /home -name "*.swp" -exec rm { } \;
            - /home 디렉터리 하위에 ".swp"인 파일 검색
            - -exec \; : 외부 명령어의 시작과 끝 표시
            - find 명령어의 실행결과인 swp 파일이 rm 명령으로 실행됨, 즉 파일 삭제됨
            - 검색후→삭제
- which 실행파일이름
    - PATH에 설정된 디렉터리만 검색
    - 절대경로를 포함한 위치 검색
    - 바이너리 파일의 경로명만 보여줌
- whereis 실행파일이름
    - 실행파일 및 소스, man 페이지 파일까지 검색
    - 꼭 실행파일 아니어도 man 페이지 파일도 가능함
- locate 파일이름
    - 파일목록 데이터베이스 검색
    - 매우빠르고 유용하지만, updatedb 명령을 1회 실행해야 사용가능함
    - updatedb 이후 설치된 실행파일 찾을 수 없음
    

## 파이프, 필터, 리디렉션

- 파이프
    - 2개의 프로그램 연결하는 연결 통로
    - '|' 사용함
    - ls -l /etc | more
    - 표준출력 : 이전명령출력→다음명령입력
- 필터
    - 필요한 것만 걸러주는 명령어
    - grep, tail, wc, sort, awk, sed 명령어
    - ps -ef | grep bash
        - ps -ef : 모든 프로세스 번호 출력
        - bash 라는 글자가 들어간 프로세스만 출력
    - rpm -qa | grep dnf
        - 설치된 패키지중 dnf가 들어간 패키지 출력
        - rpm -qa dnf 명령 실행하면 → dnf-conf 등은 출력 x
- 리디렉션
    - 표준입출력 방향 변경
    - 표준입력(키보드), 표준출력(모니터) → 이를 파일로 처리하고 싶을 때
    - ls -l > list.txt
        - ls -l 명령 결과 화면에 출력하지 않고 list.txt 파일에 저장
        - 만약에 있으면 덮어씀
    - ls -l >> list.txt
        - 기존내용에 이어서씀
    - sort < list.txt
        - list.txt 파일 정렬해서 화면에 출력
    - sort < list.txt > out.txt
        - list.txt 파일 정렬해서 out.txt 파일에 쓴다
