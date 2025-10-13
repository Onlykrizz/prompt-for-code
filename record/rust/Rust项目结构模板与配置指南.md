# Rust项目结构模板与配置指南

本文档提供不同类型Rust项目的标准结构模板和配置文件，帮助快速搭建符合最佳实践的项目框架。

## 基础项目模板

### 简单库项目结构

```
my_lib/
├── Cargo.toml              # 项目配置文件
├── README.md               # 项目说明文档
├── LICENSE                 # 开源许可证
├── CHANGELOG.md            # 变更日志
├── .gitignore              # Git忽略文件
├── .github/                # GitHub配置
│   └── workflows/
│       └── ci.yml          # 持续集成配置
├── src/                    # 源代码目录
│   ├── lib.rs              # 库入口文件
│   └── utils.rs            # 工具模块
├── tests/                  # 集成测试
│   └── integration_test.rs
├── examples/               # 使用示例
│   └── basic_usage.rs
├── benches/                # 基准测试
│   └── benchmark.rs
└── docs/                   # 文档目录
    └── api.md
```

### 命令行应用结构

```
my_cli/
├── Cargo.toml
├── README.md
├── LICENSE
├── CHANGELOG.md
├── .gitignore
├── .github/workflows/ci.yml
├── src/
│   ├── main.rs             # 应用入口
│   ├── cli.rs              # 命令行接口定义
│   ├── config.rs           # 配置管理
│   ├── error.rs            # 错误类型定义
│   └── modules/            # 功能模块
│       ├── mod.rs
│       ├── processor.rs
│       └── output.rs
├── tests/
│   └── cli_tests.rs
├── examples/
│   └── usage.rs
├── assets/                 # 静态资源
│   └── config.toml
└── scripts/                # 构建脚本
    └── install.sh
```

### 工作区项目结构

```
my_workspace/
├── Cargo.toml              # 工作区配置
├── README.md
├── LICENSE
├── .gitignore
├── .github/workflows/
│   ├── ci.yml
│   └── release.yml
├── core/                   # 核心库
│   ├── Cargo.toml
│   └── src/
│       └── lib.rs
├── cli/                    # 命令行工具
│   ├── Cargo.toml
│   └── src/
│       └── main.rs
├── web/                    # Web服务
│   ├── Cargo.toml
│   └── src/
│       └── main.rs
├── shared/                 # 共享代码
│   ├── Cargo.toml
│   └── src/
│       └── lib.rs
├── tests/                  # 工作区级集成测试
│   └── workspace_tests.rs
└── docs/                   # 项目文档
    ├── architecture.md
    └── deployment.md
```

## 配置文件模板

### Cargo.toml配置

#### 基础库配置
```toml
[package]
name = "my-awesome-lib"
version = "0.1.0"
edition = "2021"
authors = ["Your Name <your.email@example.com>"]
license = "MIT OR Apache-2.0"
description = "项目简短描述，不超过一行"
homepage = "https://github.com/username/project"
repository = "https://github.com/username/project"
documentation = "https://docs.rs/my-awesome-lib"
readme = "README.md"
keywords = ["cli", "tool", "utility"]
categories = ["command-line-utilities", "development-tools"]
include = [
    "src/**/*",
    "LICENSE*",
    "README.md",
    "CHANGELOG.md"
]

[dependencies]
# 运行时依赖
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1.0", features = ["full"] }
clap = { version = "4.0", features = ["derive"] }
anyhow = "1.0"
thiserror = "1.0"

[dev-dependencies]
# 开发和测试依赖
tokio-test = "0.4"
criterion = "0.5"
proptest = "1.0"

[[bench]]
name = "performance"
harness = false

[profile.release]
# 发布版本优化配置
lto = true
codegen-units = 1
panic = "abort"
strip = true

[profile.dev]
# 开发版本配置
debug = true
opt-level = 0

[profile.test]
# 测试版本配置
opt-level = 1
```

#### 工作区配置
```toml
[workspace]
members = [
    "core",
    "cli", 
    "web",
    "shared"
]

[workspace.dependencies]
# 统一依赖版本管理
serde = { version = "1.0", features = ["derive"] }
tokio = { version = "1.0", features = ["full"] }
anyhow = "1.0"
thiserror = "1.0"

[workspace.metadata]
# 工作区元数据
rust-version = "1.70"
```

