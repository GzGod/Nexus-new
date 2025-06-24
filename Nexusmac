#!/bin/bash
set -e

BIN_PATH="/usr/local/bin/nexus-network"

# 检查 nexus-network 是否存在
function check_nexus_binary() {
    if ! command -v nexus-network >/dev/null 2>&1; then
        echo "未检测到 nexus-network，正在下载安装..."
        curl -sSL https://cli.nexus.xyz/ | NONINTERACTIVE=1 sh
        ln -sf "$HOME/.nexus/bin/nexus-network" "$BIN_PATH"
    fi
}

# 运行节点
function start_node() {
    read -rp "请输入您的 node-id: " NODE_ID
    if [ -z "$NODE_ID" ]; then
        echo "❌ node-id 不能为空！"
        exit 1
    fi

    echo "$NODE_ID" > "$HOME/.nexus/node-id"
    echo "✅ 正在启动 Nexus 节点，按 Ctrl+C 可随时停止..."

    NODE_ID="$NODE_ID" nexus-network start --node-id "$NODE_ID"
}

check_nexus_binary
start_node
