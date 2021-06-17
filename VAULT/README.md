# ANSIBLE VAULT

> **ℹ️ Info** : For your information! <BR>
> 번수 및 파일을 암호화 하는데 사용.  <BR>

본 튜토리얼은 ansible vault 를 이용하여 다양한 방법으로 사용자 변수(username,password)를 암호화 하는 내용을 포함하고 있습니다.

## 1. Vault password

> vault password 는 ansible vault 에서 암/복호화에 사용되는 key 값이다.

### 1. Prompt

> **--ask-vault-pass** : 암/복호화 또는 playbook 실행시 매번 prompt로 입력 받는다.

- admin.yaml 생성
```bash
# ansible-vault create admin.yaml --ask-vault-pass
New Vault password: 
Confirm New Vault password: 
```
- editor 로 사용자 정보 입력 
```yaml
---
username: admin
password: P@ssW0rd
...
```
- admin.yaml 암호화 확인
```bash
# cat admin.yaml
$ANSIBLE_VAULT;1.1;AES256
31323934653362363830306533666332323461383534623237633563653333653134306333313065
6136376233316437366237383235613362613938303838370a656162373062643737356139343831
61343331386136303834633665353038626339303335383032303364346264393438643531663131
6166316261343838620a343834313930333838333361383761316434323639666666653866656563
34646663646532383035626232376535363534336464636639366533303838383264323963626538
6331653731636633346661323339663035343062343462616436
```


### 2. File

> **--vault-id / --vault-password-file** : 암/복호화 또는 playbook 실행시 파일의 내용을 사용한다.

- vault password file 생성
```bash
# echo "Super P@wer P@ssW0rd V0ult" > ansible.vault
```
- guest.yaml 생성
```bash
# ansible-vault create guest.yaml  --vault-password-file ansible.vault
```
- editor 로 사용자 정보 입력 
```yaml
---
username: guest
password: P@ssW0rd
...
```
- guest.yaml 암호화 확인
```bash
# cat guest.yaml
$ANSIBLE_VAULT;1.1;AES256
35313366333930316566303461623266663335313662636535333862616534666239613831366637
3062376664323136313630313930393266633262666139330a336235326434636431333431373362
38653130313539616465643833633736653032613037646364333332373764656433363966303131
6334613137373464390a336263393238326134633137376230323762383931653235333635306637
32306630623862613233313366383633393032383962623930616133623263306665616166626631
3335653539386331663337633364343330333731653530653465
```


## 2. Variable Encrytion

> Yaml 파일의 변수 값을 암호화한다.

### 1. Encription

> ansible vault "encrypt_string" 옵션으로 값을 암호화하면 콘솔에 결과가 출력된다.

- username 값 암호화
```bash
# ansible-vault encrypt_string 'user1' --name 'username' --vault-password-file ansible.vault
username: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          63343163393163336531616264353066323763333235336363643536623333326633343430326663
          6633383135613161616334383936653935383563663633310a643238363939343566383138633562
          66373430396436346431313638373661323632613330373866346136656266346335393232376563
          6130363038336337620a343765613065336464303139303337326161323033623133333262613230
          6265
Encryption successful
```
- password 값 암호화
```bash
# ansible-vault encrypt_string 'P@ssw0rd' --name 'password' --vault-password-file ansible.vault
password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          34363333663565343733616539616362613836323464383034336136656531383238333364313963
          6537613830373034643035363738303738613335346336320a613262343135383832376137666634
          30636238366165336164663762623230333634373733646537626630336266393437393564663061
          3538336464343839320a333561313039366332366563653231376538653635616566356639303833
          3432
Encryption successful
```

- 암호화된 username / password 값으로 user.yaml 파일 생성한다.
```yaml
---
username: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          63343163393163336531616264353066323763333235336363643536623333326633343430326663
          6633383135613161616334383936653935383563663633310a643238363939343566383138633562
          66373430396436346431313638373661323632613330373866346136656266346335393232376563
          6130363038336337620a343765613065336464303139303337326161323033623133333262613230
          6265
password: !vault |
          $ANSIBLE_VAULT;1.1;AES256
          34363333663565343733616539616362613836323464383034336136656531383238333364313963
          6537613830373034643035363738303738613335346336320a613262343135383832376137666634
          30636238366165336164663762623230333634373733646537626630336266393437393564663061
          3538336464343839320a333561313039366332366563653231376538653635616566356639303833
          3432      
...
```

### 2. Decription

> ansible debug 모듈을 이용하여 복호화한다.

```bash
# ansible localhost -m debug -a var="username" -e "@user.yaml" --vault-password-file ansible.vault
localhost | SUCCESS => {
    "username": "user1"
}
# ansible localhost -m debug -a var="password" -e "@user.yaml" --vault-password-file ansible.vault
localhost | SUCCESS => {
    "username": "P@ssW0rd"
}
```

