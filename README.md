vimfox
======

Live web development plugin for vim.


###what is vimfox?

Vimfox brings live css, javascript and html editing to vim. This means you
can edit a file in vim and directly see the result without having to refresh 
the page in the browser.

This is not my idea. A couple of days ago I was browsing on github and found 
[browser-connect](https://github.com/Bogdanp/browser-connect.vim), a vim-plugin
made by [Bogdanp](http://github.com/Bogdanp) which offers live reloading of css
files. 

I was curious about how the plugin worked and after reading up on websockets I 
decided to write my own plugin.


###installation

1. Install vimfox using pathogen / vundle or clone the repo directly into
your $HOME/.vim directory.

2. cd to the repo's root and:
        
    `$: ./sh install.sh`

   *This will download all the required modules using pip and install
   them locally in the vimfox-plugin directory. This ensures vimfox will
   work in virtualenvs.*


###how to use

Add this script to the (html) page you want to work on
```html
<script type='text/javascript' src="http://localhost:9000/vimfox/vimfox.js"></script>
```

####commands

```vim
" Start the vimfox server and make vimfox commands available to the buffer.
:VimfoxToggle
```

```vim
" Reload the file in the browser without reloading the page.
" <force> boolean (optional) => Force reload the file.
" <fname> string (optional)  => By default vimfox uses the buffer's filename. Use this
"                               if the file on the server has a different name.
:VimfoxReloadFile <force> <fname>
```

```vim
" Reload the page in the browser.
:VimfoxReloadBuffer <force>
```

####autocommands

Vimfox does not include any autocommands. This keeps the vimfox code clean
and the user in control.
You can add your own autocommands to the  ```g:vimfox_autocommands``` dictionary
where the key is the filetype and the value a list of autocommands.
Vimfox will automaticaly enable those autocommands for buffers where 
vimfox is enabled.

```vim
" autocommand examples

" call VimfoxReloadPage after every coffee file write.
let g:vimfox_autocommands['coffee'] = [
  \ "autocmd BufWritePost <buffer> VimfoxReloadPage"
  \]

" call VimfoxReloadFile every time you leave insert mode in a less file.
" The filename argument makes sure vimfox reloads 'foo.css' instead of 
" (the on the server not available) 'foo.less'.
let g:vimfox_autocmmands['less'] = [
  \ "autocmd InsertLeave <buffer> VimfoxReloadFile expand('%:r') . '.css'
  \]

####options

```vim
" host address vimfox server
g:vimfox_host = '127.0.0.1'
g:vimfox_port = 9000

" echo toggle state after VimfoxToggle
g:vimfox_echo_toggle_state = 1

" vimfox autocommands
g:vimfox_autocommands = {}
```

###disclaimer

This plugin has not been thorougly tested (as in has not been tested yet).


###contact

Comments and critique always welcome @ dydrmntion _AT_ gmail


----
Fri Jun 14 20:58:52 CEST 2013
