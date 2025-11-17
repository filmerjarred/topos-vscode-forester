

# topos-vscode-forester

VSCode support for [Forester](https://www.jonmsterling.com/jms-005P.xml), a tool for tending forests of evergreen notes. This extension was hard forked from [vscode-forester](https://github.com/Trebor-Huang/vscode-forester) and developed further by the [topos institute](https://topos.institute/)

## Features
- Language highlight.
  - Use `\startverb%tex` to retain TeX highlighting (which agrees with whatever TeX language support you happen to have installed) in verbatim environments. Otherwise the verbatim part will not be highlighted.

- Tree ID completion: You can type in a part of the title/ID/taxon to filter for trees. Press tabs to insert the ID (which will replace the title you entered).

- Hover information: hover over a link to a tree to see it's metadata and rename the tree if desired

- Automatic title hints: will automatically show the title and taxon of a tree beside a transclusion link

- Tree creation: right-click on a folder and select the "New Tree..." item, which guides you in creating a new tree. Now also supports "creating and transcluding" into existing document with one command. (Hot tip: If you have text selected when you run the command, that text will be moved to the new tree.)

- Tree rename: Easily change the title and taxon of a tree

- Navigte between trees: Ctrl+click (or Cmd+click) on tree references like `\transclude{tree-id}` to navigate to tree

## Experimental Features

- Forest status: beta status bar item showing whether or not the forest is in a valid state

- Interactive forest structure view: a new beta panel that shows the transclusion structure of a set of trees going back to the root

## Commands

| Command | Shortcut | Description |
|---------|----------|-------------|
| `Forester: New Tree` | *not-set* | Create a new tree. You will be asked for a prefix and a template to use, defaults can be set for both (including "no template") if you always use the same. If you have text selected when you execute the command the text will be moved into the new tree. |
| `Forester: New Tree From Template` | *not-set* | Same as "new tree" but will always ask for a template even if a default is set. |
| `Forester: Transclude New Tree` | `Ctrl+Shift+T` (Mac: `Cmd+Shift+T`) | Same as "new tree" but inserts a transclusion link to new tree at the cursor. |
| `Forester: Rename Tree` | | Rename the current tree, unless cursor is within a link and then rename that tree. Can also trigger via hovering the link. |
| `Forester: Show Forest Structure View` | | Display the forest structure view in the Explorer sidebar |

## Requirements

You need forester installed, see [here](https://www.jonmsterling.com/jms-005P.xml) for the instructions. Configure the paths in the settings. Since this plugin is in early development, you will often need the `HEAD` commit of forester to be compatible.

## Extension Settings

- Use `forester.path` to configure the path to forester. It needs to include the name of the executable too.
- Use `forester.config` to specify the forester config file. This should usually be edited per workspace, instead of globally.
  - In the toml file, add a line `prefixes = ["prfx", ...]` to specify the prefixes to pick from. This is used when creating new trees.
- Use `forester.defaultPrefix` to if you set this property you won't be asked for a prefix.
- Use `forester.create.author` to specify default author for new trees (omitted if not set).
- Use `forester.create.random` to control whether the tree ID is generated randomly or sequentially.
- Use `forester.create.openNewTreeMode` to control how newly created trees are opened in the editor:
  - `"off"`: Do not open the new tree
  - `"background"`: Open the new tree in the background (default)
  - `"side"`: Open the new tree to the side in a new editor column
  - `"active"`: Open the new tree as the active editor
- Use `forester.completion.showID` to toggle whether the tree ID is shown in completions. It is recommended to use smaller fonts when switching on this feature. There are also plugins to create keybindings for setting toggles, in case you need to switch it on and off quickly. VSCode also has a lot of useful settings in the `editor.suggest` section worth looking at in conjunction.
- Use `forester.decorations.enabled` to enable or disable inline title hints next to transclude/import/export commands (enabled by default).
- Use `forester.taxonCustomization` to customize how different taxons are abreviated and how they appear in the tree structure:

```json
{
  "forester.taxonCustomization": {
    "theorem": {
      "emoji": "⭐",
      "abbreviation": "thm"
    },
    "definition": {
      "emoji": "🧪",
      "abbreviation": "def"
    }
  }
}
```

