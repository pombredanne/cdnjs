<a href="http://travis-ci.org/cdnjs/cdnjs"><img src="https://secure.travis-ci.org/cdnjs/cdnjs.png" alt="Build Status" style="max-width:100%;"></a>

# cdnJS Script Repository

The repository mirroring all scripts on cdnjs.cloudflare.com, created and maintained by [Thomas Davis](https://twitter.com/neutralthoughts), [Ryan Kirkman](https://twitter.com/ryan_kirkman) and [Lachlan Collins](http://plus.google.com/116251728973496544370?prsrc=3)

We will host any version of any library. Feel free to add a pull request for an older version of a library if your site still uses it.

__Libraries must have notable popularity. 100 stars on GitHub is a good example, but as long as reasonably popularity can be demonstrated the library will be added.__
## Extensions, Plugins, Resources

[Extensions, Plugins, Resources](https://github.com/cdnjs/cdnjs/wiki/Extensions%2C-Plugins%2C-Resources)

## Conventions

* Filenames should **not** include version number and be **lowercase**
* Javascript & Css files should be minified, If the library doesn't already provide a minified version, our preferred minifier is [UglifyJS](http://marijnhaverbeke.nl/uglifyjs "UglifyJS")
* If updating an existing library, try to keep consistent with the existing structure

## Pull requests steps

1. Fork this repository
  * Install all the needed dependencies locally (you will need `node`): `npm install`
2. Add your library (following the conventions of this repository)
  * 1 commit per pull request
  * 1 library per pull request
  * The files in the pull request must correspond to a tag in the original repository (some exceptions apply)
  * include a package.json in the npm format (see `test/schemata/npm-package.json` for details - it's very simple)
  * Run `npm test` to check everything is ok
3. Send us a pull request.
  * If you are the author of the library, add `[author]` to the pull request title
  * Make sure you include in the pull description:
      1. Where you downloaded the script
      2. If it isn't clear, how you found the version of the script
  * e.g. https://github.com/cdnjs/cdnjs/pull/541
4. If the library doesn't already provide a minified version, our preferred minifier is [UglifyJS](http://marijnhaverbeke.nl/uglifyjs "UglifyJS")

## Enabling NPM auto update

We automatically update libraries that are also hosted on NPM e.g. Lodash.

This script runs automatically every 4 hours

1. Update the package.json and configure it as below and submit a pull request.

```
 // Lodash package.json
 // ...
  "npmName": "lodash",
  "npmFileMap": [{
    "basePath": "/dist/",
    "files": [
      "*"
    ]
  }],
  // ...
```

`npmName` should map to the name of the library on NPM
`npmFileMap` is a white list of files to take from the NPM tarball and host on the cdn
`basePath` will be ignored when copying over to the cdn
`files` is a pattern matcher that you can select many files with

The above example looks in the tarball whose structure might look like

```
- dist/lodash.js
- dist/lodash.min.js
- README
```

It then will look for `dist/*` which will find the two files inside the dist folder. It will now copy it over to cdnjs but without the `dist` path. Such that they will end up. `ajax/libs/lodash.js/2.0/lodash.js`

## Running the validator
1. Install all the needed dependencies locally (you will need `node`): `npm install`
2. Run the test suite: `npm test`
