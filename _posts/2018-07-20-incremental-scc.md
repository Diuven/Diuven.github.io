---
id: 203
title: Incremental SCC
date: 2018-07-20T21:11:06+00:00
author: YoungHun Roh
layout: post
guid: http://13.124.96.114/?p=203
permalink: /2018/07/20/incremental-scc/
hestia_layout_select:
  - default
categories:
  - PS / CP
---
### Incremental SCC

유향 간선을 하나씩 추가해가면서 각 시점에서의 SCC의 개수 (혹은 크기 등등) 을 구하는 문제다.

ONTAK 2017 pun 문제에서 봤다.

요약: 오프라인으로 분할정복하면  <img src="//s0.wp.com/latex.php?latex=O%28QlogQ%29+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="O(QlogQ) " title="O(QlogQ) " class="latex" />(Q는 간선(arrow)의 개수) 만에 된다.

* * *

#### Notation

A는 모든 간선들의 집합 (Arrow)
  
<img src="//s0.wp.com/latex.php?latex=A%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="A[s,e] " title="A[s,e] " class="latex" />는  <img src="//s0.wp.com/latex.php?latex=s+%5Cleq+i+%5Cleq+e&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="s &#92;leq i &#92;leq e" title="s &#92;leq i &#92;leq e" class="latex" />를 만족하는 Ai들의 집합

 <img src="//s0.wp.com/latex.php?latex=s%2Cm%2Ce+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="s,m,e " title="s,m,e " class="latex" />는 현재 분할정복하고 있는 구간에 대한 정보 ( <img src="//s0.wp.com/latex.php?latex=%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[s,e] " title="[s,e] " class="latex" />구간, 그 중점  <img src="//s0.wp.com/latex.php?latex=m%3D%28s%2Be%29%2F2+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="m=(s+e)/2 " title="m=(s+e)/2 " class="latex" />)

<img src="//s0.wp.com/latex.php?latex=B%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="B[s,e] " title="B[s,e] " class="latex" />는 구간  <img src="//s0.wp.com/latex.php?latex=%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[s,e] " title="[s,e] " class="latex" />에서 사용할 간선들 (이후 설명)

Q는 간선 개수 (<img src="//s0.wp.com/latex.php?latex=%3D%7CA%7C+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="=|A| " title="=|A| " class="latex" />)

* * *

#### 관찰

E의 속한 간선들을 사용해 SCC 분해를 하는 것은 O(|E|)만에 할 수 있다. (정점 수와 무관하다는 것에 주목)

 <img src="//s0.wp.com/latex.php?latex=A%5B1%2Ct%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="A[1,t] " title="A[1,t] " class="latex" />에 속한 간선을 사용해서 SCC를 구했다고 하자. 그러면 간선은 두 부류로 나뉜다: 양 끝점이 같은 SCC에 속하거나, 다른 SCC에 속하거나.

양 끝점이 같은 SCC에 속한 간선의 집합을 X, 다른 SCC에 속한 간선의 집합을 Y라고 하자.

만약 시각 t까지의 SCC를 전부 구해 놔서 정점들을 적당히 union 해 주었다면, X에 속하는 간선들은 시각 t 이후에는 필요하지 않다.
  
반면, 시각 t까지의 SCC 분해를 하는 데 있어서 Y에 속한 간선들은 필요하지 않다. 어자피 간선의 양 끝점은 시각 t 전에 SCC로 묶이지 않는다는 것을 알기 때문이다.

* * *

##### 알고리즘

간선이 두 부류로 나눠지므로, 분할 정복을 생각할 수 있다.

단순하게 분할 정복을 하는데, 각 구간에서 사용할 간선들은 이미 구해져 있다고 가정한다. 이를 <img src="//s0.wp.com/latex.php?latex=B%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="B[s,e] " title="B[s,e] " class="latex" />라고 하자.

<img src="//s0.wp.com/latex.php?latex=B%5Bs%2Ce%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="B[s,e] " title="B[s,e] " class="latex" />에 속하는 간선들 중에서, 인덱스가 m 이하인 간선들의 집합을 X라고 하자.

이제 <img src="//s0.wp.com/latex.php?latex=%5B1%2C+s-1%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[1, s-1] " title="[1, s-1] " class="latex" />에서 한 SCC 분해의 정보를 바탕으로 X를 사용해 다시 SCC 분해를 할 것이다. 즉, 정점들이 이미 적당히 union되어 있고, 새로운 간선들(X)을 추가해서 SCC를 다시 만드는 것이다. 다만, 지금 하는 SCC는 기록되어서는 안된다.

그러면 집합 X를 다시 두 부류로 나눌 수 있다. 양 끝점이 같은 SCC에 속한 간선들의 집합을 Y, 양 끝점이 같은 SCC에 속하지 않은 간선들의 집합을 Z라고 하자.

Y는 <img src="//s0.wp.com/latex.php?latex=%5Bs%2Cm%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[s,m] " title="[s,m] " class="latex" />구간에서 사용될 것이고, Z는 <img src="//s0.wp.com/latex.php?latex=%5Bm%2B1%2C+e%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[m+1, e] " title="[m+1, e] " class="latex" />구간에서 사용될 것이다. 그리고 <img src="//s0.wp.com/latex.php?latex=B%5Bs%2Ce%5D-X+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="B[s,e]-X " title="B[s,e]-X " class="latex" />에 속하는 간선들은 <img src="//s0.wp.com/latex.php?latex=%5Bm%2B1%2C+e%5D+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="[m+1, e] " title="[m+1, e] " class="latex" />구간에서 사용될 것이다. 그렇게 간선들을 아래 구간으로 넘겨주도록 한다.

그렇게 내려가다가, 점구간에 도달했다면 현재까지의 SCC 정보를 바깥에 기록해 준다. 즉, 답도 기록하고, union-find 구조도 갱신해 주는 것이다.

&nbsp;

한 간선은 한 깊이에서 한번만 처리되고, 따라서 <img src="//s0.wp.com/latex.php?latex=O%28QlogQ%29+&#038;bg=ffffff&#038;fg=000&#038;s=0" alt="O(QlogQ) " title="O(QlogQ) " class="latex" />이다

* * *

코드 추가, 설명 다듬기가 필요하다. 나중에 시간 나면 올릴듯.