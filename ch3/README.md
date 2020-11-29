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

## Systemd 를 이용한 서비스 관리

<br />

<table>
	<thead>
		<tr>
			<th colspan="2">
			Systemctl 명령어	
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th> start </th>	
			<td>
				서비스를 시작하는 명령어						
			</td>	
		</tr>
		<tr>
			<th> stop </th>	
			<td>
				서비스를 중지하는 명령어	
			</td>	
		</tr>
		<tr>
			<th> restart </th>	
			<td>
				현재 서비스를 중단하고, 다시 시작하는 명령어	
			</td>	
		</tr>
		<tr>
			<th> reload </th>	
			<td>
				서비스를 중단않고 다시 시작하는 명령어	
			</td>	
		</tr>
		<tr>
			<th> try-restart </th>	
			<td>
				이미실행되고 있다면, 다시 시작하라는 관리 명령어	
			</td>	
		</tr>
		<tr>
			<th> isolate </th>	
			<td>
				해당 서비스만 시작하고 나머지 서비스는 모두 중지	
			</td>	
		</tr>
		<tr>
			<th> daemon-reload </th>	
			<td>
				관리자가 System Unit 파일을 새로 생성하거나 수정했다면 그 파일을 Systemd 가인식하기 위해 모든 Unit 파일을 다시 읽어 들이는데 사용
			</td>	
		</tr>
	</tbody>
</table>

<br />

### 서비스 활성화 관련 명령어

<br />

<table>
	<thead>
		<tr>
			<th>
				Systemctl 서비스 활성화 명령어
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th> enable </th>
			<td>
				부팅시 서비스가 자동으로 시작되도록 Unit 파일 명령어 enabel 사용 <br />
				이때 이 서비스 Target 이 저장된 디렉토리에서 /etc/systemd/system 으로 링크파일이 생성, 시스템이 multi-user.target 에서 시작할 경우 자동으로 이서비스를 시작하라는 의미. <br /> 이때 링크파일은Systemd Unit 파일에서 Install 섹션이 정의된 경우에 생성된다.
			</td>
		</tr>
		<tr>
			<th> reenabel </th>
			<td>
				기존의 서비스를 비솰성화( 링크 제거 ) 후 다시 이 서비스를 활성화( 링크 재생성 ) 	
			</td>
		</tr>
		<tr>
			<th> disable </th>
			<td>
				서비스를 비활성화, 이를 위해 Unit file 의 Install 섹션을 확인후 생성했던 링크파일 제거
			</td>
		</tr>
		<tr>
			<th> is-active </th>
			<td>
				현재 서비스가 실행중인지 확인	
			</td>
		</tr>
		<tr>
			<th> is-enabled </th>
			<td>
				현재 서비스가 활성화, 비활성화 됬는지 확인 	
			</td>
		</tr>
		<tr>
			<th> is-failed </th>
			<td>
				서비스 시작이 실패했는지 확인	
			</td>
		</tr>
		<tr>
			<th> mask </th>
			<td>
				해당 서비스를 systemd 에서사용하지 않기 위해 사용, 이 명령어는 /etc/systemd/system 에 있는 Unit 파일이 /dev/null 로 변경된다. 이 서비스 Unit 에 접근하지 말라는 의미이며, mask 로 표시됬다는 메세지를 알린다.	
			</td>
		</tr>
		<tr>
			<th> unmask </th>
			<td>
				mask 상태를 해제	
			</td>
		</tr>
	</tbody>
</table>

<br />

### 서비스 상태 확인 명령어

<br />

#### 로컬서버 서비스 상태 확인

<br />

<table>
	<thead>
		<tr>
			<th colspan="2">
				로컬 서버에서 서비스 상태 확인 명령어
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th> status </th>
			<td>
				서비스 상태 확인
				<br />
				active( 상태 ) 및 서비스가사용되는 PID, 그리고 나머지 정보를 확인 가능
			</td>
		</tr>
		<tr>
			<th> cat </th>
			<td>
				Unit 파일을 확인할 경우 사용
				<br/>
				직접 수정할 경우 edit을 사용
			</td>
		</tr>
		<tr>
			<th> show </th>
			<td>
				서비스가 사용하는 모든 속성 정보를 확인
			</td>
		</tr>
		<tr>
			<th> list-dependencies </th>
			<td>
				서비스 시작전 필요한 서비스를 순서대로 정리되어 나열
			</td>
		</tr>
		<tr>
			<th> list-units --type service </th>
			<td>
				현재 사용 가능한 서비스 Unit 목록확인 
			</td>
		</tr>
		<tr>
			<th> list-unit-files </th>
			<td>
				설치된모든 Unit 파일의 목록을 확인
			</td>
		</tr>
		<tr>
			<th> list-unit-files --type service </th>
			<td>
				모든 사용 가능한 서비스 Unit 의 활성화 또는 비활성화 상태 목록을 확인
			</td>
		</tr>
		<tr>
			<th> list-units --all --state=inactive</th>
			<td>
				비활성화 된 모든 Unit 목록
			</td>
		</tr>
		<tr>
			<th> list-dependencies --after nginix.service </th>
			<td>
				Nginix 서비스가 시작되기 전에 실행되야할 서비스 목록을 순서대로 보여준다.
			</td>
		</tr>
		<tr>
			<th> list-dependencies --befor nginix.service </th>
			<td>
				Nginix 서비스가 시작된후 실행되야할 서비스 목록을 순서대로 보여준다.
			</td>
		</tr>
	</tbody>
</table>

<br />

### 원격 서버 서비스 상태 확인

<br />

<table>
	<thead>
		<tr>
			<th colspan="2">
				원겨서버 서비스 상태 확인
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th> -H root@node status serviceName.server </th>
			<td>
				-H 옵션에 사용자와 노드를 지정, 명령어 systemctl 을 이용하면 패스워드를 요구, 입력후 그 상태확인 가능
			</td>
		</tr>
		<tr>
			<th> -H root@node start serviceName.service </th>
			<td>
				서비스 시작 시도
			</td>
		</tr>
		<tr>
			<th> -H root@node stop serviceName.service </th>
			<td>
				서비스중지
			</td>
		</tr>
	</tbody>
</table>

<br />

## System Unit 파일다루기

<br />

### System Unit 파일 이해

<br />

| 섹션 및 지시어 | 설명 |
| :---: | :--- |
| [Unit] | Unit 섹션을 의미 |
| Description | Unit 섹션이 제공하는 기본적인 기능과 관련있는 의미있는 설명, systemctl status 를 사용하면 그 내용을 읽을 수 있다. |
| Doucmentation | Unit 과 관련있는 문서의 위치를 표시, man 과 URI 를 통해 그경로를 제공 |
| After | Unit 이시작되기 전에 시작돼야 할 Unit | 
| Before | Unit 이 시작후에 시작돼야 할 Unit |
| Requires | 의존 관계에 있는 Unit 이 실행되지 않는다면, 이 Unit 도 실행할 수 없다. 
| Wants | Requires 보다 더 약한 개념으로, 이 Unit 과 의존 관계에 있지만 설령 그 서비스가 시작되지 않더라도 이 Unit 의 서비스 실행에는 영향을 주지 않는다. | 
| Conflicts | Requires 와는 반대개념으로 같이 사용할 수 없는 Unit 을 말한다. 만약 같이 사용된다면 실행되지 않는다. |

<br />










