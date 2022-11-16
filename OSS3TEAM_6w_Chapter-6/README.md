# OSS3TEAM_6w_Chapter-6
6장 브랜치 요약입니다.
-----------------------------------------
<br/>

# 6-1. 새로운 작업
## 6-1-1. 브랜치 작업
### 📌 브랜치(branch)
나뭇가지, 지사, 분점 등 줄기 하나에서 뻗어 나온 갈림길을 의미함.

▶️  **저장 공간 하나에서 가상의 또 다른 저장 공간을 만드는 것!**

▶️  **개발자는 항상 안정된 코드 상태를 유지하고 개발 중인 작업과 구분하여 코드를 관리해야 하므로 이를 위해 사용하는 기능**

▶️  **잦은 버그 수정과 새로운 기능 구현 등을 위해 원본을 기반으로 새로운 사본에 기능을 추가하는 작업을 '브랜치 작업' 이라고 함.**
<br/><br/>

### 📌 git을 사용한 브랜치 작업의 이점
- 우리가 오랫동안 해 왔던 브랜치 작업의 과정  
  : 많은 내용 변경이 예상됨. --> 작업 폴더를 통째로 복사 --> 복사한 폴더 이름 변경 --> 기존의 코드는 남겨 두고, 복제된 작업 폴더에서 도전적인 작업 수행 (코드 분리)
  
  - 단점
  1. 프로젝트 유지, 관리 측면에서 효율성이 떨어진다.
  2. 많은 프로젝트 폴더를 복제하다 보면 향후 코드 통합에 어려움이 생길 수 있다.

 ❗  **git**을 사용하면 **프로젝트 작업 폴더를 복사하지 않고 기존 코드와 분리해서 사용하는 것이 가능** (더 편리함)  ❗
<br/><br/>

### 📌 commit과 branch의 기능적 차이
- **commit** : 파일의 **수정 이력 관리**에 사용
b
- **branch** : 프로젝트를 **독립적으로 관리**하는 데 사용 
<br/><br/></br> 

## 6-1-2. 깃 브랜치 특징
### 📌 가상 폴더
깃의 브랜치는 작업 폴더를 실제로 복사하지 않고 **'가상 폴더'** 로 생성하기 때문에 외부적으로는 물리적인 파일 하나만 있는 것처럼 보인다.

- 장점 : 브랜치로 생성된 가상 폴더는 빠르게 공간 이동이 가능하므로 개발자는 쉽게 브랜치를 이동하면서 유연한 개발을 하는 것이 가능하다.
<br/><br/> 

### 📌 독립적인 동작
브랜치를 이용하면 원본 폴더와 분리하여 독립적으로 개발 작업을 수행할 수 있어 **분리된 브랜치**에서 코드 **작업**한 후 **원본 코드에 병합**하는 명령만 수행하면 된다.

- 장점 : 규모가 큰 코드 수정이나 병합을 처리할 때 매우 유용하다.
<br/><br/>

### 📌 빠른 동작
깃은 **'Blob 개념'** 을 도입하여 내부를 구조화한다. Blob는 포인트와 유사한 객체로 깃은 브랜치를 변경할 때 포인터(HEAD 포인터)를 이동하여 빠르게 전환한다.  

- 장점 : 브랜치 명령을 사용하면 내부적으로 커밋을 하나 생성하여 브랜치로 할당하는데, 다른 VCS(버전 관리 시스템)들은 폴더의 파일 전체를 복사하는 반면 깃은 41바이트를 가지는          해시(SHA1) 파일 하나만 만들면 되어 파일 크기가 커도 깃이 브랜치를 생성하는 속도가 다른 VCS보다 더 빠르다.
<br/><br/></br>


# 6-2. 실습 준비(git)
## 6-2-1. 저장소 생성 및 초기화
❗  깃은 기본적으로 **main 브랜치** 하나를 가지고 있고 브랜치는 **HEAD 포인터**를 가지고 있다.  ❗