#### 二进制应用配置
```toml
[package]
name = "my-cli-app"
version = "0.1.0"
edition = "2021"
authors = ["Your Name <your.email@example.com>"]
license = "MIT OR Apache-2.0"
description = "强大的命令行工具"
homepage = "https://github.com/username/my-cli-app"
repository = "https://github.com/username/my-cli-app"
readme = "README.md"
keywords = ["cli", "productivity", "tool"]
categories = ["command-line-utilities"]

[[bin]]
name = "mycli"
path = "src/main.rs"

[dependencies]
clap = { version = "4.0", features = ["derive"] }
serde = { version = "1.0", features = ["derive"] }
serde_json = "1.0"
tokio = { version = "1.0", features = ["full"] }
anyhow = "1.0"
dirs = "5.0"
colored = "2.0"

[dev-dependencies]
assert_cmd = "2.0"
predicates = "3.0"
tempfile = "3.0"

# 构建脚本配置
[build-dependencies]
built = "0.7"

[features]
default = []
json-output = ["serde_json"]
progress-bar = ["indicatif"]

[package.metadata.deb]
# Debian包配置
maintainer = "Your Name <your.email@example.com>"
copyright = "2023, Your Name <your.email@example.com>"
license-file = ["LICENSE", "1"]
extended-description = """\
详细的应用程序描述，
可以多行显示。"""
depends = "$auto"
section = "utility"
priority = "optional"
assets = [
    ["target/release/mycli", "usr/bin/", "755"],
    ["README.md", "usr/share/doc/mycli/README", "644"],
]
```

### Rust工具链配置

#### rust-toolchain.toml
```toml
[toolchain]
channel = "stable"
components = ["rustfmt", "clippy", "rust-analyzer"]
targets = ["x86_64-unknown-linux-gnu", "x86_64-pc-windows-msvc"]
profile = "minimal"
```

#### rustfmt.toml
```toml
# 代码格式化配置
max_width = 100
hard_tabs = false
tab_spaces = 4
newline_style = "Unix"
use_small_heuristics = "Default"
fn_call_width = 80
attr_fn_like_width = 70
struct_lit_width = 18
struct_variant_width = 35
array_width = 60
chain_width = 60
single_line_if_else_max_width = 50
wrap_comments = true
format_code_in_doc_comments = true
normalize_comments = true
normalize_doc_attributes = true
license_template_path = ""
format_strings = false
format_macro_matchers = false
format_macro_bodies = true
empty_item_single_line = true
struct_lit_single_line = true
fn_single_line = false
where_single_line = false
imports_indent = "Block"
imports_layout = "Mixed"
group_imports = "StdExternalCrate"
reorder_imports = true
reorder_modules = true
reorder_impl_items = false
type_punctuation_density = "Wide"
space_before_colon = false
space_after_colon = true
spaces_around_ranges = false
binop_separator = "Front"
remove_nested_parens = true
combine_control_expr = true
overflow_delimited_expr = false
struct_field_align_threshold = 0
enum_discrim_align_threshold = 0
match_arm_blocks = true
force_multiline_blocks = false
fn_args_layout = "Tall"
brace_style = "SameLineWhere"
control_brace_style = "AlwaysSameLine"
trailing_semicolon = true
trailing_comma = "Vertical"
match_block_trailing_comma = false
blank_lines_upper_bound = 1
blank_lines_lower_bound = 0
edition = "2021"
merge_derives = true
use_try_shorthand = false
use_field_init_shorthand = false
force_explicit_abi = true
condense_wildcard_suffixes = false
color = "Auto"
unstable_features = false
disable_all_formatting = false
skip_children = false
hide_parse_errors = false
error_on_line_overflow = false
error_on_unformatted = false
report_todo = "Never"
report_fixme = "Never"
ignore = []
emit_mode = "Files"
make_backup = false
```

