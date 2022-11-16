# 📌깃허브 5장 요약
## 5-1) 서버 저장소 = 원격(remote 저장소)
* 협업 저장소의 중요성  
  * 개발자들이 소스 파일들을 수정, 의도치 않은 충동을 방지!
  * 원격 저장소에 작업 저장함에 따라 어디서든 동기화 가능
  * 깃 주소 공유, 다수의 개발자와 협업에 용이한 이점을 차지

<h2>5-2) 계정 생성과 저장소 생성</h2>
① 회원가입
<img src="https://user-images.githubusercontent.com/114343532/192197446-826faad1-06fc-4e2a-a41b-c3dd0de4573d.png" width="70%" height="70%">
② 정보 입력
<img src="https://user-images.githubusercontent.com/114343532/192197456-2a74e5d4-5c82-4e11-8441-4ee6c3987004.png" width="30%" height="30%">
③ 저장소 생성
<img src="https://user-images.githubusercontent.com/114343532/192197459-6c431d53-e800-4556-b3bb-a746a9f48a66.png" width="70%" height="70%">
④ 저장소 정보 입력
<img src="https://user-images.githubusercontent.com/114343532/192197463-06378ab9-770f-458e-83f8-291085d69254.png" width="30%" height="30%">
⑤ 저장소 생성 확인
<img src="https://user-images.githubusercontent.com/114343532/192197465-8d2dd552-08c1-4d74-ac89-3dba6028309c.png" width="70%" height="70%">

# 📌5.3 깃허브 연동 및 원격 등록
## 5.3.1 로컬 저장소
 * README 체크 X -> 새로운 로컬 저장소를 생성하고 원격 저장소 연결 방법
 * $mkdir gitstudy05 – 새 폴더 만들기
 * $cd gitstudy05
 * $git init – 저장소 깃으로 초기화     
 * Initialized empty Git repository in E:/gitstudy05/.git/
 * $echo “#gitstudy05” >>README.md – 파일 생성
 * $git add README.md – 스테이지에 등록
 * $git commit –m“first commit”- 커밋
 * 기존 저장소를 연결하는 방법
 
## 5.3.2 프로토콜
### Local
 * 서버로 이용시 폴더 경로만 입력
 * $ git remote add 원격저장소별칭 폴더경로
 * 빠른 동작 가능 / 모든 자료가 집중되는 위험성O

### HTTP
 * 깃은 HTTP 방식의 프로토컬 지원
 * HTTP는 기존 아이디와 비밀번호만으로 접속자를 인증하여 처리
 * HTTP는 익명으로도 처리할 수 있으며, 계정을 이용하여 처리할 수도 있다.

### SSH
 * 깃에서 권장하는 프로토콜
 * 높은 수준의 보안 통신으로 처리
 * 주소 앞에 ‘ssh://계정@주소’처럼 프로토콜 타입 지정
 * 접속시 인증서 사용 – 공개키는 서버에 등록, 개인키는 로컬에 저장
 * 익명 접속X

### Git
 * SSH와 유사하지만 인증 시스템X -> 보안에 취약

## 5.3.3 원격 저장소의 리모트 목록 관리
 * remote 명령어를 사용하여 원격 저장소 관리 + 현재 연결된 목록 확인 및 등록, 취소 작업 가능
 * $ git remote – 원격 저장소의 이름 출력(목록만 확인시 편리)
 * $ git remote –v 이름 + URL 확인

## 5.3.4 주소와 별칭
 * 로컬 저장소에 원격 저장소를 등록하련 서버 주소 필요 
 * 깃허브 같은 저장소 이용시 프로토콜 + 도메인 주소 형태로 되어 있다.
 * 로컬에 서버 저장소를 생성 할 때는 폴더 경로를 사용 가능
 * 별칭 – 긴 서버 URL 문자열을 별칭으로 만들어 사용 가능
 * 대표적인 별칭으로 origin 사용
 