1. 브랜치 실습을 위한 환경을 구축해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS
$ cd git     # cd 명령어를 이용하여 내 컴퓨터에서의 오늘 실습 메인 폴더인 git으로 이동한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git
$ mkdir gitstudy06     # mkdir 명령어를 이용하여 git 폴더 하부에 저장소로 사용할 'gitstudy06'이라는 이름의 새 디렉토리를 생성한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git
$ cd gitstudy06     # cd 명령어를 이용해 gitstudy06 폴더로 현재 위치를 변경한다.


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06
$ git init     # init(초기화) 명령어를 통해 gitstudy06 저장소를 초기화시킨다.
Initialized empty Git repository in C:/coding/coding/2022 OSS/git/gitstudy06/.git/


YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)     
# 초기화가 완료되면 위와 같이 현재 'main' 브랜치라는 것을 알려준다.     

```

**현재 브랜치**가 **main**이라는 것을 확인할 수 있고 **현재 브랜치의 작업 위치**도 확인할 수 있다.
<br/><br/><br/>


## 6-2-2. 기본 브랜치
❗  모든 커밋과 이력은 브랜치에 기록되므로 깃은 최소한 브랜치가 1개 이상 필요하므로 저장소를 처음 초기화하면 main(혹은 master) 브랜치 하나가 자동으로 생성이 된다.  ❗

2. 저장소 초기화 후 status 명령어를 실행해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git status     # status(상태) 명령어를 입력하면 아래와 같이 gitstudy06에서는 현재 commit할 파일이 없다는 문구가 나온다.
On branch main     # 현재 브랜치 작업 위치(main)

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

git에서는 항상 현재 작업하는 브랜치 위치를 확인하는 것이 중요하다.

다음과 같이 branch 명령어를 통해서도 현재 브랜치 확인이 가능하다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch
*main
```

branch 명령어는 생성된 모든 브랜치를 출력하는데 앞 코드에서는 깃에서 기본적으로 선택되는 브랜치인 main이 출력되었다. 하지만 꼭 main 이름으로 사용할 필요는 없다.
<br/><br/><br/>


# 6-3. 브랜치 생성
## 6-3-1. 브랜치 생성
### 📌 브랜치가 나타내는 것
- 브랜치는 **공통된 커밋**을 가리키는 지점이다.
- 브랜치는 또 하나의 **개발 분기점** 이다.
- 브랜치는 커밋처럼 **SHA1 해시키**를 가리킨다. but 해시키를 기억하기 어렵기 때문에 특정 커밋을 가리키는 **별칭**을 만드는데 이렇게 만든 별칭이 **브랜치**이다.

