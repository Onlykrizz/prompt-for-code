# 概述

把AI-AGENT_user.md复制到~/.ai-agent/AI_AGENT.md

把AI-AGENT_project.md复制为项目根目录下的AI_AGENT.md

AI-AGENT_appointment.md等其他文件直接复制到项目根目录下的ai-agent-memory目录下，例如ai-agent-memory/AI-AGENT_appointment.md

## 快捷代码片段

```
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
uv python list
uv venv --python cpython-3.14.0a5+freethreaded-windows-x86_64-none python314free

uv pip install mcp-server-git

npm install -g @modelcontextprotocol/server-filesystem
npm install -g @modelcontextprotocol/server-sequential-thinking
npm install -g @kazuph/mcp-fetch

  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "node",
      "args": [
        "C:\\Users\\sayurinana\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-filesystem\\dist\\index.js"
      ],
      "env": {}
    },
    "thinking": {
      "type": "stdio",
      "command": "node",
      "args": [
        "C:\\Users\\sayurinana\\AppData\\Roaming\\npm\\node_modules\\@modelcontextprotocol\\server-sequential-thinking\\dist\\index.js"
      ],
      "env": {}
    },
    "fetch": {
      "type": "stdio",
      "command": "node",
      "args": [
        "C:\\Users\\sayurinana\\AppData\\Roaming\\npm\\node_modules\\@kazuph\\mcp-fetch\\dist\\index.js"
      ],
      "env": {}
    }
  }
```
