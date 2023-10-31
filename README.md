# bundlechecker

Bundlecheker that built with rust and using napi.rs for node binding

## Usage
```javascript
const { checkBundlerSync } = require("@adityals/bundlechecker");

try {
  const { result, summary } = checkBundlerSync({
    configPath: "./package.json",
    compression: "brotli",
    silent: false,
  });
} catch (err) {
  console.error(err);
}
```

### Config Example
``` json
{
  "name": "my_package",
  "bundlesize": [
    {
      "path": "../index.js",
      "maxSize": "50 kB"
    },
    {
      "path": "../notfound*.js",
      "maxSize": "10 kB"
    }
  ]
}
```
The important thing is provide the `bundlesize` key, you can attach to `package.json` or any JSON file.


### Options
| name | description | required | default |
| --- | --- | --- | --- |
| configPath | Where to look config file | true | null |
| compression | Compression method | true | NoCompression |
| silent | Wether to write to stdout or not | false | false |


### Result
If `checkBundlerSync` is succeed, it'll returns an object with 2 key `result` and `summary`

```javascript
{
  result: {
    'index.js': {
      pass: true,
      actualFileSize: 0.93359375,
      sizeUnit: 'kB',
      compression: 'Brotli',
      budgetSize: 50
    },
    '../notfound*.js': {
      pass: false,
      actualFileSize: 0,
      sizeUnit: '',
      compression: '',
      budgetSize: 0,
      error: 'pattern ../notfound*.js is not getting any match'
    }
  },
  summary: { total: 2, success: 1, fail: 0, error: 1 }
}
```

> I'm new to rust and hopefully this project will help me learn more.

