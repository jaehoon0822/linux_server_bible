# 사용자 관리

<br />

## 사용자 및 그룹관리 파일

<br />

| file | 설명 |
| :---: | :---: |
| /etc/passwd | 사용자의 기본 정보를 저장하는 파일 |
| /etc/shadow | 사용자의 패스워드 관련된 정보를 저장하는 파일 |
| /etc/group | 그룹 및 그룹에 속한 사용자의 내용을 저장하는 파일 |
| /etc/gshadow | 그룹 사용자의 패스워드가 저장된 파일 |

<br />

## 사용자 생성 환경 파일과 디렉토리

<br />

| file 및 디렉토리 | 설명 |
| :---: | :---: |
| /etc/skel | 사용자 생성 시에 자동으로 사용자의 홈 디렉토리에 복사되는 파일과 디렉토리를 가진 디렉토리 |
| /etc/defalut/useradd | 사용자 생성에 사용되는 기본 내용을 정의한 파일 |
| /etc/login.defs | 암호화된 사용자의 패스워드 파일을 구성하는 요소들이 포함된 파일 |

<br />

#### /etc/default/useradd

| keyword | 설명 |
| :---: | :---: |
| GROUP=100 | User 그룹아이디. 사용자 생성시 그룹지정 없으면 사용자 이름과 동일한 그룹이 생성되는 것을 피하고 싶은 경우 -n 옵션을 사용하면 사용자는 기본적으로 이 그룹에 속하게 된다. |
| HOME=/home | 사용자 생성 시 사용자의 홈 디랙토리가 생성될 디렉토리를 정의한다. |
| INACTIVE=-1 | 패스워드 만료 후 계정이 비활성화 되는 날짜를 의미한다. -1 은 사용하지 않음, 0 은 패스워드가 만료되면 계정 비활성화 된다. | 
| EXPIRE= | 계정의 만료 날짜를 의미.YYYY-MM-DD 로 설정. |
| SHELL=/bin/bash | 사용자 생성시 사용할 shell 을 지정 | 
| CREATE\_MAIL\_SPOOL=yes | 사용자 생성 시 사용자의 메일을 저장할 파일을 생성할지 정의 -> 'yes' 면 /var/spool/mail/linux 파일에 사용자의 메일이 저장 |

<br />

#### /etc/login.defs 

<br />

| keyword | 설명 |
| MAIL\_DIR | 사용자 메일이 저장되는 디렉토리 정의. -> /var/spool/mail 을 사용 |
| PASS\_MAX\_DAYS | 패스워드 변경 없이 사용할 수 있는 최대 날짜 수를 정의. 기본값으로 99999일을 사용 |
| PASS\_MIN\_DAYS | 패스워드 변경 후 그 패스워드를 사용해야 하는 최소 날짜 수를 의미. 기본값은 0은 제한없음을 의미 |
| PASS\_WARN\_AGE | 패스워드 변경 전 경고 메세지를 보내는 날짜 수 | 
| UID\_MIN | 사용자 생성 시 할당되는 최저 UID, 기본값은 1000 |
| UID\_MAX | 사용자 생성 시 갖게 되는 최대 UID, 기본값은 60000 | 
| SYS\_UID\_MIN, SYS\_UID\_MAX | 시스템 사용자에게 사용되는 최소, 최대 UID 다. | 
| CREATE\_HOME | 사용자 생성시 홈 디렉토리를 만들지 결정한다. |
| UMASK | 사용자 생성 시 홈 디렉토리 생성 시 이 디렉토리가 갖게 되는 디렉토리 권한을 의미 |
| USERGROUPS\_ENAB | 사용자 제거시 그 사용자의 그룹데 다른 사용자가 없다면 그 그룹도 삭제할 것인지 정의. 기본값 yes. |
| ENCRYPT\_METHOD | 패스워드를 암호화하는 알고리즘 정의 |

<br />

### useradd/adduser

<br />

#### useradd 옵션

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -u | UID 지정 |
| -g | 그룹지정 |
| -G | 보조그룹 |
| -s | shell 지정 |
| -d | 사용자 홈 디렉토리 지정 |
| -e | 계정 만료 날짜. YYYY/MM/DD |
| -k | skel directory 지정 |
| -m | --creaet-home 만약 홈 디렉토리가 존재하지 않는다면, 홈 디렉토리를 만든다. 파일 그리고 디렉토리들은 skel 디렉토리안에 포함된 파일 및 디렉토리를 카피할 수 있다.  ( -k 옵션과 함께 정의할수 있다. ) |
| -c | --comment 일반적으로 로그인에 대해 짧게 설명한다. |

<br />

### usermod

<br />

#### usermod 옵션

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -L | 임시로 잠금 상태로 만드는 옵션 |
| -U | 임시 잠금 상태를 해제하는 옵션 |
| -u | UID 변경 |
| -g | GID 변경 |
| -e | 계정만료 날짜 변경 -> YYYY|MM|DD OR ""( 빈 문자열이면 만료 날짜 해제 ) |

<br />

### userdel 

<br />

#### userdel 옵션

<br />

