# git-permalink.nvim

Generate a permalink for the line or lines you are on and copy it, open it, or
both!

## Setup

Install this plugin. I use nix so I am unhelpful with other plugin managers.

Then you need to call it somehow while in normal or visual mode. The following
is an example keybinding I use:

```lua
-- Generates and copies the link in normal mode.
vim.api.nvim_set_keymap('n', '<Leader>glc', '', {
  callback = function () git_permalink.create_copy('.') end
})

-- Generates and copies the link in visual mode.
vim.api.nvim_set_keymap('v', '<Leader>glc', '', {
  callback = function () git_permalink.create_copy('v') end
})

-- Generates and copies the link in visual mode.
vim.api.nvim_set_keymap('v', '<Leader>glo', '', {
  callback = function () git_permalink.create_open('.') end
})
```

## Exposed Function

### `require('git-permalink').create_link`

- `create_link :: '.' | 'v' -> permalink`

Generates the link and returns it. Useful for integrating with other plugins
or configurations.

### `require('git-permalink').create_copy`

- `create_copy :: '.' | 'v' -> permalink`

Generates the permalink and send it to the `*` and `+` registers in neovim
(essentially to your clipboard).

Additionally it returns the permalink if you'd like to use it after sending it
to the registers.

### `require('git-permalink').create_open`

- `create_open :: '.' | 'v' -> permalink`

Generates the permalink and opens it with your default browser. It will call:

- `open <permalink>` on MacOS
- `xdg-open <permalink>` on Linux (untested)
- `start <permalink>` on Windows (untested)

Additionally it returns the permalink if you'd like to use it after opening
your browser.

### `require('git-permalink').create_copy_open`

- `create_copy_open :: '.' | 'v' -> permalink`

Just like the two above, it generates the permalink, sends it to the `*` and
`+` registers, and opens the browser.

Returns the permalink for use beyond this function.
