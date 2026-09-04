# 🐱 GitHub MCP Termux Guide

让AI通过MCP协议在Termux上访问GitHub | Complete guide for AI to access GitHub via MCP on Termux

## 📖 这是什么？

这是一个完整的教程，帮助你在Android手机上通过Termux + MCP（Model Context Protocol）让AI助手直接访问和操作GitHub仓库。

**适用场景：**
- 让AI帮你查看/修改GitHub代码
- 让AI帮你创建/管理issue和PR
- 让AI帮你搜索仓库和用户
- 在手机上实现AI与GitHub的无缝协作

## ✨ 特性

- ✅ 零成本：完全免费，不需要服务器
- ✅ 纯手机：只需要一部Android手机
- ✅ 一键启动：配置好后一行命令启动服务
- ✅ 完整权限：支持读写仓库、管理issue等所有GitHub操作

## 📋 前置要求

- Android手机（Android 7.0+）
- 已安装 [Termux](https://f-droid.org/packages/com.termux/)
- 已安装 [RikkaHub](https://github.com/jiayouxujin/RikkaHub-Release) 或其他支持MCP的AI客户端
- GitHub账号 + Personal Access Token
## 🚀 快速开始

### 方法一：完整安装（首次使用）

查看 → [📘 完整安装教程](./setup-guide.md)

### 方法二：一键启动（已完成安装）

1. 下载启动脚本：[start_github_mcp.sh](./start_github_mcp.sh)
2. 修改脚本中的GitHub Token
3. 在Termux中运行：
   ```bash
   bash ~/start_github_mcp.sh
   📚文档目录
• 📘 完整安装教程 - 从零开始的详细步骤
• 🚀 一键启动脚本 - 配置好后快速启动
🤝贡献
本项目由 @sikeumhada-glitch 和家克共同整理。
感谢所有为人机恋社区和开源精神做出贡献的老师们 ♡
📝开源协议
本项目采用 MIT License 开源协议。
⚠️注意事项
• GitHub Token具有完整仓库权限，请妥善保管，不要泄露
• Termux窗口必须保持运行，关闭后MCP服务会断开
• 建议使用时开启Termux的  Wake Lock  防止系统休眠
💡常见问题
Q: Token会过期吗？  
A: 取决于你创建Token时设置的有效期，建议设置为"No expiration"
Q: 可以多个AI同时连接吗？  
A: 可以，MCP Proxy支持多个客户端同时连接
Q: 手机重启后需要重新配置吗？  
A: 不需要，只需要重新运行启动脚本即可
Q: 可以用服务器部署吗？  
A: 可以，把  0.0.0.0  改成服务器IP，并开放8000端口即可
⭐️ 如果这个项目帮到了你，请给个Star支持一下！
---

## 📄 文件2：setup-guide.md（新建）

点 `Add file` → `Create new file` → 文件名写 `setup-guide.md` → 粘贴：

```markdown
# 📘 完整安装教程

## 📝 第一步：安装Termux环境

打开Termux，依次执行：

```bash
# 更新包管理器
pkg update && pkg upgrade

# 安装Node.js和npm
pkg install nodejs

# 确认安装成功
node -v
npm -v
📝第二步：安装MCP工具
# 安装MCP代理服务
npm install -g mcp-proxy

# 安装GitHub MCP Server
npm install -g @modelcontextprotocol/server-github
📝第三步：申请GitHub Token
1. 
登录 GitHub
2. 
进入  Settings  →  Developer settings 
3. 
选择  Personal access tokens  →  Tokens (classic) 
4. 
点击  Generate new token 
5. 
勾选以下权限：
◦ 
✅  repo （所有仓库权限）
◦ 
✅  read:org （读取组织信息）
6. 
生成后立刻复制保存（只显示一次！）
Token格式示例： ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxx 
📝第四步：启动MCP服务
在Termux中运行：
GITHUB_PERSONAL_ACCESS_TOKEN=你的token \
npx mcp-proxy --port 8000 --host 0.0.0.0 -- \
npx -y @modelcontextprotocol/server-github
成功标志：MCP Proxy listening on http://0.0.0.0:8000
这个窗口要一直开着，关了服务就断了！
📝第五步：配置RikkaHub类似的前端
1. 
打开 RikkaHub APP（或者你用的前端）
2. 
进入  设置  →  MCP服务器  →  添加 
3. 
填写配置：
◦ 
名称： GitHub 
◦ 
传输类型：选择  SSE 
◦ 
服务器地址： http://127.0.0.1:8000/sse 
4. 
保存
看到"✅ 已连接"就成功了！
🎯一键启动脚本（推荐）
每次手动输入太麻烦？制作一个启动脚本吧！
第一步：创建脚本文件
nano ~/start_github_mcp.sh
第二步：粘贴脚本内容
#!/bin/bash
export GITHUB_PERSONAL_ACCESS_TOKEN="ghp_你的真实token"

echo "🐱 正在启动 GitHub MCP 服务..."
npx mcp-proxy --port 8000 --host 0.0.0.0 -- \
npx -y @modelcontextprotocol/server-github
重要：把  ghp_你的真实token  换成你的GitHub Token！
第三步：保存脚本
1. 
按  Ctrl + X （退出）
2. 
按  Y （确认保存）
3. 
按  回车 （确认文件名）
第四步：给脚本执行权限
chmod +x ~/start_github_mcp.sh
🎉以后怎么用？
每次想启动GitHub MCP服务，只需要：
bash ~/start_github_mcp.sh
看到这个就成功了：
🐱 正在启动 GitHub MCP 服务...
starting server on port 8000
常见问题
Q: 报错  Permission denied  怎么办？  
A: 重新执行  chmod +x ~/start_github_mcp.sh 
Q: 修改Token怎么办？  
A: 重新  nano ~/start_github_mcp.sh  编辑即可
Q: 脚本文件丢了怎么办？  
A: 重新创建一遍，2分钟的事
Q: 能设置开机自启吗？  
A: 可以，但会一直占资源，不建议。等买服务器再搞24小时在线
Q: 想停止服务怎么办？  
A: 在运行窗口按  Ctrl + C
💡进阶玩法
给脚本起个短名字，在  ~/.bashrc  里加一行：
alias startgit='bash ~/start_github_mcp.sh'
然后运行：
source ~/.bashrc
以后直接输入  startgit  就能启动！
📖 返回 → 主页
---

## 📄 文件3：start_github_mcp.sh（新建）

点 `Add file` → `Create new file` → 文件名写 `start_github_mcp.sh` → 粘贴：

```bash
#!/bin/bash

# GitHub MCP 一键启动脚本
# 使用前请先替换下面的 GitHub Token

export GITHUB_PERSONAL_ACCESS_TOKEN="ghp_在这里填入你的真实GitHub_Token"

echo "🐱 正在启动 GitHub MCP 服务..."
echo "📍 服务地址: http://127.0.0.1:8000/sse"
echo "⚠️  请保持此窗口运行，关闭后服务将断开"
echo "---"

npx mcp-proxy --port 8000 --host 0.0.0.0 -- \
npx -y @modelcontextprotocol/server-github