#### clippy.toml
```toml
# Clippy检查配置
cognitive-complexity-threshold = 30
too-many-arguments-threshold = 7
type-complexity-threshold = 250
single-char-binding-names-threshold = 4
trivial-copy-size-limit = 64
pass-by-value-size-limit = 256
too-many-lines-threshold = 100
large-type-threshold = 200
enum-variant-name-threshold = 3
literal-representation-threshold = 10
trivially-copy-pass-by-ref-size-limit = 256
avoid-breaking-exported-api = true
allow-expect-in-tests = true
allow-unwrap-in-tests = true
```

## 源代码模板

### lib.rs模板

```rust
//! # 项目名称
//!
//! 项目的简短描述。
//!
//! ## 特性
//!
//! - 功能特性1
//! - 功能特性2
//! - 功能特性3
//!
//! ## 使用示例
//!
//! ```
//! use my_lib::core_function;
//!
//! let result = core_function("input");
//! assert_eq!(result, "expected_output");
//! ```
//!
//! ## 模块组织
//!
//! - [`core`] - 核心功能模块
//! - [`utils`] - 工具函数模块
//! - [`error`] - 错误处理模块

#![deny(missing_docs)]
#![deny(unsafe_code)]
#![warn(clippy::all)]
#![warn(clippy::pedantic)]
#![warn(clippy::nursery)]

pub mod core;
pub mod error;
pub mod utils;

// 重新导出常用类型和函数
pub use crate::core::{CoreStruct, core_function};
pub use crate::error::{Error, Result};

/// 库的版本信息
pub const VERSION: &str = env!("CARGO_PKG_VERSION");

/// 预处理函数，用于初始化库
///
/// # 错误
///
/// 当初始化失败时返回错误
pub fn init() -> Result<()> {
    // 初始化逻辑
    Ok(())
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_init() {
        assert!(init().is_ok());
    }

    #[test]
    fn test_version() {
        assert!(!VERSION.is_empty());
    }
}
```

### main.rs模板

```rust
//! 命令行应用程序入口

use anyhow::{Context, Result};
use clap::Parser;
use std::process;

mod cli;
mod config;
mod core;
mod error;

use cli::Cli;
use config::Config;

/// 应用程序主函数
#[tokio::main]
async fn main() {
    // 设置日志记录
    if std::env::var("RUST_LOG").is_err() {
        std::env::set_var("RUST_LOG", "info");
    }
    env_logger::init();

    // 解析命令行参数
    let cli = Cli::parse();

    // 运行应用程序
    if let Err(e) = run(cli).await {
        eprintln!("错误: {e:?}");
        process::exit(1);
    }
}

/// 应用程序主要逻辑
async fn run(cli: Cli) -> Result<()> {
    // 加载配置
    let config = Config::load(&cli.config)
        .context("配置文件加载失败")?;

    // 根据命令行参数执行相应操作
    match cli.command {
        cli::Command::Process { input, output } => {
            core::process_file(&input, &output, &config).await
                .context("文件处理失败")?;
        }
        cli::Command::Validate { file } => {
            core::validate_file(&file, &config).await
                .context("文件验证失败")?;
        }
    }

    Ok(())
}

#[cfg(test)]
mod tests {
    use super::*;
    use tempfile::tempdir;

    #[tokio::test]
    async fn test_basic_functionality() {
        // 基本功能测试
        let dir = tempdir().unwrap();
        let config_path = dir.path().join("test_config.toml");
        
        // 创建测试配置文件
        tokio::fs::write(&config_path, "# 测试配置")
            .await
            .unwrap();

        // 测试配置加载
        let config = Config::load(&config_path);
        assert!(config.is_ok());
    }
}
```

### error.rs模板

```rust
//! 错误处理模块
//!
//! 定义应用程序中使用的所有错误类型。

use std::fmt;
use thiserror::Error;

/// 应用程序主要错误类型
#[derive(Error, Debug)]
pub enum AppError {
    /// 配置文件相关错误
    #[error("配置错误: {message}")]
    Config { message: String },

    /// 文件I/O错误
    #[error("文件操作失败: {path}")]
    FileOperation { 
        path: String,
        #[source]
        source: std::io::Error,
    },

    /// 数据验证错误
    #[error("数据验证失败: {field} - {reason}")]
    Validation { field: String, reason: String },

