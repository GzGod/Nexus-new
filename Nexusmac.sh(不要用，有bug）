#!/bin/bash
set -e

BIN_DIR="$HOME/.nexus/bin"
BIN_PATH="$BIN_DIR/nexus-network"
NODE_ID_FILE="$HOME/.nexus/last_node_id"

# 安装 nexus-network（适配 macOS M 系列）
function install_nexus() {
    if [ ! -f "$BIN_PATH" ]; then
        echo "🌀 未检测到 nexus-network，正在下载安装..."
        curl -sSL https://cli.nexus.xyz/ | NONINTERACTIVE=1 sh || {
            echo "❌ 下载失败，请检查网络或重试"
            exit 1
        }
        echo 'export PATH="$HOME/.nexus/bin:$PATH"' >> ~/.zshrc
        export PATH="$HOME/.nexus/bin:$PATH"
        echo "✅ 已将 nexus-network 添加到 PATH 中"
    fi
}

# 获取 node-id（优先读取上次保存的）
function get_node_id() {
    if [[ -f "$NODE_ID_FILE" ]]; then
        NODE_ID=$(cat "$NODE_ID_FILE")
        echo "🔁 使用上次的 node-id：$NODE_ID"
    else
        read -rp "请输入您的 node-id: " NODE_ID
        if [ -z "$NODE_ID" ]; then
            echo "❌ node-id 不能为空"
            exit 1
        fi
        echo "$NODE_ID" > "$NODE_ID_FILE"
        echo "✅ 已保存 node-id：$NODE_ID"
    fi
}

# 启动节点
function start_node() {
    echo "🚀 启动 Nexus 节点..."
    echo "$NODE_ID" > "$HOME/.nexus/node-id"
    NODE_ID="$NODE_ID" "$BIN_PATH" start --node-id "$NODE_ID"
}

# 主流程
install_nexus
get_node_id
start_node
