本文将展示如何从0开始初始化一个`typescript`项目。

点击访问[原文地址](https://segmentfault.com/a/1190000041781242)

点击访问[git仓库](https://segmentfault.com/a/1190000041781242), 点击下载[代码包](https://github.com/yunzhiclub/typescript-init/archive/refs/heads/main.zip)

## 初始化
首先，我们选定一个文件夹，然后在文件夹中执行`npm init -y`命令来对项目进行初始化。
```shell
anjie@panjies-Mac-Pro typescript-init % npm init -y
Wrote to /Users/panjie/github/yunzhiclub/typescript-init/package.json:

{
  "name": "typescript-init",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/yunzhiclub/typescript-init.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/yunzhiclub/typescript-init/issues"
  },
  "homepage": "https://github.com/yunzhiclub/typescript-init#readme"
}
```
该命令将为我们生成一个`package.json`文件：
```bash
panjie@panjies-Mac-Pro typescript-init % tree
.
├── README.md
└── package.json

0 directories, 2 files

```

## 安装typescript
接下来，我们使用`npm i typescript --save-dev`来安装`ts`：
```shell
panjie@panjies-Mac-Pro typescript-init % npm i typescript --save-dev
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN typescript-init@1.0.0 No description

+ typescript@4.6.4
added 1 package from 1 contributor and audited 1 package in 2.22s
found 0 vulnerabilities
```

## typescript初始化
ts安装后，我们也需要一个初始化操作，该操作将默认生成ts的配置文件，对应的命令为`npx tsc --init`
```bash
panjie@panjies-Mac-Pro typescript-init % npx tsc --init

Created a new tsconfig.json with:                                               
                                                                             TS 
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true


You can learn more at https://aka.ms/tsconfig.json
```
该命令将为我们自动生成`tsconfig.json`，如果你想进行一些定制，则只需要打开此文件，找到对应的项进行修改或启用即可。


## index.ts
基本的初始化工作完成后，便可以创建`index.ts`，并进行代码的测试了。

```ts
'use strict';

const hello = (world: string) => {
  console.log(`hello ${world}`);
}

hello('world');
```

## 编译运行
文件创建完成后进行编译及运行:
```bash
panjie@panjies-Mac-Pro typescript-init % npx tsc index.ts
panjie@panjies-Mac-Pro typescript-init % node index.js
hello world
```

## 自动编译运行
每次变更文件化都手动执行一下编译及运行固然可行，但这种方式的确无法忍受。[tsc-watch](https://www.npmjs.com/package/tsc-watch)则专门为此而生，运行`npm install tsc-watch --save-dev`来安装`tsc-watch`：

```bash
panjie@panjies-Mac-Pro typescript-init % npm install tsc-watch --save-dev
npm WARN typescript-init@1.0.0 No description

+ tsc-watch@5.0.3
added 20 packages from 16 contributors and audited 21 packages in 3.788s
found 0 vulnerabilities
```

安装完成后，我们打开`package.json`文件，在`scripts`中增加以下`dev`项：
```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "tsc-watch --noClear -p ./tsconfig.json --onSuccess \"node ./index.js\""
  },
```

然后我们在命令行中运行`npm run dev`则可以实现：当文件变更时重新编译、重新运行的目的。

## 参考文档

* [https://www.digitalocean.com/community/tutorials/typescript-new-project](https://www.digitalocean.com/community/tutorials/typescript-new-project)
* [https://www.npmjs.com/package/tsc-watch](https://www.npmjs.com/package/tsc-watch)









