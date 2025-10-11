```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
nvm install 22
npm i -g @openai/codex

npm install -g @modelcontextprotocol/server-sequential-thinking
npm install -g @upstash/context7-mcp@latest
npm install -g @playwright/mcp@latest
npm install -g mcp-shrimp-task-manager
npm install -g mcp-deepwiki@latest
npm install -g @wonderwhy-er/desktop-commander
npm install -g @modelcontextprotocol/server-filesystem

curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install --git https://github.com/astral-sh/uv uv
uv python install cpython-3.13.8+freethreaded-linux-x86_64-gnu
uv venv --python cpython-3.13.8+freethreaded-linux-x86_64-gnu py313free-for-mcp

source py313free-for-mcp/bin/activate
uv pip install mcp-server-time
uv pip install duckduckgo-mcp-server

git clone https://github.com/oraios/serena
cd serena/
uv run serena config edit
uv run serena start-mcp-server

mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts
wget http://localhost:9999/PingFang_SC.ttc
fc-cache .
fc-list
```

```
alias cx='codex --ask-for-approval never --sandbox danger-full-access'
export EDITOR=vim
export http_proxy=http://127.0.0.1:10809
export https_proxy=http://127.0.0.1:10809
export all_proxy=http://127.0.0.1:10809
export no_proxy='127.0.0.1, localhost'
```

```
skinparam defaultFontName "PingFang SC"
```