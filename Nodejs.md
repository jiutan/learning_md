# Node.js

工具：

- `node`：运行 JavaScript 程序
- `npm`：安装和管理 Node.js 软件包（软件包管理器）

- `npx`：临时下载并运行某个 Node.js 工具（“下载后直接运行”）

- `nvm`：管理多个 Node.js 版本（Node.js 版本管理器）

### 1. Node.js

- 查看版本：`node -v`

### 2. npm（把工具安装下来）

- 安装软件包：`npm install 某个工具`
  - `-g`：全局安装

### 3. npx（把工具下载后直接运行）

运行 Node.js 工具，不一定需要你手动安装

```shell
npx skills add Agents365-ai/drawio-skill \
  -g \
  -a codex \
  --copy \
  -y
```

其中：

- `npx` 临时获取 `skills` 工具
- 运行 `skills add`
- 从 GitHub 获取 `Agents365-ai/drawio-skill`
- 安装给 Codex 使用

### 4. nvm（版本管理器）

在不同 Node.js 版本之间切换：

```shell
# 切换到22版本
nvm install 22
nvm use 22
nvm alias default 22
```

