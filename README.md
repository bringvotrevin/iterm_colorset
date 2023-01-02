# iterm_colorset

### Vim-plug
터미널에 아래 명령어를 입력
```
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```
참고 : https://github.com/junegunn/vim-plug

### Vundle
플러그인을 쉽게 관리할 수 있음
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

### Homebrew
homebrew를 설치하면 터미널 환경에서 바로 필요한 것들을 설치 할 수 있다.
터미널에 아래 입력
```
# homebrew 설치
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 설치확인
brew -v
```

### zsh, oh-my-zsh
zsh는 기본으로 있어서 설치 안했던것 같으나 일단 기록해둠. zsh는 bash를 대신하는 shell 환경이고
oh-my-zsh는 zsh를 더 편리하게 사용할 수 있도록 도와주는 프레임워크로 플러그인과 테마를 편리하게 사용하기 위해 필요
```
# zsh 설치하기
brew install zsh

# zsh 설치경로 확인하기
which zsh

# 기본 shell 변경하기
chsh -s $(which zsh)
```
```
# wget curl 설치
brew install curl

# oh-my-zsh 설치
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Norminette
```
sudo apt-get install ruby ruby-bundler ruby-dev build-essential
git clone https://github.com/42Paris/norminette.git ~/.norminette/
cd ~/.norminette/

# 설치 후
bundle
```


### alias
norminette와 gcc를 간편하게 하기 위해 alias로 설정했다
~/.zshrc 안에 아래 문구를 추가한다
```
alias norminette="~/.norminette/norminette.rb"
alias nnt="~/.norminette/norminette.rb"
alias nntr="nnt -R CheckForbiddenSourceHeader"
alias mnt="gcc -Wall -Wextra -Werror"
```

### 설정에 앞서
.vimrc 나 .zsh같은 경우 vim에서 수정시 파일에 추가입력을 하고 노멀모드에서 :source % 또는 :so % 명령어로 재로드해야함. vim모드 나가서 터미널 환경에서 source ~/.vimrc(zshrc)를 해줘도됨   
.vimrc에 플러그인을 추가할 경우 노멀모드에서 :PluginInstall을 해줘서 설치해주는것도 잊으면 안된다!

### 42 header
42서울 과제를 제출할 때에는 파일 위에 무조건 자신의 이름과 이메일이 담긴 헤더가 필요하기 때문에 헤더 설치가 필수이다
42header 플러그인을 설치해준다
```
vi ~/.vimrc
```
로 vim을 켠 뒤
```
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'pbondoer/vim-42header'
call vundle#end()
let g:hdr42user='dim'
let g:hdr42mail='dim@student.42seoul.kr'
```
를 추가해준다.
그리고 빔을 다시 켠 뒤 normal moded에서
```
:PluginInstall
```
을 해주면 설치 완료!
![](https://media.discordapp.net/attachments/801509755981004842/807644674570321940/2021-02-07_1.11.16.png)
맥북 설정-키보드에서 위 사진 맨 마지막에 있는 F1,F2등의 키를 표준 기능키로 사용한다는 박스를 체크하고vim 들어가서 F1키를 누르면 헤더가 뜬다.
또는, vim 켜고 :Stdheader를 입력해도 됨

참고 : https://github.com/pbondoer/vim-42header

### RainbowParenthese 자동설정

vim 화면 켰을 때 따로 명령어 안쳐도 바로 괄호에 색깔 입혀져서 나오게 설정함 

```~/.vimrc```에 추가하면 됨
```
" Rainbow Parentheses options {
    function! Config_Rainbow()
        autocmd! TastetheRainbow VimEnter * call Load_Rainbow() " 64bit Hack - Set VimEnter after syntax load
    endfunction

    function! Load_Rainbow()
        call rainbow_parentheses#activate()
    endfunction

    augroup TastetheRainbow
        autocmd!
        autocmd Syntax * call Config_Rainbow() " Load rainbow_parentheses on syntax load
        autocmd VimEnter * call Load_Rainbow()
    augroup END

    " rainbow_parentheses toggle
    nnoremap <silent> <Leader>t :call rainbow_parentheses#toggle()<CR>
