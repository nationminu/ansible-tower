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

![Inventories](../imgs/inventories.png)

### 1. Inventory 등록

> Menu > Inventories <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> Inventory 선택 후 상단 Permission 에서 Team 또는 User 별 Role(Admin,Update,Ad Hoc, Use, Read) 설정이 가능하다.

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

> Menu > Credentials <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>
> 작업 노드에 대한 인증을 하기위한 관리 도구이다. <BR>
> 기본 OS 계정 정보를 포함한 Machine 인증, AWS, GCP 등의 다양한 모듈을 제공한다.

![Credentials](../imgs/credentials.png)

### 1. Credentals 등록 
 
![Credentials](../imgs/create-credentials.png)
![Credentials](../imgs/list-credentials.png)

> Credentails > Create Credentials > CREDENTIAL TYPE

![Credentials](../imgs/credentials-create-credential.png)
![Credentials](../imgs/credential-types-popup-window.png)

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

> Job Template 에서 사용되는 playbook 목록을 Projects 로 구성한다. </br>
> SCM(Playbook 목록)은 Git,Svn,Manual 등 다양한 방법을 제공한다. Tutorial 에서는 github 를 이용한다.

![Projects](../imgs/projects.png)

### 1. Project 등록

> Menu > Projects <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>

![Projects](../imgs/create-projects.png)
![Projects](../imgs/list-projects.png)

## 4. Job Template 관리

> Job Template 은 Ansible Tower 에서 실행되는 최소 단위의 작업이다. </br>
> Job Template 으로 Schedule Job, Workflow Job 을 생성할 수 있다.

![Template](../imgs/templates.png)

### 1. Job Template 등록

> Menu > Template <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> </BR>

![Template](../imgs/create-templates.png)
![Template](../imgs/list-templates.png)

### 2. Job Template 실행

> Menu > Template  <img src="../imgs/launch-button.png" width=20 height=20 align="absmiddle"/> </BR>
![Template](../imgs/launch-templates-1.png)
![Template](../imgs/launch-templates-2.png)

### 2. Schedule Job
> Menu > Template > <Job Tempalte 선택> Schedule
> 등록된 Job Template 을 사용하여 Schedule Job 으로 동작한다.
![Schedule](../imgs/schedule.png)
![Schedule](../imgs/create-schedule.png) 
![Schedule](../imgs/list-schedule.png)

> Menu > Jobs <br>
> 등록된 Schedule Job 실행 확인.
![Schedule](../imgs/list-schedule-2.png)

### 3. WorkFlow Job

> Menu > Template <img src="../imgs/add-button.png" width=20 height=20 align="absmiddle"/> > Workflow Templte </BR>
> 등록된 Job Template 을 연결하여 Workflow Job 을 생성한다. <BR> 
> Tutorial 에서는 Step #1 ~ Step #3 까지의 Job Template 을 미리 생성해서 사용한다.

![Schedule](../imgs/workflow.png)
![Schedule](../imgs/create-workflow.png)
![Schedule](../imgs/visualizer-workflow-1.png)
![Schedule](../imgs/visualizer-workflow-2.png)