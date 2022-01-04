# How to add snippets to Lunarvim

## First example: Let's add existing vscode snippet package

1. Clone [https://github.com/dsznajder/vscode-es7-javascript-react-snippets](https://github.com/dsznajder/vscode-es7-javascript-react-snippets):

```bash
git clone https://github.com/dsznajder/vscode-es7-javascript-react-snippets
```

In this example we cloned it to `~/.config/lvim/snippets/` but you can store your snippets anywhere you want.

Now I do have `~/.config/lvim/snippets/vscode-es7-javascript-react-snippets/package.json`

2. And we can require package in `config.lua`:

```lua
require("luasnip/loaders/from_vscode").load { paths = { "~/.config/lvim/snippets/vscode-es7-javascript-react-snippets" } }
```

3. These snippets should work now:
   ![img1](https://github.com/sambergo/add-snippet-examples/blob/main/img/img1.png)

## Second example: Let's add custom snippets

1. Create folder:

```bash
mkdir ~/.config/lvim/snippets/my-snippets
```

2. Create `package.json` with content:

```json
{
  "name": "my-snippets",
  "author": "user",
  "engines": {
    "vscode": "^1.11.0"
  },
  "contributes": {
    "snippets": [
      {
        "language": "javascriptreact",
        "path": "./js-react.json"
      },
      {
        "language": ["javascript", "javascriptreact"],
        "path": "./javascript.json"
      }
    ]
  }
}
```

3. Create `javascript.json` with content:

```json
{
  "test console log object": {
    "prefix": "cltest",
    "body": "console.log('${1:object}:', ${1})",
    "description": "console.log object"
  },
  "test const function": {
    "prefix": "cftest",
    "body": [
      "const ${1:name} = (${2:arguments}) => {",
      "\t\treturn ${3}",
      "\t}"
    ]
  }
}
```

4. Create `js-react.json` with content:

```json
{
  "React funtion component exported": {
    "prefix": "rfce",
    "body": [
      "const ${TM_FILENAME_BASE}: React.FC = () => {",
      "\treturn (",
      "\t\t${1}",
      "\t)",
      "}",
      "",
      "export default ${TM_FILENAME_BASE}"
    ],
    "description": "React function component with export"
  }
}
```

5. Require snippets in `config.lua`:

```lua
require("luasnip/loaders/from_vscode").load { paths = { "~/.config/lvim/snippets/my-snippets" } }
```

6. Make sure it works:
   ![img2](https://github.com/sambergo/add-snippet-examples/blob/main/img/img2.png)

If you followed this your `~/.config/lvim/snippets/` should look like:

![snippets folder](https://github.com/sambergo/add-snippet-examples/blob/main/img/img3.png)
