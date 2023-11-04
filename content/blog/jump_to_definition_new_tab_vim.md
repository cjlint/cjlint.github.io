+++
title = "Jump to Definition in a New Tab in Vim and Neovim"
date = "2023-11-03"
description = "Vim commands to help open definition in a new tab without extra scripting"
tags = ["vim"]
+++

With LSP capabilities in vim, you can use the `gd` command to jump to the definition of something under your cursor. The definition file is opened in the same window, but you might have been trying to look at your original code file and the definition file side by side.

There's no built-in way to tell `gd` to open the new tab or split window without writing more vimscript or lua in your configuration files. But with a little vim-fu you can do it all with no new code, and have the flexibility of choosing a new tab vs. a new split window.

## Jumping back with `<Ctrl-O>`

`<Ctrl-O>` jumps your cursor backwards in the jump list:

```
		*CTRL-O*
CTRL-O		Go to [count] Older cursor position in jump list
			(not a motion command).
```

It's similar to hitting a "back" button in other IDEs. Sometimes, this is all you need -- you quickly checked the definition and you want to go back to your spot in the previous file, done and done.

### Combining with `:tabnew`

If you want to open that definition file more permanently, do `gd` and then `:tabnew`. Now you have one tab with your definition file and one tab that's empty. Luckily, you can still go back in the jump list with `<Ctrl-O>` while staying within this new empty tab. Hitting it once will open the definition file where you just were, and hitting it twice will open your original code file. Hooray! Plus your unsaved changes and undo history are still preserved even in this fresh tab.

### Combining with `:vs`, `:sp`

You can do the exact same thing but substituting `:vs`/`:sp` for `:tabnew`. Actually it's even easier because your new split window opens to the same file, not like the blank tab we saw with `:tabnew`. So you only need to `<Ctrl-O>` once 🎉

### Bonus: `<Ctrl-W>T`

Actually, you made a new split window first, but then you decided your screen space felt cramped and you wish you had made a new tab instead. Fret not, and instantly open your current split window in a new tab with `<Ctrl-W>T` !

### Bonus Bonus: `<Ctrl-W>d`

In the vim help documentation `<Ctrl-W>d` _claims_ that it will split your window and jump to definition under cursor all in one... but it didn't work for me, it says it cannot find the definition. Darn! But you, the reader, should try using it. Maybe it will work in your setup -- I use Neovim and lspconfig with the recommended lsp keybindings configured in my `lsp.lua`.

## Open file from a list with `<Ctrl-W>`

Sometimes when you `gd`, it will open a window showing you the options for which definition to go to. In these cases, you can hit Enter to pick one and it will be opened in the current window. Or, because the filenames happen to be right there under our cursor, we can pick one and go straight to opening it in a new tab or new split window with the respective window commands:

```
|CTRL-W_f|	CTRL-W f	   split window and edit file name under the
				   cursor
|CTRL-W_F|	CTRL-W F	   split window and edit file name under the
				   cursor and jump to the line number
				   following the file name.
|CTRL-W_gf|	CTRL-W g f	   edit file name under the cursor in a new
				   tab page
|CTRL-W_gF|	CTRL-W g F	   edit file name under the cursor in a new
				   tab page and jump to the line number
				   following the file name.
```

`<Ctrl-W>` is the prefix for a bunch of different window commands. Read through them to see if any more would be useful for you `:h ctrl-w`.
