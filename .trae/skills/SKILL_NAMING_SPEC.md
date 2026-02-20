# TestUI Skill 命名规范

## 1. 概述

本文档定义了 TestUI 项目中 Skill 的命名规范，确保所有 Skill 命名一致、清晰，便于管理和维护。

## 2. 命名基本原则

1. **一致性**：所有 Skill 命名应遵循统一的规则
2. **可读性**：命名应清晰易懂，能够快速识别 Skill 的用途和所属模块
3. **唯一性**：每个 Skill 应有唯一的名称，避免冲突
4. **简洁性**：命名应简洁明了，避免过长或复杂的命名

## 3. 一级菜单 Skill 命名规则

### 3.1 命名格式

```
testui-<菜单路由>-page
```

### 3.2 命名说明

- `testui`：固定前缀，标识为 TestUI 项目的 Skill
- `<菜单路由>`：一级菜单的路由地址，使用小写字母，单词间用连字符分隔
- `page`：固定后缀，标识为页面类型的 Skill

### 3.3 示例

| 菜单名称 | 菜单路由 | Skill 名称 |
|---------|---------|-----------|
| 首页 | home | testui-home-page |
| 连接管理 | api_test | testui-api-test-page |
| 单板阶段 | board_stage | testui-board-stage-page |
| 组装阶段 | assemble_stage | testui-assemble-stage-page |
| 统计报告 | statistics | testui-statistics-page |
| 系统设置 | system_settings | testui-system-settings-page |
| 帮助文档 | help_docs | testui-help-docs-page |

## 4. 二级菜单 Skill 命名规则

### 4.1 命名格式

```
testui-<一级菜单路由>-<二级菜单名称>
```

### 4.2 命名说明

- `testui`：固定前缀，标识为 TestUI 项目的 Skill
- `<一级菜单路由>`：所属一级菜单的路由地址，使用小写字母，单词间用连字符分隔
- `<二级菜单名称>`：二级菜单的名称，使用小写字母，单词间用连字符分隔

### 4.3 示例

#### 首页子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 欢迎页面 | 首页 | testui-home-welcome |
| 用户管理 | 首页 | testui-home-user-management |
| 项目管理 | 首页 | testui-home-project-management |

#### 连接管理子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| Modbus-rtu测试 | 连接管理 | testui-api-test-modbus-rtu |
| API测试 | 连接管理 | testui-api-test-api |
| MQTT测试 | 连接管理 | testui-api-test-mqtt |

#### 单板阶段子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 电机驱动板烧录 | 单板阶段 | testui-board-stage-motor-driver-burn |
| 电机驱动板测试 | 单板阶段 | testui-board-stage-motor-driver-test |
| LED&按键板功能测试 | 单板阶段 | testui-board-stage-led-key-test |
| 电机来料测试 | 单板阶段 | testui-board-stage-motor-incoming-test |
| 四手指功能测试 | 单板阶段 | testui-board-stage-four-finger-test |
| 单拇指功能测试 | 单板阶段 | testui-board-stage-single-thumb-test |

#### 组装阶段子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 半成品测试 | 组装阶段 | testui-assemble-stage-semi-finished-test |
| 老化测试 | 组装阶段 | testui-assemble-stage-aging-test |
| 整机测试 | 组装阶段 | testui-assemble-stage-whole-machine-test |
| OTA升级 | 组装阶段 | testui-assemble-stage-ota-upgrade |
| 整机出货检测 | 组装阶段 | testui-assemble-stage-whole-machine-shipment-test |

#### 统计报告子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 生产统计 | 统计报告 | testui-statistics-production-statistics |
| 不良分析- | 统计报告 | testui-statistics-defect-analysis |
| 报表导出 | 统计报告 | testui-statistics-report-export |

#### 系统设置子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 测试参数配置 | 系统设置 | testui-system-settings-test-parameter-config |
| 用户管理 | 系统设置 | testui-system-settings-user-management |
| 系统日志 | 系统设置 | testui-system-settings-system-log |

#### 帮助文档子菜单

| 菜单名称 | 所属一级菜单 | Skill 名称 |
|---------|-------------|-----------|
| 测试指南 | 帮助文档 | testui-help-docs-test-guide |
| 故障排除 | 帮助文档 | testui-help-docs-troubleshooting |
| 系统更新 | 帮助文档 | testui-help-docs-system-update |

## 5. 目录结构

### 5.1 基本结构

```
.trae/
└── skills/
    ├── testui-dev/             # 项目开发指南 Skill
    ├── testui-home-page/        # 首页页面 Skill
    ├── testui-api-test-page/    # 连接管理页面 Skill
    ├── testui-board-stage-page/ # 单板阶段页面 Skill
    ├── testui-assemble-stage-page/ # 组装阶段页面 Skill
    ├── testui-statistics-page/  # 统计报告页面 Skill
    ├── testui-system-settings-page/ # 系统设置页面 Skill
    ├── testui-help-docs-page/   # 帮助文档页面 Skill
    ├── testui-home-welcome/     # 首页-欢迎页面 Skill
    ├── testui-home-user-management/ # 首页-用户管理 Skill
    ├── testui-home-project-management/ # 首页-项目管理 Skill
    ├── testui-api-test-modbus-rtu/ # 连接管理-Modbus-rtu测试 Skill
    ├── testui-api-test-api/     # 连接管理-API测试 Skill
    ├── testui-api-test-mqtt/    # 连接管理-MQTT测试 Skill
    └── ... (其他二级菜单 Skill)
```

### 5.2 目录组织说明

1. 所有 Skill 目录均位于 `.trae/skills/` 目录下
2. 一级菜单 Skill 和二级菜单 Skill 同级存放，通过命名区分
3. 每个 Skill 目录应包含 `SKILL.md` 文件，定义 Skill 的具体内容

## 6. 注意事项

1. **命名大小写**：所有 Skill 名称应使用小写字母，单词间用连字符分隔
2. **特殊字符处理**：菜单名称中的特殊字符（如 &、- 等）应转换为连字符或省略
3. **长度限制**：Skill 名称应尽量简洁，避免过长的命名
4. **一致性检查**：创建新 Skill 前，应检查是否已存在同名或相似的 Skill

## 7. 版本控制

| 版本 | 日期 | 说明 |
|------|------|------|
| 1.0 | 2026-02-20 | 初始版本，定义了一级菜单和二级菜单 Skill 的命名规范 |

## 8. 参考资料

- TestUI 项目菜单配置（menu.md）
- TestUI 项目开发计划（TestUI_plan.md）