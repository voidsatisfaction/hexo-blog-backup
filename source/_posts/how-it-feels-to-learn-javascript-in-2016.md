---
layout: post
title: 2016년에 자바스크립트를 배우는 기분(스크랩)
categories:
  - JavaScript
  - ECMA Script6
tags:
  - JavaScript
---

## 출처

[How it feels to learn JavaScript in 2016 - 번역](http://www.looah.com/article/view/2054)

## 키워드


## 내용

   ## How it feels to learn JavaScript in 2016

   ## 2016년에 자바스크립트를 배우는 기분

   Edit: Thanks for pointing typos and mistakes, I’ll update the article as noted. Discussion in [HackerNews](https://news.ycombinator.com/item?id=12628921) and [Reddit](https://www.reddit.com/r/programming/comments/55okik/how_it_feels_to_learn_javascript_in_2016_xpost/).
   수정: 오타와 실수를 지적해줘서 고맙당. 말했던 대로 문서를 갱신할께. 토론은 해커뉴스랑 레딧에서.

   The following is inspired by the article “It’s the future” from Circle CI. You can read the original [here](https://circleci.com/blog/its-the-future/). This piece is just an opinion, and like any JavaScript framework, it shouldn’t be taken too seriously. No JavaScript frameworks were created      during the writing of this article.
   이건 Circle CI의 “It’s the future”에서 영감을 받아 작성된 글이야. 원본은 요기에서 읽을 수 있어. 그냥 자바스크립트 프레임워크에 대한 의견일 뿐이니까 넘 심각하게 받아들이진 말아줘. 적어도 이 글을 쓰는 동안은 새로운 자바스크립트 프레임워크가 나오진 않았어 ㅋㅋㅋ

   Hey, I got this new web project, but to be honest I haven’t coded much web in a few years and I’ve heard the landscape changed a bit. You are the most up-to date web dev around here right?
   야, 내가 새로운 웹 프로젝트를 받았거든, 근데 솔직히 내가 몇 년 동안 웹 코딩을 안했더니 뭐가 어떻게 달라졌는지 잘 모르겠어. 네가 요즘 웹 굴러가는 걸 좀 알고 있지? 좀 털어봐.

   The actual term is Front End engineer, but yeah, I’m the right guy. I do web in 2016\. Visualisations, music players, flying drones that play football, you name it. I just came back from JsConf and ReactConf, so I know the latest technologies to create web apps.
    뭐 제대로 얘기하자면 프론트엔드 엔지니어겠지만, 뭐 대충 그래, 맞아. 난 2016년에 웹을 하고 있지. 시각화, 음악 재생기, 축구 경기를 하는 날아다니는 드론이라든가. 마침 JsConf랑 ReactConf에서 막 돌아온 참이라 웹 앱을 만드는 최신 기술들을 알고 있다고 볼 수 있지.

   Cool. I need to create a page that displays the latest activity from the users, so I just need to get the data from the REST endpoint and display it in some sort of filterable table, and update it if anything changes in the server. I was thinking maybe using jQuery to fetch and display the data?
   쩐다. 난 지금 사용자들이 남긴 최근 행동들을 보여주는 페이지를 짜려고 하는데, 그러면 일단 REST를 이용해서 데이터를 불러와 필터가 되는 테이블에 표시해 준 다음, 서버에서 갱신되는 게 있다면 테이블을 업데이트 해주려고 해. 데이터 불러오고 표시하는 데 jQuery 쓰면 되지?

   Oh my god no, no one uses jQuery anymore. You should try learning React, it’s 2016\.
    야잌ㅋㅋㅋㅋ 누가 jQuery 쓴다고 그러냐. 2016년 잇 아이템인 React를 써야지.

   Oh, OK. What’s React?
   헐, 그게 뭔데?

   It’s a super cool library made by some guys at Facebook, it really brings control and performance to your application, by allowing you to handle any view changes very easily.
    페이스북 존잘러들이 만든 슈퍼쿨 짱짱 라이브러리지. 네가 웹앱 만들 때 뷰를 마음대로 다루면서 기능과 성능도 모두 챙길 수 있지.

   That sounds neat. Can I use React to display data from the server?
   쩐다... React 써서 서버에서 온 데이터도 표시할 수 있지?

   Yeah, but first you need to add React and React DOM as a library in your webpage.
    당근, 근데 일단 React랑 React DOM을 니 웹 페이지에 넣어야 됨.

   Wait, why two libraries?
   엥? 왜 두 개나 넣어야 함?

   So one is the actual library and the second one is for manipulating the DOM, which now you can describe in JSX.
    하나는 진짜 라이브러리고 다른 건 DOM 다루는 데 쓰지. 그건 JSX로 표현되는거고.

   JSX? What is JSX?
   JSX? 그건 또 뭔데?

   JSX is just a JavaScript syntax extension that looks pretty much like XML. It’s kind of another way to describe the DOM, think of it as a better HTML.
    JSX는 자바스크립트 문법을 확장하는 거야 XML처럼. DOM을 표현하는 다른 방식인데 HTML보다 훨 나음.

   What’s wrong with HTML?
   HTML 가지고 뭐가 부족하길래 그런 걸 씀?

   It’s 2016\. No one codes HTML directly anymore.
    야 2016년에 직접 HTML을 다루는 사람이 어딨어.

   Right. Anyway, if I add these two libraries then I can use React?
   알았어. 그럼 그 둘만 더하면 React 쓸 수 있는거지?

   Not quite. You need to add Babel, and then you are able to use React.
    글쎄, Babel을 추가해야 React를 쓸 수 있을껄.

   Another library? What’s Babel?
   Babel은 또 뭐임?

   Oh, Babel is a transpiler that allows you to target specific versions of JavaScript, while you code in any version of JavaScript. You don’t HAVE to include Babel to use ReactJS, but unless you do, you are stuck with using ES5, and let’s be real, it’s 2016, you should be coding in ES2016+ like the rest of the cool kids do.
    ㅋㅋ Babel은 자바스크립트를 특정 자바스크립트 버전으로 옮겨주는 녀석(transpiler)이지. ReactJS를 쓰는데 꼭 Babel을 써야할 필요는 없는데 그럼 ES5만 써야 함. 2016년인데 당근 ES2016+ 정도 써야 어디가서 자바스크립트 좀 한다고 볼 수 있지.

   ES5? ES2016+? I’m getting lost over here. What’s ES5 and ES2016+?
   ES5? ES2016+? 이게 다 뭔데... 진짜 돌아버리겠음.

   ES5 stands for ECMAScript 5\. It’s the edition that has most people target since it has been implemented by most browsers nowadays.
    ES5는 ECMAScript 5를 나타내는거야. 요즘 브라우저들에서 구현되어 돌아가고 있는 대부분의 버전이 이거라고 보면 됨.

   ECMAScript?
   ECMAScript?

   Yes, you know, the scripting standard JavaScript was based on in 1999 after its initial release in 1995, back then when JavaScript was named Livescript and only ran in the Netscape Navigator. That was very messy back then, but thankfully now things are very clear and we have, like, 7 editions of this implementation.
    엉, 표준이라 불리는 자바스크립트는 1999년에 만들어진 물건이지. 1995년에 처음 제안되기 했는데 그 땐 이름이 Livescript라고 불렸고 넷스케이프 내비게이터에서만 돌아갔어. 그 땐 모든 게 엉망진창이었는데 요즘 그나마 이렇게 된 걸 감사해야지. 아무튼 요즘 돌아가는건 일곱 번째 구현체야.

   7 editions. For real. And ES5 and ES2016+ are?
   일곱 번째라고. 흠좀무. 그럼 ES5랑 ES2016+는 뭐라고?

   The fifth and seventh edition respectively.
    다섯 번째랑 일곱 번째를 그렇게 부르지.

   Wait, what happened with the sixth?
   여섯 째한텐 도대체 뭔 일이 있었길래...

   You mean ES6? Yeah, I mean, each edition is a superset of the previous one, so if you are using ES2016+, you are using all the features of the previous versions.
    ES6 말하는거임? ㅋㅋ 뭐 다 하위호환성을 가지고 있어서 ES2016+을 쓴다면 그 이전 버전의 기능 다 쓰고 있는 거라고 보면 됨.

   Right. And why use ES2016+ over ES6 then?
   알았다... 그럼 ES6 말고 ES2016+는 왜 쓰는데?

   Well, you COULD use ES6, but to use cool features like async and await, you need to use ES2016+. Otherwise you are stuck with ES6 generators with coroutines to block asynchronous calls for proper control flow.
    뭐... 굳이 원한다면 ES6 써도 돼. 근데 async랑 await 같이 멋진걸 쓰려면 ES2016+을 써야만 해. 아니면 ES6 제너레이터로 코루틴만 쓸 수 있을거야. 비동기 호출 흐름을 제어하려면 말이지.

    > Otherwise you are stuck with ES6 generators with coroutines to block asynchronous calls for proper control flow. 의 보다 정확한 번역이 필요합니다.

   I have no idea what you just said, and all these names are confusing. Look, I’m just loading a bunch of data from a server, I used to be able to just include jQuery from a CDN and just get the data with AJAX calls, why can’t I just do that?
   ... 뭐라고 하는지 하나도 모르겠는데. 이름도 헷갈리고. 난 그냥 서버에서 데이터 불러서 보여주고 싶은 건데. CDN에서 jQuery 받아서 걍 AJAX 콜 하려는거고. 이렇게 하면 왜 안 되는데?

   It’s 2016 man, no one uses jQuery anymore, it ends up in a bunch of spaghetti code. Everyone knows that.
    2016년이잖아. 아무도 jQuery 같은 건 안 쓴다고. 그런거 썼다간 쓰레기 같은 스파게티 코드만 남아. 그것도 몰라?

   Right. So my alternative is to load three libraries to fetch data and display a HTML table.
   후... 그럼 대안으로 세 가지 라이브러리를 로드하고, 데이터를 받아와서 화면에 HTML 테이블로 뿌리면 되나?

   Well, you include those three libraries but bundle them up with a module manager to load only one file.
    음... 뭐 예전처럼 각각 포함해도 되긴 하는데 가능하면 모듈 매니저를 통해 번들로 묶어서 파일 하나만 로드하는게 낫지.

   I see. And what’s a module manager?
   응. 그럼 모듈 매니저는 또 뭔데?

   The definition depends on the environment, but in the web we usually mean anything that supports AMD or CommonJS modules.
    그건 환경마다 좀 달라. 근데 보통은 AMD나 CommonJS 모듈을 지원하는 걸 말하지.

   Riiight. And AMD and CommonJS are…?
   하............ 그럼 AMD랑 CommonJS는?

   Definitions. There are ways to describe how multiple JavaScript libraries and classes should interact. You know, exports and requires? You can write multiple JavaScript files defining the AMD or CommonJS API and you can use something like Browserify to bundle them up.
    정의, 같은 거지. 이걸 통해서 여러 개의 자바스크립트 라이브러리랑 클래스들과 어떻게 상호 작용할지 설명할 수 있음. exports랑 requires 같은 건 알지? 여러 자바스크립트 파일들을 AMD나 CommonJS API로 정의해 놓으면 Browserify 같은 걸로 묶어서 번들할 수 있음.

   OK, that makes sense… I think. What is Browserify?
   뭐 말은 되네... 근데 또 뭐 Browserify?????

   It’s a tool that allows you to bundle CommonJS described dependencies to files that can be run in the browser. It was created because most people publish those dependencies in the npm registry.
    그건 CommonJS에 정의된 파일들의 의존성을 통해 파일을 묶어서 브라우저에서 실행될 수 있게 해주는 녀석이지. 많은 사람들이 npm 레지스트리에 의존성을 올려뒀기 때문에 생겼어.

   npm registry?
   npm 레지스트리???

   It’s a very big public repository where smart people put code and dependencies as modules.
    존잘러들이 코드랑 의존성을 묶어서 모듈로 배포하는 짱짱 큰 공개 리포지터리 같은 거임.

   Like a CDN?
   CDN이랑 비슷한가?

   Not really. It’s more like a centralised database where anyone can publish and download libraries, so you can use them locally for development and then upload them to a CDN if you want to.
    꼭 그런 건 아니지. npm은 라이브러리를 올리고 내려받을 수 있는 중앙 집중형 데이터베이스 같은 건데, 개발 환경에서는 로컬에서 쓸 수 있고 나중에 원하면 CDN에 올려놔도 됨.

   Oh, like Bower!
   아, Bower처럼!!

   Yes, but it’s 2016 now, no one uses Bower anymore.
    응 그치. 근데 2016년에는 아무도 Bower 같은 거 안 씀ㅋㅋㅋ

   Oh, I see… so I need to download the libraries from npm then?
   아이고... 그럼 npm에서 라이브러리 다운로드 받으면 되겠네?

   Yes. So for instance, if you want to use React , you download the React module and import it in your code. You can do that for almost every popular JavaScript library.
    응. 예를 들어서 React를 쓴다고 치자. 그럼 React 모듈을 받아서 니 코드에 임포트 하겠지. 다른 자바스크립트 라이브러리들처럼.

   Oh, like Angular!
   아, Angular처럼!

   Angular is so 2015\. But yes. Angular would be there, alongside VueJS or RxJS and other cool 2016 libraries. Want to learn about those?
    Angular가 2015년 산이긴 하지만 뭐 암튼 그래. Angular도 VueJS랑 RxJS랑 같이 있을 수 있지. 그 녀석들도 2016년 신상이지. 궁금함?

   Let’s stick with React, I’m already learning too many things now. So, if I need to use React I fetch it from this npm and then use this Browserify thing?
   얔ㅋㅋ React에만 집중하자. 일단 새로 알게된 게 너무 많아 미칠 지경임. 자, 그럼 React를 npm에서 받아서 Browserify로 묶는다?

   Yes.
    이제 좀 알아듣네.

   That seems overly complicated to just grab a bunch of dependencies and tie them together.
   의존성 가진 몇 개를 잡아다가 묶는 것 치고는 좀 심한 거 같은 기분이 드네.

   It is, that’s why you use a task manager like Grunt or Gulp or Broccoli to automate running Browserify. Heck, you can even use Mimosa.
    그래서 말이지, Grunt나 Gulp, Broccoli 같은 태스크 매니저를 써서 Browserify를 자동으로 돌리는거야. ㅋㅋ 아님 Mimosa를 쓰던가.

   Grunt? Gulp? Broccoli? Mimosa? The heck are we talking about now?
   Grunt? Gulp? Broccoli? Mimosa? 이 망할 것들은 또 죄다 뭐야?

   Task managers. But they are not cool anymore. We used them in like, 2015, then we used Makefiles, but now we wrap everything with Webpack.
   태스크 매니저야. 근데 더이상 안 써. 2015년에 쓰던 Makefiles 같은 건데 이제는 Webpack이 다 해줘.

   Makefiles? I thought that was mostly used on C or C++ projects.
   Makefiles? 그거 C나 C++ 프로젝트할 때 사용해 봤던 것 같은데.

   Yeah, but apparently in the web we love making things complicated and then going back to the basics. We do that every year or so, just wait for it, we are going to do assembly in the web in a year or two.
    어 맞어. 근데 확실한 건 웹 세상에서는 복잡하게 만들었다가 단순하게 돌아가는 것을 좋아하기는 해. We do that every year or so, just wait for it, we are going to do assembly in the web in a year or two.

   Sigh. You mentioned something called Webpack?
   하—... 지금 Webpack이라고 뱉은거지?

   It’s another module manager for the browser while being kind of a task runner as well. It’s like a better version of Browserify.
    그건 브라우저를 위한 모듈 관리자이면서 동시에 태스크 러너 같은 것이기도 하지. Browserify보다 낫던가?

   Oh, Ok. Why is it better?
   ㅋㅋ 왜 그게 더 나은데?

   Well, maybe not better, it’s just more opinionated on how your dependencies should be tied. Webpack allows you to use different module managers, and not only CommonJS ones, so for instance native ES6 supported modules.
    음.. 아닐지도 몰라. 니가 어떤 의존성을 가지고 있는지에 따라 좀 호불호가 갈리겠는걸. Webpack은 CommonJS 말고 다른 모듈 관리자를 허용해서 네이티브 ES6 지원 모듈 같은 것도 쓸 수 있지.

   I’m extremely confused by this whole CommonJS/ES6 thing.
   난 지금 CommonJS/ES6 같은 게 헷갈려서 미츄어버리겠는데...

   Everyone is, but you shouldn’t care anymore with SystemJS.
    다들 그래. 하지만 SystemJS는 몰라도 되니까.

   Jesus christ, another noun-js. Ok, and what is this SystemJS?
   하느님 맙소사, 또 뭐시기-js야. 좋아, 그럼 SystemJS는 뭔데?

   Well, unlike Browserify and Webpack 1.x, SystemJS is a dynamic module loader that allows you to tie multiple modules in multiple files instead of bundling them in one big file.
    음... Browserify랑 Webpack 1.x랑은 다르지. SystemJS는 동적 모듈 로더인데 여러 모듈들을 하나의 큰 파일이 대신 여러 파일들로 묶을 수 있게 해주지.

   Wait, but I thought we wanted to build our libraries in one big file and load that!
   잠깐... 아까는 우리가 쓰는 라이브러리들을 하나로 크게 묶어서 한방에 로드한다며!

   Yes, but because HTTP/2 is coming now multiple HTTP requests are actually better.
    응, 그렇지. 근데 HTTP/2가 등장하면 어떨까? 이건 여러 HTTP 요청을 동시에 잘 처리해주거든.

   Wait, so can’t we just add the three original libraries for React??
   아이고... 그럼 그냥 React 쓰기로 하고 라이브러리 세 개만 넣으면 안 되는거야?

   Not really. I mean, you could add them as external scripts from a CDN, but you would still need to include Babel then.
    음, 내가 말하고 싶은건, CDN을 통해서 외부 스크립트로 추가해도 되는데, 그래도 Babel은 추가해야 할 꺼야.

   Sigh. And that is bad right?
   하......... 그게 나쁘다는거지?

   Yes, you would be including the entire babel-core, and it wouldn’t be efficient for production. On production you need to perform a series of pre-tasks to get your project ready that make the ritual to summon Satan look like a boiled eggs recipe. You need to minify assets, uglify them, inline css above the fold, defer scripts, as well as-
   당근이지. 전체 babel-core를 포함하게 되는데 그게 프로덕션에 환경에서는 효율적이지 않잖아. 프로덕션 환경에서는 사탄을 소환하는 의식이 마치 삶은 계란 조리법처럼 보이도록 일련의 사전 작업들을 수행해서 프로젝트를 준비해야 하거든. 에셋들을 작게 만들고(minify), 못생기게(uglify)한 다음에, 먼저 보일 css는 inline으로 집어넣고 스크립트는 뒤로 빼고.. 뭐 그런 일들...

   I got it, I got it. So if you wouldn’t include the libraries directly in a CDN, how would you do it?
   알았다, 알았어. 그러니까 CDN에서 라이브러리 바로 불러오지 말라는 거잖아. 그럼 넌 어떻게 하는데?

   I would transpile it from Typescript using a Webpack + SystemJS + Babel combo.
    난 보통 Typescript를 Webpack + SystemJS + Babel 콤보로 써서 트랜스파일하지.

   Typescript? I thought we were coding in JavaScript!
   뭐? Typescript? 우리 자바스크립트 얘기하고 있지 않았나???!

   Typescript IS JavaScript, or better put, a superset of JavaScript, more specifically JavaScript on version ES6\. You know, that sixth version we talked about before?
    Typescript는 자바스크립트이기도 하고 자바스크립트를 포함하기도 하지. 음, 특별히 자바스크립트 ES6의 수퍼셋이라 할 수 있겠다. 아까 말한 여섯 째 기억나지?

   I thought ES2016+ was already a superset of ES6! WHY we need now this thing called Typescript?
   난 ES2016+가 ES6의 수퍼셋이라고 들었는데, 도대체 왜 그걸 Typescript라고 불러야 하는데?

   Oh, because it allows us to use JavaScript as a typed language, and reduce run-time errors. It’s 2016, you should be adding some types to your JavaScript code.
    ㅋㅋㅋㅋㅋ 그건 자바스크립트를 타입 언어(typed language)로 쓸 수 있게 해서 런타임의 오류를 줄여주는거야. 봐, 2016년이니까 너도 이제 자바스크립트 코드에 타입을 넣어서 써야지.

   And Typescript obviously does that.
   그러니까 Typescript가 그걸 한다는 거지.

   Flow as well, although it only checks for typing while Typescript is a superset of JavaScript which needs to be compiled.
    Flow가 해. 뭐 Typescript가 자바스크립트의 수퍼셋으로 컴파일되어야 할 필요가 있을 때만 검사를 하긴 하지만.

   Sigh… and Flow is?
   이런 미ㅊ... Flow가 뭐?

   It’s a static type checker made by some guys at Facebook. They coded it in OCaml, because functional programming is awesome.
    역시 페북 존잘러들이 만든 정적 타입 분석기야. OCaml으로 만들었지. 역시 함수형 프로그래밍이 짱인듯.

   OCaml? Functional programming?
   OCaml? 함수형 프로그래밍?

   It’s what the cool kids use nowadays man, you know, 2016? Functional programming? High order functions? Currying? Pure functions?
    진정한 2016년 힙스터라면 이걸 써야지 친구. 들어는 봤나? 함수형 프로그래밍? 고차함수? 커링? 퓨어 뻥션?

   I have no idea what you just said.
   니가 뭔소릴 하는지 1도 모르겠다.

   No one does at the beginning. Look, you just need to know that functional programming is better than OOP and that’s what we should be using in 2016\.
    첨부터 다 알 필욘 없지. 자, 2016년은 역시 함수형 프로그래밍의 해니까 OOP는 집어치우자.

   Wait, I learned OOP in college, I thought that was good?
   저기요, 나 대학에서 OOP만 배웠고 그거 괜찮았는데?

   So was Java before being bought by Oracle. I mean, OOP was good back in the days, and it still has its uses today, but now everyone is realising modifying states is equivalent to kicking babies, so now everyone is moving to immutable objects and functional programming. Haskell guys had been calling it for years, -and don’t get me started with the Elm guys- but luckily in the web now we have libraries like Ramda that allow us to use functional programming in plain JavaScript.
   자바도 오라클에 팔려버리기 전까지는 그랬었지. 내가 진짜 말하고 싶었던 건 OOP가 옛날에 좋았고 요즘에도 쓰인다고 해봤자 '상태를 변경한다'는 게 아이를 발로 차는 것과 맞먹는 무시무시한 일이라는 걸 이제 다들 알게 됐다는 거야. 그러니까 다들 불변하는 오브젝트를 다루는 함수형 프로그래밍에 관심을 가지는거지. 솔직히 하스켈 진영에서 지난 몇 년 동안 노력해 온 결과라고 본다. 어, Elm은 언급하지도 말자. 아무튼 요샌 그냥 자바스크립트로도 함수형 프로그래밍을 할 수 있는 Ramda 같은 라이브러리가 있어서 다행이야.

   Are you just dropping names for the sake of it? What the hell is Ramnda?
   너 걍 아무 이름이나 막 던지는 거 아냐? 아 진짜 Ramnda가 뭔데?

    > Are you just dropping names for the sake of it? 의 보다 정확한 번역을 제안해주세요.

   No. Ramda. Like Lambda. You know, that David Chambers’ library?
    아니. Ramda. Lambda 같은거. David Chamber 라이브러리 알지?

   David who?
   David 뭐시기?

   David Chambers. Cool guy. Plays a mean Coup game. One of the contributors for Ramda. You should also check Erik Meijer if you are serious about learning functional programming.
    David Chambers. 존잘러. Coup 게임을 즐기지. Ramda의 컨트리뷰터 중 한 명이야. 그리고 진지하게 함수형 프로그래밍을 공부할꺼라면 Erik Meijer 정도는 알아둬야지.

   And Erik Meijer is…?
   Erik Meijer는 누군데...?

   Functional programming guy as well. Awesome guy. He has a bunch of presentations where he trashes Agile while using this weird coloured shirt. You should also check some of the stuff from Tj, Jash Kenas, Sindre Sorhus, Paul Irish, Addy Osmani
    그 사람은 함수형 프로그래밍 언어 그 자체라고 볼 수 있음. 장난 아님. 우스꽝스러운 색 들어간 셔츠 입고 애자일 깔아뭉게는 프리젠테이션이 대단하지. 그거 말고도 Tj, Jash Kenas, Sindre Sorhus, Paul Irish, Addy Osmani 등도 봐야할껄.

   Ok. I’m going to stop you there. All that is good and fine, but I think all that is just so complicated and unnecessary for just fetching data and displaying it. I’m pretty sure I don’t need to know these people or learn all those things to create a table with dynamic data. Let’s get back to React. How can I fetch the data from the server with React?
   알았으니까 이제 그만하지? 다 좋은데, 그냥 데이터를 받아다가 보여주는데 왜 그렇게 복잡하고 불필요한 것들이 많은지 모르겠네. 동적 데이터로 테이블 정도 만드는 데 이제까지 말한 사람들이나 기술들을 꼭 알아야 할 필요가 없을것 같은데. React로 되돌아가서, 어떻게 해야 데이터를 서버에서 받아올 수 있지?

   Well, you actually don’t fetch the data with React, you just display the data with React.
    뭐, 꼭 React로 데이터를 받아올 필요는 없어. 그냥 보여주는 데만 써도 되지.

   Oh, damn me. So what do you use to fetch the data?
   어우씨, 그럼 데이터는 어떻게 받아오는데?

   You use Fetch to fetch the data from the server.
    Fetch를 써서 받아오면 되지롱.

   I’m sorry? You use Fetch to fetch the data? Whoever is naming those things needs a thesaurus.
   뭐라고? Fetch를 써서 데이터를 fetch 해온다고? 이름 지은 놈은 사전 좀 들고 있어야 되는거 아니냐?

   I know right? Fetch it’s the name of the native implementation for performing XMLHttpRequests against a server.
    Fetch는 서버에 대해 XMLHttpRequests를 수행하는 네이티브 구현의 이름이 맞는데?

   Oh, so AJAX.
   그거 AJAX잖아.

   AJAX is just the use of XMLHttpRequests. But sure. Fetch allows you to do AJAX based in promises, which then you can resolve to avoid the callback hell.
    응 AJAX는 XMLHttpRequests를 사용하는 것 뿐이야. 근데, Fetch를 쓰면 promises에서도 AJAX를 구현할 수 있어. promise는 콜백 지옥에서 널 해방시켜 줄 거고.

   Callback hell?
   콜백 지옥?

   Yeah. Every time you perform an asynchronous request against the server, you need to wait for its response, which then makes you to add a function within a function, which is called the callback pyramid from hell.
    응. 비동기 요청을 서버에 보내고, 응답을 기다리고, 이런 걸 함수 안에 함수로 넣고... 이런 걸 콜백 지옥이라고 해.

   Oh, Ok. And this promise thing solves it?
   오. 그렇군. 그러면 promise가 그걸 해결해주고?

   Indeed. By manipulating your callbacks through promises, you can write easier to understand code, mock and test them, as well as perform simultaneous requests at once and wait until all of them are loaded.
    당연하지. promise 써서 콜백을 다루면 코드 이해하기도 쉽고 목킹이나 테스트하기도 좋아. 게다가 동시 요청을 한 번에 수행해서 다 로드될 때까지 기다릴 수도 있고.

   And that can be done with Fetch?
   Fetch가 그걸 다 해준다고?

   Yes, but only if your user uses an evergreen browser, otherwise you need to include a Fetch polyfill or use Request, Bluebird or Axios.
    응. 근데 사용자가 에버그린 브라우저를 쓰지 않으면 Fetch polyfill을 넣어 주거나 Request나 Bluebird, Axios 같은 걸 써야할 수도 있어.

    > 에버그린 브라우저: 크롬이나 파이어폭스처럼 항상 최신 버전을 유지하는 브라우저

   How many libraries do I need to know for god’s sake? How many are of them?
   도대체 얼마나 많은 라이브러리를 알아야 하는거야? 얼마나 많은거냐고?

   It’s JavaScript. There has to be thousands of libraries that all do the same thing. We know libraries, in fact, we have the best libraries. Our libraries are huuuge, and sometimes we include pictures of Guy Fieri in them.
    자바스크립트잖아. 똑같은 일을 하는 라이브러리들이 수천 수만 개나 있다고. 우린 라이브러리들을 알고 있지. 사실, 최고의 라이브러리들을 가지고 있어. 라이브러리들 사이에 Guy Fieri 사진을 끼워둘 만큼 거대하지.

    > 역주) Guy Fieri, an American restaurateur, author, game show host, and television personality. : [https://en.wikipedia.org/wiki/Guy_Fieri](https://en.wikipedia.org/wiki/Guy_Fieri "https://en.wikipedia.org/wiki/Guy_Fieri")

   Did you just say Guy Fieri? Let’s get this over with. What these Bluebird, Request, Axios libraries do?
   방금 Guy Fieri라고 했어? 일단 좀 넘어가자. Bluebird, Request, Axios 라이브러리들이 하는 일이 뭐야?

   They are libraries to perform XMLHttpRequests that return promises.
    XMLHttpRequest를 수행해서 promise를 반환하는 라이브러리들이야.

   Didn’t jQuery’s AJAX method start to return promises as well?
   jQuery의 AJAX 메소드도 promise를 반환하게 되었지 않나?

   We don’t use the “J” word in 2016 anymore. Just use Fetch, and polyfill it when it’s not in a browser or use Bluebird, Request or Axios instead. Then manage the promise with await within an async function and boom, you have proper control flow.
    2016년에 제이쿼리는 더이상 쓰지 않아. Fetch를 쓰면서 지원하지 않는 브라우저에는 폴리필 하거나, Bluebird, Request, Axios 등을 쓰지. 그리고는 async 함수의 await와 promise를 관리하면, 짜잔! 제대로 된 제어흐름이 구현되는거야.

   It’s the third time you mention await but I have no idea what it is.
   네가 'await'를 언급한게 벌써 세번째인데, 난 그게 뭔지 모르겠어.

   Await allows you to block an asynchronous call, allowing you to have better control on when the data is being fetch and overall increasing code readability. It’s awesome, you just need to make sure you add the stage-3 preset in Babel, or use syntax-async-functions and transform-async-to-generator plugin.
    Await는 async한 호출을 블락해서 데이터가 fetch될 때 통제를 잘 할 수 있게 해주고, 결과적으로 전체 코드의 가독성을 높여줘. 정말 멋지다구. 단지 바벨의 stage-3 프리셋을 추가하거나, syntax-async-functions랑 transform-async-to-generator 플러그인을 쓰면 돼.

   This is insane.
   미쳤네 미쳤어

   No, insane is the fact you need to precompile Typescript code and then transpile it with Babel to use await.
    아냐. 미친 짓이란 건 await을 쓰려면 프리컴파일된 Typescript 코드를 작성한 다음에 그걸 Babel이 변환해주는 것 같은 일을 가리키지.

   Wat? It’s not included in Typescript?
   뭐?! 그거 Typescript에 포함된 거 아니었어?

   It does in the next version, but as of version 1.7 it only targets ES6, so if you want to use await in the browser, first you need to compile your Typescript code targeting ES6 and then Babel that shit up to target ES5\.
    어. 다음 버전엔 들어갈 거야. 그치만 현재 1.7 버전은 ES6만. 그래서 await 쓰려면 니가 짠 Typescript 코드를 ES6으로 변환해야 하고 그러면 Babel이 그걸 ES5로 바꿔줄거야.

   At this point I don’t know what to say.
   이제 니가 뭐라고 하는지 진짜 모르겠다.

   Look, it’s easy. Code everything in Typescript. All modules that use Fetch compile them to target ES6, transpile them with Babel on a stage-3 preset, and load them with SystemJS. If you don’t have Fetch, polyfill it, or use Bluebird, Request or Axios, and handle all your promises with await.
    봐봐. 쉬워. 전부 Typescript로 코딩해. Fetch를 사용하는 모든 모듈은 ES6로 컴파일 되고, stage-3 프리셋으로 babel을 써서 트랜스 파일한 다음에, SystemJS로 몽땅 로드할꺼야. Fetch가 없다고? polyfill 하면 되지. 아니면 Bluebird, Request, Axios가 등장한다면 어떨까? 그리고 모든 promise 를 await 로 쉐킷쉐킷.

   We have very different definitions of easy. So, with that ritual I finally fetched the data and now I can display it with React right?
   '쉽다'는 말에 대해 너랑 나는 기준이 완전 다른 것 같아. 이런 무지막지한 과정을 거쳐서 데이터를 받아왔다치자. 이제 React로 그걸 보여주는 거지? 맞아?

   Is your application going to handle any state changes?
    니가 만들려는 애플리케이션에서 상태(state)도 관리해야 해?

   Err, I don’t think so. I just need to display the data.
   어... 아닐 거야. 난 그냥 데이터를 보여주기만 하면 돼.

   Oh, thank god. Otherwise I would had to explain you Flux, and implementations like Flummox, Alt, Fluxible. Although to be honest you should be using Redux.
    아 다행이다. Flux를 설명해야 하나 고민하고 있었거든. Flux 구현체가 Flummox, Alt, Fluxible 같은 게 있긴 하지만 솔직히 그냥 Redux 쓰는 게 낫거든.

   I’m going to just fly over those names. Again, I just need to display data.
   이름이 너무 많아서 내가 파묻힐 지도 모르겠다. 다시 말하지만 난 그냥 데이터를 보여주면 된다고.

   Oh, if you are just displaying the data you didn’t need React to begin with. You would had been fine with a templating engine.
    아하! 그냥 데이터를 보여주기만 하는 거면 React 쓸 필요 없어. 템플릿 엔진으로도 충분해.

   Are you kidding me? Do you think this is funny? Is that how you treat your loved ones?
   너 장난하냐? 아니면 재미 삼아 이러는거야? 이게 네가 사랑하는 것들을 대하는 방식이니?

   I was just explaining what you could use.
    난 그냥 니가 하게 될 일을 설명한 것 뿐야.

   Stop. Just stop.
   이제 그만하자.

   I mean, even if it’s just using templating engine, I would still use a Typescript + SystemJS + Babel combo if I were you.
    내 말은, 그냥 템플릿 엔진을 쓰는 경우에 나라면 Typescript + SystemJS + Babel 콤보를 쓸거라고.

   I need to display data on a page, not perform Sub Zero’s original MK fatality.Just tell me what templating engine to use and I’ll take it from there.
   난. 그냥. 데이터를. 페이지에. 보여주기만. 할 거라고. 모탈컴뱃에서 척추 뽑는 기술 같은 건 필요 없어. 템플릿 엔진 이름만 말해주면 그거 쓸 게.

  > Sub Zero's original MK fatality: [https://www.youtube.com/watch?v=g2JNxeWO_wA](https://www.youtube.com/watch?v=g2JNxeWO_wA "https://www.youtube.com/watch?v=g2JNxeWO_wA") 영상을 참고하세요.

   There’s a lot, which one you are familiar with?
    굉장히 많지. 넌 뭘 써 봤는데?

   Ugh, can’t remember the name. It was a long time ago.
   어... 생각이 잘 안 나. 너무 오래 전 일이라.

   jTemplates? jQote? PURE?
    jTemplates? jQote? PURE?

   Err, doesn’t ring a bell. Another one?
   음.. 아닐 걸? 다른 건 없어?

   Transparency? JSRender? MarkupJS? KnockoutJS? That one had two-way binding.
    Transparency? JSRender? MarkupJS? KnockoutJS? 이건 양방향 바인딩도 돼.

   Another one?
   또 다른 건?

   PlatesJS? jQuery-tmpl? Handlebars? Some people still use it.
    PlatesJS? jQuery-tmpl? Handlebars? 이런 거 쓰는 사람도 있더라고.

   Maybe. Are there similar to that last one?
   글쎄.. 비슷한 다른 종류는 뭐가 있어?

   Mustache, underscore? I think now even lodash has one to be honest, but those are kind of 2014\.
    Mustache, underscore? 지금 같으면 lodash를 쓰겠지만 2014년이었을 테니까.

   Err.. maybe it was newer.
   그때는 신상이었던 것 같아.

   Jade? DustJS?
    Jade? DustJS?

   No.
   아니.

   DotJS? EJS?
    DotJS? EJS?

   No.
   그것도 아니야.

   Nunjucks? ECT?
    Nunjucks? ECT?

   No.
   그것도 말고.

   Mah, no one likes Coffeescript syntax anyway. Jade?
    헐.. 아무도 Coffeescript 문법을 좋아하진 않던데. Jade?

   No, you already said Jade.
   아니. 그리고 너 Jade는 이미 말했었어.

   I meant Pug. I meant Jade. I mean, Jade is now Pug.
    내 말은 Pug. 아니 Jade. 아니 그러니까... Jade는 지금 Pug가 됐거든.

   Sigh. No. Can’t remember. Which one would you use?
   후... 아니야. 기억 안 나. 너라면 뭘 쓸 거야?

   Probably just ES6 native template strings.
    아마 ES6 네이티브 템플릿 스트링만 쓸 것 같아.

   Let me guess. And that requires ES6\.
   내가 맞춰볼게. 그러려면 ES6가 필요하겠지?

   Correct.
    맞아.

   Which, depending on what browser I’m using needs Babel.
   그걸 아무 브라우저에나 쓰려면 Babel을 사용해야겠고.

   Correct.
    응.

   Which, if I want to include without adding the entire core library, I need to load it as a module from npm.
   그 모든 라이브러리를 일일이 추가하지 않으려면 npm으로 설치해야겠고.

   Correct.
    그래.

   Which, requires Browserify, or Wepback, or most likely that other thing called SystemJS.
   그러려면 Browserify나 Webpack 아니면 SystemJS가 필히 있어야할 거야.

   Correct.
    그렇지.

   Which, unless it’s Webpack, ideally should be managed by a task runner.
   Webpack이 없다면 그것들은 태스크 러너들이 관리해야겠고.

   Correct.
    맞았어.

   But, since I should be using functional programming and typed languages I first need to pre-compile Typescript or add this Flow thingy.
   그치만 함수형 프로그래밍이나 타입형 언어를 사용하고 싶다면 프리-컴파일 Typescript나 Flow 같은 걸 끼얹어야겠지.

   Correct.
    그렇지 그렇지.

   And then send that to Babel if I want to use await.
   그러고나서 이것들을 Babel로 보내고. 내가 await을 사용한다면 말야.

   Correct.
    정확해.

   So I can then use Fetch, promises, and control flow and all that magic.
   그러면 Fetch나 promises, control flow 같은 온갖 마법을 부릴 수도 있겠고.

   Just don’t forget to polyfill Fetch if it’s not supported, Safari still can’t handle it.
    지원하지 않을 경우에 대비해서 Fetch의 polyfill을 잊지 마. 사파리는 아직도 지원 안 해.

   You know what. I think we are done here. Actually, I think I’m done. I’m done with the web, I’m done with JavaScript altogether.
   있잖아. 우리 여기까지만 하자. 나 질렸어. 웹에도 질렸고 자바스크립트 같은 것들 따위에도 죄다 질렸어.

   That’s fine, in a few years we all are going to be coding in Elm or WebAssembly.
    그거 좋네. 실은 몇 년 내에 Elm이나 WebAssembly로 갈아타야 할 거거든.

   I’m just going to move back to the backend. I just can’t handle these many changes and versions and editions and compilers and transpilers. The JavaScript community is insane if it thinks anyone can keep up with this.
   난 백엔드나 하련다. 너무 많이 바뀌어서 감당이 안 돼. 이런 걸 다 따라올 수 있다고 생각했다면 자바스크립트 커뮤니티는 미친 거야.

   I hear you. You should try the Python community then.
    그래. 그럼 너 파이썬 커뮤니티에 가봐.

   Why?
   왜?

   Ever heard of Python 3?
    파이썬 3 소식 못 들었어?

글의 구성이 매우 재미있을 뿐 아니라 내가 어느정도 최신트렌드의 물결에 같이 흘러가고 있는가를 알 수 있었다.
