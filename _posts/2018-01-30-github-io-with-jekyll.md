# 지킬(Jekyll)로 블로그 만들기

> Jekyll을 이용해서 github.io 블로그를 만들어보자



## Jekyll이란?

지킬은 다양한 포맷의 텍스트 데이터를 읽어서 변환기 및 liquid 렌더러를 통해 가공해서, 웹사이트에 바로 게시할 수 있게 해준다.
또한 jekyll은 github pages의 내부 엔진이기도 하다 -> 자신의 페이지나 블로그, 웹사이트를 github에 호스팅 할 수 있다는 것.



## 지킬 테마 고르기

http://jekyllthemes.org/ 에서 테마를 하나 고르고, 자신의 깃헙에 fork를 뜬다. 그리고 [자신의 깃헙아이디].github.io 로 repository 명을 rename을 한다.(github.io 블로그를 만들기 위함, 자동으로 호스팅해준다.)

> **블로그가 잘 나오지 않는 경우**
>
> 1. 퍼블리싱이 안되는 경우
>
>      이렇게까지 했는데 [자신의 깃헙아이디].github.io를 통해서 들어갔는데 아무것도 안뜬다면, _config.yml에서 설정을 더 해줘야한다. 아마 fork를 떴기 때문에 _config.yml의 site setting에서 url부분이 fork를 뜬 기존 블로그 url일 것이므로 자신의 url로 바꿔주면 해결된다. 
>
>    ​
>
> 2. 경로를 잘 못찾아서 css, js가 제대로 로딩이 되지 않는 경우
>
>      페이지가 로딩은 되지만, 내가 선택했던 테마대로 안나온다면 경로를 지정해줘야한다. 
>       -> 현재 css, js는 path가 /[fork뜬 repository name]/css or js로 되어있으므로, baseurl부분을 "" 이렇게 바꿔줘야한다.
>
> 위의 두 사항을 해결한 _cofing.yml은 아래와 같다.
>
> ```
> # Site settings
> title:          Tale
> description:    "Minimal Jekyll theme for storytellers"
> baseurl:        ""
> url:            "https://seobew.github.io"
>
> # Author
> author:
>   name:         seobew
>   url:          https://seobew.github.io
>   email:        seobew@gmail.com
>
> # Build settings
> markdown:       kramdown
>
> # Assets
> sass:
>   sass_dir:     _sass
>   style:        compressed
>
> # Gems
> plugins:
>   - jekyll-paginate
>
> # Permalinks
> permalink:      /:year-:month-:day/:title
> paginate:       5
> ```





##내부 구조 파악하기

* _config.yml : 전역 환경설정 파일로 yams형식을 사용한다.

* _layouts : 기본 레이아웃 폴더로, 포스트의 레아이웃 file을 저장한다.

* _posts : 마크다운 블로그 포스트 파일들을 넣는 곳이다.

  > **YYYY-MM-DD-[POST SLUG].[FORMAT] **이런식으로 포맷을 지켜줘야한다.
  >
  > 예를 들면 2018-02-01-First-Post.md 처럼!

* _site : 컴파일된 블로그 사이트 파일들이 있는 곳이다.

* _includes : partial 파일들이 있는 곳 ({% include something.html %} 처럼!)

> front-matter라는 것이 있는데, 지킬에게 어떤 파일을 처리할 방법을 알려주는 일종의 메타데이터이다. 그리고 처리할 파일은 가장 상위에 있어야하며 아래 같이 fron matter 블록으로 시작되는 파일만 처리한다. 
>
> ```
> ---
> layout: post
> title: Blogging Like a Hacker
> ---
> ```



## 포스트 만들기

**YYYY-MM-DD-[POST SLUG].[FORMAT]** 이런식으로 형식을 지키고,

front-matter를 이용해서 레이아웃, 제목, 그리고 작성자를 명시해준다. (*아래와 같이)

---
layout: post

title: "Pagination Post"

author: "Chester"

그 다음에는 자유롭게 마크다운 형식으로 작성한다음에 깃헙에 push를 하면 된당.



## 참고

지킬 공식 docs : http://jekyllrb-ko.github.io/docs/home/

놀부님 블로그 : https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/