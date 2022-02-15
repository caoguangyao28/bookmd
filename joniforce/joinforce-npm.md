# Npm 私有服务使用 (joinforce Nexus 版)

基于 nexus 构建npm 私有仓库服务，解放号 [nexus 地址](https://nexus.jointforce.com), 使用公司jira 账号，链接vpn，即可登录查看。

nexus npm 仓库服务 ，由 npm-group ， npm-private， npm-proxy 三者组成。

1. npm-group 负责组织 npm-private ， npm-proxy，npm install 时 优先取 npm-private 仓库，其次 npm-proxy（阿里镜像）···
2. npm-private 存放公司私有前端组件 或 代码模块
3. npm-proxy 代理至 阿里的镜像获取开源 前端组件或模块



## 账号接入（jira 账号）

公司 nexus ，账号权限集成 jira 账号！！无需单独设置npm 账号（用户发布 程序的账号）。

前端项目以及ci 构建时 需要统计将 node ，npm 的 registry 指定 npm-group 的地址。

eg：

```bash
npm config set registry https://nexus.jointforce.com/repository/npm-group/ 
```

或者 使用 **nrm** （npm 的源管理工具）**推荐使用** ,方便切换各种 源例如 阿里的

```bash
// 安装
npm install -g nrm
// 查看已安装源
nrm ls
// 新增源
nrm add jointforce https://nexus.jointforce.com/repository/npm-group/

// 切换至 jointforce
nrm use jointforce

```



设置好npm 源后，npm 使用方式一切如旧····（初始化项目时 链接vpn 保证先读我们的私服仓库）



## 发布自制 组件到 npm 私服

因为npm 的私服搭建是借助的nexus ，公司自部署的nexus 用户鉴权已经 集成了jira 的账号，所以无需 在生成 npm 账户

制作好npm 软件包后，进入软件包根目录，修改 package.json 文件中属性添加

````json
"publishConfig": { "registry": "https://nexus.jointforce.com/repository/npm-private/" }
````

npm 登陆到 npm-private

```bash
npm login -registry=https://nexus.jointforce.com/repository/npm-private/
// 输入 jira 账号 & 密码

// 发布
npm publish

// 可打开 web 页面https://nexus.jointforce.com/ 登陆后浏览对象仓库验证
```

Ps: 或者 nrm 中添加 npm-private 源，切换至 ，npm login





