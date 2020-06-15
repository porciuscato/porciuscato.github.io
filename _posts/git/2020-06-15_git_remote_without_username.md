---
comments: git 사용법을 정리하자.
title: git push/pull 시 username과 password 없이 하기
published: True
updated: 2020-06-15
tags: [git]
categories: [development]
---
git push/pull 시 username과 password 없이 하기



출처: [블로그](http://blog.naver.com/PostView.nhn?blogId=hancury&logNo=220778148466&categoryNo=0&parentCategoryNo=10&viewDate=&currentPage=1&postListTopCurrentPage=1&from=search)



1. github에 로그인

2. https://github.com/settings/keys 로 이동해서

3. New SSH Key 버튼 클릭

4. SSH key 이름을 만들고, ssh public key에 내용을 넣는다.

   \+ 키 생성법:

   ```bash
   $ ssh-keygen -t rsa
   ```

   공개키와 개인키를 생성한다.

   ```bash
   $ cd ~/.ssh
   $ ls
   => id_ras, id_ras.pub
   ```

   .pub가 붙은 건 공개키, 아닌 건 개인키다.

   공개키를 ssh public key 부분에 넣는다.

5. github 프로젝트 페이지에서 clone or download 클리 후 Use SSH 클릭하여 아래 링크를 복사한다.

6. git의 local project 폴더에서 

   ```bash
   $ git remote set-url origin 복사링크
   ```

7. 이제 git push/pull시 username과 password를 입력하지 않아도 된다.