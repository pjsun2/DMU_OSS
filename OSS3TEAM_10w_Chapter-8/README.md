# 8장 병합과 충돌 요약 정리입니다.
# 🔔병합
❗독립된 브랜치에서 개발 작업이 끝나면 다시 원본 브랜치에 작업한 결과를 반영해야 합니다. 분리된 브랜치를 한 브랜치로 작업을 병합(합치기)이라고 합니다.두 코드를 하나씩 직접 비교해가며 수동으로 병합하거나 깃 도구를 사용하여 자동으로 병합할 수 있습니다.❗

## 📌8.1.1 하나씩 직접 비교하는 수동 병합
#### 수동으로 병합하려면 양쪽 파일을 일일이 비교하며 바뀐 점을 찾아서 적용해야 한다.하지만 오류 없이 코드를 병합하는 것은 간단하지 않다. <br>
❗예를들어 소스 코드가 2개보다 많다면 어떻게 될까요? 원본 소스 A를 복제하여 B를 수정하고, B를 복제하여 C도 수정하고 있습니다.<br>
수정이 완료되면 B는 원본 소스 A에 수정 내역을 반영하는 작업을 해야하고, C 또한 B를 반영하여 수정된 원본 소스 A에 또다시 수정 작업을 반영해야 합니다.병합하려면 코드의 변경된 시점을 기억해야 합니다.변경된 시점을 기준으로 순차적으로 병합 처리를 하는 것이 좀 더 쉽습니다.❗ <br>

