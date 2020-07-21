# Git

> Git은 분산버전관리 시스템이다.

## 준비하기

윈도우에서 git을 활용하기 위해서 git bash를 설치한다.

초기 설치를 완료한 이후에, 계정설정을 진행한다.

```sh
$ git config --global user.email {이메일}
$ git config --global user.name {이름}
```

## 로컬 저장소 활용하기

### 1. 저장소 초기화

> 이제부터 이 디렉토리를 git으로 관리하겠다.(변경 이력 감시)

```sh
$ git init
```

- `.git` 디렉토리가 생성되며, 여기에 git과 관련된 모든 정보가 저장된다.
- 초기화를 하고나면 git bash에 `(master)`라고 표시가 되는데, 이는 이 디렉토리는 이미 git이 관리하고 있다는 뜻으로 생각할 수 있다.
- 이미 초기화한 repo에서는 다시 git init을 하지 않는다.

### 2. add

> working directory 작업공간에서 변경된 사항을 이력으로 관리하기 위해서는 반드시 staging area를 거쳐야 한다.

```sh
$ git add {staging 할 파일}
```

### 3. commit

> 이력을 확정 짓는, 즉 기록을 남기는 명령어이다.

```sh
$ git commit -m '커밋 메시지'
```

커밋 기록을 확인하고 싶다면 아래 명령어

```sh
$ git log
```

### 4. status

> git을 쓰면서 가장 많이 사용해야 하는 명령어. 현재 상황을 확인

```sh
$ git status
```

## 원격 저장소 활용하기

> 여러 서비스 중, github을 기준으로 설명.

### 1. 준비사항

- github에 회원가입 후, 빈 repo를 만든다.

### 2. 원격 저장소 등록

- 로컬 저장소와 원격 저장소를 연결.

```sh
$ git remote add origin {github repo url}
```

- 원격 저장소(remote)를 등록할건데,  `origin` 이라는 이름으로 원격 저장소를 등록하겠다.
- 원격 저장소 등록 현황을 확인하려면 아래의 명령어를 입력

```sh
$ git remote -v
```

- 등록된 원격 저장소를 삭제하는 명령

```sh
$ git remote rm origin
```

### 3. 원격 저장소 푸시

- 원격 저장소에 업로드

```sh
$ git push origin master
```

### 4. 원격 저장소에서 로컬로 가져오기

github이나 gitlab의  repo 주소를 복사해둔뒤,

```sh
$ git clone { 가져오고자 하는 repo url}
```



