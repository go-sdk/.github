# Go SDK

Minimal, focused Go modules for building services and applications with consistent
configuration, logging, lifecycle, database, and transport conventions.

Each module can be used independently. For projects that adopt the complete stack,
`app` provides a convention-based runtime that assembles the lower-level modules and
keeps application entry points small.

## Projects

| Project                                            | Purpose                                                                                                                                                                                                                                                                            | Docs                                                  |
|----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)           | Foundation utilities for configuration, logging, errors, lifecycle, command-line applications, HTTP clients, codecs, IDs, and tests.                                                                                                                                               | [Doc](https://pkg.go.dev/github.com/go-sdk/core)      |
| [`database`](https://github.com/go-sdk/database)   | GORM toolkit for MySQL, PostgreSQL, and SQLite with opt-in drivers, unified logging, connection-pool configuration, versioned migrations, cross-replica locks, JSON fields, millisecond soft deletes, and a Redis client.                                                          | [Doc](https://pkg.go.dev/github.com/go-sdk/database)  |
| [`server`](https://github.com/go-sdk/server)       | gRPC and grpc-gateway server on one port with shared request context, structured responses, JWT authentication, Protovalidate, i18n, recovery, TLS, health checks, and graceful shutdown.                                                                                          | [Doc](https://pkg.go.dev/github.com/go-sdk/server)    |
| [`taskkit`](https://github.com/go-sdk/taskkit)     | Go task library built on gocron v2, providing an auto-started dynamic job manager with cron, interval, and one-off schedules, per-job context with run IDs, unified logging and panic recovery, optional distributed locking, and a generic bounded-concurrency parallel executor. | [Doc](https://pkg.go.dev/github.com/go-sdk/taskkit)   |
| [`certkit`](https://github.com/go-sdk/certkit)     | X.509 certificate and key store toolkit for parsing, merging, conversion, issuance, revocation checking, trust-root construction, and per-version TLS inspection, supporting RSA, ECDSA, and SM2.                                                                                  | [Doc](https://pkg.go.dev/github.com/go-sdk/certkit)   |
| [`weclawbot`](https://github.com/go-sdk/weclawbot) | Go SDK for the WeChat ClawBot HTTP JSON protocol, providing QR-code login, long-polling message updates, and text message sending.                                                                                                                                                 | [Doc](https://pkg.go.dev/github.com/go-sdk/weclawbot) |
| [`app`](https://github.com/go-sdk/app)             | Convention-based integration layer for `core`, `database`, `server`, and `taskkit`, including global configuration, database and Redis access, migration and bootstrap registration, transport and task registration, and process lifecycle.                                       | [Doc](https://pkg.go.dev/github.com/go-sdk/app)       |
| [`example`](https://github.com/go-sdk/example)     | Reference application using `app`: Proto-driven PostgreSQL RBAC APIs, file routes, migrations, Docker Compose, generated Gateway bindings, and OpenAPI output.                                                                                                                     | [Doc](https://pkg.go.dev/github.com/go-sdk/example)   |

## Versions

| Project                                            | Version                                                                                                               | Last Commit                                                                                         |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)           | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/core?include_prereleases&sort=semver&style=flat-square)      | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/core?style=flat-square)      |
| [`database`](https://github.com/go-sdk/database)   | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/database?include_prereleases&sort=semver&style=flat-square)  | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/database?style=flat-square)  |
| [`server`](https://github.com/go-sdk/server)       | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/server?include_prereleases&sort=semver&style=flat-square)    | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/server?style=flat-square)    |
| [`taskkit`](https://github.com/go-sdk/taskkit)     | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/taskkit?include_prereleases&sort=semver&style=flat-square)   | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/taskkit?style=flat-square)   |
| [`certkit`](https://github.com/go-sdk/certkit)     | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/certkit?include_prereleases&sort=semver&style=flat-square)   | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/certkit?style=flat-square)   |
| [`weclawbot`](https://github.com/go-sdk/weclawbot) | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/weclawbot?include_prereleases&sort=semver&style=flat-square) | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/weclawbot?style=flat-square) |
| [`app`](https://github.com/go-sdk/app)             | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/app?include_prereleases&sort=semver&style=flat-square)       | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/app?style=flat-square)       |

## Choose a Starting Point

- Use [`app`](https://github.com/go-sdk/app) when a service can adopt the standard
  configuration, database, migration, server, and lifecycle conventions.
- Compose [`core`](https://github.com/go-sdk/core),
  [`database`](https://github.com/go-sdk/database), and
  [`server`](https://github.com/go-sdk/server) directly when the application needs a
  custom runtime or only part of the stack.
- Start from [`example`](https://github.com/go-sdk/example) when you want a complete,
  working project structure rather than isolated API examples.
- Add [`taskkit`](https://github.com/go-sdk/taskkit) to any stack when a service
  needs scheduled or dynamically managed jobs, or bounded-concurrency parallel
  execution.
- Add [`certkit`](https://github.com/go-sdk/certkit) to any stack when a service
  needs certificate handling, key stores, revocation checking, or TLS inspection.
- Add [`weclawbot`](https://github.com/go-sdk/weclawbot) to any stack when a service
  needs WeChat ClawBot integration via QR-code login, message polling, or text sending.

## Architecture

```text
example ──> app ──┬──> core
                  ├──> database ──> core
                  ├──> server ────> core
                  └──> taskkit ───> core

certkit ──> core

weclawbot ──> core

custom applications may also depend on core, database, or server directly
```

`server` and `database` remain independent, and `taskkit`, `certkit`, and
`weclawbot` depend only on `core`.
`app` intentionally couples them with `core` for applications that prefer one
standard startup and shutdown path.

## Getting Started

All modules require Go 1.27 or newer.

For a convention-based application:

```bash
go get github.com/go-sdk/app@latest
```

Keep the executable entry point declarative and import only the database driver the
application actually uses:

```go
package main

import (
	"github.com/go-sdk/app"
	_ "github.com/go-sdk/database/dbx/postgres"

	_ "example/internal/migration"
	_ "example/internal/route"
	_ "example/internal/service"
)

func main() {
	app.Main()
}
```

See the [`app` documentation](https://github.com/go-sdk/app#readme) for registration
and configuration details, or the
[`example` repository](https://github.com/go-sdk/example#readme) for an end-to-end
implementation.

For standalone modules:

```bash
go get github.com/go-sdk/core@latest
go get github.com/go-sdk/database@latest
go get github.com/go-sdk/server@latest
go get github.com/go-sdk/taskkit@latest
go get github.com/go-sdk/certkit@latest
go get github.com/go-sdk/weclawbot@latest
```

## Design Principles

- **Minimal** — keep APIs small and dependencies intentional.
- **Consistent** — share conventions for configuration, context, logging, errors, and
  lifecycle.
- **Composable** — use individual modules or adopt the integrated application runtime.
- **Explicit** — import database drivers and register migrations, transports, and
  application initialization deliberately.
- **Practical** — provide useful defaults while keeping important behavior configurable.
- **Modern Go** — target current Go releases and standard-library capabilities.

## Community

Questions, ideas, and feedback are welcome in
[GitHub Discussions](https://github.com/orgs/go-sdk/discussions).

---

# Go SDK 中文

一组精简、专注的 Go 模块，用统一的配置、日志、生命周期、数据库和传输层约定构建服务与应用。

每个模块都可以独立使用。对于采用完整技术栈的项目，`app` 提供约定式运行时，负责组装底层模块，
让应用入口保持简洁。

## 项目

| 项目                                               | 定位                                                                                                                                                                    | 文档                                                   |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)           | 基础工具库，提供配置、日志、错误处理、生命周期、命令行、HTTP 客户端、编解码、ID 和测试辅助。                                                                            | [文档](https://pkg.go.dev/github.com/go-sdk/core)      |
| [`database`](https://github.com/go-sdk/database)   | 基于 GORM 的 MySQL、PostgreSQL 和 SQLite 工具库，提供按需驱动、统一日志、连接池配置、版本迁移、跨副本锁、JSON 字段、毫秒软删除和 Redis 客户端。                         | [文档](https://pkg.go.dev/github.com/go-sdk/database)  |
| [`server`](https://github.com/go-sdk/server)       | 在同一端口提供 gRPC 和 grpc-gateway，统一请求上下文、响应结构、JWT 鉴权、Protovalidate、国际化、Recovery、TLS、健康检查和优雅停止。                                     | [文档](https://pkg.go.dev/github.com/go-sdk/server)    |
| [`taskkit`](https://github.com/go-sdk/taskkit)     | 基于 gocron v2 的任务基础类库，提供自动启动的动态任务管理器，支持 Cron、间隔和一次性调度、任务级 Context、统一日志与 panic 恢复、可选分布式锁，以及泛型受控并发执行器。 | [文档](https://pkg.go.dev/github.com/go-sdk/taskkit)   |
| [`certkit`](https://github.com/go-sdk/certkit)     | 统一的 X.509 证书工具包，支持证书、私钥、密钥库的解析、合并、转换、签发、吊销检查、信任根、TLS 分版本探测，覆盖 RSA、ECDSA 和 SM2。                                     | [文档](https://pkg.go.dev/github.com/go-sdk/certkit)   |
| [`weclawbot`](https://github.com/go-sdk/weclawbot) | 微信 ClawBot HTTP JSON 协议的 Go SDK，提供二维码登录、消息长轮询和文本消息发送。                                                                                        | [文档](https://pkg.go.dev/github.com/go-sdk/weclawbot) |
| [`app`](https://github.com/go-sdk/app)             | `core`、`database`、`server` 和 `taskkit` 的约定式整合层，统一全局配置、数据库与 Redis 访问、迁移与 Bootstrap、传输层与任务注册和进程生命周期。                         | [文档](https://pkg.go.dev/github.com/go-sdk/app)       |
| [`example`](https://github.com/go-sdk/example)     | 基于 `app` 的完整参考项目，包含 Proto 驱动的 PostgreSQL RBAC API、文件路由、迁移、Docker Compose、Gateway 生成代码和 OpenAPI。                                          | [文档](https://pkg.go.dev/github.com/go-sdk/example)   |

## 版本

| 项目                                               | 版本                                                                                                                  | 最近提交                                                                                            |
|----------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)           | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/core?include_prereleases&sort=semver&style=flat-square)      | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/core?style=flat-square)      |
| [`database`](https://github.com/go-sdk/database)   | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/database?include_prereleases&sort=semver&style=flat-square)  | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/database?style=flat-square)  |
| [`server`](https://github.com/go-sdk/server)       | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/server?include_prereleases&sort=semver&style=flat-square)    | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/server?style=flat-square)    |
| [`taskkit`](https://github.com/go-sdk/taskkit)     | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/taskkit?include_prereleases&sort=semver&style=flat-square)   | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/taskkit?style=flat-square)   |
| [`certkit`](https://github.com/go-sdk/certkit)     | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/certkit?include_prereleases&sort=semver&style=flat-square)   | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/certkit?style=flat-square)   |
| [`weclawbot`](https://github.com/go-sdk/weclawbot) | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/weclawbot?include_prereleases&sort=semver&style=flat-square) | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/weclawbot?style=flat-square) |
| [`app`](https://github.com/go-sdk/app)             | ![GitHub Tag](https://img.shields.io/github/v/tag/go-sdk/app?include_prereleases&sort=semver&style=flat-square)       | ![GitHub last commit](https://img.shields.io/github/last-commit/go-sdk/app?style=flat-square)       |

## 如何选择

- 服务可以接受统一的配置、数据库、迁移、Server 和生命周期约定时，优先使用
  [`app`](https://github.com/go-sdk/app)。
- 需要自定义运行时或只需要部分能力时，直接组合
  [`core`](https://github.com/go-sdk/core)、
  [`database`](https://github.com/go-sdk/database) 和
  [`server`](https://github.com/go-sdk/server)。
- 希望从完整项目结构开始，而不是只查看零散 API 示例时，参考
  [`example`](https://github.com/go-sdk/example)。
- 需要定时或动态管理的任务以及受控并发执行时，加入
  [`taskkit`](https://github.com/go-sdk/taskkit)。
- 需要在任意方案中处理证书、密钥库、吊销检查或 TLS 探测时，加入
  [`certkit`](https://github.com/go-sdk/certkit)。
- 需要通过二维码登录、消息长轮询或文本发送接入微信 ClawBot 时，加入
  [`weclawbot`](https://github.com/go-sdk/weclawbot)。

## 架构

```text
example ──> app ──┬──> core
                  ├──> database ──> core
                  ├──> server ────> core
                  └──> taskkit ───> core

certkit ──> core

weclawbot ──> core

自定义应用也可以直接依赖 core、database 或 server
```

`server` 与 `database` 保持相互独立，`taskkit`、`certkit` 和 `weclawbot` 只依赖 `core`。
`app` 则有意将它们与 `core` 整合，为应用提供统一的启动和停止链路。

## 快速开始

全部模块要求 Go 1.27 或更高版本。

创建约定式应用：

```bash
go get github.com/go-sdk/app@latest
```

应用入口只声明业务注册包，并按需导入实际使用的数据库驱动：

```go
package main

import (
	"github.com/go-sdk/app"
	_ "github.com/go-sdk/database/dbx/postgres"

	_ "example/internal/migration"
	_ "example/internal/route"
	_ "example/internal/service"
)

func main() {
	app.Main()
}
```

注册方式和默认配置参见 [`app` 文档](https://github.com/go-sdk/app#readme)，完整实现参见
[`example` 项目](https://github.com/go-sdk/example#readme)。

按需安装独立模块：

```bash
go get github.com/go-sdk/core@latest
go get github.com/go-sdk/database@latest
go get github.com/go-sdk/server@latest
go get github.com/go-sdk/taskkit@latest
go get github.com/go-sdk/certkit@latest
go get github.com/go-sdk/weclawbot@latest
```

## 设计原则

- **精简** — 保持 API 简洁，并谨慎引入依赖。
- **一致** — 对配置、上下文、日志、错误和生命周期采用统一约定。
- **可组合** — 既可以独立使用模块，也可以采用整合后的应用运行时。
- **显式** — 数据库驱动、迁移、传输层和业务初始化均由具体项目主动声明。
- **实用** — 提供合理默认行为，同时保留关键配置能力。
- **现代 Go** — 面向当前 Go 版本和标准库能力进行设计。

## 交流

欢迎在 [GitHub Discussions](https://github.com/orgs/go-sdk/discussions) 提问、分享想法和反馈。
