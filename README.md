# Typescript lib starter

[![Build Status](https://travis-ci.org/Hotell/typescript-lib-starter.svg?branch=master)](https://travis-ci.org/Hotell/typescript-lib-starter)
[![Standard Version](https://img.shields.io/badge/release-standard%20version-brightgreen.svg)](https://github.com/conventional-changelog/standard-version)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)


This npm library starter:

- creates package for both Node and Browser
- build creates 3 standard "bundle" formats:
  - main -> UMD bundle for Node and Browser
  - module -> transpiled files to ES5 + es2015 modules for tree shaking
  - es2015 -> raw files transpiled to latest ES standard ( es2017 ) ( this is useful if you wann transpile everthing or just wann ship untranspiled esNext code for evergreen browsers)
- type definitions are automatically generated and shipped with your package

## Start coding jedi!

`git clone https://github.com/Hotell/typescript-lib-starter <your-libary-folder-name>`

`cd <your-libary-folder-name>`

`rm -rf .git && git init`

Open `package.json` and reset following fields:
- name
- version ( It is recommended to start from 1.0.0 )
- description
- main ( "umd/typescript-lib-starter.js" => "umd/{name}.js" )
- repository.url
- author
- license ( use whatever you want )

Now install all dependencies

`yarn install`

Happy coding !

## Consumption of published library:

`yarn add my-new-library` or `npm install my-new-library`

### Webpack

```ts
// main.ts
import { Greeter } from 'my-new-library';

const mountPoint = document.getElementById('app');
const App = () => {
  const greeter = new Greeter('Stranger');
  return `<h1>${greeter.greet()}</h1>`
}
const render = (Root: Function, where: HTMLElement) => {
  where.innerHTML = Root();
}

render(App, mountPoint);
```

```html
<html>
  <head>
    <script src="bundle.js" async></script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

### UMD ( no bundler )

```html
<html>
  <head>
    <script src="node_modules/my-lib/umd/my-new-library.min.js"></script>
    <script async>
        var Greeter = MyLib.Greeter;

        var App = function() {
          var greeter = new Greeter('Stranger');
          return '<h1>'+greeter.greet()+'</h1>'
        }
        var render = function(Root, where) {
          where.innerHTML = Root();
        }

        render(App, mountPoint);
    </script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

## Publishing/Release

> NOTE: you have to create npm account and register token on your machine
> -> `npm adduser`
>
> If you are using scope don't forget to [`--scope`](https://docs.npmjs.com/cli/adduser#scope)

`yarn release`

which will do following:
- bump version and tag
- updates/creates CHANGELOG.md
- pushes to github master branch
- publishes build package to npm


### Initial Release (without bumping package.json version):

`yarn release -- --first-release`

## Check what files gonna be published to npm

- CLI output via `yarn release:preflight`
- or `yarn release:preflight:package` will create tarball which you can check

## Check size of your published NPM bundle

run `yarn build` then `npm run size`

## Format and fix lint errors

`yarn ts:style:fix`

## Generate documentation

`yarn docs`

## Commit ( via commitizen )

- this is preffered way how to create convetional-changelog valid commits
- if you preffer your custom tool we provide a commit hook linter which will error out, it you provide invalid commit message
- if you are in rush and just wanna skip commit message valiation just prefix your message with `WIP: something done` ( if you do this please squash your work when you're done with proper commit message so standard-version can create Changelog and bump version of your library appropriately )

`yarn cz` - will invoke [commitizen CLI](https://github.com/commitizen/cz-cli)
