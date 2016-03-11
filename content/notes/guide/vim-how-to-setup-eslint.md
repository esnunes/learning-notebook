---
title: "Vim: How to setup local eslint (or any other linter)?"
is: Guide
date: 2016-03-11T14:18:00
categories:
  - Vim
  - ESLint
  - Syntastic
  - Linter
---

**Update (2016-03-11): this note contains instructions to setup any nodejs
linter**

I've been using source code linting for two years. It is a simple step in the
development workflow that together with other best-practices improves
readability and maintainability of the source code.

The integration of most part of the linters with Atom editor is usually a very
simple task however to integrate them with Vim or Emacs a small effort is
needed. To integrate ESLint with Vim you can use
[Syntastic](https://github.com/scrooloose/syntastic) Vim plugin and configure
[ESLint](http://eslint.org/) on it.

At first sight (reading Syntastic github README.md file) it seems to be very
easy to do it and it is when you use a global instance of ESLint, however all
Node.js projects I work have ESLint specific rules and versions.

Checkout below the snippet that must be added to your `~/.vimrc` file to setup
local ESLint (or any other linter) support to your projects.

```vim
" Syntastic local linter support

let g:syntastic_javascript_checkers = []

function CheckJavaScriptLinter(filepath, linter)
	if exists('b:syntastic_checkers')
		return
	endif
	if filereadable(a:filepath)
		let b:syntastic_checkers = [a:linter]
		let {'b:syntastic_' . a:linter . '_exec'} = a:filepath
	endif
endfunction

function SetupJavaScriptLinter()
	let l:current_folder = expand('%:p:h')
	let l:bin_folder = fnamemodify(syntastic#util#findFileInParent('package.json', l:current_folder), ':h')
	let l:bin_folder = l:bin_folder . '/node_modules/.bin/'
	call CheckJavaScriptLinter(l:bin_folder . 'standard', 'standard')
	call CheckJavaScriptLinter(l:bin_folder . 'eslint', 'eslint')
endfunction

autocmd FileType javascript call SetupJavaScriptLinter()
```

The code above basically searches for binary files in the `node_modules/.bin`
folder of the current nodejs project. The snippet above covers `eslint` and
`standard` linters.

I'm new to Vim / Vim Script, suggestions are welcome!

