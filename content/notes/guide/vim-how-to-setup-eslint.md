---
title: "Vim: How to setup local eslint?"
is: Guide
date: 2016-02-27T15:34:00
categories:
  - Vim
  - ESLint
---

I've been using source code linting for two years. It is a simple step in the
development workflow that together with other best-practices improves
readability and maintainability of the source code.

I'm an Atom editor user but I'm trying new editors: Vim and Emacs. In order to
reach the same productivity I have using Atom, without losing quality, I had to
setup [Syntastic](https://github.com/scrooloose/syntastic) Vim plugin and 
configure [ESLint](http://eslint.org/) on it.

At first sight (reading Syntastic github README.md file) it seems to be very
easy to do it, however all Node.js projects I work on have ESLint specific rules
and versions.

Checkout below the snippet that must be added to your `~/.vimrc` file to setup
local ESLint support to your projects.

```vim
" Syntastic local ESLint support

let g:syntastic_javascript_checkers = []

function SetEslintPath()
	let l:filepath = expand('%:p:h')
	let b:syntastic_checkers = syntastic#util#findFileInParent('.eslintrc', expand('%:p:h', 1)) !=# '' ? ['eslint'] : []
	let b:syntastic_eslint_exec = split(system("cd " . l:filepath . "; npm bin"), "\n")[0] . "/eslint"
endfunction

autocmd FileType javascript call SetEslintPath()
```

I'm new to Vim / Vim Script, suggestions are welcome!

