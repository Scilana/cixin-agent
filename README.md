# Cixin Agent

面向 CIX P1 的多节点 Agent 调度 Runtime。这是此芯作品的独立源码仓库。本包提供可独立运行的 TypeScript/Node.js 调度源码、Web 演示 App、调度盘和自动化测试。

## 评委快速启动

安装 Node.js 22 或更新版本（附带 npm）。首次安装依赖需要联网；Demo 不需要模型账号、API Key、Zeabur、DevEco 或真实开发板。

在当前目录打开终端：

```sh
npm ci
npm run console
```

保持终端开启，复制终端显示的 Console token，在浏览器打开：

- 演示 App：http://127.0.0.1:3200/demo/
- 调度盘：http://127.0.0.1:3200/dashboard/

分别填入该令牌。在演示 App 中导入 examples/vector-task.json 并提交；随后在调度盘查看同一 runId 的决策、执行位置、耗时和回执。任务输入是公开测试向量，CPU 计算及执行回执是真实执行结果。按 Ctrl+C 停止服务。

## 自动验证

```sh
npm test
npm run demo
```

npm test 构建并运行测试；npm run demo 在一台电脑上临时启动两个 HTTP 节点并执行远端 CPU 向量检索，结束后清理临时数据。双节点 Demo 并不是两块实体开发板的实测。

## 内容

- src：调度策略、设备采集、节点与集群 Runtime、HTTP 协议、CPU 向量检索插件、模型 Worker 适配接口。
- web：演示任务入口与调度盘。
- test、examples：自动化测试与可导入任务样例。
- config、deploy：宿主机、P1、多板配置模板及 Linux 服务模板。
- docs：架构、网络画像、Worker 契约与接入说明。

默认只监听本机 127.0.0.1，令牌每次启动自动生成。3200 端口占用时可以先停止此前启动的 Demo，或修改 config/host.example.json 中的 port，再按新端口访问。

## 当前展示边界

没有接入模型，不含模型权重、模型密钥或真实用户数据。NOE/GPU、温度、功耗等未接入能力如实显示不可用，不用随机数伪装硬件测量。本包展示调度和任务执行闭环，不代表完整购物模型链路、P1/NOE 真机性能或调度收益已经验收。

这是独立 Cixin Agent 源码包；不包含同仓库的鸿蒙 App、云端购物服务、旧工程、PPT、node_modules、构建缓存、Git 历史及运行数据库。后续模型通过 docs/worker接入契约.md 所述接口接入。架构文档中涉及 Harmony 的部分是整体项目背景，不是本 Demo 启动依赖。

来源：分支 codex/cixin-multi-device-runtime，仓库提交 1fb7c1d。打包只调整本包 README、package.json 的开发命令，并移除跨项目源码对照测试及共享链路说明，未改变 Runtime 业务源码。Git 历史迁移校验和额外 Playwright 开发测试不属于本独立包。

## 独立仓库与本地材料

本项目从 Cixin 综合仓库的 cixin-agent 拆分，Runtime 源码来源提交为 1fb7c1d。独立运行不依赖相邻鸿蒙工程。

桌面迁移目录中的 local-materials 保存作品说明、PPT 和历史开发材料，已由 .gitignore 排除，不上传到公开仓库。原项目目录保留作为迁移备份。

