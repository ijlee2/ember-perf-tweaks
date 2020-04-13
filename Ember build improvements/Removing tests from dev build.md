# Removing tests from dev build

When you run
```
ember build
```

or

```
ember serve
```
the build runs on `development` environment by default.

Internally, ember-cli adds the test files to your development build so that you can access them using `http://localhost:4200/tests`. But in general, we run
```
ember test
```
to validate test cases.

If you want to prevent test files from being included in the dev build and slowing things down, you can use the following configuration:

```javascript
// ember-cli-build.js
let app = new EmberApp(defaults, {
  tests: false,
  ...
});
```
