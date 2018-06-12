# Jasmine-Html



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
            'jasmine',
            'jasmine-es6'
        ],
    });
}
```

## Advanced options

You can provide some tweaking to the function:

```lang=javascript
describe('in option mode', function() {
    withHtml({
        title: 'test with title',
        html: '<test-element></test-element>',
        setupTime: 1,
        beforeEach: false
    }, function(element) {
        it('should work', function() {
            expect(element().tagName).toBe('TEST-ELEMENT');
            expect(element().incr).toEqual(jasmine.any(Function));
        });
    });
});
```

The options are:

|Name|Default value | Explanation |
|----|:------------:|-------------|
|title| -empty- | Title for display, and for the internal (hidden) describe (see below technical details) |
|setupTime| 1 (ms) | Time to wait for the object to being setup, if necessary|
|assertElementIsNotNull | false | Add some internal test to assert the elements are not null |
|beforeEach | true | Create and destroy the object before/after each test instead of keeping is through the test|

## Technically

withHtml() wrap around a 'describe' call. So you can rewrite this calls:

```lang=javascript
withHtml('test', function(elements) {
    it('does some test');
});
```

Is nearly equivalent to

```lang=javascript
describe(options.title, function() {
    beforeAll( <initialize the element>);
    afterAll( <remove the element>);

    it('does some test');
});
```

If you specify "beforeEach", you need to replace the above example with:

```lang=javascript
describe(options.title, function() {
    beforeEach( <initialize the element>);
    afterEach( <remove the element>);

    it('does some test');
});
```

## BeforeAll?

You can choose to have your component instantiated only once for you whole test suite. To make that, disable "options.beforeEach". But the order in which the "it()" commands are run are reported to be sometimes random. To disable randomness in your tests, add this in your karma.conf.js:

```lang=javascript
	config.set({
		client: {
			jasmine: {
				random: false
			}
		},
```

## How to contribute?