" }
```

### NerdTree, RainbowParentheses
파일 탐색기(nerdtree) 기능과 괄호 색깔을 입혀주는(rainbowParentheses)기능을 추가했다. 파일 열고 닫을 때 빔을 열었다 닫았다하는 수고를 덜어줌, 괄호 짝맞춰서 색깔이 달라서 좀 더 보기 쉽게 해줌.
헤더 설치와 동일하게 .vimrc에
```
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'
Plugin 'junegunn/rainbow_parentheses.vim'
call vundle#end()
```
를 넣어주면 되지만 헤더 설정하며 3,4번째 줄을 제외하고는 이미 입력이 되어 있기 때문에 3,4번째 줄만 기존에 입력된것들 사이에 넣어주면 된다.   
그리고 vim 노멀 모드에서 :NERDTree, :RainbowParentheses를 치는게 여간 귀찮은 일이 아니라 Maping(단축키)까지 추가해줌(아래참고).   
각각 nnn과 rrr을 누르면 실행됨. NERDTree는 toggle이 가능해서 nnn으로 active와 deactive가 되는데 RainbowParentheses는 :RainbowParentheses! 로 deactive해줘야됨.

그리하여 내 .vimrc 파일 안에는 이렇게 들어가 있다.
```
set nocompatible
filetype off
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
Plugin 'VundleVim/Vundle.vim'
Plugin 'pbondoer/vim-42header'
Plugin 'scrooloose/nerdtree'
Plugin 'junegunn/rainbow_parentheses.vim'
call vundle#end()
set number
syntax on
set tabstop=4
set sw=4
set sts=4
set cindent
set smartindent
let g:hdr42user='dim'
let g:hdr42mail='dim@student.42seoul.kr'
" Rainbow Parentheses options {
    function! Config_Rainbow()
        autocmd! TastetheRainbow VimEnter * call Load_Rainbow() " 64bit Hack - Set VimEnter after syntax load
    endfunction

    function! Load_Rainbow()
        call rainbow_parentheses#activate()
    endfunction

    augroup TastetheRainbow
        autocmd!
        autocmd Syntax * call Config_Rainbow() " Load rainbow_parentheses on syntax load
        autocmd VimEnter * call Load_Rainbow()
    augroup END

    " rainbow_parentheses toggle
    nnoremap <silent> <Leader>t :call rainbow_parentheses#toggle()<CR>
" }
" Mapping
nnoremap rrr :RainbowParentheses<enter> 
nnoremap nnn :NERDTreeToggle<enter>
```
### itrem2 theme 

1. https://iterm2colorschemes.com/ 에서 tar.gz 또는 .zip파일 다운로드 후 압축 풀기, 하고싶은 테마 골라두기
2. iTerm2를 켠 상태에서 왼쪽 위 상단바에서 iTerm2 > Preferences > Profiles > Color > Color Presets > Import > 압축 푼 폴더 > schemes > 하고싶은 테마 선택하기

### zsh 꾸미기
* #### bullet train theme
1. https://www.slant.co/topics/7553/~theme-for-oh-my-zsh#4 에서 파일 다운로드(나는 bullet-train을 다운받음)
2. 파일을 $ZSH_CUSTOM/themes/에 넣기
```
mv bullet-train.zsh-theme ~/.oh-my-zsh/themes
```
3. vi ~/.zshrc 에서 
```
ZSH_THEME="bullet-train"
```
* #### Powerlevel9 theme 
이 테마같은 경우 깃클론으로 원하는 폴더에 넣어주어서 수월했음.
```
$ git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k
```
를 한 후 ~/.zshrc 에서
```
ZSH_THEME="powerlevel9k/powerlevel9k"
```
로 설정하면 완성

### font

D2 Coding폰트가 한글도 지원하며 예쁘길래 다운받음. 위에서 했던 oh my zsh 테마를 바꾸면 깨지는 글자가 많아서 폰트 바꾸는게 필요

(https://github.com/naver/d2codingfont)

1. 원하는 글꼴 다운로드
2. 다운로드 파일 압축해제 후 서체 설치
3. iTerm2를 켠 상태에서 왼쪽 위 상단바에서 iTerm2 > Preferences > Profiles > Text > change font > 폰트선택

### vscode extensions
![extensions](https://media.discordapp.net/attachments/801509755981004842/885087724598603786/Screen_Shot_2021-09-08_at_5.59.27_PM.png?width=1638&height=1230)

## JS

### Eslint, Prettier 설치
우테코 제한사항에 맞추기 위해 eslint와 prettier를 설치해서 규칙에 안맞는 코드 에러띄우려고 설치함
`npm install eslint eslint-config-airbnb-base eslint-plugin-import` 설치하기
후에 `.eslintrc` 파일에 아래 코드 추가하기
```
{
  "extends": ["airbnb-base"],
  "env": {
    "node": true,
    "es6": true,
    "browser": true,
    "jest": true
  },
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "max-lines-per-function": ["error", 10],
    "max-depth": ["error", 2],
    "max-params": ["error", 3],
    "consistent-return": "off",
    "object-curly-newline": "off",
    "implicit-arrow-linebreak": "off"
  }
}
```