## 3. File Encryption

> ansible vault 를 사용하여 파일 내용 전체를 암호화 한다.

- manager.yaml 파일 생성
```yaml
---
username: manager
password: P@ssW0rd
...
```

### 1. Encription

> 대상 파일을 ansible vault "encrypt" 옵션으로 파일 내용을 암호화 한다.

- manager.yaml 파일을 암호화한다.
```bash
# ansible-vault encrypt manager.yaml --vault-password-file ansible.vault 
Encryption successful
```

-- 암호화된 파일 내용을 확인한다.
```bash
# cat manager.yaml 
$ANSIBLE_VAULT;1.1;AES256
63356162666365303863663536666264616135653463653336316334643065366334373438343638
3334333131643363356361646165336234376263316239370a336138353436616336333936333137
30343730623736383734653337353036303963616665363834313861343561326133363933336236
6263346563633835360a626633323966326332306534306564633732353432616262323332626637
38303030366130373035633666613339653861306339623032356462343466303932313833386638
3535386662653237646634663763313466353839303966663661
```

### 2. Decription

- manager.yaml 파일을 복호화한다.
```bash
 ansible-vault decrypt manager.yaml --vault-password-file user.vault 
Decryption successful
```

-- 호화된 파일 내용을 확인한다.
```bash
# cat manager.yaml 
---
username: manager
password: P@ssW0rd
...
```


## 4. Running a Playbook With Vault
- playbook dubug.yaml
```yaml 
---
- hosts: localhost 
  gather_facts: false
  connection: local

  vars:
    username: !vault |
            $ANSIBLE_VAULT;1.1;AES256
            64313164336134633431336664353634663830646165646333373133623466353933353037636538
            6464633766343330626365616530653165353862303564610a383864656137346232396261346166
            63383439313531366135393433393265333266663936316637323762646332356664346261396135
            6461353931636137320a636438363333383262326332343462636661323361363333336366343563
            3136
    password: !vault |
            $ANSIBLE_VAULT;1.1;AES256
            33336233363033306637663531363036313036633432393337643161636333333061363037323033
            6333643762366164343531373132306465393630386530630a396535336634383732346236363939
            30653235383661643662366566333164326666663837656134663539366266643834626262353266
            3833636633643436330a303434663132616638303636383539313638646132343431656338343234
            3464
 
  tasks:
  - debug:
      msg:
        - "username : {{ username }}"
        - "password : {{ password }}"
...          
```

- playbook 실행
```bash
# ansible-playbook debug.yml --ask-vault-pass
# ansible-playbook debug.yml --vault-password-file ansible.vault
```
- playbook 실행 결과
```bash
PLAY [localhost] *************************************************************************************************************************

TASK [debug] *****************************************************************************************************************************
ok: [localhost] => {
    "msg": [
        "username : admin", 
        "password : P@ssw0rd"
    ]
}

PLAY RECAP *******************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0   
```

          

## 5. Multiple vault passwords

> 여러개의 vault ID 로 암호화된 변수 및 파일은 --vault-id 를 여러번 사용하여 사용이 가능하다.

- vault ID 만들기
```
echo "user vault" > username.vault
echo "password vault" > password.vault
```
          
- username 암호화
```bash
# ansible-vault encryp_string 'user' --name 'usernamme' --vault-id user@username.vault 
username: !vault |
          $ANSIBLE_VAULT;1.1;AES256;user
          63343163393163336531616264353066323763333235336363643536623333326633343430326663
          6633383135613161616334383936653935383563663633310a643238363939343566383138633562
          66373430396436346431313638373661323632613330373866346136656266346335393232376563
          6130363038336337620a343765613065336464303139303337326161323033623133333262613230
          6265
Encryption successful  
```
- password 암호화
```bash
# ansible-vault encryp_string 'P@ssW0rd' --name 'password' --vault-id pass@password.vault
password: !vault |
          $ANSIBLE_VAULT;1.1;AES256;pass
          34363333663565343733616539616362613836323464383034336136656531383238333364313963
          6537613830373034643035363738303738613335346336320a613262343135383832376137666634
          30636238366165336164663762623230333634373733646537626630336266393437393564663061
          3538336464343839320a333561313039366332366563653231376538653635616566356639303833
          3432      
```

- playbook 실행
```bash
# ansible-playbook debug.yaml --vault-id user@username.vault --vault-id pass@password.vault 
# ansible-playbook debug.yaml --vault-id user --vault-id pass
```

- ansible.cfg 설정 을 기본 vault-id 실행
```bash
# cat ansible.cfg
[defaults]
inventory = inventory
remote_user = root
vault_identity_list = user@~/ansible/username.vault , pass@~/ansible/password.vault 
          
# ansible-playbook debug.yaml 
```
          

> **:link: Referer** : 
> https://docs.ansible.com/ansible/latest/user_guide/vault.html
