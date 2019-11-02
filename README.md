# @typeonly/checker

[![Build Status](https://travis-ci.com/tomko-team/typeonly-checker.svg?branch=master)](https://travis-ci.com/tomko-team/typeonly-checker)
[![Dependencies Status](https://david-dm.org/tomko-team/typeonly-checker/status.svg)](https://david-dm.org/tomko-team/typeonly-checker)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/3728d0b89a8f456391e980c46967003f)](https://www.codacy.com/manual/paleo/typeonly-checker?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=tomko-team/typeonly-checker&amp;utm_campaign=Badge_Grade)
[![npm](https://img.shields.io/npm/dm/@typeonly/checker)](https://www.npmjs.com/package/@typeonly/checker)
![Type definitions](https://img.shields.io/npm/types/@typeonly/checker)
![GitHub](https://img.shields.io/github/license/tomko-team/typeonly-checker)

[TypeOnly](https://github.com/tomko-team/typeonly) aims to be the pure typing part of TypeScript. This package provides an API to validate JSON and JavaScript objects with TypeScript definitions, using the TypeOnly parser.

## Tutorial: How to programmatically validate JSON data

At first, it is necessary to follow [the tutorial](https://github.com/tomko-team/typeonly/blob/master/README.md#tutorial-parse-typescript-definitions-with-the-cli) of TypeOnly in order to generate RTO files (with the `.rto.json` extension) from TypeScript definitions. After this step, the RTO files are in a `dist-rto/` directory.

Now, add `@typeonly/checker` to the project:

```sh
npm install @typeonly/checker
```

Create a file `src/check-main.js` with the following content:

```ts
// src/check-main.js
const { createChecker } = require("@typeonly/checker")

const data = {
  "color": "green",
  "shape": {
    "kind": "circle",
    "x": 100,
    "y": 100,
    "radius": 50
  }
}

async function main() {
  const checker = await createChecker({
    readModules: {
      modulePaths: ["./drawing"],
      baseDir: `${__dirname}/../dist-rto`
    }
  })
  const result = checker.check("./drawing", "Drawing", data)
  console.log(result)
}

main().catch(console.error)
```

This code validates the `data` object using RTO files generated by the TypeOnly parser.

Execute it:

```sh
$ node src/check-main.js
{ valid: true }
```

## Contribute

With VS Code, our recommanded plugin is:

- **TSLint** from Microsoft (`ms-vscode.vscode-typescript-tslint-plugin`)
