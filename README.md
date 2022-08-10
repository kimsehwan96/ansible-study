# ansible-study
The tool can build various automated process about infra, security, systems.

## 내 환경

Machine : Macbook Pro 14, M1 Pro (arm64)
OS: MacOS

## Ansible

Ansible은 agent가 필요 없음. 

Ansible은 사용자가 인벤토리에서 관리하려는 머신에 관한 정보를 읽는다. 

SSH 프로토콜을 사용해 서버에 연결하여 태스크를 실행하며, Ansible은 ssh-agent와 함께 사용한다. 

플레이는 Ansible 인벤토리 파일의 호스트 선택 항목에 대해 실행 순서가 지정된 태스크 세트로 구성되어 있습니다. 태스크는 플레이를 구성하는 요소로, Ansible 모듈을 호출합니다. 플레이에서 태스크는 작성된 순서로 실행됩니다.  

Ansible은 실행 중에 시스템의 상태를 계속 파악할 수 있습니다. Ansible이 시스템을 스캔하여 시스템의 플레이북 설명과 실제 시스템 상태가 일치하지 않음을 발견하면 시스템을 플레이북과 일치시키는 데 필요한 모든 변경을 수행합니다. 

Ansible은 원격 시스템을 관리하고, 원하는 상태로 만들어 줄 수 있습니다. 기본적인 Ansible 환경은 아래와 같은 3개의 주요 구성요소를 갖습니다.

### Control noe

Ansible이 설치된 시스템을 의미합니다. 이 시스템에서 `ansible`, `ansible-inventory`와 같은 명령어 사용이 가능합니다. 

### Managed node

Ansible이 제어하는 원격 시스템, 호스트를 의미합니다.

### Inventory

논리적으로 정의된 Managed node의 리스트를 의미합니다. control node에서 Ansible을 통해 배포,관리 하고자 하는 원격 시스템, 호스트의 리스트를 생성 할 수 있습니다. 

![](https://docs.ansible.com/ansible/latest/_images/ansible_basic.svg)

## Ansible Install

Control Node가 될 시스템에 파이썬이 설치되어있고, pip 사용이 가능하다면 아래와 같이 설치 가능하다.

`python3 -m pip install ansible`

## Ansible Congiguration

Ansible은 여러가지 방법으로 설정할 수 있다. `ansible.cfg` 파일이나, 환경변수, command line option, playbook 의 keywork 및 변수등으로 설정 가능하다. 

`ansible-config` 유틸리티는 모든 설정 항목 및 디폴트 설정값을 확인 할 수 있다.

### 설정 파일

아래의 순서대로 설정 파일을 찾고 반영한다.

- ANSIBLE_CONFIG (환경변수 / 설정되어있을경우)
- ansible.cfg (현재 디렉터리)
- ~/.ansible.cfg (홈 디렉터리)
- /etc/ansible/ansible.cfg

위에서 먼저 찾는 순서대로 반영되며 나머지는 무시된다.

ansible의 설정 파일은 INI 포멧으로, 주석처리를 # (hash sign)과 ; (semicolon) 으로 가능하다. 다만 값을 입력한 라인에 인라인 주석을 처리 할 때에는 ; (semicolon) 으로 처리한다.

```ini
# some basic default values...
inventory = /etc/ansible/hosts ; This points to the file that lists your hosts
```

### ansible.cfg 파일 생성

모든 라인이 주석처리된 ansible.cfg 의 에시 파일을 아래와 같이 생성 가능하다.

`$ ansible-config init --disabled > ansible.cfg`

플러그인 설정까지 포함하려면 아래와 같이 생성한다.

`$ ansible-config init --disabled -t all > ansible.cfg`

## Ansible 사용해보기

우선 내 Local machine에 가상머신 혹은 컨테이너(Docker)가 존재한다고 가정한다. 

나는 우선 UTM을 통해 ubuntu 22.04 가상머신을 셋업했다. 

호스트 머신(Macbook)의 WiFi 네트워크 인터페이스인 en0와 브릿지 연결을 하였다.

ubuntu 22.04의 가상머신 ip 주소는 `192.168.0.4` 로 지정하였다. 