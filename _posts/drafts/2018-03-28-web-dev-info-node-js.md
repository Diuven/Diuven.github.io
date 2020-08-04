---
title: "Draft: Web Dev Info- Node.js"
date: "2018-03-28"
---

### [Node.js](https://nodejs.org)

![](images/2000px-Node.js_logo.svg_.png)

Node.js® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://developers.google.com/v8/). Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, [npm](https://www.npmjs.com/), is the largest ecosystem of open source libraries in the world.

 

* * *

JavaScript(JS)는 원래 client 기능이 HTML만으로는 부족한 것 같아서 쓰이기 시작한 언어이다. (그때는 유사 언어 취급당했다고 한다) 그래서 HTML 에 <script> 태그를 섞어서, reactive한 기능들을 만들 수 있게 된 것이고, 그때부터 많이 쓰이게 시작했다. 참고로 JS에는 온갖 기능이 다 들어있다. 객체지향, 함수지향, 절차지향(?) 전부 들어있고, 뭘 써도 된다. 그래서 무슨 언어라고 말하기가 어렵다.  나중에 JS 컴파일러나 문법 관련해서 올리면 더 자세한 내용이 있을 것.

* * *

그래서 원래는 JS는 client쪽 (프런트)에서만 약간 쓰이던 언어였는데, Node.js가 나오면서 본격적으로 서버쪽에서 쓰이기 시작했다. 원래는 php가 많이 쓰이고 있었는데 (사실 아직도 많이 쓰이는 것 같다) , 최근에 만들어지는 웹사이트들은 Node.js를 많이 사용한다.

Node.js은 대략 이렇게 쓴다:

`var http = require('http');`

http.createServer(function (req, res) { res.writeHead(200, {'Content-Type': 'text/plain'}); res.end('Hello World!'); }).listen(8080);

 

여기서 포인트는 createServer 안에 함수가 인자로 주어진다는 것, 그리고 그 함수의 인자는 req와 res라는 것이다.

의미를 해석하자면, '이러이러한 기능을 하는 http 서버를 만들고, 8080포트에서 (접속을) 듣고 있어라'라는 뜻이다.
