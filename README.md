*My personal Vim configuration. Feel free to use. This is the most beginner friendly setup i found so far.* </br></br>
Tested in: 
- MacOS Sequoia (15.4.1), MacOS Default/Built-in Terminal with its factory setup.
- Arch Linux, Alacritty Terminal Emulator + Tmux + zsh Shell. 

___

<div align="center">
   <img width=150 height=150 src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Vimlogo.svg/1200px-Vimlogo.svg.png">
</div>

___

## Prerequisites

1. **Install Vim**:
   Ensure that you have Vim installed on your system, and make sure to use the **latest version**.</br>
   Check it by running this command:
   ```bash
   vim --version
   ```
   You'll see the detailed information about your Vim installed in your machine.</br>
   If Vim ins't installed, it will just show something like `command not found: vim` </br>
   > It's mostly pre-built in every systems. Though could be not the latest or the desired version _(huge version)_.</br>
   >> The best of Vim version is the huge version with +Clipboard feature available. _But how to get some features available is depend on how Vim was compiled in your system._
   >>> You can download it from the official [Vim website](https://www.vim.org/download.php), make sure to get the latest version. Or you can also install it using your system's package manager.
   - For **Ubuntu/Debian**:
     ```bash
     sudo apt update
     sudo apt install vim
     ```
   - For **Fedora/RHEL**:
     ```bash
     sudo dnf update vim
     ```
   - For **macOS** (via Homebrew):
     ```bash
     brew update
     brew upgrade vim
     ```
3. **Install vim-plug** (Plugin Manager):
   This configuration uses [vim-plug](https://github.com/junegunn/vim-plug) as the plugin manager.</br>
   To install vim-plug, run the following command:
   ```bash
   curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
   https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
   ```
4. **Recommended** Install **Node.js**:
   This is optional configuration uses [node.js](https://nodejs.org/en), it's required to use Prettier in Vim.</br>
   To install Node.js, download it from it's official website or click [here](https://nodejs.org/en/download/).
5. **Recommended** Install **prettier** (Code Formatter):
   This is optional configuration uses NPM to install. [prettier](https://prettier.io/)</br>
  **Make sure you have node.js installed** check by running this command:
```bash
node -v
```
and check your NPM (Node Package Manager) version. By default NPM is bundled inside Node.js installation.</br>
Check by running this command:
```bash
npm -v
```
If all checks out, run this command to install prettier:
```bash
npm i -g prettier
```

## .vimrc
*.vimrc* is the configuration file for Vim.</br>
> This single file alone can customised your whole Vim experience.
>> It mostly located in user's home directory path or *~*  it's hidden in the home directory by default.
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
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } } " Fuzzy finder (FZF). 
Plug 'junegunn/fzf.vim'                   " FZF integration in Vim. See keybind setup below.

" Optional Plugins but Recommended. (Uncomment to enable)
" Plug 'wakatime/vim-wakatime'              " Wakatime time tracking. Vim needs to configured with Wakatime API Key
" Plug 'github/copilot.vim'                 " GitHub Copilot integration. Needs to be configured with API Key

" End plugin block
call plug#end()

" ===============================
" UI Customization: CoC popup colors
" ===============================
" Fixes unreadable suggestions and annoying magenta match color.
" This only applies if you're not using any Vim's colorscheme.
" Check inside Vim by running :colorscheme , if it returns default,
" You're good to go. Or else, don't uncomment this part below.
" Use autocommand so it persists across colorscheme changes (future-proof)
" highlight Pmenu       guibg=#2a2a2a guifg=#cccccc
" highlight PmenuSel    guibg=#44475a guifg=#ffffff gui=bold
" highlight PmenuSbar   guibg=#3e3e3e
" highlight PmenuThumb  guibg=#5e5e5e
" highlight CocMenuSel  guibg=#44475a guifg=#ffffff gui=bold
" highlight CocSearch   guifg=#ffb86c gui=bold
" highlight PmenuKind   guifg=#8be9fd guibg=#2a2a2a
" highlight PmenuExtra  guifg=#6272a4 guibg=#2a2a2a

" Keybindings & Custom Mappings
" ===============================

" COC.nvim keybindings
inoremap <silent><expr> <Tab> pumvisible() ? "\<C-n>" : "\<Tab>"
inoremap <silent><expr> <S-Tab> pumvisible() ? "\<C-p>" : "\<C-h>"
inoremap <silent><expr> <CR> pumvisible() ? coc#_select_confirm() : "\<CR>"

" Prettier formatting, format code with <leader>p
nnoremap <leader>p :CocCommand prettier.formatFile<CR>

" Use <leader>e to open Vim's built-in file explorer (netrw)
nnoremap <leader>e :Ex<CR>

" Disable Copilot's default tab mapping (Optional, only enable if you use Copilot) 
" let g:copilot_no_tab_map = v:true

" Cycle Copilot suggestions (Optional, only enable if you use Copilot) 
" imap <C-j> <Plug>(copilot-next)
" imap <C-k> <Plug>(copilot-previous)

" Use Ctrl-l to accept Copilot suggestion (Optional, only enable if you use Copilot) 
" imap <silent><script><expr> <C-L> copilot#Accept("\<CR>")

" Suggestion delay (Optional, only enable if you use Copilot) 
" let g:copilot_idle_delay = 100

" Open a new empty buffer with <leader>n
nnoremap <leader>n :enew<CR>

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

" Move lines up and down with <leader>j/k
nnoremap <leader>j :m .+1<CR>==
nnoremap <leader>k :m .-2<CR>==

" Move marked lines in Visual Mode with <leader>j/k
vnoremap <leader>j :m '>+1<CR>gv=gv
vnoremap <leader>k :m '<-2<CR>gv=gv

" ===============================
" End of configuration
" ===============================

```

- After paste the content to .vimrc save the file and quit Vim.
- Re-open Vim to install the registered plugins in .vimrc by and running this command, just type it:
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
___
