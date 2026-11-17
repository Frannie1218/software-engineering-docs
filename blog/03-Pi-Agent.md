# 实践课3：Pi Agent 源码安装与编译 [gufengdi]

## 基本信息
- 姓名：[谷凤頔]
- 学号：[202430224076]
- GitHub 登录名：Frannie1218
- 小组代码仓库：https://github.com/open-source-slackers/pi-hunnu-2026

---

## 任务一 实验准备：检查和安装开发工具
检查环境，Node.js 为 v24.14.0，npm 为 11.9.0，git 为 2.53.0。符合项目根目录 `package.json` 中 `"node": ">=22.19.0"` 的要求。

**截图 S1：**

<img width="604" height="119" alt="屏幕截图 2026-11-17 113546" src="https://github.com/user-attachments/assets/55777491-017e-41d1-9705-45c08ceabd60" />


---

## 任务二 下载课程仓库源码
源码已在前序作业中克隆至本地 `C:\Users\42418\pi-02\pi-hunnu-2026`。当前分支为 `main`，且 `git status` 干净无修改。提交编号为 `c3cc91632d0a1950fb122605b190233f2aa0006e`。

**截图 S2：**

<img width="500" height="137" alt="屏幕截图 2026-11-17 113649" src="https://github.com/user-attachments/assets/64f22db2-d94a-4657-bc61-c560e3f2834a" />


---

## 任务三 阅读配置，确认安装与编译的依据

**截图 S3（分为两张图）：**

<img width="503" height="101" alt="屏幕截图 2026-11-17 113752" src="https://github.com/user-attachments/assets/328c6ad2-50f8-4066-b4d2-11c6693a67b0" />

<img width="169" height="49" alt="屏幕截图 2026-11-17 113800" src="https://github.com/user-attachments/assets/8db14139-a44b-4ba6-9930-f70acec3c0ad" />


**问答：**
1. **Node.js 版本要求在哪里？** 在根目录 `package.json` 的 `"engines"` 字段中，声明了 `"node": ">=22.19.0"`。
2. **`npm run build` 实际从哪里读取命令？** 实际上是从根目录的 `package.json` 的 `"scripts"` 字段中读取 `"build"` 对应的命令（一长串 `cd` 命令），然后依次进入各个子包，执行每个子包自己 `package.json` 里的 `"build"` 命令。

---

## 任务四 安装项目依赖
执行了 `npm install --ignore-scripts`。安装成功，总计添加了 335 个包，用时 38 秒。过程中出现了 `deprecated`（依赖弃用）和 `min-release-age` 的警告，但未影响安装结果。

**截图 S4：**

<img width="603" height="153" alt="屏幕截图 2026-11-17 114001" src="https://github.com/user-attachments/assets/41833e0d-ac97-4435-b3f2-11a39bb94ac1" />


---

## 任务五 本地编译与构建产物验证
执行了 `npm run build`。构建成功后，通过 `Test-Path` 确认 `cli.js` 产物存在（返回 `True`），并运行该产物验证了版本号为 `1.5.2`。

**截图 S5：**

<img width="608" height="141" alt="屏幕截图 2026-11-17 114050" src="https://github.com/user-attachments/assets/c27e0784-bfb8-4f0e-ba1c-4c473155c122" />

<img width="584" height="67" alt="屏幕截图 2026-11-17 114135" src="https://github.com/user-attachments/assets/7ef356ba-3fa8-406d-ba3f-c332751006c9" />


---

## 任务六 启动本地源码版本并完成一次会话

**截图 S6：**

<img width="588" height="95" alt="屏幕截图 2026-11-17 114457" src="https://github.com/user-attachments/assets/ea7b98d0-eb6d-4de2-8b88-8d9d695b2c22" />

<img width="601" height="487" alt="屏幕截图 2026-11-17 114315" src="https://github.com/user-attachments/assets/0dc23a6f-102f-4354-8a8d-2ae79af3a8ae" />


**问答：**

1. **本次如何确保运行的是本地源码？** 我没有直接输入 `pi`（这可能会调用全局安装的版本），而是通过执行本地仓库根目录下的 `.\pi-test.bat` 命令来启动。这个脚本会通过 Node.js 直接加载 `packages/coding-agent/src/cli.ts` 源码，从而确保运行的是本地刚刚编译好的最新代码。
2. **源码入口与 `dist/bundle/cli.js` 入口分别适合什么场景？** 源码入口（`.\pi-test.bat`）适合开发调试阶段，修改代码后可立即生效；而 `dist/bundle/cli.js` 是构建产物，打包了所有依赖，适合对外发布、部署和终端用户直接运行。

---

## 遇到的困难与解决过程
本次实验整体非常顺利。在安装依赖和构建时遇到了一些 `npm warn` 警告（如项目配置过期、依赖弃用等），但这属于 npm 的常规提示，通过查阅文档确认不影响核心功能后，继续执行。最终编译和运行均一次成功。