![image](https://user-images.githubusercontent.com/105197524/200317261-770b1de7-a2cb-47fc-bb13-4209cc696593.png)

## 📌8.1.2 깃으로 자동 병합

1. 깃은 자동 병합은 원본을 기준으로 두 파일의 변경 이력을 비교합니다. <br>
2. 깃의 병합은 브랜치를 기준으로 합니다. <br>

따라서 과거에는 모든 병합 작업을 수동으로 해서 여려웠지만, 이제는 이러한 수동 병합 작업을 깃이 대신 처리합니다. 하지만 깃이 모든 코드의 병합을 완벽하게 처리는 할수 없고 아무리 좋은 도구라해도 자동으로 반영하지 못하는 것들이 있는데 이를 **충돌**이라 합니다.

## 📌8.1.2 병합 방식
깃은 병합을 위해 두 가지 기본적인 알고리즘 방식을 제공한다.
- Fast-Forword 병합
- 3-way 병합

두 방식으로 실습하기 전에 미리 별도의 저장소를 생성해 두겠습니다.

![제목 없음](https://user-images.githubusercontent.com/105197524/200338767-50a1d7b6-84e1-4e58-9d4b-c348dcb7e216.png)

## 📌Fast-Forward 병합
**깃의 가장 간단한 브랜치 병합은 Fast-Forward 방식이다.일반적으로 혼자 개발할 때 사용한다.**

## 📌 8.2.1 브랜치 생성과 수정 작업
브랜치를 생성 후 브랜치 커밋 확인
```
$ git checkout -b feature --- 브랜치 생성 및 이동
PC18@LAPTOP-L4CJE14H MINGW64 ~/Desktop/e/study08 (feature)

$ git rev-parse feature  --- 브랜치 커밋 확인
525bf0f445d8829a9759d215071901799791db5a
```
index.htm 파일 수정후 등록 및 커밋 후 커밋 이력 확인

```
$ code index.htm  --- feature 브랜치 안에 있는 index.htm 파일 수정
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <header>
  </header>
  <h1>hello GIT world!</h1>
</body>
</html>
```
등록 및 커밋후 커밋 이력 확인하기
```
$ git commit -am "add header" --- 등록 및 커밋
[feature a209baf] add header
1 file changed, 2 insertions(+)

$ git log  --- 커밋 이력 확인하기
commit a209bafd738333feebf1c37c6f914f7df05e9fce (HEAD -> feature)
Author: uh004 <uh004@naver.com>
Date:   Mon Nov 7 23:54:56 2022 +0900

    add header

commit 525bf0f445d8829a9759d215071901799791db5a (main)
Author: uh004 <uh004@naver.com>
Date:   Mon Nov 7 23:43:53 2022 +0900

    frist
```
feature 브랜치에 등록 및 커밋 2번하기
```
$ code index.htm  --- feature 브랜치 안에 있는 index.htm 파일 수정
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <header>
    <ul>
      <li>깃소개</li>
    </ul>
  </header>
  <h1>hello GIT world!</h1>
</body>
</html>

$ git commit -am "add menu1"  --- 등록 및 커밋
[feature 3c0edb4] add menu1
 1 file changed, 3 insertions(+)
```

```
$ code index.htm  --- feature 브랜치 안에 있는 index.htm 파일 수정
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
</head>
<body>
  <header>
    <ul>
      <li>깃소개</li>
      <li>깃설치</li>
    </ul>
  </header>
  <h1>hello GIT world!</h1>
</body>
</html>

$ git commit -am "add menu2"  --- 등록 및 커밋
[feature 140f38d] add menu2
 1 file changed, 1 insertion(+)
```
**소스트리에서 브랜치 커밋 로그를 확인해 보면 feature 브랜치가 main 브랜치에서 분리되어 header, menu1, menu2 커밋 작업을 세 번 수행한 것을 볼수 있다.**
```
$ git log --graph --oneline --all  --- 모든 커밋 이력을 한줄그래프로 확인
* 140f38d (HEAD -> feature) add menu2
* 3c0edb4 add menu1
* a209baf add header
* 525bf0f (main) frist
```
소스트리에서 확인

![제목 없음](https://user-images.githubusercontent.com/105197524/200343762-e7737cdb-1a70-4c5e-b9f3-7bcfdfbf9965.png)

## 📌8.2.2 병합 위치
**브랜치를 병합하려면 가준과 대상이 있어야 합니다.기준은 체크아웃된 현재 브랜치입니다. 우리는 main 브랜치에서 feature 브랜치로 분기하여 작업했습니다.
병합을 하기위해서 main 브랜치로 체크아웃 하겠습니다.**
```
$ git checkout main
Switched to branch 'main'
```
main 브랜치로 체크아웃하고 파일을 확인하면 feature에서 했던 작업이 사려졌습니다. 이제 feature 브랜치에서 작업한 내용을 병합해 보겠습니다.
```
code index.htm --- VS Code 실행
```

## 📌8.2.3 Fast-Forward 병합 적용
커밋 작업은 분기된 feature 브랜치에서 모두 수행했습니다. 아직 main 브랜치에는 추가된 커밋이 없습니다. 이러한 상태에서 두 브랜치를 병합해보겠습니다.
```
$ git merge feature
Updating 525bf0f..140f38d
Fast-forward
 index.htm | 6 ++++++
 1 file changed, 6 insertions(+)
```
main 브랜치와 feature 브랜치가 잘 병합된것을 확인할 수 있다. vscode를 실행하면 feature에서 수정한 내용이 적용되었습니다.
```
$ git log --oneline
140f38d (HEAD -> main, feature) add menu2
3c0edb4 add menu1
a209baf add header
525bf0f frist

$ code index.htm  --- vscode 실행
```
**Fast-Forward 병합은 병합할 하나의 브랜치 파일을 기준 브랜치로 복사하여 수정된 파일을 원본에 그대로 적용한 것과 같습니다.** <br>
**즉 원본에 추가된 내용이 없다는 가정하에 변경한 파일을 대체하는 것입니다.**

## 📌8-3 3way 병합

3way 병합은 복잡한 병합을 처리할 수 있는 방법이며, 여러 개발자와 협업으로 작업하는 경우 대부분 이 방법을 사용함.

![1](https://user-images.githubusercontent.com/105197472/200488119-1dae5b2b-4ac9-4dcc-9760-3ca6fb6d5e9b.PNG)

hotfix 브랜치를 생성하고, hotfix 브랜치로 체크아웃 하는 과정. (현재 브랜치 위치는 hotfix)

![2](https://user-images.githubusercontent.com/105197472/200488262-87d863f7-9427-4e47-8485-44730993db88.PNG)

<footer></footer> 태그를 추가하고 내용을 적는 실습 과정 진행. 커밋은 두 번으로 나누어 진행. 우선 <footer> 태그 추가하고 저장.

![3](https://user-images.githubusercontent.com/105197472/200488336-ee1ffeb4-d15a-48a4-9343-53e079cb2ea5.PNG)

    
수정한 파일은 Modified 상태가 됨. 수정한 파일을 다시 Staging Area에 등록한 후 Commit.


![4](https://user-images.githubusercontent.com/105197472/200488569-04abb2d2-56f8-4f95-9ab6-8508fa9995d8.PNG)

다시 index.html 파일에 <footer> 내용을 추가한 후 Commit.

![5](https://user-images.githubusercontent.com/105197472/200488779-f0a26cf2-01ca-43c3-b8ac-6c4026545fb8.PNG)

    
![6](https://user-images.githubusercontent.com/105197472/200488844-d57d24a6-f613-431c-8109-d80c3a3f8997.PNG)

이를 그림으로 나타내면 다음과 같음.

![7](https://user-images.githubusercontent.com/105197472/200488992-0000c7cd-9032-4884-b1fc-993a17c8e4e2.PNG)
   
소스트리에서 커밋 로그 확인.
    
![8](https://user-images.githubusercontent.com/105197472/200489090-1e22e592-a1db-4900-9901-1660fd07dc68.PNG)

현재 hotfix 브랜치에 새로운 Commit이 2개 추가 되었음. 지금까지 hotfix 브랜치에서 진행한 수정은 Fast-Forward 병합과 유사함.

## 📌 8-3-2. 마스터 변경.

브랜치 모양을 변경하는 실습을 진행. 우선 hotfix 브랜치에서 master 브랜치로 이동.
    
![9](https://user-images.githubusercontent.com/105197472/200489283-ff9c20f2-6123-42ea-87f6-9d7215dd0f7e.PNG)


![10](https://user-images.githubusercontent.com/105197472/200489318-90d90043-c43c-4511-8899-416e7d2990a7.PNG)

hotfix 브랜치의 마지막 커밋은 7277f2d, master 브랜치의 마지막 커밋은 7caf5f0임. 시간순으로 우선인 master 브랜치에 새로운 커밋을 추가할 예정.
    
![11](https://user-images.githubusercontent.com/105197472/200489473-5c01870f-1a9f-4e1e-989b-9b66be7b5554.PNG)


![12](https://user-images.githubusercontent.com/105197472/200489631-5a71743d-848b-4047-b0bf-b0ca3d26b9c6.PNG)

master 브랜치의 index.htm 파일에 menu3 추가 후 Commit
 
![13](https://user-images.githubusercontent.com/105197472/200489816-32bfe652-aac0-4c60-be3e-5819098e7c83.PNG)

![14](https://user-images.githubusercontent.com/105197472/200489859-b1f79c0c-d698-446b-a8c0-a299404e075c.PNG)

    
menu4를 추가 후 Commit

위와 같은 실습을 진행한다면 메뉴가 4개가 생성됨. master 브랜치에 추가 Commit이 발생하면 브랜치는 7caf5f0을 기준으로 hotfix와 master 브랜치로 갈라짐. 기준 Commit에서 서로 다른 브랜치의 Commit이 연결됨.
    
![15](https://user-images.githubusercontent.com/105197472/200490000-9419e370-b773-4810-93a6-d22f6a7b440f.PNG)

소스트리에서 master ㅂ랜치의 그래프 모양을 확인해 보면 Fast-Forward 병합과 다르게 브랜치가 확실하게 나뉘어져 있음.
    
![16](https://user-images.githubusercontent.com/105197472/200490106-e36cc5d8-0c8d-4760-8cc0-2662f04b475d.PNG)
    
## 📌 8.3.3 공통 조상
    
8-3-2에서 진행 실습에서 브랜치별로 각각 Commit시, hotfix와 master 브랜치로 갈라지는 것을 확인 할 수 있었음. 브랜치 모양이 갈라지는 형태로 나뉠 때는 Fast-Forward 방식의 알고리즘을 적용하여 병합할 수 없음. 이 때 사용하는 방법이 3-way 방식.

    
![17](https://user-images.githubusercontent.com/105197472/200490292-2c36fa06-bdfb-4d4a-bb79-205c38615db2.PNG)

2개의 브랜치를 병합하려면 공통 커밋을 찾아야 함. 이 공통 커밋을 공통 조상 커밋이라고 함. 공통 조상 커밋을 포함하는 브랜치와 새로운 두 브랜치, 세 개의 브랜치를 하나로 병합하는 과정에서 브랜치가 3개 있기 때문에 3-way 병합이라고 함.        
깃은 공통 조상 커밋을 자동으로 찾아줌. 이것이 다른 VCS보다 서로 다른 브랜치를 편리하게 병합할 수 있는 장점임.

    
## 📌 8.3.4 병합 커밋

    
병합은 각 브랜치에서 독립적으로 작업된 소스를 파일 하나로 결합. 깃을 사용하면 복잡한 병합도 손쉽게 처리 가능. 3-wqy 병합은 두 브랜치의 공통 조상 커밋을 자동으로 찾아주고, 이를 기준으로 병합.
그리고 병합을 완료하면 새로운 커밋을 추가해 추가로 하나를 생성. 이 생성된 커밋을 병합 커밋이라고 함. 병합 커밋은 부모 커밋이 2개임.
    
    
![18](https://user-images.githubusercontent.com/105197472/200490947-fee6a4c9-1f3b-4d53-bb61-3d29f33fd0ed.PNG)

hotfix 브랜치를 master 브랜치에 병합하는 과정 실습. hotfix 브랜치를 병합하려면 master 브랜치로 Check-out 해야함.
    

![19](https://user-images.githubusercontent.com/105197472/200492379-24ae4341-f539-4ae5-af1b-4f34c155b341.PNG)


 3-way 방식으로 두 브랜치를 병합한것을 그림으로 나타내면 아래와 같음.
    
![20](https://user-images.githubusercontent.com/105197472/200491191-7f9457d9-b8bc-44b5-a435-8eaf25d98bf6.PNG)
    
병합 후에는 커밋 로그를 확인함.
    
    
![21](https://user-images.githubusercontent.com/105197472/200491247-c3cb6df9-4152-4aa3-97a1-f8767234128b.PNG)
    
소스트리에서 확인.
    

![22](https://user-images.githubusercontent.com/105197472/200491286-6839928f-cd80-4758-b304-2b1d08da75d9.PNG)
    
## 📌 8.3.5 병합 메세지
    
3-way 병합 방식은 Fast-Forward 병합과 달리 메시지가 필요하다. 깃은 두 브랜치를 병합한 후에 새로운 커밋을 하면 동시에 메세지를 자동 생성함.자동 메세지 외에 직접 메세지를 작성 할 수 있음 merge 명령어 -e 또는 --edit 옵션을 사용하면 됨.
    

![23](https://user-images.githubusercontent.com/105197472/200491549-063f21c7-895b-4376-8537-f77d266f5e5f.PNG)
    
직접 병합 메세지를 작성하기 위한, 앞선 병합을 취소하고 새로운 메세지를 작성하여 다시 병합.
    
![24](https://user-images.githubusercontent.com/105197472/200491686-52fa7a0e-987b-4725-b89b-89bb2c4e586a.PNG)
    

![25](https://user-images.githubusercontent.com/105197472/200491830-b40c44e2-8957-4cac-86f3-baff8c8fbf53.PNG)


이를 실습하면 vi 에디터 창이 열리게 됨.
    
    
![26](https://user-images.githubusercontent.com/105197472/200491760-e83b7572-62ad-48f4-b913-26a9727417ab.PNG)
    
병합 메세지를 작성하고 종료하면, 결과 메세지가 출력되고 직접 작성한 메세지로 커밋됨.
    
# 📌 8.4 브랜치 삭제
## 8.4.1 병합 후 삭제
    
병합된 브랜치의 커밋은 원본 브랜치에 모두 적용됨. 따라서 불필요한 브랜치는 삭제 하면 됨.
삭제 할 때는 -d 옵션을 사용하는데, 이는 병합을 완료한 브랜치만 삭제 가능함.
    
![28](https://user-images.githubusercontent.com/105197472/200492097-1b0ee0cb-da73-4755-91cd-6efd4e14111e.PNG)
    
병합이 완료되지 않은 브랜치를 삭제 한다면 대문자 -D 옵션을 사용해야함.

# 📌 8.5 충돌
## 8.5.1 충돌이 생기는 상황

- 여러 개발자가 서로 다른 위치에서 파일을 수정하는 경우  
  ▶️ 깃에서 서로 다른 위치의 소스를 자동으로 병합하기 때문에 문제가 발생하지 않는다.
  
- **동일한 위치에서 두 명 이상이 서로 다르게 파일을 수정하는 경우**  
  ▶️ 두 수정 내용 중에서 어떤 것이 맞는 것인지를 깃에서 자동으로 파악할 수 없기 때문에 충돌이 발생한다.  
  ▶️ 깃은 충돌 오류임을 알려주고 개발자가 직접 어떤 수정 내용을 선택할지를 결정하여 충돌을 해결하라고 요청한다.
  
보통 **충돌**은 **3way 병합이 실패**한 경우에 많이 일어난다.
  

## 8.5.2 실습을 위한 충돌 만들기

1. 새로운 footer 브랜치를 만들고 체크아웃한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main)
$ git checkout -b footer     # 기준 브랜치인 main에서 새로운 브랜치 파생
Switched to a new branch 'footer'

뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (footer)
```
<br/>
  
2. footer 브랜치에서 index.htm 파일의 <footer>~</footer> 부분 코드를 수정하고 커밋한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (footer)
$ code index.htm     # VS Code 실행하여 index.htm 파일 편집
```

다음과 같은 내용으로 편집한다.
```html
<!DOCTYPE html>
<html></html>
<head>
    <meta charset="UTF-8" />
    <meta name = "viewport" content = "width=device-width, inital-scale=1">
    <title>Page Title</title>
</head>
<body>
    <header>
        <ul>
            <li>깃소개</li>
            <li>깃설치</li>
        </ul>
    </header>
    <h1>hello GIT world!</h1>
    <footer>
            copyright all right 2018 reserved     
            by hojinlee          <!-- copyrighter 부분을 2줄로 수정함. -->
    </footer>
</body>
</html>
```
<br/>
  
3. 이어서 커밋을 진행한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (footer)
$ git commit -am "edit footer"
[footer af8cbd3] edit footer
 1 file changed, 2 insertions(+), 1 deletion(-)
```
<br/>
  
4. 다시 main 브랜치로 이동하여 index.htm 파일을 수정한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (footer)
$ git checkout main
Switched to branch 'main'
```

index.htm 파일을 수정할 때는 충돌이 발생하도록 동일한 위치의 내용을 수정하고 커밋한다.
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>Page Title</title>
</head>
<body>
    <header>
        <ul>
            <li>깃소개</li>
            <li>깃설치</li>
            <li>커밋</li>
            <li>브랜치</li>
        </ul>
    </header>
    <h1>hello GIT world!</h1>
    <footer>
        copyright all right 2020 reserved 
        by jinyphp     <!-- 두 줄로 만들고 hojinlee를 jinyphp로 수정하였다. -->
    </footer>
</body>
</html>
```
<br/>

5. 이어서 등록 및 커밋을 진행한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main)
$ git commit -am "edit copyright"
[main f0bdc30] edit copyright
 1 file changed, 2 insertions(+), 1 deletion(-)
```
<br/>
  
6. main 브랜치와 footer 브랜치 각각에 커밋이 하나씩 추가되었다. 서로 다른 브랜치에서 각각 커밋했기 때문에 그래프가 두 갈래로 갈라져야 한다. 아래와 같이 소스트리에서 확인      가능하다.

![image](https://user-images.githubusercontent.com/99963066/201524360-adf29296-3764-4c87-a6c4-008b83e921e3.png)
<br/>
  
7. 서로 다르게 분기된 브랜치이기 때문에 **3-way 병합**을 시도해 본다. 현재 브랜치가 **main인지를 확인** 후 병합 명령어를 실행한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main)     # 기준 브랜치
$ git merge footer      # 병합 실행
Auto-merging index.htm
CONFLICT (content): Merge conflict in index.htm
Automatic merge failed; fix conflicts and then commit the result.     # 충돌 발생(깃에서 Merge Conflicts 메시지 출력)
```
index.htm 파일에서 같은 위치의 내용을 각각 다르게 수정하였기 때문에 자동 병합이 되지 않고 충돌이 발생하게 된다.
<br/><br/>

8. 소스트리에서 그래프를 확인하면 충돌 발생으로 인한 커밋되지 않은 변경 사항이 하나 추가되어 있다.

![image](https://user-images.githubusercontent.com/99963066/201524707-31a49dd7-efa2-40c1-a7a0-5c5afa483a4d.png)  

▶️ 병합 충돌이 발생하면 자동으로 커밋이 생성되지 않는다. 따라서 수동으로 해결해야 한다.
<br/>
  
9. 어떤 충돌 상태인지 알아보기 위해 깃 상태를 확인한다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main|MERGING)     # 충돌 사항 표시
$ git status
On branch main
You have unmerged paths.     # 충돌 사항
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:     # 충돌 내용이 Unmerged인 것을 확인 가능하다.
  (use "git add <file>..." to mark resolution)
        both modified:   index.htm

no changes added to commit (use "git add" and/or "git commit -a")
```
현재 충돌된 병합을 해결해야 하는 상태임을 알 수 있다.
<br/><br/>

### 충돌 예방 방법
위와 같은 충돌은 피할 수 없지만 예방은 가능하다. 
- 내부적으로 팀원 간 규칙을 정하고 상의하면서 개발을 진행하면 향후 발생할 충돌을 많이 줄일 수 있다.
- main 브랜치 내용을 자주 자신의 브랜치로 병합한다. 자주 커밋하고 병합할수록 충돌이 발생할 기회는 적다.
<br/>
  

## 8.5.3. 수동으로 충돌 해결
  
충돌 발생은 결국 **수동**으로 해결해야 한다. 
<br/><br/>

1. 충돌한 소스 코드를 확인한다.
```bash
  뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main|MERGING)    
$ code index.htm     # VS Code 실행
```
  
2. 깃은 충돌 발생 시 충돌된 코드 내용을 다음과 같이 기호와 함께 표시한다.

![image](https://user-images.githubusercontent.com/99963066/201615502-8ce03cc5-8113-4ba3-a044-2e828ccf6aee.png)

  
충돌은 다음과 같이 두 부분으로 표시된다.
```
<<<<<<< HEAD
기준이 되는 브랜치(main)의 내용
=======
병합하고자 하는 브랜치의 내용
>>>>>>> 브랜치 이름
```
<br/>

충돌한 내용을 수정할 때에는 깃에서 표시한 충돌 기호도 함께 삭제해야 한다. 코드를 수정하고 표시된 기호도 같이 삭제하여 다음과 같이 수정 후 저장한다.

![image](https://user-images.githubusercontent.com/99963066/201617760-8bb86401-7b9d-4916-9cdf-d36b6526ee36.png)
<br/>
 
3. 다음과 같은 저수준 명령어를 통해 충돌한 파일들의 집합 확인도 가능하다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main|MERGING)
$ git ls-files -u
100644 0499cb94de55176c4ed39a44f707175463e47d4a 1       index.htm
100644 840f4f46074c77f18b513d75b8d742666fd962bc 2       index.htm
100644 fe149fcf49bbfa3330b88fbd6d1f1fe99a26bb36 3       index.htm
```
<br/>

4. 충돌이 발생하면 병합 커밋을 자동으로 생성하지 않으므로 충돌을 해결한 후 병합 커밋을 직접 만들어야 한다.
직접 충돌을 해결하면 파일은 modified 상태가 된다.
```bash
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main|MERGING)
$ git add index.htm     # 스테이지에 등록

뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main|MERGING)
$ git commit -m "resolve complicit"     # 병합 커밋 작성
[main a9f5802] resolve complicit
   
뚜비@DESKTOP-SKBKL14 MINGW64 /c/OSS/git/10w chapter 08 (main)     # 충돌이 해결되어 깃의 충돌 마크가 사라짐.(|MERGING 이 사라짐)
$
```
<br/>

# 📌 8.7 리베이스
## 8.7.1 베이스
  ❗ 브랜치는 특정 커밋을 가리키는 포인터로 커밋 하나를 기준으로 **새로운 작업을 진행할 수 있는 분리된 작업 경로**를 의미합니다.
  
<br/>
  
  ![8 7 1](https://user-images.githubusercontent.com/105197546/201688206-7dd0bc32-e94a-4121-91eb-88e315dc4b12.jpg)
  새로운 브랜치가 파생되는 커밋2를 **베이스** 라고 합니다.
  
<br/>
  
## 8.7.2 베이스 변경
  ![8 7 2](https://user-images.githubusercontent.com/105197546/201689223-06250d85-e419-462e-8db1-a409ac3837a6.jpg)

## 8.7.3 리베이스 vs 병합
  |병합|리베이스|
  |:--:|:--:|
  |파생된 두 브랜치를 하나로 합치는 과정|두 브랜치를 서로 비교하지 않고 순차적으로 키멋 병합|
## 8.7.4 ~ 8.7.9 rebase 명령어
  
  <br/>
  
![1](https://user-images.githubusercontent.com/105197546/202142216-92e3aee0-7e3b-41a0-bd6c-6485a254bd59.png)
  
  <br/>
  
![2](https://user-images.githubusercontent.com/105197546/202142226-d153d6fb-269d-4e6a-bbdf-0756728276d8.png)
  
  <br/>
  
![3](https://user-images.githubusercontent.com/105197546/202142234-b904e7b3-b04a-4a57-a951-eb693618ba4b.png)
  
  <br/>
  
![4](https://user-images.githubusercontent.com/105197546/202142244-ebe3f59d-e000-40a0-b95c-ba120d8aab1d.png)
  
  <br/>
  
![5](https://user-images.githubusercontent.com/105197546/202142255-116863b9-2a0e-4ba2-b498-0dc72bc3281a.png)
  
  <br/>
  
![6](https://user-images.githubusercontent.com/105197546/202142265-840cd890-21b2-496a-9e1f-91307eef7221.png)
  
  <br/>
  
![7](https://user-images.githubusercontent.com/105197546/202142270-3a26130b-985c-4268-962c-ab5befcc9750.png)
  
  <br/>
  
![8](https://user-images.githubusercontent.com/105197546/202142279-f6dbe7e1-f35a-4f5d-b02e-2f52d3232f25.png)
  
  <br/>
  
![9](https://user-images.githubusercontent.com/105197546/202142288-4fc35349-dcca-4498-9549-31dae47978a6.png)
  
  <br/>
  

  
## 8.7.10 리베이스할 때 주의할 점
  
🚫 리베이스는 커밋 위치와 해시 값을 변경, **저장소를 외부에 공개했다면 공개된 순간부터 커밋은 리베이스를 사용하지 않는 것이 원칙**
# 📌 8.8 정리
다수의 개발자와 협업할 때 병합과 충돌을 매우 자주 발생합니다. 충돌을 해결하고 병합을 처리하는 것은 쉬운 작업이 아닙니다. 개발 과정에서 병합 충돌을 최소화하고 예방하려면, master 브랜치 내용을 자주 반영하여 병합하는 것이 좋습니다
원격 저장소의 master 브랜치를 모니터링하고, 변화된 부분을 즉시 반영하면서 작업하면 충돌을 최소화하거나 예방할 수 있습니다.
