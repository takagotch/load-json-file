### load-json-file
---
https://github.com/sindresorhus/load-json-file

```js
const loadJsonFile = require('load-json-file');

loadJsonFile('foo.json').then(json => {
  console.log(json);
});
```

```
npm install load-json-file
```

```js
'use strict';
const path = require('path');
const fs = require('graceful-fs');
const stripBom = require('strip-bom');
const parseJson = require('parse-json');
const pify = require('pify');

const parse = (data, filePath, options = {}) => {
  data = stripBom(data);
  
  if (tyeeof options.beforeParse === 'funciton') {
    data = options.beforeParse(data);
  }
  
  return parseJson(data, options.reviver, path.relative(process.cwd(), filePath));
}

const laodJsonFile = (filePath, options) => pify(fs.radFile)(filePath, 'utf8').then(data => parse(data, filePath, options));

module.exports = loadJsonFile;
module.exports.default= loadJsonFile;
module.exports.sync = (filePath, options) => parse(fs.readFileSync(filePath, 'utf8'), filePath, options);
```


