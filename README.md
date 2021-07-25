# starter
начальные настройки и прочие лафхаки

### гайд по [markdown](https://github.com/zanudazanudnaya/21school_stuff/blob/master/library/cheatsheet_gh-markdown.md)
### шпора по [vim](https://eax.me/vim-commands/)
### Установка [homebrew](https://brew.sh/index_ru)
### основные команды по работе с Git [здесь](https://github.com/robotrainer/school21/blob/master/README.md)
### генератор python [makefail](https://github.com/hgranule/makefile_gen_py)
### ML_21school [полезности](https://github.com/VariyaKh/ML_21school)

### 1 - bash: upgrate to zsh to oh-my-zsh
Зачем переходить на zsh - [habr](https://habr.com/ru/post/326580/).

Установка под WSL:
1. Устанавливаем zsh sudo `apt-get install zsh`
2. Скачиваем и устанавливаем oh-my-zsh `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
3. Перезагружаем терминал

Настройка:
1. Чтобы выбрать новую тему, в файле ~/.zshrc исправьте значение переменной `ZSH_THEME="agnoster"` и перезагрузите терминал.
   * Тема agnoster: для нормальной работы требуется скачать шрифты [fonts-powerline](https://github.com/powerline/fonts) и перезагрузка терминала.
     * Для VSCode: не забудьте скачать и установить сами шрифты себе, [DejaVuSansMono](https://github.com/powerline/fonts/tree/master/DejaVuSansMono).
       Заходим в терминал → кликаем   на значок слева сверху → Настройки → Шрифт → Выбираем `DejaVu Sans Mono for Powerline`.
   * Делим строку (~с текущей директорией и >input) на две строки: редактируем файл `~/.oh-my-zsh/themes/agnoster.zsh-theme` → 82 строка (раздел promt_end), `echo -n "%{%f%}"` меняем   на `echo -n "\n%{%f%}"`. Если хотите чтобы перед input у вас был символ ">", то `echo -n "\e[m\n>%{%f%}"` и перезагрузка терминала.
2. Чтобы были подсказки по установке пакетов - добавляем строчку в ~/.zshrc,  `. /etc/zsh_command_not_found`

### 2 - Vim: [Vundle plugin manager](https://github.com/VundleVim/Vundle.vim) ###
Устанавливаем плагин согласно инструкции, в пункте, где надо прописывать в ~/.vimrc (если его нет, то создайте этот файл) - комментируем дефолтные плагины, которые показаны для иллюстрации.
* Если ставили zsh, то следуя одному из пункту установки – пишем в ~/.vimrc в конце файла, под всеми настройками.
`set shell=/bin/zsh`

### 3 - Vim: [NERDTree + nerdtree-git-plugin](https://github.com/Xuyuanp/nerdtree-git-plugin)
1. Прописываем в ~/.vimrc в разделе плагинов для Vundle
```
Plugin 'scrooloose/nerdtree'
Plugin 'Xuyuanp/nerdtree-git-plugin'
```
2. Под Vundle прописываем настройки для плагина
```
"/NERDTree settings/
let g:NERDTreeIndicatorMapCustom = {
    \ "Modified"  : "✹",
    \ "Staged"    : "✚",
    \ "Untracked" : "✭",
    \ "Renamed"   : "➜",
    \ "Unmerged"  : "═",
    \ "Deleted"   : ":heavy_multiplication_x:",
    \ "Dirty"     : "✗",
    \ "Clean"     : "✔︎",
    \ 'Ignored'   : '☒',
    \ "Unknown"   : "?"
    \ }
"Stick this in your vimrc to open NERDTree with Ctrl+n (you can set whatever key you want):
"Bind ctrl+n
map <C-n> :NERDTreeToggle<CR>
"Show hidden files
let NERDTreeShowHidden=1
```
3. Для установки и обновления плагином в vim пишем ```:PluginInstall```, чтобы открыть дерево используем ctrl+n, переключаться между окон в vim ctrl+w

### 4 - Vim: [Monokai тема](https://github.com/tomasr/molokai) + Syntax hightlight ###
1. Создаем папку под настройки vim в домашнем каталоге, если ее там нет ```mkdir -p ~/.vim/colors```
2.	Скачиваем, устанавливаем и удаляем скачанную папку
```
git clone https://github.com/sickill/vim-monokai.git ~/vim-monokai && mv -v ~/vim-monokai/colors/monokai.vim ~/.vim/colors/ && rm -Rf ~/vim-monokai
```
3.	[Airline: темы стрелок](https://github.com/vim-airline/vim-airline). Прописываем в ~/.vimrc в раздел bundle:
```
Plugin 'vim-airline/vim-airline'
Plugin 'Yavor-Ivanov/airline-monokai-subtle.vim'
```
4.	Прописываем в ~/.vimrc в конце дока
```
"подсветка синтаксиса
syntax enable

"/Theme settings/
"выбор цветовой схемы
colorscheme monokai
let g:airline_theme = 'monokai_subtle'

"если стрелки не заработали
let g:airline_powerline_fonts = 1
```
5.	Для установки и обновления плагинов через Vundle в vim пишем ```:PluginInstall``` и перезагружаем терминал

### 6 - Vim: Code lifehack's ###
Пропишите данные команды в конце файла vim ~/.vimrc:
```
"/Code lifehack's/
"показать нумерацию строк
set number

"подсвечивает курсор
set cursorline

"подсвечивает текущую строчку
set cursorcolumn

"копирует отступы с текущей строки и добавляет их при добавлении новой
set autoindent

"c indent = копирует отступы с текущей строки и добавляет их при добавлении новой для *.c файлов
set cindent

"добавляет ) после написания символа (
inoremap ( ()<left>
inoremap () ()

"добавляет } после написания символа {
inoremap { {}<Left><enter><up><end>
inoremap {} {}<Left>

"добавляет " после написания символа "
inoremap " ""<left>
inoremap "" ""

"подсвечивает красным пробелы в конце строки
highlight ExtraWhitespace ctermbg=red guibg=red
match ExtraWhitespace /\s\+$\|\s+\s{1}/

"подсвечивает синим строку, если та будет превышать 80 знаков
highlight MoreThan80 ctermbg=blue guibg=blue
:2match MoreThan80 /\%81v.\+/

"определяет ширину 1ой Tab'уляции в 4 пробела
set tabstop=4

"определяет ширину 1ой Tab'уляции в 4 пробела, при сдвиге выделенного вертикального блока вправо
set shiftwidth=4

```
