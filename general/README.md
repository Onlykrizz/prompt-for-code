# 概述

把CLAUDE-user.md复制到~/.claude/CLAUDE.md

把CLAUDE-project.md复制为项目根目录下的CLAUDE.md

CLAUDE-appoint.md等其他文件直接复制到项目根目录下的claude-memory目录下，例如claude-memory/CLAUDE-appoint.md

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