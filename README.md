# Development-environment-setting

### Linux 설치
Mac에서 ubuntu 부팅 usb 만들기 [link](https://lynmp.com/ko/article/roa0ea27bfcdf035b8) \
이후 Bios(F2 연타) 진입하여 부팅 순서 변경 \
+) xmp 지원시 xmp enabled로 변경 [link](https://shine72.tistory.com/18)

### Linux 세팅
Chrome 설치 [link](https://itsfoss.com/install-chrome-ubuntu/) \
한글 설치 [link](https://iworldt.tistory.com/11) \
Slack 설치 [link](https://slack.com/intl/ko-kr/downloads/linux) \
gcc 설치
```
sudo apt install gcc
```
CLion 설치 [link](https://www.jetbrains.com/help/clion/installation-guide.html) \
VScode 설치 [link](https://code.visualstudio.com/docs/setup/linux)

### 설치 되어있는 패키지들의 새로운 버젼이 있는지 확인 (밑의 과정 하기 전에 필수)
```
sudo apt-get update
```
  
### GPU 기본적인 설정이 안되어 있는 경우
GPU drive —> CUDA —> cudnn 순서로 설치 진행
1) NVIDIA GPU driver [link](https://pstudio411.tistory.com/entry/Ubuntu-2004-Nvidia%EB%93%9C%EB%9D%BC%EC%9D%B4%EB%B2%84-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0)
2) CUDA [link](https://developer.nvidia.com/cuda-toolkit-archive) --> run_file(local)로 해야함. ".run" 실행후 driver 설치는 체크 해제해야함. 안 그러면 사전에 깔려있는 driver 
3) cudNN [download link](https://developer.nvidia.com/rdp/cudnn-archive) [install guide1](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html) [install guide2](https://kyumdoctor.co.kr/30)
4) Final check
```
nvcc --V (check CUDA version)
nvidia-smi (check whether the GPU is correctly detected)
```

### CUDA가 여러개 설치되어있고 필요할 때마다 변경해야하는 경우
1) /usr/local/cuda symbolic link 제거 후 원하는 버전으로 변경
```
cd /usr/local
sudo rm cuda
sudo ln -s cuda-XX.XX cuda
ls -la (check symbolic link)
```
2) ~/.zshrc에 아래 추가 (없을 때만) (zshell이 아니라 기본 쉘 사용하고 있는 경우 ~/.bashrc에 추가)
```
export CUDA_HOME=/usr/local/cuda
export PATH=$PATH:$CUDA_HOME/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
```
3) ~/.profile 수정
```
export PATH=/usr/local/cuda-XX.XX/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-XX.XX/lib64:$LD_LIBRARY_PATH
```
4) 수정 사항 반영
```
source ~/.bashrc
source ~/.profile
```
5) 확인
```
nvcc -V
```

### z shell 설치
1) zsh 설치
```
sudo apt-get install zsh
zsh --version
chsh -s /usr/bin/zsh (z shell을 기본 쉘로 설정)
이후 꼭 linux에서 로그아웃했다가 다시 로그인하기! 그래야 기본 쉘 바뀜!
echo $SHELL (—>   /usr/bin/zsh 이 나와야함)
```
2) oh-my-zsh 설치
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
3) Powerlevel10k 설치 [link](https://velog.io/@t1won/Ubuntu-powerlevel10k-%EC%84%A4%EC%B9%98) [link](https://github.com/romkatv/powerlevel10k#installation)
(git clone 후 ‘~/zshrc’ 안을 ZSH_THEME="powerlevel10k/powerlevel10k”로 수정)
4) 터미널 나갔다가 들어오면 하라는대로 잘 따라가면 됨
5) .p10k.zsh 가서 색변경 (source ~/.p10k.zsh 해야 적용됨) [link](https://github.com/romkatv/powerlevel10k/blob/master/README.md#change-the-color-palette-used-by-your-terminal)
```
typeset -g POWERLEVEL9K_DIR_BACKGROUND=27
typeset -g POWERLEVEL9K_DIR_FOREGROUND=254
typeset -g POWERLEVEL9K_ANACONDA_BACKGROUND=27
```

### vim 및 vim pluggin 설치 (자동 완성 플러그인은 바로 밑에 부연 설명. 과정이 김)
1) vim 설치
```
sudo apt-get install vim
```
3) vim-plug 설치 [link](https://github.com/junegunn/vim-plug/wiki/tutorial)
2) ~/.vimrc 에 플러그인 추가 (lightline, nerdtree, coc.nvim) [link](https://medium.com/@huntie/10-essential-vim-plugins-for-2018-39957190b7a9)
3) 변화 반영
```
:source ~/.vimrc. (vim 상에서 진행!)
```
4) 플러그인 설치 
```
:PlugInstall
```

