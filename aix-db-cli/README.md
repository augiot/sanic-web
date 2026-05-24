# @apconw/aix-db-cli

Aix-DB 数据问答命令行工具。通过浏览器登录后，直接在终端发起数据问答查询。

## 安装

```bash
npm install -g @apconw/aix-db-cli
```

## 快速开始

```bash
# 1. 登录（默认服务地址 http://localhost:18080）
aix-db-cli login

# 自定义服务地址
aix-db-cli login --url http://your-server:18080

# 2. 查看可用数据源
aix-db-cli datasources

# 按类型过滤
aix-db-cli datasources --type mysql

# 3. 数据问答
aix-db-cli chat "有哪些数据表？" --datasource 48

# 流式输出（逐字打印）
aix-db-cli chat "查询销售额趋势" --datasource 48 --stream

# 显示执行步骤
aix-db-cli chat "各表行数统计" --datasource 48 --verbose
```

## 命令

### `login`

浏览器登录，保存 JWT token（有效期 24 小时）到 `~/.config/aix-db-cli/config.json`。

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `--url <baseUrl>` | `http://localhost:18080` | Aix-DB 服务地址 |

### `datasources`

列出已注册的数据源。

| 选项 | 说明 |
|------|------|
| `--type <type>` | 按类型精确过滤（mysql, pg, ck, starrocks...）|
| `--name <name>` | 按名称模糊过滤 |

### `chat <question>`

发起数据问答查询，答案输出到 stdout。

| 选项 | 默认值 | 说明 |
|------|--------|------|
| `--datasource <id>` | 必填 | 数据源 ID |
| `--qa-type <type>` | `DATABASE_QA` | 问答模式 |
| `--timeout <seconds>` | `180` | 超时时间（秒）|
| `--verbose` | false | 显示 SQL 生成等执行步骤 |
| `--stream` | false | 流式逐字输出 |

## 发布到 npm

```bash
cd aix-db-cli
npm publish --access public
```

## Token 过期

Token 有效期 24 小时。过期后重新运行 `aix-db-cli login` 即可。
