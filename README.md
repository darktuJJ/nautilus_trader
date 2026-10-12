**简体中文** · [English](README.en.md)

# <img src="https://github.com/nautechsystems/nautilus_trader/raw/develop/assets/nautilus-trader-logo.png" alt="NautilusTrader" width="500">

[![rustc](https://img.shields.io/crates/msrv/nautilus-core?color=ea7233&logo=rust&label=rustc)](https://crates.io/crates/nautilus-core)
[![crates.io](https://img.shields.io/crates/v/nautilus-core?logo=rust)](https://crates.io/crates/nautilus-core)
[![codspeed](https://img.shields.io/endpoint?url=https://codspeed.io/badge.json)](https://codspeed.io/nautechsystems/nautilus_trader)
![pythons](https://img.shields.io/pypi/pyversions/nautilus_trader)
![pypi-version](https://img.shields.io/pypi/v/nautilus_trader)
[![Downloads](https://img.shields.io/pepy/dt/nautilus-trader?color=blue)](https://pepy.tech/projects/nautilus-trader)
[![Discord](https://img.shields.io/badge/Discord-%235865F2.svg?logo=discord&logoColor=white)](https://discord.gg/NautilusTrader)

| 分支      | 版本                                                                                                                                                                                                                        | 状态                                                                                                                                                                                              |
| :-------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `master`  | [![version](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnautechsystems%2Fnautilus_trader%2Fmaster%2Fversion.json)](https://packages.nautechsystems.io/simple/nautilus-trader/index.html)  | [![build](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml/badge.svg?branch=master)](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml)  |
| `nightly` | [![version](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnautechsystems%2Fnautilus_trader%2Fnightly%2Fversion.json)](https://packages.nautechsystems.io/simple/nautilus-trader/index.html) | [![build](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml/badge.svg?branch=nightly)](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml) |
| `develop` | [![version](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnautechsystems%2Fnautilus_trader%2Fdevelop%2Fversion.json)](https://packages.nautechsystems.io/simple/nautilus-trader/index.html) | [![build](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml/badge.svg?branch=develop)](https://github.com/nautechsystems/nautilus_trader/actions/workflows/build.yml) |

| 平台               | Rust   | Python    |
| :----------------- | :----- | :-------- |
| `Linux (x86_64)`   | 1.99.0 | 3.13-3.14 |
| `Linux (ARM64)`    | 1.99.0 | 3.13-3.14 |
| `macOS (ARM64)`    | 1.99.0 | 3.13-3.14 |
| `Windows (x86_64)` | 1.99.0 | 3.13-3.14 |

- **文档**：<https://nautilustrader.io/docs/>
- **官网**：<https://nautilustrader.io>
- **支持**：[support@nautilustrader.io](mailto:support@nautilustrader.io)

## 简介

NautilusTrader 是一个开源、生产级、Rust 原生的引擎，用于构建多资产、多交易场所的交易系统。

该系统在单一的事件驱动架构中涵盖研究、确定性模拟和实盘执行，Python 则作为策略逻辑、配置和编排的控制层。

这种分离既提供了编译型交易引擎的性能和安全性，又保留了 Python 在系统组合和策略开发上的灵活性。对于关键任务型工作负载，交易系统也可以完全用 Rust 编写。

同一套策略和执行算法代码可以在回测和实盘系统中运行，从而减少部署差异。不过，实盘执行仍会引入交易场所、传输、时序、持久化、外部活动和对账等方面的行为，这些可能无法在模拟中复现。参见[回测与实盘的差异](docs/concepts/live.md#backtest-and-live-differences)。

NautilusTrader 与资产类别无关。任何提供 REST API 或 WebSocket 数据流的交易场所，都可以通过模块化适配器接入。目前的集成涵盖加密货币交易所（CEX 和 DEX）、传统市场（外汇、股票、期货、期权）以及博彩交易所。

![nautilus-trader](https://github.com/nautechsystems/nautilus_trader/raw/develop/assets/nautilus-trader.png "nautilus-trader")

## 功能特性

- **快速**：Rust 核心，使用 [mimalloc](https://crates.io/crates/mimalloc) 内存分配器，并基于 [tokio](https://crates.io/crates/tokio) 实现异步网络。
- **可靠**：由 Rust 保障类型安全和线程安全，可选基于 Redis 的状态持久化。
- **可移植**：可在 Linux、macOS 和 Windows 上运行，支持使用 Docker 部署。
- **灵活**：模块化适配器可接入任何 REST API 或 WebSocket 数据流。
- **高级**：支持 `IOC`、`FOK`、`GTC`、`GTD`、`DAY`、`AT_THE_OPEN`、`AT_THE_CLOSE` 等订单有效期类型，以及高级订单类型和条件触发。支持 `post-only`、`reduce-only` 和冰山单等执行指令。支持 `OCO`、`OUO`、`OTO` 等关联订单。
- **可定制**：支持用户自定义组件，或使用[缓存](https://nautilustrader.io/docs/latest/concepts/cache)和[消息总线](https://nautilustrader.io/docs/latest/concepts/message_bus)从零组装整个系统。
- **回测**：可同时针对多个交易场所、多个品种和多个策略进行回测，使用纳秒级精度的历史报价 tick、成交 tick、K 线、订单簿和自定义数据。
- **实盘**：研究与实盘部署使用完全相同的策略实现。
- **多交易场所**：可同时在多个交易场所运行做市和跨场所策略。
- **AI 训练**：引擎速度足以训练 AI 交易智能体（RL/ES）。

![nautilus](https://github.com/nautechsystems/nautilus_trader/raw/develop/assets/nautilus-art.png "nautilus")

> *nautilus（鹦鹉螺）——源自古希腊语，意为“水手”，naus 意为“船”。*
>
> *鹦鹉螺壳由模块化的腔室组成，其生长因子近似于对数螺线。
> 我们的想法是，这可以转化为设计与架构的美学。*

## 为什么选择 NautilusTrader？

交易策略研究通常在 Python 中以向量化方式进行，而生产交易系统则另行使用编译型语言、以事件驱动架构实现。

NautilusTrader 消除了这种割裂。

Rust 原生核心为研究和实盘执行提供确定性的事件驱动运行时，而 Python 则作为控制层。两种环境使用相同的架构、执行语义和时间模型，使策略无需重新实现即可从研究走向生产。

Rust 原生 v2 运行时通过 [PyO3](https://pyo3.rs) 提供 Python 绑定。在 v2 过渡期间，v1 只在 `develop_v1` 分支上接收关键安全补丁。迁移步骤和兼容性细节请参阅 [v2 迁移指南](https://github.com/nautechsystems/nautilus_trader/blob/develop/MIGRATION_V2.md)。安装预编译的 wheel 不需要 Rust 工具链。

本项目做出了[健全性承诺（Soundness Pledge）](https://raphlinus.github.io/rust/2020/01/18/soundness-pledge.html)：

> “本项目的目标是没有健全性（soundness）bug。
> 开发者会尽最大努力避免此类 bug，并欢迎大家帮助分析和修复。”

> [!NOTE]
>
> **MSRV：** NautilusTrader 高度依赖 Rust 语言和编译器的改进。
> 因此，最低支持的 Rust 版本（MSRV）通常等于 Rust 的最新稳定版。

## 集成

NautilusTrader 采用模块化设计，通过*适配器*工作：适配器将交易场所和数据提供商的原始 API 转换为统一接口和标准化的领域模型，从而实现连接。

以下集成已可用或在计划中；详情请参阅 [docs/integrations/](https://nautilustrader.io/docs/latest/integrations/)：

| 名称                                                       | ID                    | 类型                    | 状态                                                      | 文档                                              |
| :--------------------------------------------------------- | :-------------------- | :---------------------- | :-------------------------------------------------------- | :------------------------------------------------ |
| [AX Exchange](https://architect.exchange)                  | `AX`                  | Derivatives Exchange    | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/architect_ax.md)        |
| [Betfair](https://betfair.com)                             | `BETFAIR`             | Sports Betting Exchange | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/betfair.md)             |
| [Binance](https://binance.com)                             | `BINANCE`             | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/binance.md)             |
| [Blockchain](docs/integrations/blockchain.md)              | `BLOCKCHAIN`          | DeFi Data Provider      | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/blockchain.md)          |
| [Bybit](https://www.bybit.com)                             | `BYBIT`               | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/bybit.md)               |
| [CoinAPI](https://www.coinapi.io/?ref=nautilus)            | `COINAPI`             | Data Provider           | ![status](https://img.shields.io/badge/beta-yellow)       | [Guide](docs/integrations/coinapi.md)             |
| [Coinbase](https://coinbase.com)                           | `COINBASE`            | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/coinbase.md)            |
| [Databento](https://databento.com)                         | `DATABENTO`           | Data Provider           | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/databento.md)           |
| [Deribit](https://www.deribit.com)                         | `DERIBIT`             | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/deribit.md)             |
| [Derive](https://www.derive.xyz)                           | `DERIVE`              | Crypto Exchange (DEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/derive.md)              |
| [dYdX](https://dydx.trade)                                 | `DYDX`                | Crypto Exchange (DEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/dydx.md)                |
| [FinFeed](https://www.finfeedapi.com/?ref=nautilus)        | `FINFEED`             | Data Provider           | ![status](https://img.shields.io/badge/planned-lightgrey) | -                                                 |
| [Hyperliquid](https://hyperliquid.xyz)                     | `HYPERLIQUID`         | Crypto Exchange (DEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/hyperliquid.md)         |
| [Interactive Brokers](https://www.interactivebrokers.com)  | `INTERACTIVE_BROKERS` | Brokerage (multi-venue) | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/interactive_brokers.md) |
| [Kalshi](https://kalshi.com)                               | `KALSHI`              | Prediction Market (CEX) | ![status](https://img.shields.io/badge/planned-lightgrey) | -                                                 |
| [Kraken](https://kraken.com)                               | `KRAKEN`              | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/kraken.md)              |
| [Lighter](https://lighter.xyz)                             | `LIGHTER`             | Crypto Exchange (DEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/lighter.md)             |
| [Lighter on Robinhood](https://robinhoodchain.lighter.xyz) | `LIGHTER_ROBINHOOD`   | Crypto Exchange (DEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/lighter.md)             |
| [OKX](https://okx.com)                                     | `OKX`                 | Crypto Exchange (CEX)   | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/okx.md)                 |
| [Polymarket](https://polymarket.com)                       | `POLYMARKET`          | Prediction Market (DEX) | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/polymarket.md)          |
| [Tardis](https://tardis.dev)                               | `TARDIS`              | Crypto Data Provider    | ![status](https://img.shields.io/badge/stable-green)      | [Guide](docs/integrations/tardis.md)              |

- **ID**：集成适配器客户端的默认客户端 ID。
- **类型**：集成的类型（通常是交易场所的类型）。

对于 Lighter on Robinhood，`LIGHTER_ROBINHOOD` 是需要注册的交易场所和显式客户端 ID。共享的 Lighter 工厂仍以 `LIGHTER` 作为兼容性默认值。

### 状态

- `planned`：计划在未来开发。
- `building`：正在构建中，可能尚不可用。
- `beta`：已完成到最低可用状态，处于 beta 测试阶段。
- `stable`：功能集和 API 已稳定，集成已经过开发者和用户合理程度的测试（可能仍存在一些 bug）。

更多详情请参阅[集成](https://nautilustrader.io/docs/latest/integrations/)文档。

## 路线图

[路线图](https://github.com/nautechsystems/nautilus_trader/blob/develop/ROADMAP.md)概述了 NautilusTrader 的战略方向。当前的优先事项包括稳定 Rust 原生核心、改进文档以及提升代码易用性。

开源项目专注于面向个人和小团队量化交易者的单节点回测和实盘交易。为了专注于核心引擎和生态的可持续性，UI 仪表盘、分布式编排和内置 AI/ML 工具不在范围之内。其他外部集成（如数据库、云服务和监控工具）也不在范围之内，除非在[开源范围](https://github.com/nautechsystems/nautilus_trader/blob/develop/ROADMAP.md#open-source-scope)中明确列出。

在开源范围内的新集成提案，应先通过 RFC issue 讨论其适用性，再提交 PR。相关指南请参阅[社区贡献的集成](https://github.com/nautechsystems/nautilus_trader/blob/develop/ROADMAP.md#community-contributed-integrations)。

## 安全

[![OpenSSF Scorecard](https://api.scorecard.dev/projects/github.com/nautechsystems/nautilus_trader/badge)](https://scorecard.dev/viewer/?uri=github.com/nautechsystems/nautilus_trader)

安全是 NautilusTrader 项目的首要任务之一。我们在依赖选择、开发、构建和发布的各个环节都实施了安全控制。

- Rust 依赖仅来自 crates.io；锁文件使用加密校验和锁定依赖。
- 新的依赖和工具版本在采用前需经过一段发布冷却期。
- 第三方 Python 包仅从 wheel 安装。
- 使用 `cargo-vet` 审计 Rust 依赖来源。
- 使用 `cargo-deny` 强制执行与 `LGPL-3.0-only` 兼容的许可证白名单。
- TLS 和大多数运行时加密通过 Rust 的 [aws-lc-rs](https://github.com/aws/aws-lc-rs) 使用 AWS-LC。
- Ed25519 签名使用 [ed25519-dalek](https://github.com/dalek-cryptography/curve25519-dalek)。
- 在 pre-commit 阶段，Gitleaks 扫描密钥泄露，Zizmor 审计 GitHub Actions。
- CODEOWNERS 要求对关键基础设施、依赖清单和锁文件进行审查。
- 受保护分支要求签名提交并通过 CI。
- CodeQL 在向 `master` 发起的发布 PR 和推送到 `nightly` 时运行。
- 与审计相关的 PR 和每日审计会运行 `cargo-audit`、`cargo-deny` 和 `cargo-vet`。
- OSV Scanner 和 `pip-audit` 也会在与审计相关的 PR 上以及每天运行。
- `cargo-fuzz` 模糊测试覆盖部分适配器和签名接口。
- GitHub Actions 固定到提交 SHA；加固的 CI 运行器将网络出口限制在白名单内。
- Python 产物附带 SLSA 构建来源证明。
- 容器镜像使用 Sigstore 签名，并附带经过证明的 SPDX SBOM。
- PyPI 和 crates.io 通过受保护的 `release` 环境使用 OIDC 可信发布。
- `release` 环境从不运行 PR 或 fork 的代码。
- 发布标签不可更改。

OpenSSF Scorecard 在人工审查、CI 加固和安全审计之外，提供自动化的仓库健康度信号。

### 报告漏洞

请通过 [GitHub Security Advisories](https://github.com/nautechsystems/nautilus_trader/security/advisories/new) 私下报告，或发送邮件至 <security@nautechsystems.io>（可应要求提供 PGP 密钥）。

- 我们会在 48 小时内确认收到报告，并在 30 天内修复严重漏洞。
- 除非报告者希望匿名，否则我们会在相关公告和发布说明中致谢并署名。

详情请参阅：

- [安全策略](SECURITY.md)：范围、协调披露以及逐步的发布验证。
- [安全架构](docs/developer_guide/security.md)：从构建到发布的供应链。
- [负责任披露](https://nautilustrader.io/security/responsible-disclosure/)：完整的披露政策。
- [供应链安全](https://nautilustrader.io/security/supply-chain/)：完整的供应链政策。
- [CI/CD 安全](.github/OVERVIEW.md#security)：GitHub Actions 的安全控制。

## 版本与发布

> [!WARNING]
>
> **NautilusTrader 仍在积极开发中**。部分功能可能尚不完整；虽然 API 正变得越来越稳定，但不同版本之间仍可能出现不兼容的变更。
> 我们会**尽力**在发布说明中记录这些变更。

我们力争遵循**每两周发布一次**的节奏，但实验性或较大的功能可能会导致延期。

### 分支

我们力求所有分支都保持稳定、构建通过。

- `master`：对应最新发布版本的源代码；推荐用于生产环境。
- `nightly`：`develop` 分支的每日快照，用于早期测试；在 **14:00 UTC** 以及需要时合并。
- `develop`：面向贡献者和功能开发的活跃开发分支。

> [!NOTE]
>
> v2 发布候选版本是迈向 **2.x 版本稳定 API** 的过渡。
> 达到这一里程碑后，我们计划为所有 API 变更实施正式的弃用流程。
> 这种方式让我们目前能保持快速的开发节奏。

## 精度模式

NautilusTrader 为其核心值类型（`Price`、`Quantity`、`Money`）支持两种精度模式，它们的内部位宽和最大小数精度不同。

- **高精度**：128 位整数，最多 16 位小数精度，数值范围更大。
- **标准精度**：64 位整数，最多 9 位小数精度，数值范围较小。

> [!NOTE]
>
> 默认情况下，官方 Python wheel 在所有支持的平台上均以高精度（128 位）模式发布。
>
> 对于纯 Rust crate，高精度模式在所有平台（包括 Windows）上都可用，因为 Rust 通过软件模拟处理 `i128`/`u128`。除非显式启用 `high-precision` 特性标志，否则默认使用标准精度。

更多详情请参阅[安装指南](https://nautilustrader.io/docs/latest/getting_started/installation)。

**Rust 特性标志**：要在 Rust 中启用高精度模式，请在 Cargo.toml 中添加 `high-precision` 特性：

```toml
[dependencies]
nautilus-model = { version = "*", features = ["high-precision"] }
```

## 安装

我们建议使用最新的受支持 Python 版本，并在虚拟环境中安装 [nautilus_trader](https://pypi.org/project/nautilus_trader/)，以隔离依赖。

**支持两种安装方式**：

1. 从 PyPI *或* Nautech Systems 包索引安装预编译的二进制 wheel。
2. 从源码构建。

> [!TIP]
>
> 我们强烈建议使用 [uv](https://docs.astral.sh/uv) 包管理器配合“原版” CPython 进行安装。
>
> Conda 和其他 Python 发行版*可能*可用，但不受官方支持。

### 从 PyPI 安装

本仓库和[文档](https://nautilustrader.io/docs/latest)针对的是 v2。要使用 Python 的 pip 包管理器从 PyPI 安装 v2 发布候选版 wheel：

```bash
pip install -U nautilus_trader --pre
```

v2 发布候选版 wheel 使用 `2.0.0rcN` 版本号，用于在最终 `2.0.0` 发布之前供社区测试。我们不建议在生产环境（例如控制真实资金的实盘交易）中使用发布候选版。

在 `2.0.0` 发布之前，必须使用 `--pre` 参数。否则 pip 会安装最新的稳定版 v1 wheel，其 Python API 与 v2 文档不同：

```bash
# Installs the latest stable v1 wheel, which cannot run the v2 documentation
pip install -U nautilus_trader
```

使用 `visualization` 额外依赖，安装交互式业绩报告（tearsheet）和图表所需的可选依赖：

```bash
pip install -U "nautilus_trader[visualization]" --pre
```

详情请参阅[安装指南](https://nautilustrader.io/docs/latest/getting_started/installation#extras)。

### 从 Nautech Systems 包索引安装

Nautech Systems 包索引（`packages.nautechsystems.io`）符合 [PEP-503](https://peps.python.org/pep-0503/) 规范，同时托管 `nautilus_trader` 的稳定版和开发版二进制 wheel。用户可以借此安装最新稳定版，或安装预发布版本进行测试。

#### 稳定版 wheel

稳定版 wheel 与 PyPI 上 `nautilus_trader` 的正式发布版本对应，使用标准版本号。

安装最新稳定版：

```bash
pip install -U nautilus_trader --index-url=https://packages.nautechsystems.io/simple
```

> [!TIP]
>
> 使用 `--extra-index-url` 代替 `--index-url`，即可同时搜索 PyPI 和 Nautech Systems 包索引。
> pip 会在两个索引中选择最匹配的版本，不会优先考虑任何一个索引。

#### 开发版 wheel

主包索引会发布来自 `nightly` 和 `develop` 两个分支的 v2 开发版 wheel，让用户可以在稳定版发布之前测试新功能和修复。

这一流程还有助于节省计算资源，方便获取 CI 流水线中测试过的确切二进制文件，同时遵循 [PEP-440](https://peps.python.org/pep-0440/) 版本规范：

- `develop` wheel 使用版本后缀 `.devYYYYMMDD+run`。
- `nightly` wheel 在基础版本已是预发布版本时使用 `.devYYYYMMDD`，否则使用 `aYYYYMMDD`。

| 平台               | Develop | Nightly |
| :----------------- | :------ | :------ |
| `Linux (x86_64)`   | ✓       | ✓       |
| `Linux (ARM64)`    | -       | ✓       |
| `macOS (ARM64)`    | -       | ✓       |
| `Windows (x86_64)` | -       | ✓       |

> [!WARNING]
>
> 我们不建议在生产环境（例如控制真实资金的实盘交易）中使用开发版 wheel。

#### 安装命令

默认情况下，pip 会安装最新稳定版。添加 `--pre` 参数可确保考虑预发布版本，包括开发版 wheel。

安装最新的可用预发布版本（包括开发版 wheel）：

```bash
pip install -U nautilus_trader --pre --index-url=https://packages.nautechsystems.io/simple
```

#### 可用版本

你可以在[包索引](https://packages.nautechsystems.io/simple/nautilus-trader/index.html)上查看 `nautilus_trader` 的所有可用版本。

以编程方式获取并列出可用版本：

```bash
curl -s https://packages.nautechsystems.io/simple/nautilus-trader/index.html | sed -n 's/.*<a href="\([^"]*\)".*/\1/p' | awk -F'#' '{print $1}' | sort
```

> [!IMPORTANT]
>
> 在 Linux 上安装二进制 wheel 之前，请用 `ldd --version` 确认 glibc 版本为 **2.35** 或更高。

#### 分支更新

- `develop` 分支 wheel（`.devYYYYMMDD+run`）：每次合并提交都会持续构建和发布。
- `nightly` 分支 wheel（`.devYYYYMMDD` 或 `aYYYYMMDD`）：每天在 **14:00 UTC** 自动合并 `develop` 分支时（如有变更）构建和发布。

#### 保留策略

- `develop` 分支 wheel：只保留最近一次构建的 wheel。
- `nightly` 分支 wheel：每个平台只保留最近 30 个发布日期的 wheel。

#### 验证构建来源

项目发布的所有产物都附带由 CI/CD 流水线生成的加密证明：

- Python wheel 和源码分发包（PyPI、GitHub Releases、Nautech Systems 包索引）：[SLSA](https://slsa.dev/) 构建来源证明。
- Docker 镜像（`ghcr.io/nautechsystems/nautilus_trader`、`ghcr.io/nautechsystems/jupyterlab`）：无密钥 [cosign](https://github.com/sigstore/cosign) 签名以及 SPDX SBOM 证明。

两者均通过 [Sigstore](https://www.sigstore.dev/) 签发，并绑定到特定的提交 SHA，因此验证可以确保产物由 NautilusTrader 官方 GitHub Actions 工作流生成，且此后未被篡改。

逐步的验证命令请参阅 `SECURITY.md` 中的[验证发布](SECURITY.md#verifying-releases)。

> [!IMPORTANT]
>
> 验证 Python 产物需要 [GitHub CLI](https://cli.github.com/)（`gh`），验证 Docker 镜像需要 [cosign](https://github.com/sigstore/cosign)。
> 来自 `develop` 和 `nightly` 分支的开发版 wheel 同样附带证明。

### 从源码安装

如果先安装了 `pyproject.toml` 中指定的构建依赖，就可以使用 pip 从源码安装。

1. 安装 [rustup](https://rustup.rs/)（Rust 工具链安装器）：
   - Linux 和 macOS：

       ```bash
       curl https://sh.rustup.rs -sSf | sh
       ```

   - Windows：
       - 下载并安装 [`rustup-init.exe`](https://win.rustup.rs/x86_64)
       - 使用 [Build Tools for Visual Studio 2022](https://visualstudio.microsoft.com/visual-cpp-build-tools/) 安装“使用 C++ 的桌面开发”
   - 验证（任意系统）：
       在终端中运行：`rustc --version`

2. 在当前 shell 中启用 `cargo`：
   - Linux 和 macOS：

       ```bash
       source $HOME/.cargo/env
       ```

   - Windows:
   - Windows：
     - 打开一个新的 PowerShell

3. 安装 [clang](https://clang.llvm.org/)（LLVM 的 C 语言前端）：
   - Linux（同时安装 [lld](https://lld.llvm.org/)，用作 Rust 链接器以加快构建）：

       ```bash
       sudo apt-get install clang lld
       ```

   - macOS:
   - macOS：

       ```bash
       xcode-select --install
       ```

   - Windows：
       1. 在 [Build Tools for Visual Studio 2022](https://visualstudio.microsoft.com/visual-cpp-build-tools/) 中添加 Clang：
          - 开始 | Visual Studio Installer | 修改 | 勾选 C++ Clang tools for Windows (latest) | 修改
       2. 在当前 shell 中启用 `clang`：

          ```powershell
          [System.Environment]::SetEnvironmentVariable('path', "C:\Program Files\Microsoft Visual Studio\2022\BuildTools\VC\Tools\Llvm\x64\bin\;" + $env:Path,"User")
          ```

   - 验证（任意系统）：
       在终端中运行：`clang --version`

4. 安装 uv（更多细节请参阅 [uv 安装指南](https://docs.astral.sh/uv/getting-started/installation)）：

    - Linux 和 macOS：

        ```bash
        curl -LsSf https://astral.sh/uv/install.sh | sh
        ```

    - Windows（PowerShell）：

        ```powershell
        irm https://astral.sh/uv/install.ps1 | iex
        ```

5. 用 `git` 克隆源码，然后在项目根目录同步依赖：

    ```bash
    git clone --branch develop --depth 1 https://github.com/nautechsystems/nautilus_trader
    cd nautilus_trader
    make sync
    ```

> [!NOTE]
>
> `--depth 1` 参数只获取最新的提交，克隆更快、更轻量。

6. 使用 uv 项目环境。

    uv 项目环境位于 `python/.venv`，与 `python/pyproject.toml` 相邻。请在 `python/` 目录下直接运行 uv 项目命令，或在仓库根目录传入 `--project python`。

    在 Linux 和 macOS 上进行 PyO3 编译时，请在 `make sync` 之后于仓库根目录、在 Bash 或 Zsh 中运行以下命令。Fish 的命令请参阅开发者指南中的[环境设置](docs/developer_guide/environment_setup.md#4-configure-environment-variables)。在每个 shell 中将 `PYO3_PYTHON` 设置为本仓库的 `python/.venv/bin/python`；如果之前保存的 export 仍指向根目录的 `.venv/bin/python`，请替换掉。

    ```bash
    # Set the Python executable path for PyO3
    export PYO3_PYTHON="$PWD/python/.venv/bin/python"

    # Linux only: Set the library path for the uv-managed Python runtime
    PYTHON_LIB_DIR="$("$PYO3_PYTHON" -c 'import sysconfig; print(sysconfig.get_config_var("LIBDIR"))')"
    export LD_LIBRARY_PATH="$PYTHON_LIB_DIR${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}"

    # Required for Rust tests when using uv-installed Python
    export PYTHONHOME="$("$PYO3_PYTHON" -c 'import sys; print(sys.base_prefix)')"
    ```

> [!NOTE]
>
> `LD_LIBRARY_PATH` 的 export 仅适用于 Linux，macOS 上不需要。
>
> 使用 `uv` 安装的 Python 运行 `make cargo-test` 时，需要设置 `PYTHONHOME` 变量。
> 否则，依赖 PyO3 的测试可能找不到 Python 运行时。

7. 以 release 模式构建并安装 NautilusTrader：

    ```bash
    make build
    ```

其他选项和更多细节请参阅[安装指南](https://nautilustrader.io/docs/latest/getting_started/installation)。

## Redis

在 NautilusTrader 中使用 [Redis](https://redis.io) 是**可选的**，仅在将其配置为[缓存](https://nautilustrader.io/docs/latest/concepts/cache)数据库或[消息总线](https://nautilustrader.io/docs/latest/concepts/message_bus)的后端时才需要。更多详情请参阅[安装指南](https://nautilustrader.io/docs/latest/getting_started/installation#redis)的 **Redis** 部分。

## Makefile

项目提供了一个 `Makefile`，用于自动化大部分开发相关的安装和构建任务。部分目标包括：

- `make install`：以 `release` 构建模式安装，包含所有依赖组和额外依赖。
- `make install-debug`：与 `make install` 相同，但使用 `debug` 构建模式。
- `make sync`：安装 Python 依赖，但不构建包。
- `make build`：以 `release` 模式（默认）构建并安装包。
- `make build-debug`：以 `debug` 模式构建并安装包。
- `make build-wheel`：以 `release` 模式构建 wheel。
- `make cargo-test`：使用 `cargo-nextest` 运行所有 Rust crate 测试。
- `make clean`：删除构建产物、缓存和构建目录。
- `make distclean`：**注意** 使用 `FORCE=1` 运行时，会删除所有不在 git 索引中的产物，包括尚未 `git add` 的源文件。
- `make docs`：用 Sphinx 构建 Python 文档，用 Cargo 构建 Rust 文档。
- `make pre-commit`：对所有文件运行 pre-commit 检查。
- `make ruff`：使用 `python/pyproject.toml` 对所有文件运行 Ruff（自动修复）。
- `make pytest`：使用 `pytest` 运行所有测试。
- `make cargo-ci-benches`：构建 CI 使用的 Rust 基准测试。
- `make cargo-codspeed-build`：构建用于 CodSpeed 对比的 Rust 基准测试子集。

> [!TIP]
>
> 运行 `make help` 可查看所有可用 make 目标的说明。

> [!TIP]
>
> 运行基础设施集成测试的方法，请参阅 [crates/infrastructure/TESTS.md](https://github.com/nautechsystems/nautilus_trader/blob/develop/crates/infrastructure/TESTS.md) 文件。

## 示例

指标和策略可以用 Python 或 Rust 开发。对于性能和延迟敏感的应用，我们推荐使用 Rust。以下是一些示例：

- 通过 PyO3 暴露的[指标](https://github.com/nautechsystems/nautilus_trader/tree/develop/crates/indicators/src/)实现。
- 直接使用 `BacktestEngine` 的[回测](https://github.com/nautechsystems/nautilus_trader/tree/develop/examples/backtest/)示例。
- 用 Rust 编写的 [EMA 交叉回测](https://github.com/nautechsystems/nautilus_trader/blob/develop/crates/backtest/examples/engine_ema_cross.rs)示例。

## Docker

Docker 容器按以下变体标签构建：

- `nautilus_trader:latest` 安装了最新发布版本。
- `nautilus_trader:nightly` 安装了 `nightly` 分支的最新代码。
- `jupyterlab:latest` 安装了最新发布版本，并附带 `jupyterlab` 以及一个带配套数据的回测示例笔记本。
- `jupyterlab:nightly` 安装了 `nightly` 分支的最新代码，并附带 `jupyterlab` 以及一个带配套数据的回测示例笔记本。

可以按如下方式拉取容器镜像：

```bash
docker pull ghcr.io/nautechsystems/<image_variant_tag> --platform linux/amd64
```

运行以下命令即可启动回测示例容器：

```bash
docker pull ghcr.io/nautechsystems/jupyterlab:nightly --platform linux/amd64
docker run -p 8888:8888 ghcr.io/nautechsystems/jupyterlab:nightly
```

然后在浏览器中打开以下地址：

```bash
http://127.0.0.1:8888/lab
```

> [!WARNING]
>
> 示例使用 `log_level="ERROR"`，因为 Nautilus 的日志输出会超过 Jupyter 的 stdout 速率限制，导致笔记本在较低日志级别下卡住。

## 开发

我们力求为这个 Rust 与 Python 混合的代码库提供尽可能愉快的开发体验。有用的信息请参阅[开发者指南](https://nautilustrader.io/docs/latest/developer_guide/)。

[Nautilus Engineering](https://github.com/nautechsystems/nautilus_engineering) 维护着 Nautilus 各项目共享的工程规范、lint 配置、pre-commit 定义、工具版本锁定和仓库检查。本仓库按 `.nautilus-engineering.lock` 中记录的版本引入了部分文件；项目特定的策略和 CI 配置仍保留在本地。

> [!TIP]
>
> Rust 代码修改后，运行 `make build-debug` 进行编译，是最高效的开发工作流。

修改 PyO3 绑定、存根注解或被包装的 Rust 文档后，请在仓库根目录重新生成 Python 产物：

```bash
make py-stubs
```

请提交该目标所修改的 `.pyi` 文件和 PyO3 包装文档注释。详情请参阅[生成的 Python 产物](docs/developer_guide/rust.md#generated-python-artifacts)。

### 使用 Rust 进行测试

[cargo-nextest](https://nexte.st) 是 NautilusTrader 的标准 Rust 测试运行器。它的主要优点是将每个测试隔离在独立的进程中，避免相互干扰，从而保证测试的可靠性。关于完整测试套件的支持以及普通 `cargo test` 的局限，请参阅 [Rust 测试指南](docs/developer_guide/testing.md#rust-tests)。

运行以下命令即可安装 cargo-nextest：

```bash
cargo install cargo-nextest
```

> [!TIP]
>
> 使用 `make cargo-test` 运行 Rust 测试，它会以高效的配置使用 **cargo-nextest**。

## 参与贡献

感谢你考虑为 NautilusTrader 做出贡献。我们欢迎能改进项目的高质量工作。在开始较大的改动之前，请先提交 [issue](https://github.com/nautechsystems/nautilus_trader/issues)，与团队讨论问题和方案。小型、独立的修复无需事先沟通。

开始之前，请务必查看项目路线图中列出的[开源范围](https://github.com/nautechsystems/nautilus_trader/blob/develop/ROADMAP.md#open-source-scope)，了解哪些在范围之内、哪些不在。

准备开始贡献时，请务必遵循 [CONTRIBUTING.md](https://github.com/nautechsystems/nautilus_trader/blob/develop/CONTRIBUTING.md) 文件中的指南，其中包括签署贡献者许可协议（CLA），以确保你的贡献能被纳入项目。

> [!NOTE]
>
> Pull request 应以 `develop` 分支（默认分支）为目标。新功能和改进在发布前都会合并到这里。

再次感谢你对 NautilusTrader 的关注！我们期待审阅你的贡献，与你一起改进这个项目。

## 社区

欢迎加入我们在 [Discord](https://discord.gg/NautilusTrader) 上的用户和贡献者社区，交流讨论并及时了解 NautilusTrader 的最新公告和功能。无论你是想参与贡献的开发者，还是只想进一步了解这个平台，都欢迎来我们的 Discord 服务器。

被[开源范围](https://github.com/nautechsystems/nautilus_trader/blob/develop/ROADMAP.md#out-of-scope)排除的功能和集成，也不在 NautilusTrader 官方渠道（包括 GitHub 和 Discord）的讨论范围之内。这包括关于下游实现的 “Show & Tell” 帖子，即使不提供贡献、也不请求支持或合入上游。关于核心交易引擎正确性和性能的报告仍然欢迎，但请聚焦于核心行为。

> [!WARNING]
>
> NautilusTrader 不发行、推广或背书任何加密货币代币。任何与此相反的声明或信息都是未经授权且虚假的。
>
> NautilusTrader 的所有官方更新和通知仅通过 <https://nautilustrader.io>、我们的 [GitHub](https://github.com/nautechsystems)、我们的 [Discord 服务器](https://discord.gg/NautilusTrader) 或我们经过认证的 X（Twitter）账号 [@NautilusTrader](https://x.com/NautilusTrader) 发布。
>
> 如果你遇到任何可疑活动，请向相应平台举报，并通过 <info@nautechsystems.io> 联系我们。

## 许可证

NautilusTrader 的源代码在 GitHub 上以 [GNU 宽通用公共许可证 v3.0（LGPL-3.0）](https://www.gnu.org/licenses/lgpl-3.0.en.html)发布。欢迎为项目做出贡献，但需要签署标准的[贡献者许可协议（CLA）](https://github.com/nautechsystems/nautilus_trader/blob/develop/CLA.md)。

---

NautilusTrader™ 由 Nautech Systems 开发和维护，这是一家专注于开发高性能交易系统的科技公司。更多信息请访问 <https://nautilustrader.io>。

使用本软件须遵守[免责声明](https://nautilustrader.io/legal/disclaimer/)。

© 2015-2026 Nautech Systems Pty Ltd. 保留所有权利。


![nautechsystems](https://github.com/nautechsystems/nautilus_trader/raw/develop/assets/ns-logo.png "nautechsystems")
<img src="https://github.com/nautechsystems/nautilus_trader/raw/develop/assets/ferris.png" alt="Ferris" width="128">
