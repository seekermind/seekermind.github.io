---
layout: post
title: Ultisnips tab to next placeholder not working when snippet entry is selected from coc menu
description: I use Ultisnips along with coc(Concurer of Completion). I came across this unique problem and solved it. 
summary: You need to add a block in your vimrc which is given in coc-snippets github readme page.
tags: 
---

So I came across this unique and specific problem today that when I select a snippet fom coc autocompletion menu, 'tab to go to next placeholder' does not work. Clicking tab just writes a tabspace which is very annoying. Turns out this **problem does not occure when I expand a snippet by clicking tab** (my map for UltiSnipsExpandTrigger).

So at this point, I realized that this problem is related with coc extension coc-snippets and went for a quick visit to its github page. And there I found the solution.

Make `<tab>` used for trigger completion, completion confirm, snippet expand and jump like VSCode
```vim
inoremap <silent><expr> <TAB>
      \ pumvisible() ? coc#_select_confirm() :
      \ coc#expandableOrJumpable() ? "\<C-r>=coc#rpc#request('doKeymap', ['snippets-expand-jump',''])\<CR>" :
      \ <SID>check_back_space() ? "\<TAB>" :
      \ coc#refresh()

function! s:check_back_space() abort
  let col = col('.') - 1
  return !col || getline('.')[col - 1]  =~# '\s'
endfunction

let g:coc_snippet_next = '<tab>'
```


