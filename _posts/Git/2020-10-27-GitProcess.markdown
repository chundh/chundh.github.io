---
layout: post
title:  "Git Process"
categories: [Class, Git]
---

## Git의 영역
- Local workspace
  * Git의 repository를 clone하는 폴더이며, .git을 통해서 폴더 내부 파일의 변화를 추적하는 곳이다.
  * add 명령어를 통해 현재 상태를 update 할 수 있다.
- Staging Area
  * Local workspace에서 add명령어를 실행한 파일이 저장되는 곳이다.
  * rm 명령어로 해당 영역에 있는 데이터를 삭제할 수 있다.
  * commit 명령어로 데이터를 Local repository로 보낼 수 있다.
- Local repository
  * commit된 파일이 저장되는 곳이다.
  * push를 통해 Git으로 업로드 할 수 있다.
  * 스냅샷 형태로 업로드를 해서 언제든지 과거의 파일 상태를 확인하는 등 자동으로 버전관리가 된다.
- 위 과정을 통해 Git repository에 업로드가 완료된다.