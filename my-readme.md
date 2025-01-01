# 初始化配置项目

## 迭代1
1.npm install一下前端工程
2. 将[VueStaticResourceResolver.java](webserver/src/main/java/io/micronaut/web/router/resource/VueStaticResourceResolver.java)注释掉，不注入容器中


## 迭代2
参考链接：https://github.com/KodeChicken/kestra/blob/main/.github/CONTRIBUTING.md#develop-backend
1.  前端配置修改
- 新增文件：[.env.development.local](ui/.env.development.local)
  - 填充内容：VITE_APP_API_URL=http://localhost:8080
- npm run dev
2. cli后端配置
  - 参考上述链接配置
  - cli args填充，详见：ServerType.java
    - server webserver
    - server standalone
    - server local
      3.webserver build.gradle修改
  - 注释掉 dependsOn(':ui:assembleFrontend')，不需要打包前端，前后端独立启动

## 迭代3
cli application.yaml中添加cors配置
vite.config.js中删除：import {commit} from "./plugins/commit"
vite.config.js中删除：commit()

## 迭代4
看历史commit记录
总之一句话参考CONTRIBUTING.md文件中的操作来配置项目

# 插件配置
```text
# 插件下载
1.官方插件地址：https://github.com/orgs/kestra-io/repositories?q=plugin-
2.maven仓库地址：https://repo1.maven.org/maven2/io/kestra/plugin/

3.cli app启动类配置KESTRA_PLUGINS_PATH环境变量
```

# 脚本相关
```text
# python等相关任务的运行依赖docker环境，需要本地安装docker并启动docker服务
```

# 任务输出文件
```text
任务执行完的输出文件保存在./data目录下，用命令空间、id、task-id等参数分层命令

```

# 注意事项
```text
如果您在执行上述流程时遇到任何问题，这可能是与 Docker 相关的问题（例如 Docker in-Docker 设置，这可能很难在 Windows 上配置）。将 runner 属性设置为 PROCESS 以在与流相同的进程中运行 Python 脚本任务，而不是在 Docker 容器中运行，如以下示例所示。这将避免任何与 Docker 相关的问题。
taskRunner:
      type: io.kestra.plugin.core.runner.Process
详细解释以及配置参考：https://kestra.io/docs/tutorial/outputs
会报错：pip install XXX，会将包安装在全局下，homebrew管理的python禁止全局安装包，目的是为了避免多项目下的依赖冲突，所以推荐虚拟环境下的包安装，所以该问题在kestra自动化运行python脚本时无法解决(也可以用下列方式解决)，只能利用docker环境去运行

sudo ln -s $(which pip3) /usr/local/bin/pip
sudo ln -s $(which python3) /usr/local/bin/python

sudo pip3 install --break-system-packages polars
sudo pip3 uninstall polars --break-system-packages
```