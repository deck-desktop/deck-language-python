# Python for Deck

basedpyright, for `.py` and `.pyi`. A project is anything with a `pyproject.toml` — a folder
without one gets no server, which is the usual cause of "it works here and not there".

```sh
npm rm -g pyright     # they claim the same bin names
npm i -g basedpyright
```

## Why basedpyright rather than pyright

Same type checking, plus semantic tokens. Open-source pyright advertises no
`semanticTokensProvider` at all, so type names stay the colour Monaco's grammar makes them —
which for Python is plain text, since its grammar tags every name as an identifier.

## The token colours are not decoration

basedpyright emits types the base palette does not cover, and **an unstyled semantic token
overrides the grammar's colour with nothing**. Without the `decorator` rule here, `@dataclass`
goes from blue to white and adding the server looks like a regression. `selfParameter` and
`clsParameter` are there for the same reason.

## Installing it

From inside Deck: **Settings -> Plugins -> Browse**, pick it, and it loads straight away.

By hand: copy this folder into `%APPDATA%\Deck\languages\` (`Deck-Dev` for a debug build).
`docs/languages.md` in the Deck repository documents the format.

## What a definition can and cannot do

It is **data**, not code. `language.json` is parsed field by field and never executed, which is
why a language is a different kind of thing from a plugin even though both are folders Deck
reads at startup. The worst a malformed one can do is skip itself.
