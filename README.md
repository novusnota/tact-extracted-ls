# tact-extracted-ls

⚡ Tact language server (of LSP specification), extracted and re-packaged from its official [VSCode extension](https://github.com/tact-lang/tact-vscode).

⚙ Automatically builds upon updates in the upstream VSCode extension through Github Actions.

## Known issues

* Formatter from the Tact's [VSCode extension](https://github.com/tact-lang/tact-vscode) is not a part of language server implementation (i.e. not in `server.ts`), and therefore it's unaccessible in such re-packaged form.

## Installation

The only requirement is having a Node.js version 16 or higher installed. Then, run the following command to install the extracted Tact language server:

```bash
npm i -g tact-extracted-ls
```

<details>
  <summary>Alternatives</summary>
  <p></p>

  Using `yarn`:

  ```bash
  yarn global add tact-extracted-ls
  ```

  Using `pnpm`:

  ```bash
  pnpm add -g tact-extracted-ls
  ```

  Using `bun`:

  ```bash
  bun add -g tact-extracted-ls
  ```

</details>

<p></p>

## Clients

The following editors and IDEs have available clients:

<!--
  TODO: plugins or PRs to support default configuration
  (or at least submit a PR for default configuration)

- [Helix](https://helix-editor.com/) (built-in support)
- Sublime Text (plugin is in the making)
- Emacs        (plugin is in the making)
- Neovim: nvim-lspconfig, mason-lsp
-->

* [Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=KonVik.tact-lang-vscode)
* Sublime Text ([see below](#sublime-text))
* Vim ([see below](#vim))
* Neovim ([see below](#neovim))
* Helix ([see below](#helix))
* Oni ([see below](#oni))
* IntelliJ IDEA and related IDEs from JetBrains ([see below](#jetbrains))

### Sublime Text

First, install the [**LSP** package](https://packagecontrol.io/packages/LSP) if it's not installed already.

Then, open its settings (**Preferences: LSP Settings** in the command palette, <kbd>Ctrl/Cmd</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>), then add this config:

```json
{
  "clients": {
    "Tact": {
      "enabled": true,
      "command": ["tact-extracted-ls", "--stdio"],
      "selector": "source.tact"
    }
  }
}
```

### Vim

For Vim 8 or later install the plugin [prabirshrestha/vim-lsp](https://github.com/prabirshrestha/vim-lsp) and add the following to `.vimrc`:

```vim
if executable('tact-extracted-ls')
  au User lsp_setup call lsp#register_server({
        \ 'name': 'tact',
        \ 'cmd': {server_info->['tact-extracted-ls', '--stdio']},
        \ 'allowlist': ['tact'],
        \ })
endif
```

For Vim 8 or Neovim using [YouCompleteMe](https://github.com/ycm-core/YouCompleteMe), add the following to `.vimrc`:

```vim
let g:ycm_language_server =
    \ [
    \   {
    \     'name': 'tact',
    \     'cmdline': [ 'tact-extracted-ls', '--stdio' ],
    \     'filetypes': [ 'tact' ],
    \   }
    \ ]
```

For Vim 8 or Neovim using [neoclide/coc.nvim](https://github.com/neoclide/coc.nvim), according to [it's Wiki article](https://github.com/neoclide/coc.nvim/wiki/Language-servers#bash), add the following to your `coc-settings.json`:

```jsonc
  "languageserver": {
    "tact": {
      "command": "tact-extracted-ls",
      "args": ["--stdio"],
      "filetypes": ["tact"],
      "ignoredRootPaths": ["~"]
    }
  }
```

### Neovim

For Neovim 0.8 and later:

```lua
vim.api.nvim_create_autocmd('FileType', {
  pattern = 'tact',
  callback = function()
    vim.lsp.start({
      name = 'tact-extracted-ls',
      cmd = { 'tact-extracted-ls', '--stdio' },
    })
  end,
})
```

For Neovim prior to 0.8 and using [autozimu/LanguageClient-neovim](https://github.com/autozimu/LanguageClient-neovim), add the following to `init.vim`:

```vim
let g:LanguageClient_serverCommands = {
    \ 'tact': ['tact-extracted-ls', '--stdio']
    \ }
```

### Helix

Create or open `~/.config/helix/languages.toml` (Use `~\AppData\Roaming\helix\languages.toml` on Windows) and add the following:

```toml
[[language]]
name = "tact"
language-servers = ["tact-extracted-ls"]

[language-server.tact-extracted-ls]
command = "tact-extracted-ls"
args = [ "--stdio" ]
```

### Oni

On the config file (**File → Preferences → Edit Oni config**) add the following configuration:

```javascript
"language.tact.languageServer.command": "tact-extracted-ls",
"language.tact.languageServer.arguments": ["--stdio"],
```

### JetBrains

As of now, Language Server Protocol support is unofficial and only available in IntelliJ IDEA and related IDEs from JetBrains through 3rd-party plugins. Instead, please use the official extension for all things TON in IntelliJ IDEs: [intellij-ton](https://plugins.jetbrains.com/plugin/23382-ton).

### The rest

Didn't find your editor on the list? Try searching for tips in the respective documentation or related community resources.

Note, that some editors may not support the Language Server Protocol (LSP), in which case you're out of luck until such support is added by editor maintainers or external contributors, such as yourself.

If you did manage to set up and use the Tact language server in your editor, then please file an issue or submit a PR to this repository and explain how you did it 🤗

## Contributing

If you have any issues which arise ONLY in the case of using provided language servers outside of VSCode, please, file an issue to [the present repository](https://github.com/novusnota/tact-extracted-ls/issues).

In any other case, please, file issues to the upstream extension repository: [Tact VSCode extension](https://github.com/tact-lang/tact-vscode).

## Credits

Based on [The Open Network](https://ton.org).

Packaged with 🤍 by [Novus Nota](https://github.com/novusnota).

## License

* Packaging: [MIT](https://github.com/novusnota/tact-extracted-ls/blob/main/LICENSE) © [Novus Nota](https://github.com/novusnota)
* [VSCode extension](https://github.com/tact-lang/tact-vscode): [Apache License 2.0](https://github.com/tact-lang/tact-vscode/blob/main/LICENSE)