    /// 网络请求错误
    #[error("网络请求失败")]
    Network(#[from] reqwest::Error),

    /// 序列化/反序列化错误
    #[error("数据序列化失败")]
    Serialization(#[from] serde_json::Error),

    /// 通用错误
    #[error("内部错误: {0}")]
    Internal(#[from] anyhow::Error),
}

/// 应用程序Result类型别名
pub type Result<T> = std::result::Result<T, AppError>;

impl AppError {
    /// 创建配置错误
    pub fn config<S: Into<String>>(message: S) -> Self {
        Self::Config {
            message: message.into(),
        }
    }

    /// 创建文件操作错误
    pub fn file_operation<S: Into<String>>(path: S, source: std::io::Error) -> Self {
        Self::FileOperation {
            path: path.into(),
            source,
        }
    }

    /// 创建验证错误
    pub fn validation<S: Into<String>>(field: S, reason: S) -> Self {
        Self::Validation {
            field: field.into(),
            reason: reason.into(),
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_error_creation() {
        let err = AppError::config("测试配置错误");
        assert!(matches!(err, AppError::Config { .. }));
        assert_eq!(err.to_string(), "配置错误: 测试配置错误");
    }

    #[test]
    fn test_error_chain() {
        let io_err = std::io::Error::new(std::io::ErrorKind::NotFound, "文件未找到");
        let app_err = AppError::file_operation("test.txt", io_err);
        
        assert!(matches!(app_err, AppError::FileOperation { .. }));
        assert!(app_err.source().is_some());
    }
}
```

### cli.rs模板

```rust
//! 命令行接口定义

use clap::{Parser, Subcommand};
use std::path::PathBuf;

/// 应用程序命令行接口
#[derive(Parser)]
#[command(
    name = "my-cli",
    version = env!("CARGO_PKG_VERSION"),
    author = "Your Name <your.email@example.com>",
    about = "强大的命令行工具",
    long_about = None
)]
pub struct Cli {
    /// 配置文件路径
    #[arg(short, long, value_name = "FILE")]
    pub config: Option<PathBuf>,

    /// 启用详细输出
    #[arg(short, long)]
    pub verbose: bool,

    /// 指定输出格式
    #[arg(long, value_enum, default_value_t = OutputFormat::Text)]
    pub format: OutputFormat,

    /// 子命令
    #[command(subcommand)]
    pub command: Command,
}

/// 支持的输出格式
#[derive(clap::ValueEnum, Clone, Debug)]
pub enum OutputFormat {
    /// 纯文本输出
    Text,
    /// JSON格式输出
    Json,
    /// YAML格式输出
    Yaml,
}

/// 应用程序子命令
#[derive(Subcommand)]
pub enum Command {
    /// 处理文件命令
    Process {
        /// 输入文件路径
        #[arg(short, long)]
        input: PathBuf,

        /// 输出文件路径
        #[arg(short, long)]
        output: Option<PathBuf>,

        /// 并发处理线程数
        #[arg(long, default_value = "4")]
        threads: usize,

        /// 启用压缩
        #[arg(long)]
        compress: bool,
    },

    /// 验证文件命令
    Validate {
        /// 要验证的文件路径
        file: PathBuf,

        /// 严格模式验证
        #[arg(long)]
        strict: bool,
    },

    /// 显示配置信息
    Config {
        /// 显示默认配置
        #[arg(long)]
        defaults: bool,
    },
}

#[cfg(test)]
mod tests {
    use super::*;
    use clap::CommandFactory;

    #[test]
    fn verify_cli() {
        Cli::command().debug_assert();
    }

    #[test]
    fn test_help() {
        let help = Cli::command().render_help();
        assert!(help.to_string().contains("强大的命令行工具"));
    }
}
```

## 测试文件模板

### 单元测试模板

```rust
//! 单元测试示例

#[cfg(test)]
mod tests {
    use super::*;

    /// 测试正常情况
    #[test]
    fn test_normal_case() {
        let input = "test input";
        let expected = "expected output";
        let result = process_function(input);
        assert_eq!(result, expected);
    }

    /// 测试错误情况
    #[test]
    fn test_error_case() {
        let invalid_input = "";
        let result = process_function(invalid_input);
        assert!(result.is_err());
    }

    /// 测试边界情况
    #[test]
    fn test_edge_cases() {
        // 空字符串
        assert!(process_function("").is_ok());
        
        // 极长字符串
        let long_string = "a".repeat(10000);
        assert!(process_function(&long_string).is_ok());
        
        // 特殊字符
        assert!(process_function("🦀").is_ok());
    }

    /// 异步测试示例
    #[tokio::test]
    async fn test_async_function() {
        let result = async_process_function().await;
        assert!(result.is_ok());
    }

    /// 参数化测试
    #[test]
    fn test_multiple_inputs() {
        let test_cases = vec![
            ("input1", "output1"),
            ("input2", "output2"),
            ("input3", "output3"),
        ];

        for (input, expected) in test_cases {
            let result = process_function(input);
            assert_eq!(result, expected, "Failed for input: {}", input);
        }
    }
}
```

### 集成测试模板

```rust
//! 集成测试
//! 
//! tests/integration_test.rs

use assert_cmd::Command;
use predicates::prelude::*;
use std::fs;
use tempfile::tempdir;

/// 测试CLI基本功能
#[test]
fn test_cli_help() {
    let mut cmd = Command::cargo_bin("my-cli").unwrap();
    cmd.arg("--help");
    cmd.assert()
        .success()
        .stdout(predicate::str::contains("强大的命令行工具"));
}

/// 测试文件处理功能
#[test]
fn test_file_processing() {
    let temp_dir = tempdir().unwrap();
    let input_file = temp_dir.path().join("input.txt");
    let output_file = temp_dir.path().join("output.txt");

    // 创建测试输入文件
    fs::write(&input_file, "test content").unwrap();

    // 运行命令
    let mut cmd = Command::cargo_bin("my-cli").unwrap();
    cmd.arg("process")
        .arg("--input")
        .arg(&input_file)
        .arg("--output")
        .arg(&output_file);

    cmd.assert().success();

    // 验证输出文件
    assert!(output_file.exists());
    let output_content = fs::read_to_string(&output_file).unwrap();
    assert!(!output_content.is_empty());
}

/// 测试错误处理
#[test]
fn test_invalid_input() {
    let mut cmd = Command::cargo_bin("my-cli").unwrap();
    cmd.arg("process")
        .arg("--input")
        .arg("nonexistent.txt");

    cmd.assert()
        .failure()
        .stderr(predicate::str::contains("错误"));
}

/// 测试配置文件功能
#[test]
fn test_config_file() {
    let temp_dir = tempdir().unwrap();
    let config_file = temp_dir.path().join("config.toml");

    // 创建配置文件
    fs::write(&config_file, r#"
        [general]
        verbose = true
        
        [processing]
        threads = 2
    "#).unwrap();

    let mut cmd = Command::cargo_bin("my-cli").unwrap();
    cmd.arg("--config")
        .arg(&config_file)
        .arg("config")
        .arg("--defaults");

    cmd.assert().success();
}
```

### 基准测试模板

```rust
//! 性能基准测试
//!
//! benches/benchmark.rs

use criterion::{black_box, criterion_group, criterion_main, Criterion, BenchmarkId};
use my_lib::{process_function, async_process_function};

/// 基本性能测试
fn benchmark_process_function(c: &mut Criterion) {
    let input = "test input data";
    
    c.bench_function("process_function", |b| {
        b.iter(|| process_function(black_box(input)))
    });
}

/// 不同输入大小的性能对比
fn benchmark_different_sizes(c: &mut Criterion) {
    let mut group = c.benchmark_group("size_comparison");
    
    for size in [100, 1000, 10000].iter() {
        let input = "a".repeat(*size);
        group.bench_with_input(
            BenchmarkId::new("process", size),
            size,
            |b, _| b.iter(|| process_function(black_box(&input)))
        );
    }
    
    group.finish();
}

/// 异步函数基准测试
fn benchmark_async_function(c: &mut Criterion) {
    let rt = tokio::runtime::Runtime::new().unwrap();
    
    c.bench_function("async_process", |b| {
        b.to_async(&rt).iter(|| async_process_function())
    });
}

/// 内存分配测试
fn benchmark_memory_usage(c: &mut Criterion) {
    c.bench_function("memory_intensive", |b| {
        b.iter(|| {
            let data: Vec<String> = (0..1000)
                .map(|i| format!("item_{}", i))
                .collect();
            black_box(data);
        })
    });
}

criterion_group!(
    benches,
    benchmark_process_function,
    benchmark_different_sizes,
    benchmark_async_function,
    benchmark_memory_usage
);
criterion_main!(benches);
```

## CI/CD配置模板

### GitHub Actions CI配置

```yaml
# .github/workflows/ci.yml
name: 持续集成

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

env:
  CARGO_TERM_COLOR: always
  RUST_BACKTRACE: 1

jobs:
  check:
    name: 检查代码格式和静态分析
    runs-on: ubuntu-latest
    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@stable
        with:
          components: rustfmt, clippy

      - name: 缓存依赖
        uses: actions/cache@v3
        with:
          path: |
            ~/.cargo/registry
            ~/.cargo/git
            target
          key: ${{ runner.os }}-cargo-${{ hashFiles('**/Cargo.lock') }}
          restore-keys: |
            ${{ runner.os }}-cargo-

      - name: 检查代码格式
        run: cargo fmt --all -- --check

      - name: Clippy静态分析
        run: cargo clippy --all-targets --all-features -- -D warnings

      - name: 检查文档
        run: cargo doc --no-deps --document-private-items

  test:
    name: 运行测试
    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest, macos-latest]
        rust: [stable, beta]
    runs-on: ${{ matrix.os }}
    
    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@master
        with:
          toolchain: ${{ matrix.rust }}

      - name: 缓存依赖
        uses: actions/cache@v3
        with:
          path: |
            ~/.cargo/registry
            ~/.cargo/git
            target
          key: ${{ runner.os }}-${{ matrix.rust }}-cargo-${{ hashFiles('**/Cargo.lock') }}

      - name: 运行单元测试
        run: cargo test --verbose

      - name: 运行集成测试
        run: cargo test --test integration_test

      - name: 运行文档测试
        run: cargo test --doc

  coverage:
    name: 代码覆盖率
    runs-on: ubuntu-latest
    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@stable

      - name: 安装tarpaulin
        run: cargo install cargo-tarpaulin

      - name: 生成覆盖率报告
        run: cargo tarpaulin --verbose --all-features --workspace --timeout 120 --out Xml

      - name: 上传到codecov
        uses: codecov/codecov-action@v3

  security:
    name: 安全审计
    runs-on: ubuntu-latest
    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装cargo-audit
        run: cargo install cargo-audit

      - name: 安全漏洞检查
        run: cargo audit

  benchmark:
    name: 性能基准测试
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    
    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@stable

      - name: 运行基准测试
        run: cargo bench

      - name: 存储基准结果
        uses: benchmark-action/github-action-benchmark@v1
        with:
          name: Rust Benchmark
          tool: 'cargo'
          output-file-path: target/criterion/report/index.html
          github-token: ${{ secrets.GITHUB_TOKEN }}
          auto-push: true
```

### 发布流程配置

```yaml
# .github/workflows/release.yml
name: 发布

on:
  push:
    tags:
      - 'v*'

env:
  CARGO_TERM_COLOR: always

jobs:
  create-release:
    name: 创建发布
    runs-on: ubuntu-latest
    outputs:
      upload_url: ${{ steps.create_release.outputs.upload_url }}
    steps:
      - name: 创建Release
        id: create_release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          draft: false
          prerelease: false

  build:
    name: 构建发布版本
    needs: create-release
    strategy:
      matrix:
        include:
          - os: ubuntu-latest
            target: x86_64-unknown-linux-gnu
            name: linux
          - os: windows-latest
            target: x86_64-pc-windows-msvc
            name: windows
          - os: macos-latest
            target: x86_64-apple-darwin
            name: macos
    runs-on: ${{ matrix.os }}

    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@stable
        with:
          targets: ${{ matrix.target }}

      - name: 构建发布版本
        run: cargo build --release --target ${{ matrix.target }}

      - name: 打包二进制文件 (Unix)
        if: matrix.os != 'windows-latest'
        run: |
          tar czf my-cli-${{ matrix.name }}.tar.gz \
            -C target/${{ matrix.target }}/release \
            my-cli

      - name: 打包二进制文件 (Windows)
        if: matrix.os == 'windows-latest'
        run: |
          7z a my-cli-${{ matrix.name }}.zip \
            ./target/${{ matrix.target }}/release/my-cli.exe

      - name: 上传发布资产 (Unix)
        if: matrix.os != 'windows-latest'
        uses: actions/upload-release-asset@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ needs.create-release.outputs.upload_url }}
          asset_path: ./my-cli-${{ matrix.name }}.tar.gz
          asset_name: my-cli-${{ matrix.name }}.tar.gz
          asset_content_type: application/gzip

