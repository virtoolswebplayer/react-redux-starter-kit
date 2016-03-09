React Redux Starter Kit
=======================

[![Join the chat at https://gitter.im/davezuko/react-redux-starter-kit](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/davezuko/react-redux-starter-kit?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://travis-ci.org/davezuko/react-redux-starter-kit.svg?branch=master)](https://travis-ci.org/davezuko/react-redux-starter-kit?branch=master)
[![dependencies](https://david-dm.org/davezuko/react-redux-starter-kit.svg)](https://david-dm.org/davezuko/react-redux-starter-kit)
[![devDependency Status](https://david-dm.org/davezuko/react-redux-starter-kit/dev-status.svg)](https://david-dm.org/davezuko/react-redux-starter-kit#info=devDependencies)
[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com/)

> ### 让eslint检测分号?
> 运行npm install之后, 打开 `.eslintrc`, 修改 `semi` 规则 将 `never` 改成 `always`, 然后运行 `npm run lint:fix` -- 就是这么简单! 另外, 你可以按照上面的方法,扩展你喜欢的 ESLint 配置; 自定义项目代码风格满足你的团队需求.

This starter kit is designed to get you up and running with a bunch of awesome new front-end technologies, all on top of a configurable, feature-rich webpack build system that's already setup to provide hot reloading, CSS modules with Sass support, unit testing, code coverage reports, bundle splitting, and a whole lot more.

The primary goal of this project is to remain as **unopinionated** as possible. Its purpose is not to dictate your project structure or to demonstrate a complete sample application, but to provide a set of tools intended to make front-end development robust, easy, and, most importantly, fun. Check out the full feature list below!

Table of Contents
-----------------
1. [Requirements](#requirements)
1. [Features](#features)
1. [Getting Started](#getting-started)
1. [Starting a New Project](#starting-a-new-project)
1. [Usage](#usage)
1. [Structure](#structure)
1. [Webpack](#webpack)
1. [Server](#server)
1. [Styles](#styles)
1. [Testing](#testing)
1. [Deployment](#deployment)
1. [Troubleshooting](#troubleshooting)

Requirements
------------

* node `^4.2.0`
* npm `^3.0.0`

功能及特点
--------

* [React](https://github.com/facebook/react) (`^0.14.0`)
  * Includes react-addons-test-utils (`^0.14.0`)
* [Redux](https://github.com/rackt/redux) (`^3.0.0`)
  * react-redux (`^4.0.0`)
  * redux-devtools
    * use `npm run dev:nw` to display them in a separate window.
  * redux-thunk middleware
* [react-router](https://github.com/rackt/react-router) (`^2.0.0`)
* [react-router-redux](https://github.com/rackt/react-router-redux) (`^3.0.0`)
* [Webpack](https://github.com/webpack/webpack)
  * [CSS modules!](https://github.com/css-modules/css-modules)
  * sass-loader
  * postcss-loader with cssnano for style autoprefixing and minification
  * Bundle splitting for app and vendor dependencies
  * CSS extraction during builts that are not using HMR (like `npm run compile`)
  * Loaders for fonts and images
* [Koa](https://github.com/koajs/koa) (`^2.0.0-alpha`)
  * webpack-dev-middleware
  * webpack-hot-middleware
* [Karma](https://github.com/karma-runner/karma)
  * Mocha w/ chai, sinon-chai, and chai-as-promised
  * [Airbnb's Enzyme](https://github.com/airbnb/enzyme) with [chai-enzyme](https://github.com/producthunt/chai-enzyme)
  * PhantomJS
  * Code coverage reports
* [Babel](https://github.com/babel/babel) (`^6.3.0`)
  * [babel-plugin-transform-runtime](https://www.npmjs.com/package/babel-plugin-transform-runtime) so transforms aren't inlined
  * [babel-preset-react-hmre](https://github.com/danmartinez101/babel-preset-react-hmre) for:
    * react-transform-hmr (HMR for React components)
    * redbox-react (visible error reporting for React components)
  * [babel-plugin-transform-react-constant-elements](https://babeljs.io/docs/plugins/transform-react-constant-elements/) save some memory allocation
  * [babel-plugin-transform-react-remove-prop-types](https://github.com/oliviertassinari/babel-plugin-transform-react-remove-prop-types) remove `PropTypes`
* [ESLint](http://eslint.org)
  * Uses [Standard Style](https://github.com/feross/standard) by default, but you're welcome to change this!
  * Includes separate test-specific `.eslintrc` to support chai assertions

如何开始
---------------

克隆项目安装node模块:

```shell
$ git clone https://github.com/davezuko/react-redux-starter-kit.git
$ cd react-redux-starter-kit
$ npm install                   # Install Node modules listed in ./package.json (may take a while the first time)
$ npm start                     # Compile and launch
```

创建一个新项目
----------------------

创建一个新项目按照下面的的步骤操作

```shell
$ git checkout -b <your-project-name> new-project
$ npm install                   # There are a few npm dependencies in this branch that aren't in master
$ npm run make:project          # Make your new project
$ rm -rf .git && git init       # Start a new git repository
```

用法
-----

Before delving into the descriptions of each available npm script, here's a brief summary of the three which will most likely be your bread and butter:

* 实时开发? 运行 `npm start` 启动开发服务器.
* 编译到 dist? 运行 `npm run compile`. 编译后的文件存放在 `dist`目录
* 部署? `npm run deploy`.

**注意:** This package makes use of [debug](https://github.com/visionmedia/debug) 调试体验. For convenience, all of messages are prefixed with `app:*`. If you'd like to to change what debug statements are displayed, you can override the `DEBUG` environment variable via the CLI (e.g. `DEBUG=app:* npm start`) or tweak the npm scripts (`betterScripts` in `package.json`).

非常棒, 下面详细说明 `npm command` 的命令:

* `npm start` - 启动一个`koa`服务器， `localhost:3000`. 在开发环境下会启用`热替换`.
* `npm run compile` - 编译应用到`dist`目录 (`~/dist` by default).
* `npm run dev` - 和 `npm start` 效果相同, 但是它会启动 `nodeman` 来监听服务器端的代码改动,并自动重启server
* `npm run dev:nw` - 和 `npm run dev` 效果相同, 另外会在一个新窗口打开 `redux devtools`
* `npm run dev:no-debug` - 和 `npm run dev` 效果相同，但不启用`redux devtools`
* `npm run test` -运行Karma单元测试并且生成代码覆盖报告
* `npm run test:dev` - 运行Karma单元测试并监听测试代码变化,如有变化会重新启动测试; 不生成代码覆盖率报告.
* `npm run deploy`- 运行 代码质量、单元测试, 测试通过以后, compiles your application to disk.
* `npm run lint`- 对所有 `.js` 文件进行代码规则检测.
* `npm run lint:fix` - 检测代码并尝试修复 `.js` . [请查看这篇文章](http://eslint.org/docs/user-guide/command-line-interface.html#fix).

**注间:** 部署到指定环境时，务必要指定`NODE_ENV`环境变量 ,只有指定了`NODE_ENV` webpack 才会使用正确的配置. 例如: `NODE_ENV=production npm run compile` 会编译应用程序并且将编译后的`_production.js` 保存到 `~/build/webpack/_production.js`.

### 配置

项目的基础配置 `~/config/_base.js`. 你可重新定义 `src`目录 和 `dist` 目录, 调整编译选项, tweak your vendor dependencies, 等等. 一般情况下, 你可以做一些修改s in here **without ever having to touch the webpack build configuration**. 如果你想增加一个新的环境, 你可创建一个以该环境名称命名的文件，并指定 `NODE_ENV` 添加一个前缀 `_` in `~/config` (see `~/config/_production.js` for an example).

通用配置选项:

* `dir_src` - 应用的源码目录
* `dir_dist` - 编译之后的存放目录
* `server_host` - koa Server 的主机名或ip地址
* `server_port` - Koa server 的服务端口
* `compiler_css_modules` - whether or not to enable CSS modules
* `compiler_devtool` - what type of source-maps to generate (set to `false`/`null` to disable)
* `compiler_vendor` - 对第三方库进行拆分打包

目录结构
---------

```
.
├── bin                      # 构建/启动 脚本
├── build                    # 所有的构建
│   └── webpack              # Environment-specific configuration files for webpack
├── config                   # 项目配置
├── server                   # Koa 服务程序 (使用 webpack middleware 中间件)
│   └── main.js              # 服务端程序的入口点
├── src                      # 整个应用程序的源码目录
│   ├── components           # 常规的 React 组件 (generally Dumb components)
│   ├── containers           # 可以提供上下文环境的组件 (比如. Redux Provider)
│   ├── layouts              # 可以完成网页布局结构的组件
│   ├── redux                # Redux-specific pieces
│   │   ├── modules          #reducers/constants/actions 都放在这里
│   │   └── utils            # Redux-specific 工具类脚本目录
│   ├── routes               # 应用程序的路由定义
│   ├── static               # 静态资源目录 (not imported anywhere in source code)
│   ├── styles               # Application-wide styles (generally settings)
│   ├── views                # Components that live at a route
│   └── main.js              # 整个应用程序的入口点
└── tests                    # 单元测试
```

### Components vs. Views vs. Layouts

**TL;DR:** They're all components.

This distinction may not be important for you, but as an explanation: A **Layout** is something that describes an entire page structure, such as a fixed navigation, viewport, sidebar, and footer. Most applications will probably only have one layout, but keeping these components separate makes their intent clear. **Views** are components that live at routes, and are generally rendered within a **Layout**. What this ends up meaning is that, with this structure, nearly everything inside of **Components** ends up being a dumb component.

Webpack
-------

### Vendor Bundle
You can redefine which packages to bundle separately by modifying `compiler_vendor` in `~/config/_base.js`. These default to:

```js
[
  'history',
  'react',
  'react-redux',
  'react-router',
  'react-router-redux',
  'redux'
]
```

### Webpack Root Resolve
Webpack is configured to make use of [resolve.root](http://webpack.github.io/docs/configuration.html#resolve-root), which lets you import local packages as if you were traversing from the root of your `~/src` directory. Here's an example:

```js
// current file: ~/src/views/some/nested/View.js

// What used to be this:
import SomeComponent from '../../../components/SomeComponent'

// Can now be this:
import SomeComponent from 'components/SomeComponent' // Hooray!
```

### Globals

These are global variables available to you anywhere in your source code. If you wish to modify them, they can be found as the `globals` key in `~/config/_base.js`. When adding new globals, also add them to `~/.eslintrc`.

* `process.env.NODE_ENV` - the active `NODE_ENV` when the build started
* `__DEV__` - True when `process.env.NODE_ENV` is `development`
* `__PROD__` - True when `process.env.NODE_ENV` is `production`
* `__TEST__` - True when `process.env.NODE_ENV` is `test`
* `__DEBUG__` - True when `process.env.NODE_ENV` is `development` and cli arg `--no_debug` is not set (`npm run dev:no-debug`)
* `__BASENAME__` - [npm history basename option](https://github.com/rackt/history/blob/master/docs/BasenameSupport.md)

Server
------

This starter kit comes packaged with an Koa server. It's important to note that the sole purpose of this server is to provide `webpack-dev-middleware` and `webpack-hot-middleware` for hot module replacement. Using a custom Koa app in place of [webpack-dev-server](https://github.com/webpack/webpack-dev-server) will hopefully make it easier for users to extend the starter kit to include functionality such as back-end API's, isomorphic/universal rendering, and more -- all without bloating the base boilerplate. Because of this, it should be noted that the provided server is **not** production-ready. If you're deploying to production, take a look at [the deployment section](#deployment).

Styles
------

Both `.scss` and `.css` file extensions are supported out of the box and are configured to use [CSS Modules](https://github.com/css-modules/css-modules). After being imported, styles will be processed with [PostCSS](https://github.com/postcss/postcss) for minification and autoprefixing, and will be extracted to a `.css` file during production builds.

**NOTE:** If you're importing styles from a base styles directory (useful for generic, app-wide styles), you can make use of the `styles` alias, e.g.:

```js
// current file: ~/src/components/some/nested/component/index.jsx
import 'styles/core.scss' // this imports ~/src/styles/core.scss
```

Furthermore, this `styles` directory is aliased for sass imports, which further eliminates manual directory traversing; this is especially useful for importing variables/mixins.

Here's an example:

```scss
// current file: ~/src/styles/some/nested/style.scss
// what used to be this (where base is ~/src/styles/_base.scss):
@import '../../base';

// can now be this:
@import 'base';
```

Testing
-------

To add a unit test, simply create a `.spec.js` file anywhere in `~/tests`. Karma will pick up on these files automatically, and Mocha and Chai will be available within your test without the need to import them.

Coverage reports will be compiled to `~/coverage` by default. If you wish to change what reporters are used and where reports are compiled, you can do so by modifying `coverage_reporters` in `~/config/_base.js`.

Deployment
----------

Out of the box, this starter kit is deployable by serving the `~/dist` folder generated by `npm run compile` (make sure to specify your target `NODE_ENV` as well). This project does not concern itself with the details of server-side rendering or API structure, since that demands an opinionated structure that makes it difficult to extend the starter kit. However, if you do need help with more advanced deployment strategies, here are a few tips:

If you are serving the application via a web server such as nginx, make sure to direct incoming routes to the root `~/dist/index.html` file and let react-router take care of the rest. The Koa server that comes with the starter kit is able to be extended to serve as an API or whatever else you need, but that's entirely up to you.

Have more questions? Feel free to submit an issue or join the Gitter chat!

Troubleshooting
---------------

### `npm run dev:nw` produces `cannot read location of undefined.`

This is most likely because the new window has been blocked by your popup blocker, so make sure it's disabled before trying again.

Reference: [issue 110](https://github.com/davezuko/react-redux-starter-kit/issues/110)

### Babel Issues

Running into issues with Babel? Babel 6 can be tricky, please either report an issue or try out the [stable v0.18.1 release](https://github.com/davezuko/react-redux-starter-kit/tree/v0.18.1) with Babel 5. If you do report an issue, please try to include relevant debugging information such as your node, npm, and babel versions.

### Internationalization Support

In keeping with the goals of this project, no internationalization support is provided out of the box. However, [juanda99](https://github.com/juanda99) has been kind enough to maintain a fork of this repo with internationalization support, [check it out!](https://github.com/juanda99/react-redux-starter-kit)

### High editor CPU usage after compilation

While this is common to any sizable application, it's worth noting for those who may not know: if you happen to notice higher CPU usage in your editor after compiling the application, you may need to tell your editor not to process the dist folder. For example, in Sublime you can add:

```
	"folder_exclude_patterns": [".svn",	".git",	".hg", "CVS",	"node_modules",	"dist"]
```
