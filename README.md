# gulp-demo

使用封装好的 gulp 包作为依赖，来打包本地静态资源

## Write process

### gulp-file-common

发布在 npm 官网里的[gulp-file-common](https://www.npmjs.com/package/gulp-file-common)

1. lib 目录下放的就是 gulp 的配置文件 gulpfile.js，里面导出了三个方法，可以作为命令来用，包括
   clean、build 和 start。
   1.1 clean 用来清除临时打包和打包文件夹
   1.2 build 是将所有静态资源打包（打包后的目录结构和原来的一样）
   1.3 start 是开启一个 web 服务，打开一个端口显示页面

2. bin 目录下放的是 cli 脚本文件，主要包括了引入 gulp-cli 脚本，以及其他 gulp 参数
   2.1 --cwd 指定运行目录
   2.2 --gulpfile 指定 gulp 配置文件的目录

## Script setup

打开项目后，下载对应依赖，主要是 gulp-file-common

```shell
npm install
```

本地需配置 pages.config.js 文件（和 package.json 同级）
文件内容主要是静态资源以及打包文件的路径
如:

```js
module.exports = {
  // 路径
  build: {
    src: "src", //资源目录（需要编译压缩的）
    dist: "release", //打包好的文件夹
    temp: ".tmp", //临时打包文件夹
    public: "public", //静态资源（不需要编译压缩）
    paths: {
      styles: "assets/styles/*.scss", //样式文件（用的是scss)
      scripts: "assets/scripts/*.js", //js文件
      pages: "**/*.html", //html文件
      images: "assets/images/**", //图片文件
      fonts: "assets/fonts/**", //字体文件
    },
  },
};
```

## Use

### clean

```shell
npm run clean
```

清除临时的和最终打包好的文件夹, 默认是.tmp 和 release,

### build

```shell
npm run build
```

编译并压缩所有静态资源（包括 src 和 public 目录下的所有资源）并放入打包文件夹, 默认是.tmp 和 release.

### start

```shell
npm run start
```

编译并压缩静态资源（包括 src 目录下的所有资源）并放入临时打包文件夹, 默认是.tmp, 然后启动一个 web 服务，
打开端口为 3002 的网页显示项目

### lint

```shell
npm run lint
```

使用 eslint 检索代码格式，并输出不符合配置的文件，配置文件为.eslintrc.json(和 package.json 同级)
