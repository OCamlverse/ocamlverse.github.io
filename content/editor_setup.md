---
tags: [ecosystem, learning]
---

# Editor Setup

[Merlin](https://github.com/ocaml/merlin) is the tool used for code completion, type querying, locating definitions etc for OCaml. Regardless of which editor you use, you'll want to install Merlin for your ocaml compiler with `opam install merlin`.

## Visual Studio Code

This is the easiest editor to set up for OCaml.
Just install the [OCaml Platform extension](https://github.com/ocamllabs/vscode-ocaml-platform)
(see README for instructions).

## Vim or Neovim

Vim and [neovim](https://neovim.io/) are relatively complex tools, and their configuration requires editing their `.vimrc` file (in the case of Neovim, it's `.config/nvim/init.vim` on Linux).
If you use neovim, you can either use Merlin, which is OCaml's main code-information tool,
or [ocaml-lsp](https://github.com/ocaml/ocaml-lsp),
which is a language server protocol wrapper on top of Merlin.

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

Use `:help merlin` to find out the keybindings.
A completion engine, like `Ale`, is recommended as well.

### OCaml LSP

Neovim supports LSP servers natively. To add LSP support to Vim, you'll need an extra addon.
To run Neovim with LSP support, the easiest way is to install [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/blob/master/CONFIG.md#ocamllsp)
and configure the necessary lines for ocaml-lsp support.
Make sure to install `ocaml-lsp` via opam and you're done.

## emacs

Install tooling libraries and the user-setup assitant with

```
opam install user-setup merlin tuareg ocamlformat ocp-indent
```

Then run the user-setup installation

```
opam user-setup install
```