![브랜치는 공통된 커밋을 가리키는 지점](https://gitbookdown.dallasdatascience.com/img/git_branch_merge.png)

*(이미지 출처 : https://gitbookdown.dallasdatascience.com/branching-git-branch.html)*

위 그림에서 왼쪽에서 2번째 커밋 부분이 공통된 커밋을 가리키는 지점이므로 브랜치라고 할 수 있다.
<br/><br/>

### 📌 브랜치 생성
- **사용자 브랜치** : 처음 생성되는 기본 main 브랜치 외의 브랜치는 사용자가 직접 branch 명령어를 입력하여 생성해야 한다. (사용자가 직접 정의하는 브랜치)

- 브랜치 생성 개수에는 제한이 없다. 따라서 필요한 만큼 여러 브랜치를 생성하고 각 브랜치를 구별하기 위해 이름을 지정해 주면 된다.  
<br/>

❗  **브랜치 이름 생성하는 방법**  ❗

```bash
$ git branch 브랜치이름 커밋 ID
```

▶️ 위와 같이 입력하면 현재 **HEAD 포인터 기준**으로 내가 작성한 이름의 **새로운 브랜치**를 생성한다. 뒤에 지정한 **커밋 ID** 인자 값을 지정하면 지정한 **커밋 ID** 기준      으로 브랜치를 생성할 수 있다.

▶️ **새 브랜치를 생성하면 포인터만 있는 브랜치가 생성**된다. 이렇게 새롭게 생성된 브랜치는 독립된 공간을 할당하여 기존 작업 영역에 영향을 주지 않는 새로운 가상 공간이      된다.
<br/><br/>

3. 저장소에 새로운 파일을 하나 생성한 후 저장하여 실습 환경을 만들어 보자.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ code branch.htm     # branch.htm이라는 이름의 파일을 VSCODE를 통해 편집할 수 있게 해 준다.
```

```html
<h1>브랜치 실습을 합니다.</h1>     <!-- branch.htm 에 작성할 코드 내용 -->
```

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git add branch.htm     # 추적 등록

YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git commit -m "first"     # 커밋 메시지 작성
[main (root-commit) 9f802ee] first
 1 file changed, 1 insertion(+)      # 커밋이 하나 생성되었다.     
 create mode 100644 branch.htm
```

마지막 커밋 ID인 100644를 기준으로 브랜치를 생성, 추가해 본다.

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch footer     # footer라는 이름의 브랜치 생성

YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch     # 브랜치 목록 확인
  footer     # 생성된 브랜치
* main     # 현재 브랜치
```
<br/><br/>

## 6-3-2. 브랜치 이름
### 📌 브랜치 이름 작성 규칙
- 기호(-), 마침표(.)로 시작이 불가하다.
- 연속적인 마침표(..)를 포함할 수 없다.
- 빈칸, 공백 문자, 물결(~), 캐럿(^), 물음표(?), 별표, 대괄호([]) 등은 포함할 수 없다.
- 아스키 제어 문자를 포함할 수 없다.
- **브랜치 이름은 중복해서 사용하지 않아야 한다.**

```bash
YuBeenSo@DESKTOP-SKBKL14 MINGW64 /c/coding/coding/2022 OSS/git/gitstudy06 (main)
$ git branch footer     # 바로 앞서서 만들었던 브랜치 이름을 그대로 사용하여 생성해 보았다.
fatal: a branch named 'footer' already exists     # 결과로 'footer'라는 이름의 브랜치는 이미 존재한다는 에러 문구가 뜬다.
```
<br/><br/>

## 6-3-3. 소스트리 브랜치
### 📌 소스트리로 새로운 브랜치 생성
1. 소스트리의 새 탭에서 **Add** 버튼을 클릭, 그 후 **탐색**을 눌러 앞서 만든 gitstudy06 폴더를 찾아 선택한 후 **추가** 클릭

![image](https://user-images.githubusercontent.com/99963066/194833006-73923b15-6c86-4b4b-a3d9-78c552053d0d.png)
<br/><br/>

2. **main 브랜치를 선택**하고 커밋 목록에서 **커밋을 하나 선택**하여 마우스 오른쪽 버튼을 눌러 **브랜치..** 메뉴를 선택하거나 위쪽에 있는 **브랜치 생성 버튼**을 클릭하    여 소스트리에 브랜치를 하나 추가한다.

![image](https://user-images.githubusercontent.com/99963066/194834549-494b2186-8212-4e74-9edd-dc23691892dc.png)
<br/><br/>

3. 브랜치.. 나 브랜치 생성 버튼을 클릭하면 다음과 같은 브랜치 생성 창이 열린다. 소스트리에서 **커밋을 선택**하여 브랜치를 생성하는 것은 **지정한 커밋을 기준으로 브랜치를 생성**한다는 의미이다. 커밋 목록에서 브랜치를 생성하면 **명시된 커밋** 부분에 브랜치가 체크되어 있는 것을 볼 수 있다. main의 최종 커밋(HEAD)을 기준으로 브랜치를 생성할 때는 **작업 사본 부모** 항목을 선택한다.

![image](https://user-images.githubusercontent.com/99963066/194836838-454f7591-1567-49d2-939d-af1ac45cfd0a.png)
<br/><br/>

4. 위에서 새로운 feature 브랜치를 하나 추가했다. 소스트리 왼쪽에서 추가한 브랜치인 feature를 볼 수 있다. 브랜치는 총 3개이고 현재 브랜치는 feature가 되는 것도 확인 가능하    다.

![image](https://user-images.githubusercontent.com/99963066/194837680-de540f96-d3e9-4f6e-a7bb-36d3339c6fdd.png)

# 6.4 브랜치 확인
## 6.4.1 간단한 브랜치 목록

#git branch 명령어 사용시
현재 모든 브랜치가 나열 된다.
*는 현재 선택된 브랜치를 의미합니다.

## 6.4.2 브랜치 해시

브랜치는 특정한 커밋의 해시 값을 가리킵니다.
rev-parse 명령어를 사용하면 브랜치의 해시 값을 확인 할 수 있습니다.


![6-4-2](https://user-images.githubusercontent.com/105197472/195127702-9b186c34-9d9e-4fe5-ab7a-feb149a07483.PNG)


## 6.4.3 브랜치 세부 내용 확인
branch 명령어는 간단한 브랜치 이름만 출력 합니다. 하지만 branch 명령어 뒤에 -v또는 -verbose 옵션을 함께 사용하면 브랜치 이름, 커밋ID, 커밋 메세지를 볼 수 있습니다.


![6-4-3](https://user-images.githubusercontent.com/105197472/195128064-5a24f1f7-01f1-43bd-ae4a-18d31bc5ca96.PNG)


# 6.5 브랜치 이동

## 6.5.1 체크아웃

체크아웃이란 현재 브랜치를 더나, 새로운 브랜치로 들어간다는 의미.
❗ 깃은 하나의 워킹 디렉터리만 가지고 있어 다른 브랜치에서 작업하려면 반드시 브랜치를 변경하여 워킹 디렉터리를 재 설정해야 합니다.


![체크아웃1](https://user-images.githubusercontent.com/105197472/195129982-9305b23f-9868-414a-b171-64b806ff262e.PNG)


![체크아웃2](https://user-images.githubusercontent.com/105197472/195130012-559c693b-f842-4c21-bcda-b38d17bb62ab.PNG)



dev_2 앞에 *는 브랜치 이름 앞으로 브랜치가 변경 되었다는 의미입니다!

## 6.5.2 브랜치 작동 원리

checkout 명령어로 브랜치가 변경되면 깃은 내부적으로 몇 가지 동작을 수행합니다.
1. 브랜치가 이동하면 HEAD 포인터도 함께 이동합니다.
2. 브랜치를 변경하려면 기존 브랜치의 워킹 디렉터리를 정리해야 합니다.

## 6.5.3 소스트리

소스트리에서 브랜치를 변경하는 방법은, 마우스 오른쪽 버튼을 누른 후, 체크아웃 메뉴를 선택하면 된다.

## 6.5.4 이전 브랜치

브랜치를 이동하려면 브랜치 이름을 적어줘야 한다. 
❗새로운 브랜치 아닌 ❗이전 브랜치로 편하게 이동하는 방법은 대시 기호를 이용하면 된다.


![이전 브랜치2](https://user-images.githubusercontent.com/105197472/195132567-629c9779-26e2-4c1d-b633-bbc6311077c7.PNG)


## 6.5.5 워킹 디렉터리정리

깃은 향후 충돌을 방지하기 위해 워킹 디렉터리에 작업이 남아 잇다면 경고 메세지를 보여주고 브랜치를 변경 할 수 없게 제한하기 때문에,
❗현재 작업하고 있는 워킹 디렉터리를 정리하고 체크아웃을 사용하여 브랜치를 이동해야 합니다!

# 6.6 브랜치 공간

## 6.6.1 브랜치 로그

현재까지 작업한 로그 기록을 확인 해보면


![6-1 1](https://user-images.githubusercontent.com/105197472/195135120-8959febc-9d78-45f4-b838-640f2e401f5a.PNG)

이 내역을 참고하여 커밋 과정을 나타내면


![6-1 2](https://user-images.githubusercontent.com/105197472/195135277-1226830b-f6b6-4f16-8fd1-43bd19511b84.PNG)


## 6.6.2 브랜치 소스 확인

현재까지는 master 브랜치에서만 코드를 수정하고 커밋 했다.
footer 브랜치의 소스 코드 내용을 확인 하면


![6621](https://user-images.githubusercontent.com/105197472/195136307-591c16f2-3b14-4b95-8c3c-d7e39075849f.PNG)


이제 master 브랜치로 ❗체크아웃하여 소스 코드를 확인해 보면,


![6622](https://user-images.githubusercontent.com/105197472/195136478-f522167b-6bea-408b-8391-46ebe983cc39.PNG)


footer는 한 줄 짜리 정보를 워킹 디렉터리에 가지고 있는 상태고, master는 두 줄짜리 정보를 워킹 디렉터리에 가지고 있는 상태라는 점이 다르다.


6.7 HEAD 포인터 : 깃의 대표적인 객체 포인터
●6.7.1 마지막 커밋
HEAD 작업 중인 브랜치의 마지막 커밋 ID를 가리키는 참조 포인터
깃은 HEAD 포인터를 부모 커밋으로 대체, 빠르게 스냅샷 생성
커밋 로그 이용하여 HEAD 확인
infoh@DESKTOP MINGW64 /e/gitstudy06 (master)
$ git checkout footer ##브랜치 이동
Switched to branch ‘footer’

infoh@DESKTOP MINGW64 /e/gitstudy06 (footer)
$ git log  --graph --all ##로그 확인  
* commit dcdb1c1fa4ef78bedd8dc13bc267e99391cc9782 (master)
¦ Author: hojin <infohojin@gmail.com>
¦ Date:   Sat May 11 18:45:35 2019 +0900
¦      master working...
¦
* commit d84766c7f87b1d9d234050949c48681ba4e35da8 (HEAD -> footer, feature) #HEAD 위치
Author: hojin <infohojin@gmail.com>
Date:   Sat May 11 17:10:02 2019 +0900
●6.7.2 브랜치 HEAD
브랜치를 이동하면 HEAD 포인트도 이동
infoh@DESKTOP MINGW64 /e/gitstudy06 (footer)
$ git checkout master ##브랜치 이동
Switched to branch ‘master’

infoh@DESKTOP MINGW64 /e/gitstudy06 (master)
$ git log  --graph --all ##로그 출력 
* commit dcdb1c1fa4ef78bedd8dc13bc267e99391cc9782 (HEAD -> master) #HEAD 위치
* commit dcdb1c1fa4ef78bedd8dc13bc267e99391cc9782 (master)
¦ Author: hojin <infohojin@gmail.com>
¦ Date:   Sat May 11 18:45:35 2019 +0900
¦      master working...
¦
* commit d84766c7f87b1d9d234050949c48681ba4e35da8 (footer, feature)
Author: hojin <infohojin@gmail.com>
Date:   Sat May 11 17:10:02 2019 +0900
     first
●6.7.3 소스트리 HEAD
각 브랜치의 마지막 위치를 브랜치 아이콘으로 표시
●6.7.4 상대적 위치
HEAD 포인터는 커밋 생성 및 브랜치 관리에 유용, 명령어 입력의 기준점으로 사용
마지막 커밋 위치인 HEAD를 기준으로 상대적 커밋 위치 지정
상대적 커밋 위치를 지정할 때는 캐럿(^)과 물결(~) 기호를 사용
##최근에는 해시키를 사용하는 것이 편리
●6.7.5 AHEAD, BHEAD
원격 저장소와 연동하여 깃을 관리하면 앞에 A 또는 B가 붙은 로컬 저장소와 원격 저장소의 브랜치 HEAD가 있다. AHEAD와 BHEAD는 서로 다른 저장소 간 HEAD 포인트의 위치 차이를 의미
AHEAD는 서버로 전송되지 않은 로컬 커밋 
로컬 저장소의 HEAD 포인트를 기준으로 로컬 브랜치에 있는 커밋이 서버의 커밋 개수보다 많은 경우
BHEAD는 로컬 저장소로 내려받지 않은 커밋이 있는 것 
원격 저장소의 커밋이 자신의 로컬 저장소보다 더 최신 상태

6.8 생성과 이동: 브랜치 생성은 branch 명령어, 브랜치 이동은 checkout 명령어 사용
●6.8.1 자동 이동 옵션 
체크아웃할 때 –b 옵션 사용하면 브랜치 생성과 이동 한 번에 가능
infoh@DESKTOP MINGW64 /e/gitstudy06 (master)
$ git checkout –b hotfix ##체크아웃
Switched to a new branch ‘hotfix’ ##브랜치 생성
infoh@DESKTOP MINGW64 /e/gitstudy06 (hotfix) ##체크아웃

infoh@DESKTOP MINGW64 /e/gitstudy06 (hotfix)
$ git branch –v ##브랜치 목록
  feature d84766c first
  footer  d84766c first 
* hotfix dcdb1c1 master working... ##현재의 브랜치
master  dcdb1c1 master working... ##브랜치 생성만 했기 때문에 같은 커밋 ID를 가리킴
●6.8.2 커밋 이동
브랜치 이름은 커밋 해시키와 동일 -> 브랜치 이름 대신 커밋 해시키 사용하여 체크아웃 가능 이때 해시키를 전체 사용하지 않고 앞의 7자리 정도만 사용해도 무리X 유일한 해시 값이 가지는 특징
infoh@DESKTOP MINGW64 /e/gitstudy06 (hotfix)
$ git brach –v ##브랜치 목록
  feature d84766c first
  footer  d84766c first
* hotfix  dcdb1c1 master working...
  master dcdb1c1 master working...

infoh@DESKTOP MINGW64 /e/gitstudy06 (hotfix)
$git checkout dcdb1c1 ##커밋으로 브랜치 이동
Note: checking out ‘dcdb1c1’.
You are in ‘detached HEAD’ state.You can look aroud, make experimental chages and commit them, and you can discard any  commits you make in this state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may do so (now or later) by using –b with the checkout command again. Example:

 git checkout – b <new-branch-name>
HEAD is now at dcdb1c1 master working...
infoh@DESKTOP MINGW64 /e/gitstudy06 ((dcdb1c1...))

●6.8.3 HEAD를 활용한 이동
HEAD 포인터를 사용하면 좀 더 간편하게 체크 아웃 할 수 있다.
예) $ git checkout HEAD~1 ##현재의 한 단계 전
뒤에 숫자만 바꾸면 여러 단계 이전으로 이동 가능
●6.8.4 돌아오기
과거의 커밋으로 체크아웃했다면 대시(-)를 사용하여 다시 현재로 돌아올 수 있다.

infoh@DESKTOP MINGW64 /e/gitstudy06 ((dcdb1c1...))
$ git checkout - ##이전 브랜치로 이동
Switched to branch ‘hotfix’

infoh@DESKTOP MINGW64 /e/gitstudy06 (hotfix) #브랜치 복귀
브랜치 이름을 입력하면 브랜치의 마지막 커밋 위치인HEAD 포인터로 복귀
$ git checkout master ##특정 브랜치로 복귀
  
  
# 6.9 원격 브랜치

## 6.9.1 리모트 브랜치

💬 **리모트 브랜치**:원격 저장소에 생성한 브랜치 <br>
1. 원격 저장소와 로컬 저장소의 브랜치 이름을 보통 같지만 반드시 일치하지 않아도 가능하다. <br>
2. 리모트 브랜치는 보통 별칭/브랜치 이름 형태이다. <br>

## 6.9.2 실습 준비

### ⚡ 깃허브 실습 저장소에 New repository 클릭 후 새 저장소 생성
![실습1](https://user-images.githubusercontent.com/105197524/194878535-b499048e-8612-4f32-89ca-c6acb3a5f68a.png)

**새 저장소 생성 후 다음과 같이 실행**
```bash
$ git remote add origin 주소 ->원격 저장소 등록
$ git remote -v -> 원격 저장소 목록
```
![실습2](https://user-images.githubusercontent.com/105197524/194878543-353236e0-7cce-4fbe-a5cc-0de1a9d08af1.png)

## 6.9.3 브랜치 추적

## 🔭 브랜치 추적:원격 저장소 브랜치를 가리키는 것 다른 용어로 트래킹 브랜치 <br>
### 로컬 저장소는 마지막으로 연결된 리모트 브랜치의 커밋 해시 값을 항상 가지고 있음

## 6.9.4 브랜치 업로드

### ⚡ 등록된 원격 저장소의 리모트 브랜치는 remote show 명령어로 확인 가능
![실습3-1](https://user-images.githubusercontent.com/105197524/194880929-d806a7b2-ecdf-4933-bde6-2a66bfd3d5d0.png)

### ⚡ 로컬 저장소에서 main 브랜치를 전송하기
```bash
$ git push -u origin main -> main 브랜치 전송
$ git push -u origin hotfix -> hotfix 브랜치 전송
```
## 🔭 원격 저장소에 잘들어감
![실습4](https://user-images.githubusercontent.com/105197524/194878549-46a310ee-742a-4cad-a8d7-ef196bf9613d.png)


## 6.9.5 이름이 다른 브랜치

### ⚡  다른 개발자가 만든 원격 서버의 브랜치를 테스트하려고 할 때 자신의 브랜치 이름과 같으면 충돌이 발생한다.이때 브랜치를 직접 수동으로 지정할 때는 콜론(:)으로 구분한다.

```bash
$ git push -u origin feature:function -> 다른 이름으로 브랜치 전송
```
![실습5](https://user-images.githubusercontent.com/105197524/194878550-6bf29046-6bb4-423f-ac8a-0e7d23830521.png)

## 6.9.6 업스트림 트래킹

## 🔭 업스트림 트래킹:로컬 저장소의 브랜치와 원격 저장소의 브랜치를 업로드할 수 있도록 매칭되는 것

### ⚡ 새롭게 저장소를 복제
```bash
$ git clone https://github.com/uh004/gitstudy06.git gitstudy06_clone -> 복제
$ cd gitstudy06_clone -> 폴더 이동
$ git branch -v ->브랜치 목록
$ git branch -r -> 리모트 브랜치 목록
$ git branch -vv -> 트래킹 브랜치 목록
$ git checkout --track origin/function -> 업스트림 브랜치 생성
```
![실습6](https://user-images.githubusercontent.com/105197524/194878553-f06d0e18-c114-4191-a457-26c523e80a71.png)
```bash
$ code branch.htm -> 복제된 gitstudy06_clone의 function 브랜치를 수정합니다. 입력
```
### ⚡ 복제 저장소 -> 원격 저장소 push
![실습7](https://user-images.githubusercontent.com/105197524/194878557-d5f5bfbe-a10c-48e9-b324-27fceca75796.png)
### ⚡ 원격 저장소 -> 원본 저장소 pull
![실습8](https://user-images.githubusercontent.com/105197524/194878560-ab6656b5-db90-404b-b5cb-8505e1ac731c.png)


## 6.9.7 원격 브랜치 복사

### ⚡ 원격 저장소에 브랜치 aaa 생성
![제목 없음](https://user-images.githubusercontent.com/105197524/194883294-541e9504-ab48-4006-8de5-b347a2dc8ad6.png)
```bash
$ git fetch -> 브랜치 커밋 가져오기
$ git branch -r -> 원격 브랜치 확인
$ git checkout -b aaa origin/aaa -> 브랜치 생성 및 이동
$ code branch.htm -> 새로운 .... 작업을 합니다. 입력
$ git commit -am "testing aaa" -> 등록 및 커밋
$ git push -> 커밋 전송
```
![실습9](https://user-images.githubusercontent.com/105197524/194878561-d3c32b88-2821-4fb9-bd8c-0069ef283f6e.png)

## 6.9.8 업스트림 연결

### ⚡ 원격 저장소에 브랜치 bbb 생성
![실습10](https://user-images.githubusercontent.com/105197524/194878562-2e1f7ce0-7eb1-4614-9719-f3d0a01f6694.png)

```bash
$ git fetch ->서버의 브랜치 정보 갱신
$ git branch -r -> 원격 브랜치 목록
$ git checkout -b bug -> 브랜치 생성
$ git branch -vv -> 트래킹 브랜치 목록
$ git branch -u origin/bbb -> 업스트림 연결
$ git branch -vv ->트래킹 브랜치 목록
```
![실습11](https://user-images.githubusercontent.com/105197524/194878564-e8f425fb-0116-478c-827d-441ec0b363b1.png)

### 📄 로컬 저장소의 bug 브랜치가 원격 저장소에 있는 aaa 리모트 브랜치의 트래킹 브랜치로 업스트림 된것을 확인

## 6.10 ~ 6.11 브랜치 전송과 삭제

### ⚡ 브랜치 푸시
![6 10](https://user-images.githubusercontent.com/105197546/195139052-8f252002-1372-40b3-a92f-5f95699d8341.png)

```bash
처음으로 로컬 저장소에 새로운 원격 저장소가 등록되면 위와 같이 오류가 발생합니다.
따라 파란색 선과 같이
$git push --set-upstream origin master
를 통해 업스트림을 설정해야 합니다.
```
### ⚡ 브랜치 패치
![6 10 2](https://user-images.githubusercontent.com/105197546/195139748-2a0e3523-d4f7-4ba3-a4af-6287e869140a.png)
![6 10 2-1](https://user-images.githubusercontent.com/105197546/195139762-89d01d69-532a-485d-8469-1f9475715533.png)

```bash
원격 저장소에서 페치된 커밋들을 새로운 로컬 브랜치로 바영하려면 변합 명령을 실행해야 합니다.
테스트만 하고 싶을 때는 원격 브랜치의 포인터를 사용하여 임시 브랜치를 생성, 체크아웃 할 수 있습니다.
```
### ⚡ 6.11 브랜치 삭제
![6 11 1 일반적인 삭제](https://user-images.githubusercontent.com/105197546/195140164-0fb5a32d-98d0-4d1d-967b-9638936bc583.png)
```bash
-d 옵션은 스테이지 상태가 깨끗할 때만 삭제를 허용합니다.
-D 옵션은 강제로 브랜치를 삭제 할 수 있습니다.
```
![6 11 1-1 삭제완료](https://user-images.githubusercontent.com/105197546/195140463-7e6967c6-0269-41a8-8ebc-9be8576c4143.png)
```bash
삭제가 된 모습을 확인할 수 있습니다.
```
![6 11 4 리모트 브랜치 삭제](https://user-images.githubusercontent.com/105197546/195140812-0aa6748e-af3c-4eee-9466-70432c81e448.png)
```bash
다음 명령어를 사용하면 리모트 브랜치도 삭제 가능합니다.
```

----------------------------------
<H2>6장의 브랜치에 관해 요약을 마칩니다. 감사합니다.</H2>
