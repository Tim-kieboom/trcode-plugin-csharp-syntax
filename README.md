# C# syntax for TerminalCode

Syntax highlighting for C# (`.cs`, `.csx`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin.

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `csharp.wasm`, the tree-sitter grammar built for WebAssembly,
- `manifest.toml`, which says which files are C# (`[language]`: `extensions`, `comment`) and has the
  highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **C#**, and turn it on. C# files are colored when they are opened, and `ctrl+/` comments a line with `//`.

## Where the grammar comes from

The grammar and the query are those of [tree-sitter/tree-sitter-c-sharp](https://github.com/tree-sitter/tree-sitter-c-sharp) at v0.24.0 (d4bbe18)
(MIT, `LICENSE-GRAMMAR`). The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/tree-sitter/tree-sitter-c-sharp && cd tree-sitter-c-sharp
git checkout v0.24.0
tree-sitter build --wasm -o csharp.wasm
```

The module is large (about 7 MB), so a C# file takes a moment (about 0.15 s on a laptop) to set up when it is opened.

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes the first of two patterns on the same text; the grammar's file is written for the last).

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