| 옵션 | 설명 |
| :---: | :---: |
| 옵션없으면 | 홈 디렉토리는 남기고 계정삭제 |
| -r | --remove 홈 디렉토리까지 삭제 |
| -f | --fource 로그인 상태에서도 계정 삭제 |

<br />

### chown

<br />

파일이나 디렉토리의 소유권자를 변경하는 명령어

<br />

chown user:group 

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -r | --recursive 하위 디렉토리와 파일의 소유권자까지 변경 |

### /etc/nologin

<br />

root 를 제외한 나머지 계정 접근금지   
처음에는 파일이 존재하지 않으므로, 새롭게 생성해야 한다.

<br />

### 사용자 정보 모니터링

<br />

#### 사용자 정보를 모니터링해 저장하는 파일 목록

<br />

| file | 셜명 |
| :---: | :---: |
| /var/run/utmp | 각 사용자의 현재 로그인 정보를 기록, 명령어 who 나 w 를 이용해 정보확인가능 |
| /var/log/wtmp | 사용자의 모든 로그인과 로그아웃을 기록하는 파일, 명령어 last 를 이용해 확인 가능 |
| /var/log/btmp | 사용자 로그인 실패를 기록하는 파일, 명령어 lastb 로 확인 가능 |
| /var/log/lastlog | 사용자의 가장 최근 로그인 정보를 기록하는 파일,  명령어 lastlog 로 확인 가능 |
| /var/log/secure | 인증 및 권한 부여에 대한 정보를 저장, ssh 관련된 모든 정보를 기록하며 텍스트 파일로 저장되기에 vim 으로 확인가능 |

<br />

> pts 는 psuedo terminal slave 는 xterm 이나 ssh 로 접속한 경우 사용된 가상 터미널 접속을 의미
>

<br />

## 리눅스 패스워드 관리

<br />

### 두 파일의 구조 분석

<br />

#### /etc/passwd ( 구분자= : )

| name | x | 1003 | 1003 | :: | /home/name | /bin/zsh |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| loginname | password | UID | GID | GECOS | home directory | shell |

<br />

| field name | 설명 |
| :---: | :---: |
| loginname | 사용자 이름 |
| password | 패스워드를 나타내는 field |
| UID | UserID, 일반 사용자의 경우 1000 부터 60000까지 자동으로 할당 |
| GID | GroupID, 1000 부터 60000 까지 자동할당. 기본적으로 사용자의 이름과 동일한 그룹이 생성. 피하고 싶다면 useradd -n 옵션 사용. 그려면 user 그룹에 속하게 된다. |
| GECOS( General Electric Comprehensive Operating System ) | 사용자 이름 및 기타정보, 이메일이나 전화번호 또는 직책등을 기록하는 공간. useradd -c 옵션을 사용한다.  |
| home directory | 사용자 home directory |
| shell | 사용자 지정 shell |

<br />

#### /etc/shadow 파일 구조

<br />

| name | $6$asdfa | 16582 | 0 | 99999 | 7 | :: | 16800 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| loginname | EncryptedPassword | LastPasswordChange | Minimum | Maximum | warn | Inactive | Expire |

<br />

### pwdconv 와 pwunconv 사용

| 명령어 | 설명 |
| :---: | :---: |
| pwunconv | /etc/passwd 에서 암호화된 password 를 확인가능. 이때 /etc/shaodw 를 찾아도 존해하지 않은 디렉토리라고 나온다. |
| pwconv | /etc/passwd 에 password 부분이 x 로 표시되며, 암호화된 password 를 알아보기 위해서는 /etc/shadow 를 찾아보아야 한다. |

<br />

> ***" 파일 /etc/passwd 는 누구나( other ) 읽을 수 잇는 권한을 갖고 있다. 권한 rw-r--r-- 에서 마지막 r-- 가 이부분을 의미한다. 즉 누구나 이파일에 접근해 암호화된 부분을 읽은 후에 패스워드 크래킹을 시도할 수 있어서 오직 root 만 접근이 가능한 ( -r-------- ) /etc/shadow 파일에 암호화된 부분을 분리해서 저장한 것이다. "*** 
>

이부분은 p69 를 보도록 하자. 자세히 설명 잘 되어있다.

## 리눅스 패스워드 에이징 사용

<br />

> ***" 패스워드 에이징이란 리눅스 시스템에서 패스워드의 수명을 결정하는 방법을 의미한다. "***
>

<br />

| 명령어 | 설명 |
| :---: | :---: |
| chage | 페스워드 에이징을 수정 |

<br />

#### chage 옵션

| 옵션 | 설명 |
| :---: | :---: |
| -l [username] | --list 사용자들의 기본정보를 제공 | 
| -m | --mindays 암호 최소 사용 날짜 설정 |
| -M | --Maxdays 암호 최대 사용 날짜 설정 |
| -W | --Warndays 경고날짜 설정 |
| -I | --Inactive 암호 만료후 비활성(잠금)까지의 기간 |
| -E | --Expiredate 계정 만료 기간 |

## 그룹 관리

<br />

### 리눅스 그룹의 몇 가지 특징

