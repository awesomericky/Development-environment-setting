# Development-environment-setting

### Linux 설치
Mac에서 ubuntu 부팅 usb 만들기 [link](https://lynmp.com/ko/article/roa0ea27bfcdf035b8)
이후 Bios(F2 연타) 진입하여 부팅 순서 변경 
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
2) CUDA [link](https://developer.nvidia.com/cuda-toolkit-archive)
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
2) ~/.bashrc에 아래 추가 (없을 때만)
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
