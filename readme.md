# karma-jasmine-es6

The system here is a *hack* while waiting for karma to deliver a fix. A PR is currently under work here: [karma#2834](https://github.com/karma-runner/karma/pull/2834).

## Installation

This library has no runtime depandancies. But if you need to test web components, you probably will need the polyfills.

Install it

```lang=bash
npm install -D karma-jasmine-es6
```

## Usage in Karma

Add it as a "framework" in karma.conf.js:

```lang=javascript
module.exports = function(config) {
    config.set({
        frameworks : [
            'jasmine-es6',
            'jasmine'
        ],
    });
}
```

!! jasmine-es6 must come before 'jasmine', since jasmine-es6 will hook into window.__karma__.start and delay it the necessary time.

## Limits

This does not cover the case where the module is not loaded correctly. No message is logged by the plugin in that case, look at the console.
