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