* 한 명의 사용자는 한 개 이상의 그룹의 맴버가 될 수 있다.   
* 여러 개의 그룹에 속한 사용자는 현재 그룹에서 그 사용자가 속한 다른 그룹으로의 변경이 패스워드 없이 가능하다.
* 특정 그룹에 속한지 않든 사용자를 그 그룹으로 변경하려면 패스워드가 필요하며, 그 그룹은 미리 패스워드를 생성한 후 사용자에게 패스워드를 부여하면 그 그룹으로의 변경이 가능하다.
* 한 명 또는 여러 명의 사용자는 특정 그룹의 그룹 관리자가 될 수 있다.
* 그룹 관리자는 그룹의 패스워드를 생성, 변경, 삭제할 수 있으며, 그룹에 사용자를 축하거나 삭제도 가능하다.

<br />

이 내용은 p72 에 적힌 내용이다.

<br />

### 리눅스 그룹의 종류

<br />

| :---: | :---: |
| 시스템 그룹 | 시스템 사용자와 마찬가지로 시스템에 설치되는 애플리 케이션을 위해 사용하는 그룹. |
| 일반 그룹 | 일반 사용자를 관리하기 위해 사용되는 그룹 |

<br />

| :---: | :---: |
| 기본 그룹 | 사용자는 반드시 한 개 이상 그룹의 맴버가 되야 하며, 이 그룹은 /etc/passwd 파일에 GID 가 표시되고, 파일과 디렉토리의 권한에도 참여 |
| 보조 그룹 | 사용자는 기본 그룹이외에 다른 그룹의 사용자가 될 수 있다. /etc/group 파일에 특정 그룹의 사용자로 나타나고, 파일과 디렉토리의 권한에 참여하지 못한다. |
| UPG( User Private Group ) | 사용자가 생성될 때마다 기본적으로 그 사용자와 같은 이름으로 생성되는 그룹을 칭하는 이름 |

<br />

| 명령어 | 설명 |
| :---: | :---: |
| id | 현재 사용자의 uid, gid, groups 에 대한 정보 제공 |
| groups | 현재 사용자의 groups 에 대한 정보 제공 |

<br />

#### 그룹 관리에 사용되는 파일

<br />

| 파일 | 설명 |
| :---: | :---: |
| /etc/group | 그룹 정보를 가진 파일 |
| /etc/gshadow | 그룹의 패스워드 정보를 가진 파일 |

<br />

* /etc/group 

<br />

| :---: | :---: | :---: | :---: |
| mail | x | 12 | postfix,exim |
| group name | password | GroupID | Usre List |

<br />

* /etc/gshadow

<br />

| :---: | :---: | :---: | :---: |
| mail | ! | name | postfix,exim |
| group name | Encrypted Password | Administrators | Usre List |

<br />

### 명령어를 사용한 리죽스 그룹 관리

<br />

#### gropadd

<br />

| 명령어 | 설명 |
| :---: | :---: |
| groupadd | 그룹 생성 |

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -g | GID 부여 |

<br />

#### groupmod

<br />

| 명령어 | 설명 |
| :---: | :---: |
| groupmod | 그룹 정보 수정 |

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -g | GID 수정 |
| -n | --new 이름 수정 |

<br />

#### groupdel

<br />

| 명령어 | 설명 |
| :---: | :---: |
| groupdel | 그룹 삭제 |

<br />


#### gpasswd

<br />

| 명령어 | 설명 |
| :---: | :---: |
| gpasswd | 그룹 비밀번호 부여 |
| newgrp | 기본 그룹을 변경 |

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -A | --Administrator 그룹 관리자 입명 -> gpasswd -A name groupName |
| -a | --add 그룹 맴버 추가 |
| -d | --delete 그룹 맴버 삭제 |
| -R | --restrict 특정 그룹으로 변경을 허용치 않음, 제대로된 password 입력에도 invalid password 메세지 발생 |
| -r | --remove-password 패스워드 삭제 |

<br />

#### newgrp 를 사용한 그룹변경

<br />

| 명령어 | 설명 |
| :---: | :---: |
| newgrp | 기본 그룹을 변경 |

<br />

| 옵션 | 설명 |
| :---: | :---: |
| -g | 로그아웃 하더라도 변경된 기본 그룹 유지 |

<br />

#### grpconv 와 grpunconv 

<br />

| 명령어 | 설명 |
| :---: | :---: |
| grpconv | /etc/group 의 password 부분이 암호화된 password 를 보여준다. 하지만 /etc/gshadow 는 존재하지 않게된다. |
| grpunconv | /etc/group 의 password 부분이 x 로 변경. /etc/gshaodw 에 접근하여 확인가능 |

<br />

#### 파일 무결성 검사 

<br />

| 명령어 | 설명 |
| :---: | :---: |
| grpck | group file 의 무결성 검사 |
| pwck | password 파일의 무결성 검사 |

<br />

## Sudoers 파일을 이용한 root 권한 부여

<br />

### visudo 를 이용한 /etc/sudoers 파일 편집 

<br />

| 명령어 | 설명 |
| :---: | :---: |
| visudo | /etc/sudores 파일을 열어 수정 |

자세한건 p82 를 참고하자.

<br />



<br />
