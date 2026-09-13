# Go SDK

A collection of minimal, focused Go libraries for building services and applications.

`go-sdk` provides small, reusable modules with consistent defaults and APIs. Each module is designed to work well on its own while integrating naturally with the rest of the SDK.

## Projects

| Project                                          | Description                                                                                                                                                                         |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)         | Base library with configuration, logging, errors, lifecycle, HTTP client, JSON and YAML codecs, sequence generation, and test helpers                                               |
| [`server`](https://github.com/go-sdk/server)     | Service kit serving native gRPC and grpc-gateway HTTP on one port, with unified request context, logging, JWT auth, validation, recovery, TLS, and graceful shutdown                |
| [`database`](https://github.com/go-sdk/database) | GORM database kit for MySQL, PostgreSQL, and SQLite, with unified logging, versioned migrations, cross-replica migration locks, JSON fields, and millisecond-timestamp soft deletes |

## Design Principles

- **Minimal** — keep APIs small and dependencies intentional
- **Consistent** — share common conventions for lifecycle, logging, errors, and context
- **Composable** — use each module independently or combine them as needed
- **Practical** — provide sensible defaults while keeping important behavior configurable
- **Modern Go** — target current Go releases and standard library capabilities

## Architecture

`core` provides the common foundation used by higher-level modules. `server` and `database` depend on `core` but remain independent of each other, so applications can depend only on the functionality
they need.

```text
server   ───> core
database ───> core
```

## Getting Started

All modules require Go 1.27 or higher and can be installed with `go get`:

```bash
go get github.com/go-sdk/core
go get github.com/go-sdk/server
go get github.com/go-sdk/database
```

## Community

Questions, ideas, and feedback are welcome in [GitHub Discussions](https://github.com/orgs/go-sdk/discussions).

---

# Go SDK 中文

一组用于构建 Go 服务和应用的精简、专注的基础类库。

`go-sdk` 提供一组小型、可复用且具有统一默认行为和 API 风格的模块。每个模块都可以独立使用，同时也能够自然地与 SDK 中的其他模块组合。

## 项目

| 项目                                             | 描述                                                                                                                               |
|--------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)         | 基础类库，提供配置、日志、错误处理、生命周期、HTTP 客户端、JSON 和 YAML 编解码、序列生成和测试辅助                                 |
| [`server`](https://github.com/go-sdk/server)     | 服务基础类库，在同一端口提供原生 gRPC 和 grpc-gateway HTTP，统一请求上下文、访问日志、JWT 鉴权、参数校验、Recovery、TLS 和优雅停止 |
| [`database`](https://github.com/go-sdk/database) | 基于 GORM 的数据库基础类库，支持 MySQL、PostgreSQL 和 SQLite，统一日志、版本化迁移、跨副本迁移锁、JSON 字段和毫秒时间戳软删除      |

## 设计原则

- **精简** — 保持 API 简洁，并谨慎引入依赖
- **一致** — 对生命周期、日志、错误和上下文等基础能力采用统一约定
- **可组合** — 每个模块既可以独立使用，也可以按需组合
- **实用** — 提供合理的默认行为，同时保留关键配置能力
- **现代 Go** — 面向当前 Go 版本和标准库能力进行设计

## 架构

`core` 提供高层模块共享的基础能力。`server` 和 `database` 都依赖 `core`，但相互独立，使应用只需要依赖实际使用的功能。

```text
server   ───> core
database ───> core
```

## 快速开始

全部模块要求 Go 1.27 或更高版本，可使用 `go get` 安装：

```bash
go get github.com/go-sdk/core
go get github.com/go-sdk/server
go get github.com/go-sdk/database
```

## 交流

欢迎在 [GitHub Discussions](https://github.com/orgs/go-sdk/discussions) 提问、分享想法和反馈。
