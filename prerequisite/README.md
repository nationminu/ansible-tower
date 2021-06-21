# Ansiblde Tower 데모 준비

> Ansible Tower 튜토리얼을 진행하기 위한 사전 준비: <BR>
> 사용자 관리 > Organizations, Teams, Users 관리 <BR>
> 작업 관리 > Inventory, Credentals, Projects, Job Template 관리 <BR>


# 1. 사용자 관리

## 1. Organizations 관리
> Ansible Tower 에서 가장 높은 관리 조직으로, Users, Teams, Projects 및 Inventories 의 모음이다.

![TowerHierarchy](../imgs/TowerHierarchy.png)

### 1. Organizations 등록

> Menu > Organizations > <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/>

![Organizations](../imgs/organizations.png)

![Organizations](../imgs/create-organizations.png)

![Organizations](../imgs/list-organizations.png)

## 2. Teams 관리

> Menu > Teams > <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> Organization 에 속한 Team 을 등록한다.

![Teams](../imgs/teams.png)

![Teams](../imgs/create-teams.png)

![Teams](../imgs/list-teams.png)

## 3. Users 관리

> Menu > Users > <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/></BR>
> Organization 에 속한 User 를 등록한다.

![Users](../imgs/users.png)

![Users](../imgs/create-users.png)

![Users](../imgs/list-users.png)

## 4. Team 설정

> Menu > TEAMS > <TEAM이름> 수정 > USERS > <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> 상단에 USERS 로 이동후 사용자 추가

![JoinTeams](../imgs/join-teams.png)

![JoinTeams](../imgs/join-teams-2.png)

![JoinTeams](../imgs/join-teams-3.png)

## 5. Permission 설정

> Organizations 상단 PERMISSIONS 에서 Team 또는 User 별 Role(Admin, Execute, Project Admin, Inventory Admin, ...) 설정이 가능하다.
> Teams, Users 상단 PERMISSIONS 에서 리소스별(Job Templates, PROJECTS ,INVENTORIES, ...) 접근 권한 설정이 가능하다.

- Organizations User Role 설정
![Permission](../imgs/users-permissions.png)

- Organizations Team Role 설정
![Permission](../imgs/teams-permissions.png)

- Teams,Users 리소스별 권한
![Permission](../imgs/permissions.png)

# 2. 작업 관리

## 1. Inventory 관리
> 작업 대상 노드의 집합으로 그룹,호스트를 관리 할 수 있다.

### 1. Inventory 등록

> Menu > Inventories <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> Inventory 선택 후 상단 Permission 에서 Team 또는 User 별 Role(Admin,Update,Ad Hoc, Use, Read) 설정이 가능하다.

![Inventories](../imgs/inventories.png)

![Inventories](../imgs/create-inventories.png)

![Inventories](../imgs/list-inventories.png)

![Inventories](../imgs/permission-inventories.png)

### 3. Hosts 등록 

> Inventory 선택 > Hosts <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> Inventories 의 Hosts 을 관리한다.

![Hosts](../imgs/hosts-inventories.png) 

![Hosts](../imgs/create-hosts.png) 

### 2. Group 등록 

> Inventory 선택 > Groups <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> Inventories 의 Group 을 관리한다.

![Groups](../imgs/groups-inventories.png)
 
![Groups](../imgs/create-groups.png)

> Inventory 선택 > Groups > Group 선택 > Hosts,Groups
![Groups](../imgs/join-groups.png)

> Inventories > Inventory 선택 > Hosts
![Groups](../imgs/list-hosts.png)

## 2. Credentals 관리
> 작업 노드에 대한 인증을 하기위한 관리 도구이다. <BR>
> 기본 OS 계정 정보를 포함한 Machine 인증, AWS, GCP 등의 다양한 모듈을 제공한다.

### 1. Credentals 등록

> Menu > Credentials

![Credentials1](../imgs/qs-credentials-setup-screen.png)

> Credentials > Demo Credential

![Credentials2](../imgs/credentials-home-with-demo-credential-details.png)

> Creentials > Create Credentials

![Credentials3](../imgs/credentials-create-credential.png)

> Credentails > Create Credentials > CREDENTIAL TYPE

![Credentials4](../imgs/credential-types-popup-window.png)


### 2. 지원하는 Credential Type

> **:link: Referer** : 
> https://docs.ansible.com/ansible-tower/latest/html/userguide/credentials.htmSD
- Amazon Web Services
- Ansible Galaxy/Automation Hub API Token
- Ansible Tower
- GitHub Personal Access Token
- GitLab Personal Access Token
- Google Compute Engine
- Insights
- Machine
- Microsoft Azure Resource Manager
- Network
- OpenShift or Kubernetes API Bearer Token
- OpenStack
- Red Hat Satellite 6
- Red Hat Virtualization
- Source Control
- Vault
- VMware vCenter

## 3. Projects 관리

### 1. Project 등록

## 4. Job Template 관리

### 1. Job Template 등록
