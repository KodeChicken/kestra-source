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
cors配置
package.json 中删除"prepare": "cd .. && husky ui/.husky && rm -f .git/hooks/*"
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
```

# 脚本相关
```text
# python等相关任务的运行依赖docker环境，需要本地安装docker并启动docker服务
```

# 任务输出文件
```text
任务执行完的输出文件保存在./data目录下，用命令空间、id、task-id等参数分层命令

```
