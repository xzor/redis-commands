# Redis Commands (with module support)

[![Build Status](https://travis-ci.org/NodeRedis/redis-commands.png?branch=master)](https://travis-ci.org/NodeRedis/redis-commands)
[![Code Climate](https://codeclimate.com/github/NodeRedis/redis-commands/badges/gpa.svg)](https://codeclimate.com/github/NodeRedis/redis-commands)
[![Test Coverage](https://codeclimate.com/github/NodeRedis/redis-commands/badges/coverage.svg)](https://codeclimate.com/github/NodeRedis/redis-commands/coverage)

This module exports all the commands that Redis supports.

## Install

```shell
$ npm install redis-commands
```

## Usage with module (in this case RediSearch module)

1. You need at least the BETA version of redis `4.0-rc2`
2. Start redis with `redis-server --loadmodule /path/to/module.so`
3. CLI redis and dump avaliable commands with `COMMAND`
4. add to `commands.json`

```javascript
//example usage in redis.io
redis.pipeline([
    ['flushall'],
    ['ft.create', 'products', 'name', 10.0, 'description', 1.0, 'price', 'NUMERIC'],
    ['ft.add',  'products',  'skor', 1.0, 'FIELDS', 'name', 'Acme 40-Inch 1080p LED TV', 'description',  'Enjoy enhanced color and clarity with stunning Full HD 1080p', 'price', 277.99],
]).exec(function(err, res) { 
    // null if success
});
```

## Usage

```javascript
var commands = require('redis-commands');
```

`.list` is an array contains all the lowercased commands:

```javascript
commands.list.forEach(function (command) {
  console.log(command);
});
```

`.exists()` is used to check if the command exists:

```javascript
commands.exists('set') // true
commands.exists('other-command') // false
```

`.hasFlag()` is used to check if the command has the flag:

```javascript
commands.hasFlag('set', 'readonly') // false
```

`.getKeyIndexes()` is used to get the indexes of keys in the command arguments:

```javascript
commands.getKeyIndexes('set', ['key', 'value']) // [0]
commands.getKeyIndexes('mget', ['key1', 'key2']) // [0, 1]
```

## Acknowledgment

Thank [@Yuan Chuan](https://github.com/yuanchuan) for the package name. The original redis-commands is renamed to [@yuanchuan/redis-commands](https://www.npmjs.com/package/@yuanchuan/redis-commands).
