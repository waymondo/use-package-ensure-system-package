# Deprecated

This extension now resides within the official
[`use-package`](https://github.com/jwiegley/use-package) distribution.

# use-package-ensure-system-package

You’re using [`use-package`](https://github.com/jwiegley/use-package)
to manage your Emacs environment. Well played. Maybe you then want to
ensure related system binary packages exist along side of these
package/feature declarations? Oh nice, me too.

## Setup

* Obviously you need to be using
  [`use-package`](https://github.com/jwiegley/use-package).

* Make sure your `exec-path` is cognisant of all binary package names
that you would like to ensure
exist. [`exec-path-from-shell`](https://github.com/purcell/exec-path-from-shell)
is a good way to do this.

* This package leverages
  [`system-packages`](https://github.com/jabranham/system-packages) to
  provide the default install behavior for different systems. If you
  need to customize this beforehand, you may.

## Install

Note: This is only available on [`MELPA`](https://melpa.org).

``` emacs-lisp
(use-package use-package-ensure-system-package
  :ensure t)
```

## Usage

Here’s an example:

``` emacs-lisp
(use-package rg
  :ensure t
  :ensure-system-package rg
  :chords (":G" . rg-projecet))
```

This will expect a global binary package to exist called `rg`. If it
does not, it will use your system package manager to attempt an
install of a binary by the same name asyncronously. For example, for
most `macOS` users it would call: `brew install rg`.

Good default stuff. What if you want to customize the install command?

``` emacs-lisp
(use-package tern
  :ensure t
  :ensure-system-package (tern . "npm i -g tern"))
```

`:ensure-system-package` can take a cons. In that case, its `cdr`
should be a string that will get piped to `(async-shell-command)` to
install the darn thing if it doesn’t exist.

Also you may also pass in a list of cons-es in the same format:

``` emacs-lisp
(use-package ruby-mode
  :ensure-system-package
  ((rubocop     . "gem install rubocop")
   (ruby-lint   . "gem install ruby-lint")
   (ripper-tags . "gem install ripper-tags")
   (pry         . "gem install pry")))
```

## Roadmap

- [ ] Better compatibility with the `:defer` and `:defer-install` keywords.
