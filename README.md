# DeAMD

A Gulp stream transforming a UMD-style script to the one without AMD detection

## Objective

A UMD-style JavaScript file (for example, a bundle script generated by browserify with standalone option)
works universally in CommonJS environment, in AMD-loaders like RequireJS, or as a standalone script.

As UMD script has AMD detection feature in it, it is troublesome if you want to use the script as a standalone where RequireJS is already loaded.

This transformer removes the AMD detection feature by wrapping the script with a closure and overriding `define` or `require` functions from RequireJS.

## Usage

```javascript
var gulp = require('gulp');
var browserify = require('browserify');
var deamd = require('deamd');

gulp.task('build', function() {
  browserify({
    entries: [ "./src/main.js" ],
    standalone: 'MyPackage'
  })
  .bundle()
  .pipe(source('main-bundle.js'))
  .pipe(deamd())
  .pipe(gulp.dest('./build/'));
});
```
