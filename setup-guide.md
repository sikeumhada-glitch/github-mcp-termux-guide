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
