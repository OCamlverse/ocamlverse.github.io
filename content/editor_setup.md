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
  let g:opamshare=substitute(system('opam var share'),'\n$','','''')
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

## Emacs

Emacs and OCaml have a long history together and the support for OCaml in Emacs
is truly excellent.

### Using Opam

Install tooling libraries and the user-setup assitant with:

```
$ opam install user-setup merlin tuareg ocamlformat ocp-indent
```

Then run the user-setup installation:

```
$ opam user-setup install
```

### Manual Setup

Alternatively you can setup Emacs manually yourselves. You'll still need to install
Merlin from Opam first:

```
$ opam install merlin
```

Now it's time for the actual configuration in Emacs. Here's a minimal `init.el` to get you started:

``` emacs-lisp
(require 'package)

(add-to-list 'package-archives
             '("melpa" . "https://melpa.org/packages/") t)
;; keep the installed packages in .emacs.d
(setq package-user-dir (expand-file-name "elpa" user-emacs-directory))
(package-initialize)
;; update the package metadata is the local cache is missing
(unless package-archive-contents
  (package-refresh-contents))

(unless (package-installed-p 'use-package)
  (package-install 'use-package))

(require 'use-package)
(setq use-package-verbose t)

(use-package tuareg
  :ensure t
  :mode (("\\.ocamlinit\\'" . tuareg-mode)))

(use-package dune
  :ensure t)

;; Merlin configuration
(use-package merlin
  :ensure t
  :config
  (add-hook 'tuareg-mode-hook #'merlin-mode)
  (add-hook 'merlin-mode-hook #'company-mode)
  ;; we're using flycheck instead
  (setq merlin-error-after-save nil))

(use-package merlin-eldoc
  :ensure t
  :hook ((tuareg-mode) . merlin-eldoc-setup))

;; This uses Merlin internally
(use-package flycheck-ocaml
  :ensure t
  :config
  (flycheck-ocaml-setup))
```

Now you'll have everything you'd expect from an OCaml IDE within the comfort of your Emacs. All those packages have good documentation, that you're encouraged to check out. In particular you might find those resources very useful:

* [tuareg-mode](https://github.com/ocaml/tuareg)
  * [tuareg cheat-sheet](https://ocamlpro.github.io/ocaml-cheat-sheets/tuareg-mode.pdf)
* [merlin-mode](https://ocaml.github.io/merlin/editor/emacs/)

If you're into utop you can also setup some integration with it like this:

``` emacs-lisp
;; utop configuration
(use-package utop
  :ensure t
  :config
  (add-hook 'tuareg-mode-hook #'utop-minor-mode))
```

Note that this will shadow the keybinding for starting/switching to the toplevel in
`tuareg-mode`, which is intentional.

### Emacs Prelude

The popular Emacs distribution [Emacs Prelude](https://prelude.emacsredux.com/) bundles support for OCaml. More details [here](https://prelude.emacsredux.com/en/latest/modules/ocaml/).

### Emacs LSP Support

Emacs has great support for LSP and can be used directly with OCamlLSP. Emacs has two LSP modes:

- [lsp-mode](https://emacs-lsp.github.io/lsp-mode/): Very feature-rich with many bells and whistles.
- [eglot](https://github.com/joaotavora/eglot): A more spartan mode for the people who value minimalism.

Both are great and support OCaml. If you're into LSP you should check them out.
