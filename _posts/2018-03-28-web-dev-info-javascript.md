---
id: 78
title: 'Web Dev Info - JavaScript'
date: 2018-03-28T20:35:58+00:00
author: YoungHun Roh
layout: post
guid: http://13.124.96.114/?p=78
permalink: /2018/03/28/web-dev-info-javascript/
hestia_layout_select:
  - default
categories:
  - Info
---
### JavaScript

**JavaScript,** often abbreviated as **JS**, is a high-level, interpreted programming language. It is a language which is also characterized as dynamic, weakly typed, prototype-based and multi-paradigm.

&#8212; wikipedia

&nbsp;

<img src="http://13.124.96.114/wp-content/uploads/2018/03/JavaScript-logo.png" alt="" class="alignnone wp-image-79" width="294" height="294" srcset="http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo.png 1052w, http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo-150x150.png 150w, http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo-300x300.png 300w, http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo-768x768.png 768w, http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo-1024x1024.png 1024w, http://www.diuven.ga/wp-content/uploads/2018/03/JavaScript-logo-50x50.png 50w" sizes="(max-width: 294px) 100vw, 294px" />       <img src="http://13.124.96.114/wp-content/uploads/2018/03/javascript_logo_without_title.png" alt="" class="alignnone wp-image-80" width="245" height="278" srcset="http://www.diuven.ga/wp-content/uploads/2018/03/javascript_logo_without_title.png 344w, http://www.diuven.ga/wp-content/uploads/2018/03/javascript_logo_without_title-265x300.png 265w" sizes="(max-width: 245px) 100vw, 245px" />

* * *

JavaScript는 언어이다. 그냥 C언어, JAVA언어, Python언어라고 부르듯, 수많은 프로그래밍 언어 중 하나일 뿐이다. 앞으로 웹 리뷰에서 JS에 관련된 많은 것들이 올라올 것인데, 모두 이 언어에 기반하고 있는 것들이다.

위의 소개글에 나와 있듯 high-level, dynamic, weakly typed, multi-paradigm이다. 멀티 파라다임은 함수 지향, 객체 지향 그런거 다 섞여 있다는 뜻이다. 다시 말해서, 온갖 기능이 다 들어있는 언어이다. 그리고 그만큼 어렵기도 하다.

<div style="width: 610px" class="wp-caption alignnone">
  <img class="irc_mi" src="http://www.globalnerdy.com/wordpress/wp-content/uploads/2012/01/javascript-wat.jpg" onload="typeof google==='object'&&google.aft&&google.aft(this)" alt="Image result for wat javascript" width="600" height="258" />
  
  <p class="wp-caption-text">
    영상 <a href="https://www.destroyallsoftware.com/talks/wat">wat</a> 하이라이트
  </p>
</div>

[xkcd : types](https://xkcd.com/1537/)

* * *

##### ECMAScript

C나 C++에도 C99 / C11, C++11 / C++17 등이 있는것 처럼, JS도 표준이 있다. 심지어 해마다 나온다. ECMA라는 단체에서 [내세운 기준](https://www.ecma-international.org/publications/standards/Ecma-262.htm)을 따른 언어를 ECMAScript라고 한다. 만약 ECMAScript 2016이면 그때의 기준을 따른 언어를 뜻한다. 그리고 JS는 ECMAScript 중 하나이다. 헷갈리면 [여기](https://medium.freecodecamp.org/whats-the-difference-between-javascript-and-ecmascript-cba48c73a2b5)에도 설명되어 있다.

ECMAScript에는 여러 가지가 있다. 나온 해를 따라서 ES2016이라고 부르기도 하고, 몇번째 버전인지를 따져서 ES7이라고 하기도 한다. 헷겔리게도 2015년에 나온 ES가 6번째 버전이라, ES2015는 ES6과 같은 말이다. 그리고 JS에 기반을 두는 대부분의 프레임워크들은 ES6을 쓴다. (왜냐면 ES5가 1999년에 나왔거든) 자세한건 [여기](https://bytearcher.com/articles/es6-vs-es2015-name/)에.

* * *

##### Transpiler

[Transpiler](https://en.wikipedia.org/wiki/Source-to-source_compiler)는 그냥 compiler하고는 다르게, 소스코드를 소스코드로 바꿔주는 기능을 가진다. A라는 언어를 B라는 언어로 &#8216;번역&#8217;해준다고 생각하면 될 듯 하다.

아무튼, JS는 위로 쌓아 올려진 프레임워크나 라이브러리가 너무 많아서 모던 웹 개발을 하려면 어찌되었든 JS를 쓸 수밖에 없게 된다. 그래서 그런지 JS transpiler는 엄청나게 많다. 누군가 만들어놓은 목록은 [여기](https://github.com/jashkenas/coffeescript/wiki/list-of-languages-that-compile-to-js)에 있다. 그 중에서 많이 쓰이는 것들은 Babel, CoffeeScript, TypeScript 등이 있다. 같은 기능을 하는 코드를 이것들을 써서 작성한 것이 [여기](https://blessedgong.wordpress.com/2016/10/25/coffeescript-vs-es6-vs-typescript/)에 있다.

[Babel](https://babeljs.io/) : ES6(ES2015)를 ES5 (구버전)으로 번역해주는 Transpiler이다. Babel을 씀으로서 Backward compatibility (옛날 브라우저도 지원해준다는 뜻) 은 걱정이 없게 되겠다. 만약 접속 대상이 IE6같은걸 쓸 수도 있다 싶으면 babel로 코드를 downgrade해서 쓰면 될 것이다.

[CoffeeScript](http://coffeescript.org/) : JS로 변환될 수 있는 언어이다. 문법은 약간 다르다고 하는데, Ruby하고 비슷하다고 한다(?). CoffeeScript2부터는 ES6을 지원한다.

[TypeScript](http://www.typescriptlang.org) : MS(!!)에서 개발한 언어이다. 그래서 당연히 VS같은 IDE에서 잘 돌아간다고 한다. CoffeeScript는 JS하고 약간 떨어진 반면, TypeScript는 좀 더 JS에 더 가깝다고 한다. C#이나 JAVA하고 비슷한 면이 있다고도 한다.

* * *

굳이 JS에 대해서 설명하는 이유는 babel이니 coffeescript같은 이름들에 휘둘리지 말라는 의도에서이다. 구글링하는데 이런 이름들때문에 더 헷갈리게 될까봐 (나도 많이 그랬다. 그래서 이 기회에 찾아본 것) 설명하는 것이다.

나중에 기회가 되면 CoffeeScript같은 것들을 써보고는 싶지만 (코드가 짧고 간결하다고 한다&#8230;),  굳이 지금 써볼 필요는 없을듯.

* * *

&nbsp;

JAVA하고 비슷한가요?

&#8212; 안비슷하다. 듣기에는 개발 초창기에 당시 잘나가던 JAVA의 인기에 편승해서 성공좀 해보려고 이름을 이렇게 지었다고 한다. 흔한 meme으로 JAVA와 JavaScript는 ham하고 hamster가 비슷한 만큼 비슷하다고 한다.