## 5.3.5 원격 저장소에 연결

 * 원격 저장소와 연결하려면 add옵션 사용
 * $ git remote add 원격저장소별칭 원격저장소URL
 * 원격 저장소 추가시 인자 값으로 원격 저장소 URL 같이 입력
 * infoh@hojin MINGW64 /e/gitstudy05(master)
 * $ git remote add origin http://github.com/jinygit/gitstudy05.git - 자신의 서버 주소 입력 infoh@hojin MINGW64 /e/gitstudy05(master)
 * $ git remote –v 원격 저장소 목록 확인
 * origin http://github.com/jinygit/gitstudy05.git (fetch)
 * origin http://github.com/jinygit/gitstudy05.git (push)
 * 원격 저장소와 연결되면 fetch와 push 두 주소를 출력
 * 별칭은 중복선택X

## 5.3.6 소스트리에서 원격 브랜치

 * 원격 저장소를 등록하면 기존 master 브랜치와 local/master 같은 별칭/브랜치가 자동 생성된다

## 5.3.7 별칭 이름 변경과 정보
 * 별칭 이름 변경 $ git remote rename 변경전 변경후
 * 상세 정보 확인 $ git remote show 원격저장소별칭

## 5.3.8 원격 서버 삭제
 * 등록된 원격 저장소 삭제
 * $ git remote rm 원격저장소별칭

# 📌5-4 서버 전송
 * 지역 저장소와 원격 저장소를 연결시킨 후에는 로컬 저장소의 커밋들을 원격 저장소로 업로드할 수 있다.

## 5-4-1 push: 서버에 전송
 * push : 원격 저장소로 커밋된 파일들을 업로드하는 동작
 * push 명령어를 사용하기 전 미리 작업해 둔 원격 저장소와 연결된 서버 목록을 확인해 본다.
 * $git remote –v : 원격 저장소와 연결된 서버 목록을 확인하는 명령어
<img src="https://user-images.githubusercontent.com/114343532/192238302-3e4f20f5-554a-47c5-a077-beacafbdb7ea.png" width="70%" height="70%">

*  출력된 결과의 2번째 줄에서 ‘gitstudy05’라는 업로드가 가능한 원격 저장소가 등록된 것과 그 저장소의 별칭은 origin으로 설정된 것을 확인할 수 있다.
 
 * $git push 원격저장소별칭 브랜치이름 : 별칭 이름을 가지는 서버의 master 브랜치에 현재 브랜치를 업로드한다.
 * 브랜치(branch) : 독립적으로 어떤 작업을 진행하기 위한 개념으로 한 시점에서 개발자들이 각자 독립적인 작업 영역(저장소) 안에서 마음대로 소스 코드를 변경할 수 있다.
 * 위 명령어를 사용하여 현재 master 브랜치를 origin 서버로 전송해 본다.
<img src="https://user-images.githubusercontent.com/114343532/192238378-d48e1ea5-b1a9-4ccf-a9f7-2d6b13a4d168.png" width="70%" height="70%">
 
 * 앞에서 언급한 저장소 ‘gitstudy05’의 별칭 origin을 사용하였고 이를 push 명령어를 이용하여 main 브랜치를 origin이라는 원격 저장소로 전송시켰다.
 
 * 내 깃허브 저장소 gitstudy05를 확인해 보면 서버에 새로운 main 브랜치가 생성이 되고, main 브랜치 안에 있는 소스 코드가 저장소에 그대로 업로드된 것을 볼 수 있다. gitstudy 저장소에는 앞서서 README.md 파일을 커밋했었는데 이 md 파일이 깃허브의 gitstudy05 저장소에 올라가게 된 것이다.
<img src="https://user-images.githubusercontent.com/114343532/192238397-60136e23-5d60-4a52-add8-d9cc8db912d6.png" width="70%" height="70%">
 
 * 이렇게 원격 저장소에 push하면 main 저장소가 로컬 저장소의 main 브랜치와 서버의 main 브랜치 이렇게 총 2개가 생성이 된다.

## 원격 저장소의 용도
1. 자신의 로컬 저장소를 백업하는 용도
2. 다른 사람과 협업하는 용도

# 📌5-5. 자동으로 내려받기
 * 위와 반대로 원격 저장소에서 커밋된 코드를 내려받는 방법을 알아본다.

## 5-5-1. clone: 복제
 * $git clone 저장소 주소 : 기존 저장소를 이용하여 새로운 저장소를 생성하게 해준다. clone 명령어는 초기화 init 명령어 외에 원격 서버 접속에 필요한 추가 설정을 자동으로 수행한다. 서버의 연결 설정을 마친 후 서버 안에 있는 모든 커밋된 코드 이력들을 한 번에 내려받는다.

