# api documentation for  [reactify (v1.1.1)](https://github.com/andreypopp/reactify)  [![npm package](https://img.shields.io/npm/v/npmdoc-reactify.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-reactify) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-reactify.svg)](https://travis-ci.org/npmdoc/node-npmdoc-reactify)
#### Browserify transform for JSX (a superset of JS used by React.js)

[![NPM](https://nodei.co/npm/reactify.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/reactify)

[![apidoc](https://npmdoc.github.io/node-npmdoc-reactify/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-reactify/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-reactify/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-reactify/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Andrey Popp",
        "url": "http://andreypopp.com"
    },
    "bugs": {
        "url": "https://github.com/andreypopp/reactify/issues"
    },
    "dependencies": {
        "react-tools": "~0.13.0",
        "through": "~2.3.4"
    },
    "description": "Browserify transform for JSX (a superset of JS used by React.js)",
    "devDependencies": {
        "browserify": "4.x.x",
        "coffeeify": "~0.x.x",
        "concat-stream": "~1.4.8",
        "es6-module-jstransform": "^0.1.3",
        "jshint": "^2.5.10",
        "mocha": "~1.9.0",
        "semver": "~1.1.4"
    },
    "directories": {},
    "dist": {
        "shasum": "a8f119596273c0d4bfb1abea0c14c2601ea03bba",
        "tarball": "https://registry.npmjs.org/reactify/-/reactify-1.1.1.tgz"
    },
    "gitHead": "9708efc75e5c7f2dd3950e7debcd7cd3f73b6a00",
    "homepage": "https://github.com/andreypopp/reactify",
    "keywords": [
        "react",
        "browserify",
        "browserify-transform",
        "jsx",
        "js",
        "plugin",
        "transform"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "andreypopp"
        },
        {
            "name": "petehunt"
        }
    ],
    "name": "reactify",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/andreypopp/reactify.git"
    },
    "scripts": {},
    "version": "1.1.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module reactify](#apidoc.module.reactify)
1.  [function <span class="apidocSignatureSpan"></span>reactify (filename, options)](#apidoc.element.reactify.reactify)
1.  [function <span class="apidocSignatureSpan">reactify.</span>toString ()](#apidoc.element.reactify.toString)



# <a name="apidoc.module.reactify"></a>[module reactify](#apidoc.module.reactify)

#### <a name="apidoc.element.reactify.reactify"></a>[function <span class="apidocSignatureSpan"></span>reactify (filename, options)](#apidoc.element.reactify.reactify)
- description and source-code
```javascript
function reactify(filename, options) {
  options = options || {};

  var buf = [];

  function write(chunk) {
    if (!Buffer.isBuffer(chunk)) {
      chunk = new Buffer(chunk)
    }
    return buf.push(chunk)
  }

  function compile() {
    var source = Buffer.concat(buf).toString();
    // jshint -W040
    if (isJSXFile(filename, options)) {
      try {
        var output = ReactTools.transform(source, {
          es5: options.target === 'es5',
          sourceMap: true,
          sourceFilename: filename,
          stripTypes: options['strip-types'] || options.stripTypes,
          harmony: options.harmony || options.es6
        });
        this.queue(output);
      } catch (error) {
        error.name = 'ReactifyError';
        error.message = filename + ': ' + error.message;
        error.fileName = filename;
        this.emit('error', error);
      }
    } else {
      this.queue(source);
    }
    return this.queue(null);
    // jshint +W040
  }

  return through(write, compile);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.reactify.toString"></a>[function <span class="apidocSignatureSpan">reactify.</span>toString ()](#apidoc.element.reactify.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
...
  if (!Buffer.isBuffer(chunk)) {
    chunk = new Buffer(chunk)
  }
  return buf.push(chunk)
}

function compile() {
  var source = Buffer.concat(buf).toString();
  // jshint -W040
  if (isJSXFile(filename, options)) {
    try {
      var output = ReactTools.transform(source, {
        es5: options.target === 'es5',
        sourceMap: true,
        sourceFilename: filename,
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
