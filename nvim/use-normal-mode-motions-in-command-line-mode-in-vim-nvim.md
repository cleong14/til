# August 30, 2023 TIL - Use Normal-Mode Motions in Command-Line Mode in Vim/Nvim

By default you can press `CTRL-f` (or otherwise see `set cedit`) when on the Vim
command-line, which opens the command-line window where you can edit the command
using normal-mode Vim editing keys.

See `:help c_ctrl-f` for more information.

```vim
" :help c_ctrl-f
7. Command-line window				*cmdline-window* *cmdwin*
							*command-line-window*
In the command-line window the command line can be edited just like editing
text in any window.  It is a special kind of window, because you cannot leave
it in a normal way.


OPEN						*c_CTRL-F* *q:* *q/* *q?*

There are two ways to open the command-line window:
1. From Command-line mode, use the key specified with the 'cedit' option.
2. From Normal mode, use the "q:", "q/" or "q?" command.
   This starts editing an Ex command-line ("q:") or search string ("q/" or
   "q?").  Note that this is not possible while recording is in progress (the
   "q" stops recording then).

When the window opens it is filled with the command-line history.  The last
line contains the command as typed so far.  The left column will show a
character that indicates the type of command-line being edited, see
|cmdwin-char|.

Vim will be in Normal mode when the editor is opened.

The height of the window is specified with 'cmdwinheight' (or smaller if there
is no room).  The window is always full width and is positioned just above the
command-line.


EDIT

You can now use commands to move around and edit the text in the window.  Both
in Normal mode and Insert mode.

It is possible to use ":", "/" and other commands that use the command-line,
but it's not possible to open another command-line window then.  There is no
nesting.
							*E11* *E1188*
The command-line window is not a normal window.  It is not possible to move to
another window or edit another buffer.  All commands that would do this are
disabled in the command-line window.  Of course it _is_ possible to execute
any command that you entered in the command-line window.  Other text edits are
discarded when closing the window.


CLOSE							*E199*

There are several ways to leave the command-line window:

<CR>		Execute the command-line under the cursor.  Works both in
		Insert and in Normal mode.
CTRL-C		Continue in Command-line mode.  The command-line under the
		cursor is used as the command-line.  Works both in Insert and
		in Normal mode.  There is no redraw, thus the window will
		remain visible.
:quit		Discard the command line and go back to Normal mode.
		":close", CTRL-W c, ":exit", ":xit" and CTRL-\ CTRL-N also
		work.
:qall		Quit Vim, unless there are changes in some buffer.
:qall!		Quit Vim, discarding changes to any buffer.

Once the command-line window is closed the old window sizes are restored.  The
executed command applies to the window and buffer where the command-line was
started from.  This works as if the command-line window was not there, except
that there will be an extra screen redraw.
The buffer used for the command-line window is deleted.  Any changes to lines
other than the one that is executed with <CR> are lost.

If you would like to execute the command under the cursor and then have the
command-line window open again, you may find this mapping useful: >

	:autocmd CmdwinEnter * map <buffer> <F5> <CR>q:


VARIOUS

The command-line window cannot be used when there already is a command-line
window (no nesting).

Some options are set when the command-line window is opened:
'filetype'	"vim", when editing an Ex command-line; this starts Vim syntax
		highlighting if it was enabled
'rightleft'	off
'modifiable'	on
'buftype'	"nofile"
'swapfile'	off

It is allowed to write the buffer contents to a file.  This is an easy way to
save the command-line history and read it back later.

If the 'wildchar' option is set to <Tab>, and the command-line window is used
for an Ex command, then two mappings will be added to use <Tab> for completion
in the command-line window, like this: >
	:inoremap <buffer> <Tab> <C-X><C-V>
	:nnoremap <buffer> <Tab> a<C-X><C-V>
Note that hitting <Tab> in Normal mode will do completion on the next
character.  That way it works at the end of the line.
If you don't want these mappings, disable them with: >
	au CmdwinEnter [:>] iunmap <buffer> <Tab>
	au CmdwinEnter [:>] nunmap <buffer> <Tab>
You could put these lines in your vimrc file.

While in the command-line window you cannot use the mouse to put the cursor in
another window, or drag statuslines of other windows.  You can drag the
statusline of the command-line window itself and the statusline above it.
Thus you can resize the command-line window, but not others.

The |getcmdwintype()| function returns the type of the command-line being
edited as described in |cmdwin-char|.

Nvim defines this default CmdWinEnter autocmd in the "nvim_cmdwin" group: >
    autocmd CmdWinEnter [:>] syntax sync minlines=1 maxlines=1
<
You can disable this in your config with "autocmd! nvim_cmdwin". |default-autocmds|


AUTOCOMMANDS

Two autocommand events are used: |CmdwinEnter| and |CmdwinLeave|.  You can use
the Cmdwin events to do settings specifically for the command-line window.
Be careful not to cause side effects!
Example: >
	:au CmdwinEnter :  let b:cpt_save = &cpt | set cpt=.
	:au CmdwinLeave :  let &cpt = b:cpt_save
This sets 'complete' to use completion in the current window for |i_CTRL-N|.
Another example: >
	:au CmdwinEnter [/?]  startinsert
This will make Vim start in Insert mode in the command-line window.

					*cmdline-char* *cmdwin-char*
The character used for the pattern indicates the type of command-line:
	:	normal Ex command
	>	debug mode command |debug-mode|
	/	forward search string
	?	backward search string
	=	expression for "= |expr-register|
	@	string for |input()|
	`-`	text for |:insert| or |:append|
```

## Use Cases

- Use Vim/Nvim normal-mode motions while editing in command-line mode
- Improves continuity in overall editing workflow in Vim/Nvim

## References

- [vi - Using normal-mode motions in command-line mode in Vim - Stack Overflow](https://stackoverflow.com/questions/7186880/using-normal-mode-motions-in-command-line-mode-in-vim/7189573#7189573)