**앞에서 업로드한 원격 저장소를 다른 이름의 로컬 저장소로 복제해 보자.**

<img src="https://user-images.githubusercontent.com/114343532/192238420-85449a9c-84a0-4f3a-989c-088d98e9ead9.png" width="70%" height="70%">

 * 아까 gitstudy05의 상위 폴더인 git으로 cd 명령어를 이용해 디렉토리를 변경한 후 git 폴더 안에 ‘gitstudy05_clone’이라는 복제할 새 폴더를 mkdir 명령어를 이용해 만들고 디렉토리를 변경한 모습이다.
 
 <img src="https://user-images.githubusercontent.com/114343532/192238449-fd0190c0-f9ac-4f1b-9ded-edb12fded863.png" width="70%" height="70%">
 
  * 내 원격 저장소를 gitstudy05_clone 폴더에 clone 명령어를 이용해 복제하였다.
  
  <img src="https://user-images.githubusercontent.com/114343532/192238465-442d0491-cd2d-4262-b3c1-7224fae8bb89.png" width="70%" height="70%">
  
* 위처럼 ls –all 명령어를 이용해 원격 서버가 정상석으로 복제된 것을 확인할 수 있다. 그리고 git-remote –v 명령어를 이용하면 원격 저장소 목록 또한 살펴볼 수 있다.

## 5-5-2. Pull: 서버에서 내려받기
 * pull : 복제 후 원격 저장소의 갱신된 내용을 추가로 내려받기 위해 사용할 수 있는 명령어이다. pull 명령어는 로컬 저장소보다 최신인 갱신된 원격 저장소의 커밋 정보를 현재 로컬 저장소로 내려받는다.
 
  <img src="https://user-images.githubusercontent.com/114343532/192238475-09d3c710-9358-4685-a063-01e7268855a7.png" width="70%" height="70%">
  
   * 실습을 위해 원본 로컬 저장소인 gitstudy05로 이동한 후 ‘code server.htm’ 이라는 코드를 입력해 VSCode로 이동 후 다음과 같이 코드를 작성했다.
   
  <img src="https://user-images.githubusercontent.com/114343532/192238479-fbfd96b4-ae60-483b-a187-358da3fa0751.png" width="70%" height="70%">
  
   * 이제 add와 commit 명령어를 이용하여 위에서 작성한 sever.htm 파일을 커밋시킨다.
   
   <img src="https://user-images.githubusercontent.com/114343532/192238486-7a229e71-e316-4696-96cd-33c878ccdecb.png" width="70%" height="70%">
   
 * 이어서 push 명령어를 이용해 커밋한 내용을 원격 저장소(서버)로 업로드한다. 
 
 <img src="https://user-images.githubusercontent.com/114343532/192238497-cddb7cb5-7b4a-4023-9d0e-51d38e1dbe33.png" width="70%" height="70%">
 
  * 이제 복제된 저장소인 ‘gitstudy05_clone’으로 이동해 log 명령어를 이용해 커밋 로그를 확인해 보자.
  
 <img src="https://user-images.githubusercontent.com/114343532/192238497-cddb7cb5-7b4a-4023-9d0e-51d38e1dbe33.png" width="70%" height="70%">

  * 복제된 저장소에는 아직 gitstudy05에서 처음 커밋했을 때의 커밋 하나만 있다.  이번에는 pull 명령어를 이용해 원격 저장소에서 갱신된 새 커밋 정보를 가지고 와 보겠다.
  
 <img src="https://user-images.githubusercontent.com/114343532/192238507-6bece26e-a5c1-4058-8d44-b71e866fa239.png" width="70%" height="70%">
 
  * pull 명령엉는 원격 저장소에 갱신된 커밋을 로컬 저장소의 커밋 정보와 비교하여 갱신한다. 원격 저장소에서 복제된 저장소를 동기화한 것이다. log 명령어를 통해 확인해 보면 gitstudy05_clone 저장소에서도 2번째 커밋 이력(커밋 메시지: good day)을확인할 수 있다. 
  
  <img src="https://user-images.githubusercontent.com/114343532/192238515-9f0b011a-5a62-449f-812b-141c8a9b878a.png" width="70%" height="70%">

