### Installation

- Backup your previous configuration (if any exists)

### Archive Installation

- On the home/landing page for the project find the blue "<> CODE" button click it and select Local > Download ZIP.
- Extract the archive to:
  `~/.config/nvim` (Linux)
  `~/.config/nvim` (MacOS)
  `%userprofile%\AppData\Local\nvim\` (Windows)
- Ensure your extraction method did not extract with a parent folder. For example in ~/.config/nvim you should have init.lua not another folder called kickstart.nvim.

### Git Clone Installation

- From a terminal cd/dir to:
  `~/.config/nvim` (Linux)
  `~/.config/nvim` (MacOS)
  `%userprofile%\AppData\Local\nvim\` (Windows)

- Run: `git clone https://github.com/mihlali-jordan/nvim-config.git ~/.config/nvim` OR: `gh repo clone mihlali-jordan/nvim-config.nvim`
- Run Neovim (from terminal or shortcut) and allow lazy.nvim to download files and set up the basics.
- Once the setup is complete, restart Neovim.
- **You're ready to go!**

- (Recommended/Optional) Fork this repo (so that you have your own copy that you can modify).
- Clone the kickstart repo into `$HOME/.config/nvim/` (Linux/Mac) or `%userprofile%\AppData\Local\nvim\` (Windows)
  - If you don't want to include it as a git repo, you can just clone it and then move the files to this location

Additional system requirements:

- Make sure to review the readmes of the plugins if you are experiencing errors. In particular:
  - [ripgrep](https://github.com/BurntSushi/ripgrep#installation) is required for multiple [telescope](https://github.com/nvim-telescope/telescope.nvim#suggested-dependencies) pickers.
- See [Windows Installation](#Windows-Installation) if you have trouble with `telescope-fzf-native`

#### Example: Adding an autopairs plugin

In the file: `lua/custom/plugins/autopairs.lua`, add:

```lua
-- File: lua/custom/plugins/autopairs.lua

return {
  "windwp/nvim-autopairs",
  -- Optional dependency
  dependencies = { 'hrsh7th/nvim-cmp' },
  config = function()
    require("nvim-autopairs").setup {}
    -- If you want to automatically add `(` after selecting a function or method
    local cmp_autopairs = require('nvim-autopairs.completion.cmp')
    local cmp = require('cmp')
    cmp.event:on(
      'confirm_done',
      cmp_autopairs.on_confirm_done()
    )
  end,
}
```

This will automatically install [windwp/nvim-autopairs](https://github.com/windwp/nvim-autopairs) and enable it on startup. For more information, see documentation for [lazy.nvim](https://github.com/folke/lazy.nvim).

#### Example: Adding a file tree plugin

In the file: `lua/custom/plugins/filetree.lua`, add:

```lua
-- Unless you are still migrating, remove the deprecated commands from v1.x
vim.cmd([[ let g:neo_tree_remove_legacy_commands = 1 ]])

return {
  "nvim-neo-tree/neo-tree.nvim",
  version = "*",
  dependencies = {
    "nvim-lua/plenary.nvim",
    "nvim-tree/nvim-web-devicons", -- not strictly required, but recommended
    "MunifTanjim/nui.nvim",
  },
  config = function ()
    require('neo-tree').setup {}
  end,
}
```

This will install the tree plugin and add the command `:Neotree` for you. You can explore the documentation at [neo-tree.nvim](https://github.com/nvim-neo-tree/neo-tree.nvim) for more information.
