## Table of contents

* [Introduction](#introduction)
* [Find tests](#find-tests)
* [Isolate tests](#isolate-tests)
* [Verbose mode](#verbose-mode)
* [Find stack elements](#find-stack-elements)

## Introduction

Debugging frontend tests can be difficult because the stack traces are much less helpful than in the backend. There are two reasons for this:

* Because so much of our frontend code is asynchronous, the stack trace will often just point to code that executes a queue of jobs when you usually want to know what code submitted the job.
* Jasmine, our testing framework, does not support showing accurate line numbers in stack traces. We looked into fixing this in [#9648](https://github.com/oppia/oppia/issues/9648) but abandoned the idea once it was clear that Jasmine lacked the functionality we needed.

Here's an example frontend test stack trace:

```text
Chrome Headless 83.0.4103.116 (Mac OS 10.15.5) Assets Backend API Service on dev mode should handle rejection when fetching a file fails FAILED
	Error: Automatic conversion to Blob is not supported for response type.
	    at _toBlob (core/templates/combined-tests.spec.js:92825:11)
	    at _maybeConvertBody (core/templates/combined-tests.spec.js:92870:20)
	    at TestRequest../node_modules/@angular/common/fesm5/http/testing.js.TestRequest.flush (core/templates/combined-tests.spec.js:92745:16)
	    at UserContext.<anonymous> (core/templates/combined-tests.spec.js:61955:17)
	    at ZoneDelegate../node_modules/zone.js/dist/zone.js.ZoneDelegate.invoke (core/templates/pages/about-page/about-page.module.js:237519:30)
	    at ProxyZoneSpec../node_modules/zone.js/dist/proxy.js.ProxyZoneSpec.onInvoke (core/templates/combined-tests.spec.js:427781:43)
	    at ZoneDelegate../node_modules/zone.js/dist/zone.js.ZoneDelegate.invoke (core/templates/pages/about-page/about-page.module.js:237518:36)
	    at Zone../node_modules/zone.js/dist/zone.js.Zone.run (core/templates/pages/about-page/about-page.module.js:237276:47)
	    at runInTestZone (core/templates/combined-tests.spec.js:427336:38)
	    at UserContext.<anonymous> (core/templates/combined-tests.spec.js:427351:24)
Chrome Headless 83.0.4103.116 (Mac OS 10.15.5): Executed 1 of 2277 (1 FAILED) (0 secs / 0.046 secs)
```

The `zone.js` stack elements relate to the [zone.js](https://github.com/angular/angular/tree/master/packages/zone.js) package that is handling our asynchronous operations. Notice that the line numbers are unreasonably large. This is because to run our tests, we load all our testing code and dependencies into `combined-tests.spec.js`. The line numbers refer to the resulting "mega-file," which doesn't actually exist on the file system.

Below, we'll discuss some strategies you can use to overcome these difficulties.

## Find tests

You can use test names to find test code files, but you can't just search for the whole name. You have to understand how test names are constructed. For example, here's the kind of test structure that produced the test name "Assets Backend API Service on dev mode should handle rejection when fetching a file fail" above:

```js
describe('Assets Backend API Service', () => {
  describe('on dev mode', () => }
    it('should handle rejection when fetching a file fails', () => {
      ...
    });
  });
});
```

The strings from the `describe` and `it` functions get concatenated with space (` `) delimiters to create the test name. The name of the `it` block usually starts with `should`, so we recommend searching the codebase for the portion of the test name from `should` to the end (e.g. "should handle rejection when fetching a file fails" in this case).

## Isolate tests

Once you have identified which test is failing, you often want to run that test in isolation next. This will let you get results quickly as you try other debugging strategies. Thankfully, you just have to change the `it()` of your test to `fit()`. You can even do this multiple times to mark multiple tests for running. Then when you run the frontend tests, only those tests with `fit()` will run. Note that `fdescribe()` works the same way.

**Remember to revert your `fit()` and `fdescribe()` changes before committing!**

## Verbose mode

By default, we suppress log output from the tests to the terminal when running the frontend tests. This keeps the test output clean so it's easy to find which tests failed. However, this output can be useful for debugging. For example, if you add `console.log()` or `console.error()` statements to your tests for debugging, the output from those statements will be suppressed by default. To view this output, pass `--verbose` when you run the frontend tests:

```console
python -m scripts.run_frontend_tests --verbose
```

**Only use --verbose when you are running a few tests in isolation. Otherwise, you will be swamped with way too many log messages.**

## Find stack elements

While you can't use the line numbers in a stack trace to find the associated code, you can sometimes use the function or class names. For example, in the example above we could try searching the codebase for `_maybeConvertBody`. The success of this technique depends on how frequently the string you search for occurs in the codebase. If the string occurs a lot, you will have a hard time figuring out which occurrence is the one you are interested in.
