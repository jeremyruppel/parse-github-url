# parse-github-url [![NPM version](https://img.shields.io/npm/v/parse-github-url.svg)](https://www.npmjs.com/package/parse-github-url) [![Build Status](https://img.shields.io/travis/jonschlinkert/parse-github-url.svg)](https://travis-ci.org/jonschlinkert/parse-github-url)

> Parse a github URL into an object.

**HEADS UP! Breaking changes in 0.3.0!!!**

See the [release history](#history) for details.

**Why another GitHub URL parser library?**

Seems like every lib I've found does too much, like both stringifying and parsing, or converts the URL from one format to another, only returns certain segments of the URL except for what I need, yields inconsistent results or has poor coverage.

## TOC

- [Usage](#usage)
- [Example results](#example-results)
- [Related projects](#related-projects)
- [History](#history)
- [Running tests](#running-tests)
- [Contributing](#contributing)
- [Author](#author)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Usage

```js
var gh = require('parse-github-url');
gh('https://github.com/jonschlinkert/micromatch');
```

Results in:

```js
{
  "owner": "jonschlinkert",
  "name": "micromatch",
  "repo": "jonschlinkert/micromatch",
  "branch": "master"
}
```

## Example results

Generated results from test fixtures:

```js
// assemble/verb#1.2.3
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "1.2.3"
}

// assemble/verb#branch
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "branch"
}

// assemble/verb
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git+https://github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git+ssh://github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git://gh.pages.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git://github.assemble.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git://github.assemble.two.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git://github.com/assemble/verb
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git://github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git@gh.pages.com:assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// git@github.com:assemble/verb.git#1.2.3
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "1.2.3"
}

// git@github.com:assemble/verb.git#v1.2.3
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "v1.2.3"
}

// git@github.com:assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// github:assemble/verb
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// http://github.com/assemble
{
  "owner": "assemble",
  "name": null,
  "repo": null,
  "branch": "master"
}

// http://github.com/assemble/verb
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// http://github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// http://github.com/assemble/verb/tree
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// http://github.com/assemble/verb/tree/master
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// http://github.com/assemble/verb/tree/master/foo/bar
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master/foo/bar"
}

// https://assemble.github.com/assemble/verb/somefile.tar.gz
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://assemble.github.com/assemble/verb/somefile.zip
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://assemble@github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://gh.pages.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/assemble/verb
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/assemble/verb.git
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/assemble/verb/blob/1.2.3/README.md
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "1.2.3"
}

// https://github.com/assemble/verb/blob/249b21a86400b38969cee3d5df6d2edf8813c137/README.md
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/assemble/verb/blob/master/assemble/index.js
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/assemble/verb/tree/1.2.3
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "1.2.3"
}

// https://github.com/assemble/verb/tree/feature/1.2.3
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "feature/1.2.3"
}

// https://github.com/repos/assemble/verb/tarball
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}

// https://github.com/repos/assemble/verb/zipball
{
  "owner": "assemble",
  "name": "verb",
  "repo": "assemble/verb",
  "branch": "master"
}
```

## Related projects

* [github-short-url-regex](https://www.npmjs.com/package/github-short-url-regex): Regular expression (Regex) for matching github shorthand (user/repo#branch). | [homepage](https://github.com/regexps/github-short-url-regex)
* [is-git-url](https://www.npmjs.com/package/is-git-url): Regex to validate that a URL is a git url. | [homepage](https://github.com/jonschlinkert/is-git-url)
* [parse-github-short-url](https://www.npmjs.com/package/parse-github-short-url): Parse a string (github shorthand url) into an object with `user`, `repo`, `branch` using the… [more](https://www.npmjs.com/package/parse-github-short-url) | [homepage](https://github.com/tunnckoCore/parse-github-short-url)

## History

**v0.3.0**

To be more consistent with node.js/package.json conventions, the following properties were renamed in `v0.3.0`:

* `repo` is now `name` (project name)
* `repopath` is now `repository` (project repository)
* `user` is now `owner` (project owner or org)

## Running tests

Install dev dependencies:

```sh
$ npm i -d && npm test
```

## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/jonschlinkert/parse-github-url/issues/new).

## Author

**Jon Schlinkert**

* [github/jonschlinkert](https://github.com/jonschlinkert)
* [twitter/jonschlinkert](http://twitter.com/jonschlinkert)

## License

Copyright © 2016 [Jon Schlinkert](https://github.com/jonschlinkert)
Released under the MIT license.

***

_This file was generated by [verb](https://github.com/verbose/verb) on January 17, 2016._