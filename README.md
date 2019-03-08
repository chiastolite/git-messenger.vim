git-messenger.vim
=================

[git-messenger.vim][repo] is a Vim/Neovim plugin for 'looking a commit message under the cursor'
quickly.

When you modifying unfamiliar codes, you would sometimes wonder 'why was this line added?' or 'why
this value was chosen?' in the source code. The answer sometimes lays in a commit message,
especially in message of the last commit which modifies the line.

This plugin shows the message of the last commit in a 'popup window'. The popup window is
implemented in

- Floating window on Neovim 0.4 or later
- Preview window on Vim 8+ or Neovim 0.3 or earlier

The floating window is definitely recommended since it can shows the information near the cursor.

Screencast with Neovim v0.4.0-dev:

<img alt=screencast src="https://github.com/rhysd/ss/blob/master/git-messenger.vim/demo.gif?raw=true" width=734 height=620/>



## Installation

If you use any package manager, please follow its instruction.

With [vim-plug](https://github.com/junegunn/vim-plug):

```vim
Plug 'rhysd/git-messenger.vim'
```

With [dein.vim](https://github.com/Shougo/dein.vim):

```vim
call dein#add('rhysd/git-messenger.vim', {
            \   'lazy' : 1,
            \   'on_cmd' : 'GitMessenger',
            \   'on_map' : '<Plug>(git-messenger-',
            \ })
```

With [minpac](https://github.com/k-takata/minpac):

```vim
call minpac#add('rhysd/git-messenger.vim')
```

When you're using Vim's builtin packager, please follow instruction at `:help pack-add`.

To enable a floating window support, you need to install Neovim 0.4 or later. The version is not
yet released, so you need to install Neovim by building from source at this point. If you use macOS,
it's quite easy with Homebrew.

```
$ brew install neovim --HEAD
```



## Usage

### Commands

```
:GitMessenger
```

It opens a popup window with the last commit message which modified the line at cursor. The popup
window will be automatically closed when you move the cursor so you don't need to close it manually.

```
:GitMessengerClose
```

Though a popup window is automatically closed by default, it closes the popup window explicitly. It
is useful when you set `g:git_messenger_close_on_cursor_moved` to `v:false`.

### Mappings

Some `<Plug>` mappings are available to operate a popup window. They can be mapped to your favorite
key sequences. For example:

```vim
nmap <Leader>cm <Plug>(git-messenger)
nmap <Leader>cM <Plug>(git-messenger-into-popup)
```

- `<Plug>(git-messenger)`: The same as running `:GitMessenger` command.
- `<Plug>(git-messenger-close)`: The same as running `:GitMessengerClose` command.
- `<Plug>(git-messenger-into-popup)`: Moves the cursor into the popup window. It's useful when you want to scroll the content and close the window.
- `<Plug>(git-messenger-scroll-down-1)`: Scroll down the popup window by 1 line directly
- `<Plug>(git-messenger-scroll-up-1)`: Scroll up the popup window by 1 line directly
- `<Plug>(git-messenger-scroll-down-page)`: Scroll down the popup window by 1 page directly
- `<Plug>(git-messenger-scroll-up-page)`: Scroll up the popup window by 1 page directly

If `g:git_messenger_no_default_mappings` is not set to `v:false`, this plugin also defines
following default mapping.

```vim
nmap <Leader>gm <Plug>(git-messenger)
```

### Variables

Some global variables are available to configure the behavior of this plugin.

#### `g:git_messenger_close_on_cursor_moved` (Default: `v:true`)

When this value is set to `v:false`, a popup window is no longer closed automatically when moving a
cursor after the window is shown up.

#### `g:git_messenger_git_command` (Default: `"git"`)

`git` command to retrieve commit messages. If your `git` executable is not in `$PATH` directories,
please specify the path to the executable.

#### `g:git_messenger_no_default_mappings` (Default: `v:true`)

When this value is set to `v:false`, it does not define any key mappings. `<Plug>` mappings are
still defined since they don't make any conflict with existing mappings.



## License

Distributed under [the MIT License](LICENSE)

[repo]: https://github.com/rhysd/git-messenger.vim