      - name: 上传发布资产 (Windows)
        if: matrix.os == 'windows-latest'
        uses: actions/upload-release-asset@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          upload_url: ${{ needs.create-release.outputs.upload_url }}
          asset_path: ./my-cli-${{ matrix.name }}.zip
          asset_name: my-cli-${{ matrix.name }}.zip
          asset_content_type: application/zip

  publish-crate:
    name: 发布到crates.io
    needs: build
    runs-on: ubuntu-latest
    if: startsWith(github.ref, 'refs/tags/v')

    steps:
      - name: 检出代码
        uses: actions/checkout@v4

      - name: 安装Rust工具链
        uses: dtolnay/rust-toolchain@stable

      - name: 发布到crates.io
        run: cargo publish --token ${{ secrets.CRATES_TOKEN }}
```

## 文档模板

### README.md模板

```markdown
# 项目名称

[![CI](https://github.com/username/project/workflows/CI/badge.svg)](https://github.com/username/project/actions)
[![Crates.io](https://img.shields.io/crates/v/project.svg)](https://crates.io/crates/project)
[![Documentation](https://docs.rs/project/badge.svg)](https://docs.rs/project)
[![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-blue.svg)](LICENSE)

项目的简短描述，一句话说明这个项目是做什么的。

## 特性

- ✨ 核心功能1
- 🚀 核心功能2  
- 🛡️ 核心功能3
- 📦 核心功能4

## 安装

### 使用cargo安装

```bash
cargo install project-name
```

### 从源码构建

```bash
git clone https://github.com/username/project.git
cd project
cargo install --path .
```

### 预编译二进制文件

从 [Releases](https://github.com/username/project/releases) 页面下载适合您操作系统的预编译二进制文件。

## 使用方法

### 基本用法

```bash
# 基本命令
project-name --help

# 处理文件
project-name process --input file.txt --output result.txt

# 验证文件
project-name validate file.txt
```

### 配置文件

创建配置文件 `config.toml`:

```toml
[general]
verbose = true
threads = 4

[processing]
format = "json"
compress = true
```

然后使用配置文件：

```bash
project-name --config config.toml process --input file.txt
```

### 作为库使用

在您的 `Cargo.toml` 中添加依赖：

```toml
[dependencies]
project-name = "0.1"
```

然后在代码中使用：

```rust
use project_name::{core_function, Config};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let config = Config::default();
    let result = core_function("input", &config)?;
    println!("结果: {}", result);
    Ok(())
}
```

## API文档

详细的API文档请查看 [docs.rs](https://docs.rs/project-name)。

## 示例

查看 [examples](examples/) 目录获取更多使用示例。

## 贡献

我们欢迎各种形式的贡献！请查看 [CONTRIBUTING.md](CONTRIBUTING.md) 了解如何参与项目开发。

### 开发环境设置

1. 克隆仓库: `git clone https://github.com/username/project.git`
2. 安装Rust: https://rustup.rs/
3. 运行测试: `cargo test`
4. 运行示例: `cargo run --example basic`

## 许可证

本项目采用双许可证:

* Apache License 2.0 ([LICENSE-APACHE](LICENSE-APACHE))  
* MIT License ([LICENSE-MIT](LICENSE-MIT))

## 致谢

感谢所有贡献者和以下优秀的开源项目：

- [项目1](https://github.com/project1) - 功能描述
- [项目2](https://github.com/project2) - 功能描述

## 更新日志

查看 [CHANGELOG.md](CHANGELOG.md) 了解版本更新历史。
```

这些模板提供了完整的Rust项目结构和配置文件，可以根据具体需求进行调整和定制。通过使用这些模板，可以快速搭建符合最佳实践的Rust项目，提高开发效率和代码质量。