---
title: "Draft: SSHS 계산용 컴퓨터 세팅"
date: "2020-08-04"
---

학교에 수치해석이나 NN 학습용, 등등 computational power가 필요한 프로젝트를 위한 계산용 컴퓨터가 있다.

스펙은...

`Intel Xeon CPU E5-2687 v4 @ 3.00GHz Nvidia TITAN Xp (1B02) 3개, TITAN X (Pascal) (1B00) 1개 Samsung DDR4 32GB 8개 Ubuntu 16.04 LTS`

대충 이렇고, CPU 코어 48개, RAM 256GB, Swap영역 256GB, GPU 는 TITAN 4개 정도라고 생각하면 될 것 같다. (CPU하고 RAM에 비해서 GPU가 너무 적은거 아닌가 싶다만)

주변 기기로는 뭔지 모를 Wasabi Mango UHD 모니터, UPS 2개 (아직 미설치), RAID 5(6인가?)가 있다. 디테일은 나중에...

* * *

### 스토리

이 컴퓨터는 전에 있던 물리쌤이 작년쯤에 들여온건데, 그분은 가시고 다른 분이 관리중이다. 처음 생길때 이름을 quark로 정하신 것 같고, 다른 분이 오시면서 UPS나 RAID같은 백업 수단을 마련하셨다.

근데 계산컴을 쓰려는 사람들은 보통 NN하는 친구들이고 주로 Tensorflow를 사용하지만, 물리과 특성상 TF보다는 CUDA정도만 사용해서 C로 짜는 경우가 많은 것 같다.

작년 R&E할때는 대충 다 세팅이 되어 있어서 그냥 썼지만, 어떻게 세팅되어있는지를 몰라서 필요한 패키지같은 것들을 깔 때 많이 불편했다. 그래서 이번에 OS를 다시 깔고, 유저 파일만 옮겨서 다시 세팅하기로 했다.

작년에 내가 사용한게 거의 초창기에 사용한거라 학생 관리자가 없기도 했고, 나는 리눅스를 자주 쓰는 관계로 관리할 수 있을 것 같아서 쌤한테 물어봤더니 관리자를 할 수 있게 되었다.

그래서 이 컴퓨터를 세팅해야 하는데, TF 1.8, OpenCV, Keras 정도까지 일반 사용자가 사용하도록 하는 게 목적이다. 그리고 문서도 좀 만들어서 어떻게 사용하는지를 적어 놓는것도 생각하고 있다.

사실 내가 관리자이긴 하지만 quark컴은 쓰는 사람이 좀 있어서 내가 맘대로 끄고 키거나 리셋할 수 없기 때문에, 옆에 있는 덜 좋은 컴퓨터로 연습삼아 해봤다. 그리고 이 컴퓨터 이름은 lepton으로 정했다.

lepton의 스펙은

`Intel CPU i5 7700? NVIDIA GTX 1080 2개? RAM 16GB Ubuntu 16.04 LTS`

이다. 그냥 그래픽이 두개인 데탑이라고 생각하면 될 듯 하다.

* * *

그래서, 이 글은 ubuntu 16.04를 갓 설치한 상태의 lepton 컴퓨터를 세팅하는 과정이다.

 

뭔가 작업이 끊기고 다시 세팅을 시작할 때는 웬만하면 다음을 실행시킨다. 물론 OS를 깐 직후에도 한번 해주자.

`sudo apt-get update && sudo apt-get upgrade`

이는 로컬에 있는 패키지 리스트를 업데이트하고, 만약 내가 설치한 패키지가 업데이트되었다면 그 패키지를 업그레이드한다.

 

##### SSH 연결 세팅

openssh server로 ssh라는 서비스를 돌릴 수 있다. 다음과 같이 서비스의 상황을 확인할 수 있다.

`sudo service ssh status`

서버를 세팅하려면 /etc/ssh/sshd\_config파일을 손보면 된다. 다음과 같이 접근해서 수정하자.

`sudo vim /etc/ssh/sshd_config`

이러면 vim 에디터가 실행된다. 여기서 `ListenAddress`가 접근 가능한 주소를 관리하는 부분이다. 기본값은 전부 허용이니, 별 상관 없으면 주석해놓고 무시하자.

같은 파일에서

`#Banner /etc/issue.net`

을 주석해제 (#을 지우기) 하면 /etc/issue.net에 있는 내용이 ssh로 연결하는 모든 유저에게 공지로 뜬다. 한글도 되는지는 잘 모르겠으나, 나름 유용하니 필요하다면 쓰자.

적당히 편집했으면, 나와서 ssh 서비스를 재시작하자.

`sudo service ssh restart`

 

여기서부터는 [이 링크](https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07)가 가장 정확하다. 먼저 읽어보고 영어가 귀찮거나 헷갈리는 부분이 있으면 이 글을 참고하는 것이 좋을 듯 하다.

### 그래픽 드라이버 설치

[링크1](https://askubuntu.com/questions/481414/install-nvidia-driver-instead-of-nouveau) [링크2](http://pythonkim.tistory.com/48)

세팅을 켜서 System > Administration > Hardware drivers 에 들어가면 어떤 장치를 사용하는지, 그리고 각종 드라이버 세팅을 볼 수 있다고 한다.

어떤 GPU가 연결되어 있는지를 확인하는 방법은 여러 가지가 있지만, 여기서는 아래 방법으로 충분하다.

`lspci -vnn | grep VGA -A 12`

그러면 길게 뭐가 나오는데, NVIDA의 경우에는 이름이 바로 나오지는 않고 1b02처럼 Hex 코드로 나오니, 추가적인 구글링을 해서 무슨 GPU인지 확인하면 된다.

확인했으면, 직적 NVIDA 공식 사이트에서 드라이버 설치 파일을 받는다. .run파일로 받으면 된다. (참고: `wget "링크"`를 하면 터미널에서 바로 파일을 받을 수 있다. curl도 있다는데 잘 모르겠다.)

받고 나면, 다운로드한 위치로 가서 `chmod a+x *.run`으로 실행 가능한 파일으로 세팅하고, `sudo ./*.run`을 해서 실행시켜보자. (물론 \*에는 자신의 파일 이름을 치자. 그냥 \*로 해도 되긴 할테지만, 안그러는게 좋다)

 

 

 

+nvidia-smi

 

### CUDA 설치하기

CUDA는...

### CuDNN

### Tensorflow-gpu, keras 설치

위의 작업을 전부 끝냈으면 여기는 쉽다.

`sudo pip3 install tensorflow-gpu keras`

를 하면 깔린다.

아, 여기서 만약 `pip3 install --upgrade pip`같은 짓을 했다가는 무슨 일이 일어날지 모른다. 패스가 꼬여서 무조건 껏다켜야되는데, 그 후에 이상한 일이 생길 수도 있다. pip가 어떻게 돌아가는지 잘 몰라서 그냥 pip3만 사용하기를 추천한다.

다 깔린 것 같으면, python3을 열고 `import tensorflow`와 `import keras`가 되면 성공한 것이다. 또한 TF를 import한 후에 바깥의 터미널에서 `nvidia-smi`를 쳐보면 GPU의 메모리가 사용중임을 알 수 있다.

pycharm
