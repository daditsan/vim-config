My personal Vim configuration. Feel free to use.

## Prerequisites

1. **Install Vim**:
   Ensure that you have Vim installed on your system. It's mostly pre-built in every systems but you can also download it from the official [Vim website](https://www.vim.org/download.php), or install it using your system's package manager.

   - For **Ubuntu/Debian**:
     ```bash
     sudo apt install vim
     ```

   - For **macOS** (via Homebrew):
     ```bash
     brew install vim
     ```

2. **Install vim-plug** (Plugin Manager):
   This configuration uses [vim-plug](https://github.com/junegunn/vim-plug) as the plugin manager. To install vim-plug, run the following command:

   ```bash
   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
   https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
   ```

3. **Recommended** Install **Node.js**:
   This is optional configuration uses [node.js](https://nodejs.org/en) it's required to use Prettier in Vim. To install Node.js, download it from it's official website or click [here](https://nodejs.org/en/download/).

4. **Recommended** Install **prettier** (Code Formatter):
   This is optional configuration uses NPM to install. [prettier](https://prettier.io/)
  **Make sure you have node.js installed** check by running this command:
```bash
node -v
```
and check your NPM (Node Package Manager) version. By default NPM is bundled inside Node.js installation. Check by running this command:
```bash
npm -v
```
If all checks out, run this command to install prettier:
```bash
npm i -g prettier
```

## .vimrc
*.vimrc* is the congiuration file for Vim. This one file can customised your Vim experience.
It mostly located in user's home directory path or *~*. Hidden in the home directory by default.
If you can't find it, proceed to create it. Go to Home directory by running this in terminal:
```bash
cd
```
Then, create the .vimrc file:
```bash
touch .vimrc
```
Open it with Vim:
```bash
vim .vimrc
```
Copy this setup below and paste it in your .vimrc file, and save.
```vimscript
" Adytia Isanda's Vim Configuration
" ===============================
" This file is designed to be easily shared and versioned in a repository.
" Make sure to follow the setup instructions in the README for proper installation.
" Keybindings and settings are tailored to improve productivity and ease of use.

" Set leader key to space
let mapleader = " "

" Basic Settings
" ===============================
" Enable line numbers and relative line numbers for easier navigation
set number
set relativenumber

" Better search behavior (ignore case, smart case, incremental search)
set ignorecase
set smartcase
set incsearch
set hlsearch

" Split settings for better usability
set splitbelow
set splitright

" Tabs & Indentation (4 spaces per tab)
set tabstop=4
set shiftwidth=4
set expandtab
set smarttab

" Allow mouse support (works in all modes)
set mouse=a

" Show matching parentheses
set showmatch

" Syntax highlighting
syntax on

" Enable filetype plugin & indenting
filetype plugin indent on

" Minimal statusline (displays filename, filetype, line number, etc.)
set laststatus=2
set statusline=%f\ %y\ %m%r%=%-14.(%l,%c%V%)\ %P

" Plugin Manager - vim-plug (Make sure vim-plug is installed before using this)
call plug#begin('~/.vim/plugged')

" Plugin List
Plug 'neoclide/coc.nvim', {'branch': 'release'}
Plug 'wakatime/vim-wakatime'              " Wakatime time tracking. Vim needs to configured with Wakatime API Key
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } } " Fuzzy finder (FZF). 
Plug 'junegunn/fzf.vim'                   " FZF integration in Vim. See keybind setup below.
Plug 'github/copilot.vim'                 " GitHub Copilot integration. Needs to be configured with API Key

" End plugin block
call plug#end()

" Keybindings & Custom Mappings
" ===============================

" Use <leader>e to open Vim's built-in file explorer (netrw)
nnoremap <leader>e :Vex<CR>

" Disable Copilot's default tab mapping (optional)
let g:copilot_no_tab_map = v:true

" Use Ctrl-J to accept Copilot suggestion
imap <silent><script><expr> <C-J> copilot#Accept("\<CR>")

" Suggestion delay (optional)
let g:copilot_idle_delay = 100

" Close a current buffer with <leader>e
nnoremap <leader>x :bd<CR>

" Escape key mappings
nnoremap <Esc> :nohlsearch<CR>
tnoremap <Esc> <C-\><C-n>

" Command mode keybinding (use ; instead of :)
nnoremap ; :

" Open FZF :Files with <leader>fa
nnoremap <leader>fa :Files<CR>

" Switch buffers with Tab and Shift+Tab
nmap <Tab> :bn<CR>
nmap <S-Tab> :bp<CR>

" Open terminal with <leader>t
nnoremap <leader>t :term<CR>

" Search & Replace word under cursor with <leader>r
nnoremap <leader>r :let word = expand('<cword>')<CR>:let replacement = input('Replace "' . word . '" with: ')<CR>:if replacement != ""<CR>:execute ':%s/\<' . word . '\>/' . replacement . '/g'<CR>:endif<CR>

" Move lines up and down with <leader>j/k
nnoremap <leader>j :m .+1<CR>==
nnoremap <leader>k :m .-2<CR>==

" Move marked lines in Visual Mode with <leader>j/k
vnoremap <leader>j :m '>+1<CR>gv=gv
vnoremap <leader>k :m '<-2<CR>gv=gv

" ===============================
" End of configuration
" ===============================

" Enable format code text with coc-prettier on save (:w)
autocmd BufWritePre *.js,*.ts,*.jsx,*.tsx,*.json,*.css,*.scss,*.md,*.html :silent! CocCommand prettier.formatFile

```

After paste the content to .vimrc save the file, and restart Vim.
After that Install the registered plugins in .vimrc by running this command in Vim, just type it:
```vim
:PlugInstall
```
Wait until every it tells *Finishing ... Done!* and every list showing *Already installed*

then restart Vim.

## After Installation Config
### 1. Install coc-prettier plugin. This integrates Prettier into Coc's LSP ecosystem.

In Vim, run:
```vim
:CocInstall coc-prettier
```

### 2. Customize Coc config 
Run this command in Vim 
```vim
:CocConfig
```
and paste this syntax below to set Prettier as your formatter:
```json
{
  "prettier.disableSuccessMessage": true,
  "coc.preferences.formatOnSaveFiletypes": [
    "javascript",
    "typescript",
    "javascriptreact",
    "typescriptreact",
    "json",
    "html",
    "css",
    "markdown"
  ]
}
```
Save it.

### 3. Restart Vim, You're all set!
