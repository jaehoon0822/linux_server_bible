# 서비스 관리

<br />

## System 구성요소 이해

<br />

<table>
	<thead>
		<tr>
			<th colspan="2">Systemd 구성요소</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="2"> Systemd 유틸리티</td>
		<tr>
		<tr>
			<td> Systemd 데몬</td>
			<td> Systemd 타겟</td>
		<tr>
		<tr>
			<td colspan="2"> Systemd 코어</td>
		<tr>
		<tr>
			<td colspan="2"> Systemd 라이브러리</td>
		<tr>
		<tr>
			<td colspan="2"> 리눅스 커널</td>
		<tr>
	</tbody>
<table>

<br />
	
### 리눅스 커널

<br />

>
***" 서비스데몬 Systmd 를 사용하기 위해서는 먼저 리눅스 커널에서 이 서비스를 지원하기 위한 옵션이 활성화 되어야 한다. "*** 
>

<br />

| 옵션 | 설명 |
| :--- | :--- |
| cgroup( control group ) | PID대신 프로세스를 추적 |
| autofs | 파일시스템을 자동으로 마운트하게 지원 |
| dbus | 애플리케이션 간 일대일 통신을 지원 |

<br />

### Systmed 라이브러리

<br />

> ***" 커널에서 Systemd 를 지원하기 위한 옵션이 활성화 되면 libnotify, libudev, libpam, libcap, tcpwrapper, libaudit 같은시스템 라이브러리가 설치돼야 사용할 수 있다. "***
>

<br />

### Systemd 코어

<br />

> ***" Systemd 코어는 service,socket, mount 와같은 모든 System Unit 을 관리할 뿐 아니라 모든 로그 데이터를 저장하는 역할을 하는데, systemctl 과 같은 Systemd 유틸리티가 이 코어 부분을 관리할 수 있다. "***
>

<br />

### Systemd 데몬과 Target

<br />

> ***" Systemd 서비스를제공하는 데몬으로서 systemd, journald, networkd 등이 사용되며, 시스템 실행 모드 Target 으로서 multi-user, grphical, reboot, basic, shutdown 등이사용된다 "***
>

<br />

### Systemd 유틸리티

<br />

> ***" Systemd 가 제공하는 모든 기능을 사용자가 실제로 사용 가능케 하는 유틸리트로서 systmectl, journalctl, notify, analyze 등이 사용된다. "***
>

<br />

## Systemd 부팅과정

<br />

### SysV Init 부팅과정 && Systemd 를이용한 부팅과정

<br />

p146 ~ p147 을 살펴보자.

<br />

## Systemd 명령어와 Unit 이해

<br />

### Systemd Unit 의 이해

<br />

> ***" Systemd Unit 파일은서비스 시작에 필요한 모든 내용을 기록한 설정파일을 의미하며, 이 파일들은 모두 특정 디렉토리에 저장된다. "***
>

<br />

> ***systemctl start httpd.service***
>

<br />

httpd.service 이 Unit file 이며, service 부분을 Unit type 이라 부른다.

<br />

>*** 이 Unit 은 결국 서비스 시작이 정의된 파일을 가리킨다.***
>

<br />

#### Unit file 이 저장된 디렉토리

<br />

| 디렉토리 | 설명 |
| :---: |:--- |
| /run/systemd/system | Systemd 가 실행 시에 생성되는 Systemd Unit 파일을 저장하는 버퍼 디렉토리, 부팅 이후 정보만 저장, 종료후 정보 삭제됨 |
| /etc/systemd/system | 시스템 관리자가 수동으로 생성하거나 관리하는 Systmed Unit 파일이 저장되는 디렉토리 |

<br /> 

### Unit 의 유형

<br />

| Unit type | 설명 |
| :---: | :--- |
| service | 시스템 서비스를 위해 사용되는 유닛, 시작과 중지 명령을 이용해 관리 |
| target | Systemd Unit 이 한 그룹으로 이뤄진 경우이며, 다른 Unit 이 그 상태를 변경할 때 동기화 기능을 제공 |
| automount | 자동으로 마운트 지점을 설정 |
| device | 리눅스 커널이 인식하는 장치 파일 |
| mount | /etc/fstab 에 정의된 파일 시스템을 마운트하기 위해 사용되는 지점 |
| path | 파일 시스탬 내의 파일이나 디렉토리를 위해 사용 |
| scope | 외부에서 생성된 시스템 프로세스 관리를 위해 사용 |
| slice | Control Group 과 관련, 시스템의 자원들이 어느 프로세스에 제한이 되거나 할당되게 허용하는 역할 |
| snapshot | systemctl snapshot 에 의해 자동생성, 시스템의 변경 이후 현재의 상태를 다시 구성하게 허용하는 역할 |
| socket | 네트워크와 프로세스 간 통신에 사용되는 소켓, .service 파일과 항상 관련있다. |
| swap | 스왑 장치나 스왑 파일에 사용 |
| timer | Cron 처럼 지정된 일정에 따라 Unit 활성화를 위해 Systemd 가 사용하는 타이머 |

<br />