### 자동완성 vim 플러그인 설치
1) node.js와 yarn 설치 [link](https://blog.system32.kr/205)
yarn 설치시 error 나면 sudo 붙여서 해보기 
이후에 [link](https://jsikim1.tistory.com/158) 나와있는대로 node.js 버전 업그레이드 해야함 (>12.2)
2) coc.nvim 이라는 vim 플러그인 설치 [link](https://github.com/neoclide/coc.nvim)
3) :CocInstall coc-pyright, coc-clangd [link](https://johngrib.github.io/wiki/vim-auto-completion/#cocnvim)
4)  .vimrc에 다음 추가 (lightline 시작할 때부터 돌아가게 함)
```
set laststatus=2
```
5) 변화 반영 (vim 상에서 진행!)
```
:source ~/.vimrc.
```

### miniconda 설치
1) .sh 설치 파일 실행 [link](https://docs.conda.io/en/latest/miniconda.html) (기본 초기화 yes!)
2) ~/.bashrc에 생성된 conda 경로 잡는 부분을 ~/.zshrc로 이동 (z shell 사용하는 경우)
3) 부가 설정 + 필요한 환경 생성 후 
```
conda config --set auto_activate_base false (자동 실행 막음)
condo create -n (env 이름) (조건)
condo activate (env 이름)
```

### 기타 설치 (tmux, git, htop, gpustat, imagemagick)
```
sudo apt-get install tmux
sudo apt-get install terminator
sudo apt install git-all
sudo apt-get install htop
sudo apt-get install gpustat
sudo apt-get install imagemagick (==> can use 'display' command in terminal to view image)
```

### git ssh key 생성 및 등록
1) key 생성 및 local ssh-agent에 등록 [link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
2) 생성한 key git에 등록 [link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

### CF
- NVIDIA NVML Driver/library version mismatch 해결방법 [link](https://dfso2222.tistory.com/69)

### Ubuntu desktop gui 등에 문제가 생겨서 이상하게 나타나는 경우
```
sudo apt-get update
sudo apt-get install --reinstall ubuntu-desktop
```

### git branch 생성 후 커밋
```
git branch XXX  (XXX branch local에 생성)
git checkout XXX  (XXX branch로 현재 상태 변경)
(위 두 줄은 git checkout -b XXX 와 동일)
(파일들 수정 후)
git add .
git commit -m "남기고 싶은 메세지"
git push origin XXX
```
git branch 이름 변경하기 [link](https://thdev.tech/git/2016/12/19/Git-Branch-Name-Change/)

git branch 삭제
```
git branch -d XXX (로컬에서 branch 삭제)
git push origin --delete XXX (원격에서 삭제)
```

git add/commit 취소 [link](https://gmlwjd9405.github.io/2018/05/25/git-add-cancle.html)

### git clone 후 새로운 repository로 push
```
# 기존 repository의 history를 지우고 싶은 경우
git clone OLD.git
cd OLD
rm -rf *.git
git init
git add .
git commit -m "xxx"
git remote add origin NEW.git
git push -u origin master

# 기존 repository의 history를 지우고 싶은 경우
git clone --mirror OLD.git
cd OLD
git remote set-url --push origin NEW.git
git push --mirror
```

### Ubuntu desktop ssh 접속 [link](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server) [link](https://codechacha.com/ko/ubuntu-install-openssh/) [link](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)
- 접속하려고 하는 pc가 바로 랜선에 꼽아져있고 고유 외부 ip가 있는 경우
```
ssh username@ 접속 pc 외부 ip (-p 포트) [기본 포트: 22]
```
- 접속하려고 하는 pc가 공유기에 꼽아져있는 경우 -> ifconfig로 나온 주소는 공유기가 접속하려고 하는 pc에 부여한 내부 ip. 공유기 주소로 접속후 포트 포워딩으로 해당 pc에 접속
```
ssh username@공유기 외부 ip -p 포트 [포트: 포워딩한 포트]
```
포트 포워딩은 공유기 관리자 사이트에서 진행 [link](https://velog.io/@dev2820/raspberry-pi-ssh-%EC%97%B0%EA%B2%B0%ED%95%98%EA%B8%B0)

### Ubuntu 방화벽 확인 [link](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=adsl6662&logNo=221175610821)

### Ubuntu terminator 단축키
```
* 수평 분할        : Ctrl + Shift + O
* 수직 분할        : Ctrl + Shift + E
* 현재 활성 창 닫기  : Ctrl + Shift + W
* 터미네이터 실행    : Ctrl + Alt + T
* 터미네이터 종료    : Ctrl + Shift + Q
* 창 전환          : Alt + 방향키
```

### MAC iterm2 단축키 [link](http://choesin.com/%ED%82%A4%EB%B3%B4%EB%93%9C-%EB%8B%A8%EC%B6%95%ED%82%A4%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-mac%EC%97%90%EC%84%9C-%EC%A6%89%EC%8B%9C-%EC%A0%84%EC%B2%B4-%ED%99%94%EB%A9%B4-%ED%84%B0%EB%AF%B8)
```
* 새창 열기        : option + space
* 창 수평 분할      : command + D
* 창 수평 분할      : command + shift + D
```

### Git
```
git push <remote-name> <local-branch-name>:<remote-branch-name>
```
