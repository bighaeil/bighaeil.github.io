#intellij tip
##package dots to folder

프로젝트를 git 으로 clone 하고 프로젝트를 열고
package 를 추가했는데 Project View 에 정상적으로 group 되어 있지 않다면

당연히 ex) com.example.demo 로 있어서 **com/example/demo** 인 줄 알았는데
폴더 이름이 **com.example.demo** 이였다.

##해결방법
1. "com.example.demo" right click > Refactor > Move Package or Directory click
2. 별 설정이나 변경없이 OK 하면 알아서 변경된다.
---
3. (만약) Project 에서 <span style="color:red">빨간줄</span>이 생긴다면 ex) not access class intellij 를 재시작하세요.
