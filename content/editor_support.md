---
tags: [ecosystem, learning]
---

# Editor Support

[Merlin](https://github.com/ocaml/merlin) is the tool used for code completion, type querying, locating definitions etc for OCaml. Regardless of which editor you use, you'll want to install Merlin for your ocaml compiler with `opam install merlin`.

## Visual Studio Code
This is the easiest editor to set up for OCaml.

## Vim or Neovim
Vim and Neovim are relatively complex tools, and their configuration requires editing their `.vimrc` file (in the case of Neovim, it's `.config/nvim/init.vim` on Linux). 

### Merlin Plugin

In order to just have basic Merlin support, all you need is to add this snippet to enable Merlin's VIM plugin:

```
if executable('opam')
  let g:opamshare=substitute(system('opam config var share'),'\n$','','''')
  if isdirectory(g:opamshare."/merlin/vim")
    execute "set rtp+=" . g:opamshare."/merlin/vim"
  endif
endif
```

This approach has the advantage of loading the same plugin version as is available in Merlin via OPAM, preventing any mismatches.

#### Bindings

You can disable Merlin's default keybindings and create your own with the line
```
let g:merlin_disable_default_keybindings = 1.
```
but normally, Merlin's keybindings are good enough. Note that Merlin precedes all its bindings with <LocalLeader>, which by default is backslash (`\`). You can find out more about the leader keys and changing them in vim's help (type `:help leader`).
  
Here are the default bindings (substitute your choice of LocalLeader instead of `\`:
* `\t`: get the type of the current expression
* `gd`: this is a standard binding that Merlin overrides for OCaml files. Go to definition.
* `C-x C-o`: get a completion suggestion from Merlin.
* `\t` in visual mode: get the type of the selection
* `\n`: grow the enclosing expression to get its type
* `\p`: shrink the enclosing expression
* `]]`: Another standard Vim binding -- Merlin makes sure it jumps between phrases properly.
* `[[`: The opposite of the above binding.

#### Extra Options

* To add automatic documentation lookup (if available) when completing, add the line
  ```
  let g:merlin_completion_with_doc = 1
  ```
  This is particularly useful when using Deoplete for instant completion.

## Vim-Plug

Installing anything beyond Merlin itself gets much easier once we have a proper plugin manager for Vim/Neovim.
We recommend [Vim-Plug](https://github.com/junegunn/vim-plug).
Installing Vim-Plug involves placing the following lines in your config file:

```
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.vim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source $MYVIMRC
endif

call plug#begin('~/.vim/plugged')

" Put plugin calls here
" Example plugin declaration. (Github repo path minus the github.com part)
" Plug 'junegunn/seoul256.vim'

call plug#end()
```

Once you start up Vim/Neovim, use `:PlugInstall` to install any plugins in your config file
that are yet to be installed, and `:PlugUpdate` to update the plugins that are installed.

## Deoplete

To make the most of Merlin's completions, you'll want to install Deoplete, which instantly
suggests completion options for you, like Intellisense on Visual Studio Code.

In the plugin section, add the plugins

```
Plug 'Shougo/deoplete.nvim'
Plug 'copy/deoplete-ocaml'
```

Elsewhere in your config file, add these lines:

```
" enable deoplete
let g:deoplete#enable_at_startup = 1

" this is the default, make sure it is not set to "omnifunc" somewhere else in your vimrc
let g:deoplete#complete_method = "complete"

" other completion sources suggested to disable
let g:deoplete#ignore_sources = {}
let g:deoplete#ignore_sources.ocaml = ['buffer', 'around', 'member', 'tag']

" no delay before completion
let g:deoplete#auto_complete_delay = 0
```

You now should have instant completion via Merlin!

## emacs
