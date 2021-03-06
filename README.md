## TODO

- [x] hooks 支持
- [x] 规范支持，eslint 规则，prettier 规则，husky 代码提交校验
- [x] less module 支持
- [x] 可选链语法，Null 判断运算符支持
- [x] vw 支持
- [x] 开发局部热更新支持
- [x] 开发时开启 react development 模式
- [x] 开启 tree shaking，lodash 替换为 lodash-es，按需加载支持
- [x] 编译时去掉 vconsole 代码

> [react-use](https://streamich.github.io/react-use/?path=/story/animation-usespring--docs) 该库封装了开发常用逻辑，快速上手 hooks 开发

## 如何快速新建一个路由页面

1. vscode 安装 `Create Item By Template` 插件
2. F1 | ctrl p 唤起输入框后键入路径，这个项目是 src/routes/{your-route-name}
3. 将在对应的路径里生成页面模板
4. 想自定义的话可以修改或者添加模板的话，可以编辑 .vscode 文件夹中的 create-item.template.js 文件

## 代码提交规范

> npm run commit 开始编辑提交信息

1. 提交类型

| code          | info                                          |
| ------------- | --------------------------------------------- |
| feat: msg     | 新功能 feature                                |
| fix: msg      | 修复 bug                                      |
| docs: msg     | 只是修改了文档:注释、README.md 等             |
| style: msg    | 格式，不影响代码运行的变动                    |
| refactor: msg | 重构即不是新增功能，也不是修改 bug 的代码变动 |
| perf: msg     | 代码更改可以提高性能                          |
| merge: msg    | merge                                         |
| test: msg     | 添加缺失测试或更正现有测试                    |
| build: msg    | 编译代码                                      |
| ci: msg       | 持续集成，这里应该用不到                      |
| chore: msg    | 构建过程或辅助工具的变动                      |
| revert: msg   | revert 一个先前的提交                         |

2. 涉及范围

这里我们以版本号划分范围，此次提交代码所涉及到的发布版本。如果涉及多个版本则以 4.14.10~4.27.10 表示

3. 简要描述

4. 详细描述

5. 破坏性的修改描述

6. 是否有关联 issues

完成后会触发 eslint 和 prettier 的钩子，格式化和美化代码

## 结构

```
project
└───config 配置文件夹
└───public 入口文件html
└───build  打包后文件夹
└───script 启动打包脚本
│
└───src 业务开发
    └─── images 图片统一存放的位置
    │
    └─── components 通用组件, 需要通用组件自己加，默认有一个 AuthComponent
    │       │
    │       └─── AuthComponent 用于授权所用，业务一般不需要管，需要对授权特殊管理才管
    │
    └─── hooks 业务自定义hooks，默认有列表页请求hooks
    │       │
    │       └─── useFetchList listView逻辑封装
    │       │
    │       └─── useBtnDebounce 点击按钮防抖
    │
    └─── routes 路由页面
    │       │
    │       └───index.js 读取app_config.js中的路由配置表，自动生成支持异步加载和预加载的路由组件
    │       │
    │       └───login 登录页面 调试用，点击登录，可跳转到首页
    │       │
    │       └───home 默认首页
    │       │     └─components home 页面 抽出来的组件
    │       │     └─home.js
    │       │     └─index.less
    │       │
    │       │
    │       ...
    │
    └─── app.js 业务入口，授权，路由的一些全局处理在这里进行
    │
    └─── app_config.js 路由配置表，api请求配置表等其他配置表
    │
    └─── context.js 全局上下文在这里配置出来
    │
    └─── index.js 入口文件，与业务无关的在这里配置
    │
    └─── index.less 通用样式，重置默认样式
```

## 项目命名规则

例：test-app test-aha-app

## 配置广场入口链接

配置入口链接，老授权 web 的 url 如下，sign_suffix 前规定加个?initContext=1, 脚手架提供存储上下文的能力，如果不需要则不加 initContext

举例：

旧授权："url":"\${home.url}/test-app/build/index.html#/home?initContext=1#sign_suffix"（另一个好处是规避 test-app/build/index.html#/home&id=xx&appkey=xx&signnature=xxx 识别不了的现象）

新授权: "url":"\${home.url}/test-app/build/index.html#/home?initContext=1

## 增加了 window.\$\$context 上下文

增加上下文的概念：url 上有 initContext=1，第一次进入项目的时候，当前 url 的所有参数就是上下文。F5 刷新页面也算第一次进入。

存储：以 package.json 的项目名 name，转成大写加双$$号，例如项目名是test-app,则上下文存储到sesstion里头的$$TESPAPP 里头

## 项目的多入口，分享页等

如果你有一个 detail 页，这个页面是要分享的，为了保证闭环，请将必要信息一并设置好再加上，initContext === '1'

例如 home 页面是你的首页，detail 是分享页
home 链接：build/index.html#/home?communityId=1&organizationId=2&appId=3&业务必要参数=4&categoryId=5&ns=6

详情页的的 url：build/index.html#/home?detailId=1

调用 sdk 时，shareMenu 配置的链接就应该是 build/index.html#/home?initContext=1&detailId=xx&communityId=1&organizationId=2&appId=3&业务必要参数=4&categoryId=5&ns=6

## FAQ

- eslint 规则问题，在 zapp 直接打开开发 eslint 规则不生效，先用 vscode 打开独立项目开发吧，后面修改
