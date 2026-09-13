# Go SDK

A collection of minimal, focused Go libraries for building services and applications.

`go-sdk` provides small, reusable modules with consistent defaults and APIs. Each module is designed to work well on its own while integrating naturally with the rest of the SDK.

## Projects

| Project                                          | Description                                                                            |
|--------------------------------------------------|----------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)         | A minimal Go core library for logging, errors, lifecycle, HTTP clients, JSON, and more |
| [`server`](https://github.com/go-sdk/server)     | A minimal Go service kit for gRPC and grpc-gateway on one port                         |
| [`database`](https://github.com/go-sdk/database) | A minimal Go database kit for GORM with MySQL, PostgreSQL, and SQLite                  |

## Design Principles

- **Minimal** — keep APIs small and dependencies intentional
- **Consistent** — share common conventions for lifecycle, logging, errors, and context
- **Composable** — use each module independently or combine them as needed
- **Practical** — provide sensible defaults while keeping important behavior configurable
- **Modern Go** — target current Go releases and standard library capabilities

## Architecture

`core` provides the common foundation used by higher-level modules. `server` and `database` remain separate so applications can depend only on the functionality they need.

---

# Go SDK 中文

一组用于构建 Go 服务和应用的精简、专注的基础类库。

`go-sdk` 提供一组小型、可复用且具有统一默认行为和 API 风格的模块。每个模块都可以独立使用，同时也能够自然地与 SDK 中的其他模块组合。

## 项目

| 项目                                             | 描述                                                                               |
|--------------------------------------------------|------------------------------------------------------------------------------------|
| [`core`](https://github.com/go-sdk/core)         | 精简的 Go 核心基础类库，提供日志、错误处理、生命周期、HTTP 客户端、JSON 等通用能力 |
| [`server`](https://github.com/go-sdk/server)     | 精简的 Go 服务基础类库，在同一端口提供 gRPC 和 grpc-gateway                        |
| [`database`](https://github.com/go-sdk/database) | 基于 GORM 的精简 Go 数据库基础类库，支持 MySQL、PostgreSQL 和 SQLite               |

## 设计原则

- **精简** — 保持 API 简洁，并谨慎引入依赖
- **一致** — 对生命周期、日志、错误和上下文等基础能力采用统一约定
- **可组合** — 每个模块既可以独立使用，也可以按需组合
- **实用** — 提供合理的默认行为，同时保留关键配置能力
- **现代 Go** — 面向当前 Go 版本和标准库能力进行设计

## 架构

`core` 提供高层模块共享的基础能力。`server` 和 `database` 保持相互独立，使应用只需要依赖实际使用的功能。
