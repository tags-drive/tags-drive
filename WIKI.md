# Wiki

- [Wiki](#wiki)
  - [File search](#file-search)
  - [Trash](#trash)
  - [Preview](#preview)
  - [Other](#other)

## File search

**Tags Drive** provides search with logical expression. You can use logical operators:

- `!` – logical NOT
- `&` – logical AND
- `|` – logical OR
- `(`, `)`

For example, you have tags with id `1`, `5`, `23`. You want to find files with tags `1` and `5` and without `23`, but files must not have tags `1` and `5` at the time. You can use next search request: `!(1&5)&!23`

Additional information about logical algebra on Wikipedia: [Boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra)

## Trash

There are 2 ways to delete a file

- **Trash**: you can move a file into Trash. Then file will be deleted after 1 week.

- **Force delete**: you can delete a file immediately

## Preview

You can open Preview Window by click on file preview. You can switch files by arrows.

## Other

- You can keep files with same filenames
- You can upload files by Drag-and-Drop
- You can tag files before upload on Upload Window
- You can sort files by name, size and adding time
