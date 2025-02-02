---
title: writing-files-with-nodejs
displayTitle: 'Writing files with Node.js'
description: 'How to write files using Node.js'
authors: flaviocopes, MylesBorins, fhemberger, LaRuaNa, ahmadawais, clean99, ovflowd, vaishnav-mk
category: learn
---

## Wiriting a file

The easiest way to write to files in Node.js is to use the `fs.writeFile()` API.

```js
const fs = require('fs');

const content = 'Some content!';

fs.writeFile('/Users/joe/test.txt', content, err => {
  if (err) {
    console.error(err);
  }
  // file written successfully
});
```

### Writing a file synchronously

Alternatively, you can use the synchronous version `fs.writeFileSync()`:

```js
const fs = require('fs');

const content = 'Some content!';

try {
  fs.writeFileSync('/Users/joe/test.txt', content);
  // file written successfully
} catch (err) {
  console.error(err);
}
```

You can also use the promise-based `fsPromises.writeFile()` method offered by the `fs/promises` module:

```js
const fs = require('fs/promises');

async function example() {
  try {
    const content = 'Some content!';
    await fs.writeFile('/Users/joe/test.txt', content);
  } catch (err) {
    console.log(err);
  }
}
example();
```

By default, this API will **replace the contents of the file** if it does already exist.

**You can modify the default by specifying a flag:**

```js
fs.writeFile('/Users/joe/test.txt', content, { flag: 'a+' }, err => {});
```

#### The flags you'll likely use are

<table>
  <tr>
    <th>Flag</th>
    <th>Description</th>
    <th>File gets created if it doesn't exist</th>
  </tr>
  <tr>
    <td><code>r+</code></td>
    <td>This flag opens the file for <b>reading</b> and <b>writing</b></td>
    <td style="text-align: center;">❌</td>
  </tr>
  <tr>
    <td><code>w+</code></td>
    <td>This flag opens the file for <b>reading</b> and <b>writing</b> and it also positions the stream at the <b>beginning</b> of the file</td>
    <td style="text-align: center;">✅</td>
  </tr>
  <tr>
    <td><code>a</code></td>
    <td>This flag opens the file for <b>writing</b> and it also positions the stream at the <b>end</b> of the file</td>
    <td style="text-align: center;">✅</td>
  </tr>
  <tr>
    <td><code>a+</code></td>
    <td>This flag opens the file for <b>reading</b> and <b>writing</b> and it also positions the stream at the <b>end</b> of the file</td>
    <td style="text-align: center;">✅</td>
  </tr>
</table>

* You can find more information about the flags in the [fs documentation](/api/fs/#file-system-flags).

## Appending content to a file

Appending to files is handy when you don't want to overwrite a filewith new content, but rather add to it.

### Examples

A handy method to append content to the end of a file is `fs.appendFile()` (and its `fs.appendFileSync()` counterpart):

```js
const fs = require('fs');

const content = 'Some content!';

fs.appendFile('file.log', content, err => {
  if (err) {
    console.error(err);
  }
  // done!
});
```

#### Example with Promises

Here is a `fsPromises.appendFile()` example:

```js
const fs = require('fs/promises');

async function example() {
  try {
    const content = 'Some content!';
    await fs.appendFile('/Users/joe/test.txt', content);
  } catch (err) {
    console.log(err);
  }
}
example();
```