## 서버 저장소(원격 저장소)
 * 서버를 이용하여 코드를 안전하게 보관 할 수 있음.

## 협업 저장소
 * 깃은 여러 개발자와 협업하려고 탄생한 도구임.

## 5-1-2, 연속된 작업
 * 서버 저장소는 여러 컴퓨터에 동일한 깃 저장소를 복제하고, 작업한 결과물을 다시 서버로 통합함.

## 5-1-3. 새 멤버 깃의 원격 저장소 주소만 알려 주면 모두 해결.

## 5-2. 깃허브 서버 준비에 관한 준비 내용.

## 5-3. 깃허브 연동 및 원격 등록.
 * 깃허브에 새 저장소를 생성했다면 로컬 저장소와 연결해야 함.

## 5.3.2 프로토콜
 * 서버와 통신하려면 프로토콜을 사용해야 함, 깃은 Local, HTTP, SSH, Git 네 종류의 전송 방식을 지원.

### Local: 로컬 컴퓨터에 원격 저장소를 생성하는 것을 의미. 자신의 컴퓨터를 Network File System(NFS)등 서버로 이용할 때 편리. 간단하게 원격 서버 구축 가능 및 빠른 동작, 하지만 자신의 컴퓨터로 모든 자료가 모이는 것이 단점.

### HTTP: 깃은 HTTP 방식의 프로토콜을 지원한다. 서버에 접속하려면 로그인 절차를 걸쳐야 하는데, 기존 아이디와 비밀번호 만으로 접속자를 인증하여 처리 가능. 익명 가능, 계정을 이용하여 처리 가능

### SSH: 깃에서 권장하는 프로토콜, 높은 수준의 보안 통신으로 처리. SSH 접속을 할 때는 인증서를 만들어 사용, 공개키는 서버에 등록, 개인키는 로컬에 저장. 익명 접속 불가능. 기업에서 깃 서버를 운영할 때 적합한 프로토콜.

### Git: 깃의 데몬 서비스를 위한 전용 프로토콜 방식 의미. SSH와 유사하지만 인증 시스템이 없어 보안에 취약.

# 📌5.6 수동으로 내려 받기
 * 원격 저장소 내용을 내려 받는 방법은 pull & fetch 둘의 차이점은 병합을 자동 처리하는지의 여부.


## 5.6.1 자동 병합
 * 풀은 현재 커밋보다 최신 정보가 있을 때 내려받음. 이는 임시 영역에 저장. 내려 받은 최신 커밋들은 현재 브런치로 자동으로 로컬 파일과 원격 서버 파일을 합치는 과정인 병합 처리를 사용. pull 명령어가 자동으로 병합하지 못할 때는 페치 방식을 사용

## 5.6.2 fetch
 * 페치는 코드를 수동으로 내려 받는 작업을 한다. 내려 받은 후 현재 브랜치와 자동 병합하지 않음.

## 5.6.3 merge 명령어로 수동 병합
 * fetch는 데이터를 내려받기만 할 뿐 자동 병합하지 않는다, 내려 받은 데이터를 로컬 저장소에 적용 하려면 병합 명령어를 사용해야 하는데, 이때 merge 명령어가 사용 됨.

# 📌5.7 순서
 * 여러 명이 협력해서 개발하는 경우에는 순차적으로 푸시 해야함.

## 5.7.1 최신 상태
 * 원격 저장소에 푸시하려면 자신의 로컬 저장소를 최신 상태로 유지하는 것이 기본. 커밋이 순차적이지 않을 경우 깃은 푸시 동작을 거부한다. 즉, 개발자1 개발자2가 있는 경우 개발자1이 푸시를 했을 때, 개발자 2는 푸시된 내용을 적용 한 후 자신의 내용을 푸시해야 푸시가 정상적으로 이루어짐.

## 5.7.2 충돌 방지.
 * 위와 같은 구조는 충돌을 방지 하기 위함이다. 충돌을 방지 하기 위해서는 pull > coding > commit > pull > push의 과정을 권장한다.

# 📌5.8
 * 정리 마무리
