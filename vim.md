Vim

# Vim

Native packages: https://shapeshed.com/vim-packages/

## Keys

" inoremap jk <ESC>
" let mapleader = "ä"

### Plugins

" AwesomeVimColorschemes
set background=dark
colorscheme scheakur

" NERDTree
nnoremap <C-t> :NERDTreeToggle<CR>

### TagBar

" Mapping to open and close the panel
nmap <F8> :TagbarToggle<CR>

### Ctrlsf

" (Ctrl+F) Open search prompt (Normal Mode)
nmap <C-F>f <Plug>CtrlSFPrompt 
" (Ctrl-F + n) Open search prompt with current word (Normal Mode)
nmap <C-F>n <Plug>CtrlSFCwordPath
" (Ctrl-F + t) Toggle CtrlSF window (Normal Mode)
nnoremap <C-F>t :CtrlSFToggle<CR>
" (Ctrl-F + t) Toggle CtrlSF window (Insert Mode)
inoremap <C-F>t <Esc>:CtrlSFToggle<CR>


## Basic config

" Syntax highlight on
syntax on

" Show line numbers
set number

" Don't create a swapfile
set noswapfile

" Highlight all search results
set hlsearch 
" Ignore case for searching
set ignorecase 
" Search while typing
set incsearch 

" Default indent settings
set tabstop=4
set shiftwidth=4
" Expand tab to spaces
set expandtab

" Indent by file type
filetype plugin indent on

" Terminal default size
set termwinsize=10x0
" Show terminal below edit window
set splitbelow
" Support mouse for panel resize
set mouse=a

" Make Vim always render the sign column:
set signcolumn=yes


## Plugins

### Awesome Vim Colorschemes

Git: https://github.com/rafi/awesome-vim-colorschemes.git

set background=dark
colorscheme scheakur

### CMake

Git: https://github.com/cdelledonne/vim-cmake.git

### NERDTree

Git: https://github.com/preservim/nerdtree.git

## Fswitch

au! BufEnter *.cpp let b:fswitchdst = 'hpp,h'
au! BufEnter *.h let b:fswitchdst = 'cpp,c'

### Ctrlsf

Git: https://github.com/dyng/ctrlsf.vim.git

" Use the ack tool as the backend
let g:ctrlsf_backend = 'ack'
" Auto close the results panel when opening a file
let g:ctrlsf_auto_close = { "normal":0, "compact":0 }
" Immediately switch focus to the search window
let g:ctrlsf_auto_focus = { "at":"start" }
" Don't open the preview window automatically
let g:ctrlsf_auto_preview = 0
" Use the smart case sensitivity search scheme
let g:ctrlsf_case_sensitive = 'smart'
" Normal mode, not compact mode
let g:ctrlsf_default_view = 'normal'
" Use absoulte search by default
let g:ctrlsf_regex_pattern = 0
" Position of the search window
let g:ctrlsf_position = 'right'
" Width or height of search window
let g:ctrlsf_winsize = '46'
" Search from the current working directory
let g:ctrlsf_default_root = 'cwd'

### TagBar

Git: https://github.com/preservim/tagbar.git

Requirements: exuberant-ctags

" Focus the panel when opening it
let g:tagbar_autofocus = 1
" Highlight the active tag
let g:tagbar_autoshowtag = 1
" Make panel vertical and place on the right
let g:tagbar_position = 'botright vertical'

### YouCompleteMe

Git: https://github.com/ycm-core/YouCompleteMe.git

Requirements:
- Min: build-essential cmake vim-nox python3-dev
- Full: mono-complete golang nodejs default-jdk npm

Install: python3 install.py --all

let g:ycm_global_ycm_extra_conf = '~/.vim/bundle/YouCompleteMe/.ycm_extra_conf.py'
let g:ycm_confirm_extra_conf = 0
set completeopt-=preview
let g:ycm_autoclose_preview_window_after_insertion = 1
let g:ycm_clangd_args=['--header-insertion=never']

### Vim-Ale

Git: https://github.com/dmerejkowsky/vim-ale.git

### vim-gitgutter

Git: https://github.com/airblade/vim-gitgutter

### vim-sensible

Git: https://github.com/tpope/vim-sensible.git

### auto-pairs

Git: https://github.com/jiangmiao/auto-pairs.git

### vim-gutentags

Git: https://github.com/ludovicchabant/vim-gutentags.git

### vim-airline

Git:
- https://github.com/vim-airline/vim-airline.git
- https://github.com/vim-airline/vim-airline-themes.git

### vim-polyglot

Git: https://github.com/sheerun/vim-polyglot.git


# Overall config

" Syntax highlight on
syntax on

" Show line numbers
set number

" Don't create a swapfile
set noswapfile

" Highlight all search results
set hlsearch 
" Ignore case for searching
set ignorecase 
" Search while typing
set incsearch 

" Indent by file type
filetype plugin indent on

" Terminal default size
set termwinsize=10x0
" Show terminal below edit window
set splitbelow
" Support mouse for panel resize
set mouse=a

" Make Vim always render the sign column:
set signcolumn=yes

" Plugins

" AwesomeVimColorschemes
set background=dark
colorscheme meta5

" NERDTree
nnoremap <C-t> :NERDTreeToggle<CR>

" TagBar
nmap <F8> :TagbarToggle<CR>

" Ctrlsf
" (Ctrl+F) Open search prompt (Normal Mode)
nmap <C-F>f <Plug>CtrlSFPrompt 
" " (Ctrl-F + n) Open search prompt with current word (Normal Mode)
nmap <C-F>n <Plug>CtrlSFCwordPath
" " (Ctrl-F + t) Toggle CtrlSF window (Normal Mode)
nnoremap <C-F>t :CtrlSFToggle<CR>
" " (Ctrl-F + t) Toggle CtrlSF window (Insert Mode)
inoremap <C-F>t <Esc>:CtrlSFToggle<CR>

" Use the ack tool as the backend
let g:ctrlsf_backend = 'ack'
" Auto close the results panel when opening a file
let g:ctrlsf_auto_close = { "normal":0, "compact":0 }
" Immediately switch focus to the search window
let g:ctrlsf_auto_focus = { "at":"start" }
" Don't open the preview window automatically
let g:ctrlsf_auto_preview = 0
" Use the smart case sensitivity search scheme
let g:ctrlsf_case_sensitive = 'smart'
" Normal mode, not compact mode
let g:ctrlsf_default_view = 'normal'
" Use absoulte search by default
let g:ctrlsf_regex_pattern = 0
" Position of the search window
let g:ctrlsf_position = 'right'
" Width or height of search window
let g:ctrlsf_winsize = '46'
" Search from the current working directory
let g:ctrlsf_default_root = 'cwd'

" YoucCompleteMe
let g:ycm_global_ycm_extra_conf = '~/.vim/pack/plugins/start/YouCompleteMe/.ycm_extra_conf.py'
let g:ycm_confirm_extra_conf = 0
set completeopt-=preview
let g:ycm_autoclose_preview_window_after_insertion = 1

packadd termdebug

set tabstop=8
set shiftwidth=8
set noexpandtab
set list
set listchars=tab:>-,trail:!

set colorcolumn=80

autocmd FileType c setlocal shiftwidth=8 tabstop=8




