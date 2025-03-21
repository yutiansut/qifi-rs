# QIFI-RS

QIFI-RS 是 QIFI（Quantaxis Financial Interface）的 Rust 实现，用于快速处理和转换金融交易的账户数据结构。

## 功能特点

- 提供了标准化的期货/股票交易账户数据结构
- 快速的数据序列化和反序列化
- 支持从 JSON/BSON 格式加载和转换数据
- 内置数据转换工具，易于使用
- 兼容 MongoDB 数据库操作

## 数据结构

该库提供了多种数据结构用于量化金融分析和交易:

- `QIFI`: 标准账户数据结构
- `Account`: 账户资金信息
- `Position`: 持仓信息
- `Order`: 订单信息
- `Trade`: 交易记录
- `Transfer`: 资金转账记录
- `Execution`: 执行策略信息
- `Bar`/`Tick`: 行情数据结构

## 安装和使用

在 `Cargo.toml` 中添加依赖:

```toml
[dependencies]
qifi-rs = "0.3.0"
```

## 使用示例

### 从 JSON 字符串加载 QIFI 数据

```rust
use qifi_rs::{QIFI, from_str, from_serde_value};
use serde_json::Value;

let qifi_string = r#"{"account_cookie": "T01B2_IF2004_1min", ...}"#;
let qifi: Value = from_str(qifi_string).unwrap();
let qifi_struct: QIFI = from_serde_value(qifi).unwrap();
```

### 转换结构体为 MongoDB 文档

```rust
use qifi_rs::to_doc;
use qifi_rs::QIFI;

let qifi = QIFI::default(); // 或其他方式获取的 QIFI 实例
let doc = to_doc(qifi);
// 现在可以将 doc 插入到 MongoDB 中
```

## 数据兼容性

库设计考虑了数据兼容性，使用 `#[serde(default)]` 注解来处理可能缺失的字段，确保新旧版本的数据格式都能正确解析。例如，新增的 `executions` 字段即使在旧数据中不存在，也不会导致解析错误。


## 版本

当前版本: 0.4.0 