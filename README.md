# Abigail [![NPM version][npm-image]][npm] [![Build Status][travis-image]][travis] [![Coverage Status][coveralls-image]][coveralls]

<!--![abigail][.svg] -->

> Minimal task runner.

## Installation
```bash
npm install abigail --global
```

## Usage
```bash
abigail glob:script glob:script ...
```
__[Can re-use your npm script.][1]__

### `-e` `--execute`
Execute script after ready.
### `-i` `--ignore`
Using `~/.gitignore`&`./.gitignore`, Exclude from the glob.

## Example

### Upon detecting a change at `lib/**/*.js`
to Execute `npm run test`.

```bash
abigail lib/**/*.js:test
#  +79 ms @ @ Using ./package.json
#  +83 ms @ @ Start watching lib/**/*.js for npm run test
#   +2sec @ @ File lib/hoge.js has been changed.
# ...
#   +6sec @ @ Finish npm run test Exit code 0.
```

./package.json
```json
{
  "scripts":{
    "test":"mocha"
  },
  "devDependencies": {
    "mocha": "^2.2.1"
  }
}
```

### Execute script, and then watching.
```bash
abigail lib/**/*.coffee:compile -e
#  +79 ms @ @ Using ./package.json
#  +83 ms @ @ Start watching lib/**/*.coffee for npm run compile
#   +0 ms @ @ Execute npm run compile
# ...
#  +331ms @ @ Finish npm run compile Exit code 0.
```

./package.json
```json
{
  "scripts":{
    "compile":"coffee -o src -c lib"
  },
  "devDependencies": {
    "coffee-script": "^1.8.0"
  }
}
```

### Can use raw script
```bash
abigail *.html:'chrome-cli reload'
#  +89 ms @ @ Using ./package.json
# +107 ms @ @ Start watching *.html for chrome-cli reload
#   +1sec @ @ File README.html has been changed.
#   +0 ms @ @ Execute chrome-cli reload
#  +87 ms @ @ Finished chrome-cli reload, Exit code 0.
```

Use [chrome-cli][2], Like a LiveReload.

## TODO
* TEST

License
=========================
MIT by 59naga

[.svg]: https://cdn.rawgit.com/59naga/abigail/master/.svg?

[npm-image]: https://badge.fury.io/js/abigail.svg
[npm]: https://npmjs.org/package/abigail
[travis-image]: https://travis-ci.org/59naga/abigail.svg?branch=master
[travis]: https://travis-ci.org/59naga/abigail
[coveralls-image]: https://coveralls.io/repos/59naga/abigail/badge.svg?branch=master
[coveralls]: https://coveralls.io/r/59naga/abigail?branch=master

[1]: http://lostechies.com/derickbailey/2012/04/24/executing-a-project-specific-nodenpm-package-a-la-bundle-exec/
[2]: https://github.com/prasmussen/chrome-cli