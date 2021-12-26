# Development-environment-setting

Mac에서 ubuntu 부팅 usb 만들기 [link](https://lynmp.com/ko/article/roa0ea27bfcdf035b8)

### 설치 되어있는 패키지들의 새로운 버젼이 있는지 확인 (밑의 과정 하기 전에 필수)
```
  sudo apt-get update
```
  
### GPU 기본적인 설정이 안되어 있는 경우
GPU drive —> CUDA —> cudnn 순서로 설치 진행

### z shell 설치
1) zsh 설치
```
  sudo apt-get install zsh
  zsh —version
  chsh -s /usr/bin/zsh (z shell을 기본 쉘로 설정)
  echo $SHELL (—>   /usr/bin/zsh 이 나와야함)
```
2) oh-my-zsh 설치
```
  sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
3) Powerlevel10k 설치 [link](https://jungseob86.tistory.com/7)
4) git clone 후 ‘~/zshrc’ 안을 ZSH_THEME="powerlevel10k/powerlevel10k”로 수정
5) 터미널 나갔다가 들어오면 하라는대로 잘 따라가면 됨
6) .p10k.zsh 가서 색변경 (source ~/.p10k.zsh 해야 적용됨) [link](https://github.com/romkatv/powerlevel10k/blob/master/README.md#change-the-color-palette-used-by-your-terminal)
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
1) .sh 설치 파일 실행 [link](https://docs.conda.io/en/latest/miniconda.html)
2) 부가 설정 + 필요한 환경 생성 후 
```
  conda config --set auto_activate_base false (자동 실행 막음)
  condo create -n (env 이름) (조건)
  condo activate (env 이름)
```

### 기타 설치 (tmux, git, htop, gpustat, imagemagick)
```
  sudo apt-get install tmux
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
