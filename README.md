**NOTE**: I'm extracting the core of [putdoc](https://github.com/natevw/putdoc) into its own package. This is currently still a work-in-progress.

# loading-docs

Reads in JSON-like objects from a folder/file structure on disk.

## Installation

This library is published on npm, so you can install via:

```
npm install --save loading-docs
```

## Usage

```
TODO: simple example
```

## Folder → Object mapping

The basic idea is:

* folders generate objects
* files generate entries therein


Thus, given the input…

```
some_folder/
  file1.txt    ('content of file1')
  file2.html   ('content of file2')
  subfolder/
    file.three.json ('["parsed", "content", "of", "file:", 3]')
    content.md      ('# Heading\n\nSome content.')
    helper.js       ('alert("Hello world!")')
```

This library will output…

```
{
  "file1": "content of file1",
  "file2": "content of file2",
  "subfolder": {
    "file.three": ["parsed", "content", "of", "file:", 3],
    "content": "# Heading\n\nSome content.",
    "helper": "alert(\"Hello world!\")"
  }
}
```

Note that:

1. Nested folders become nested objects
2. Each file's name (dropping the last extension) becomes the key for its generated entry
3. Each file's content (parsed as a UTF-8 string) becomes the value for its generated entry

### Special case: .json files

Note also that when the file's extension was `.json`, the string value is parsed as JSON and (if successful) the resulting value is used instead.

In this way, you can generate values of non-string types: arrays, numbers, booleans, `null`, and/or nesting entries inside an object without a folder-of-files.

This special built-in handling applies **only** to JSON files. In the example above, the `.html`/`.md`/`.js` files simply have their extensions stripped and generate plain string values as in the general rules. [TODO: enable plugins to extend this]

### Special case: _data files

[TODO: explain field merging]

### Special case: _attachments folder

[TODO: decide, explain binary fields]


### Special case: _docs folder

[TODO: explain nested documents]


## See also

[TODO: explain couchapp/etc. heritage]


## ISC License

Copyright © 2017–2019 Nathan Vander Wilt

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
