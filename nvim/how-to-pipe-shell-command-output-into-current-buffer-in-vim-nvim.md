# September 13, 2023 TIL - How to Pipe Shell Command Output Into Current Buffer in Vim/Nvim

Easily pipe (properly formatted/decoded) shell command output(s) into current buffer in Vim/Nvim.

```vimdoc
							*:r!* *:read!*
:[range]r[ead] [++opt] !{cmd}
			Execute {cmd} and insert its standard output below
			the cursor or the specified line.  A temporary file is
			used to store the output of the command which is then
			read into the buffer.  'shellredir' is used to save
			the output of the command, which can be set to include
			stderr or not.  {cmd} is executed like with ":!{cmd}",
			any '!' is replaced with the previous command |:!|.
			See |++opt| for the possible values of [++opt].
```

```vim
" `ls | head -n 3` output piped into current buffer
:r !ls | head -n 3
" > init.lua
" > settings.json
" > README.md

" `cal` output piped into current buffer
:r !cal
" >  September 2023     
" >  Su Mo Tu We Th Fr Sa  
" >                  1  2  
" >  3  4  5  6  7  8  9  
" >  10 11 12 _1_3 14 15 16  
" >  17 18 19 20 21 22 23  
" >  24 25 26 27 28 29 30  
```

## Use Cases

- A better/simpler way to pipe shell command output(s) into the current buffer in Vim/Nvim
- `:r !ls | head -n 3` is a cleaner version of `:put = execute('!ls \| head -n 3')`

## Reference

- See `:help :r!` or `:help :read!`

