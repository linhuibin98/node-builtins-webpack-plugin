# node-builtins-webpack-plugin

Polyfill Node.js core modules in Webpack.

This module is only needed for [Webpack 5+](https://github.com/webpack/changelog-v5#automatic-nodejs-polyfills-removed).

## Install

```sh
npm install node-builtins-webpack-plugin
```

## Usage

Add the following to your `webpack.config.js`:

```js
const NodeBuiltinsPlugin = require('node-builtins-webpack-plugin');

module.exports = {
	// Other rules...
	plugins: [
		new NodeBuiltinsPlugin(),
	],
};
```

`console`, `process`, and most deprecated/internal Node.js core modules are not polyfilled by default. If you still need to polyfill them, you can use the `additionalAliases` option:

```js
const NodeBuiltinsPlugin = require('node-builtins-webpack-plugin');

module.exports = {
	// Other rules...
	plugins: [
		new NodeBuiltinsPlugin({
			additionalAliases: ['process', 'punycode'],
		}),
	],
};
```

The `fs` module resolves to nothing because its functionality cannot replicated in the browser.

## API

### new NodeBuiltinsPlugin(options?)

#### options

Type: `object`

`onlyAliases` is mutually exclusive with `excludeAliases` and `additionalAliases`.

#### excludeAliases

If you don't want a module to be polyfilled, you can specify aliases to be skipped here.

```js
const NodeBuiltinsPlugin = require('node-builtins-webpack-plugin');

module.exports = {
	// Other rules...
	plugins: [
		new NodeBuiltinsPlugin({
			excludeAliases: ['console'],
		}),
	],
};
```

#### additionalAliases

Alternatively, you can choose to add certain aliases to the list of polyfilled modules. For example, you can choose to polyfill `console`.

```js
const NodeBuiltinsPlugin = require('node-builtins-webpack-plugin');

module.exports = {
	// Other rules...
	plugins: [
		new NodeBuiltinsPlugin({
			additionalAliases: ['console'],
		}),
	],
};
```

#### onlyAliases

You can also choose to only include certain aliases, ignoring the defaults. For example, you can have only `console` polyfilled.

```js
const NodeBuiltinsPlugin = require('node-builtins-webpack-plugin');

module.exports = {
	// Other rules...
	plugins: [
		new NodeBuiltinsPlugin({
			onlyAliases: ['console'],
		}),
	],
};
```

## Aliases

### Globals

- `Buffer`
- `console`
- `process`

### Modules

- `assert`
- `buffer`
- `console`
- `constants`
- `crypto`
- `domain`
- `events`
- `http`
- `https`
- `os`
- `path`
- `punycode`
- `process`
- `querystring`
- `stream`
- `_stream_duplex`
- `_stream_passthrough`
- `_stream_readable`
- `_stream_transform`
- `_stream_writable`
- `string_decoder`
- `sys`
- `timers`
- `tty`
- `url`
- `util`
- `vm`
- `zlib`
