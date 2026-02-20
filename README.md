# TestUI 项目说明

## 项目概述

TestUI是一个基于PySide6和qfluentwidgets组件库开发的桌面端测试应用，采用MVVM架构设计，旨在提供一个功能完整、界面美观、交互流畅的测试管理系统。

## 架构设计

### MVVM架构分层

| 层级 | 职责 | 实现方式 |
|------|------|----------|
| **View层** | 仅负责UI渲染（窗口、菜单、按钮等组件），无业务逻辑 | 使用qfluentwidgets提供的组件库 |
| **ViewModel层** | 处理交互逻辑（菜单切换、主题修改、搜索触发），作为View与Model的中间层 | 自定义Python类，处理信号槽 |
| **Model/Service层** | 负责数据处理（配置读取、用户信息获取） | 自定义服务类，处理数据操作 |
| **Infra层** | 封装通用能力（配置解析、主题管理、依赖注入） | 工具类和辅助模块，包括依赖注入容器 |

### 目录结构

```
TestUI/
├── app/
│   ├── view/                # View层：UI组件
│   │   ├── main_window.py   # 主窗口
│   │   ├── menu/            # 菜单组件
│   │   ├── pages/           # 页面组件（一级菜单对应页面）
│   │   │   ├── home_page.py
│   │   │   ├── api_test_page.py
│   │   │   ├── board_stage_page.py
│   │   │   ├── assemble_stage_page.py
│   │   │   ├── statistics_page.py
│   │   │   ├── system_settings_page.py
│   │   │   └── help_docs_page.py
│   │   ├── subpages/        # 子页面组件（二级菜单对应页面）
│   │   │   ├── home/        # 首页子菜单页面
│   │   │   │   ├── welcome_page.py
│   │   │   │   ├── user_management_page.py
│   │   │   │   └── project_management_page.py
│   │   │   ├── api_test/     # 连接管理子菜单页面
│   │   │   │   ├── modbus_rtu_test_page.py
│   │   │   │   ├── api_test_page.py
│   │   │   │   └── mqtt_test_page.py
│   │   │   ├── board_stage/  # 单板阶段子菜单页面
│   │   │   │   ├── motor_driver_burn_page.py
│   │   │   │   ├── motor_driver_test_page.py
│   │   │   │   ├── led_key_test_page.py
│   │   │   │   ├── motor_incoming_test_page.py
│   │   │   │   ├── four_finger_test_page.py
│   │   │   │   └── single_thumb_test_page.py
│   │   │   ├── assemble_stage/  # 组装阶段子菜单页面
│   │   │   │   ├── semi_finished_test_page.py
│   │   │   │   ├── aging_test_page.py
│   │   │   │   ├── whole_machine_test_page.py
│   │   │   │   ├── ota_upgrade_page.py
│   │   │   │   └── whole_machine_shipment_test_page.py
│   │   │   ├── statistics/   # 统计报告子菜单页面
│   │   │   │   ├── production_statistics_page.py
│   │   │   │   ├── defect_analysis_page.py
│   │   │   │   └── report_export_page.py
│   │   │   ├── system_settings/  # 系统设置子菜单页面
│   │   │   │   ├── test_parameter_config_page.py
│   │   │   │   ├── user_management_page.py
│   │   │   │   └── system_log_page.py
│   │   │   └── help_docs/    # 帮助文档子菜单页面
│   │   │       ├── test_guide_page.py
│   │   │       ├── troubleshooting_page.py
│   │   │       └── system_update_page.py
│   │   └── components/      # 通用组件（搜索框、主题调节等）
│   ├── viewmodel/           # ViewModel层：业务逻辑
│   │   ├── main_viewmodel.py
│   │   ├── menu_viewmodel.py
│   │   ├── pages/           # 页面ViewModel
│   │   ├── subpages/        # 子页面ViewModel
│   │   │   ├── home/        # 首页子菜单ViewModel
│   │   │   ├── api_test/     # 连接管理子菜单ViewModel
│   │   │   ├── board_stage/  # 单板阶段子菜单ViewModel
│   │   │   ├── assemble_stage/  # 组装阶段子菜单ViewModel
│   │   │   ├── statistics/   # 统计报告子菜单ViewModel
│   │   │   ├── system_settings/  # 系统设置子菜单ViewModel
│   │   │   └── help_docs/    # 帮助文档子菜单ViewModel
│   │   └── components/      # 组件ViewModel
│   ├── model/               # Model层：数据模型
│   │   ├── menu_model.py
│   │   ├── user_model.py
│   │   └── config_model.py
│   └── service/             # Service层：数据服务
│       ├── config_service.py
│       └── theme_service.py
├── infra/                   # 基础设施层
│   ├── utils/               # 工具类
│   ├── config/              # 配置管理
│   └── di/                  # 依赖注入容器
│       ├── container.py     # 依赖注入容器配置
│       ├── providers.py     # 依赖提供者（单例、工厂等）
│       └── modules/         # 按模块组织的依赖配置
├── res/                     # 资源文件
│   ├── icons/               # 图标
│   └── styles/              # 样式
├── config/                  # 配置文件
│   └── app_config.yml       # 应用配置
├── main.py                  # 应用入口
└── requirements.txt         # 依赖管理
```

## 菜单配置

### 主菜单

| 菜单名称 | 图标文件 | 路由地址 | 显示位置 | 功能说明 |
|---------|---------|---------|---------|--------|
| 首页 | icon_home.svg | home | 顶部 | 系统启动时的首页 |
| 连接管理 | icon_ch_vInput.svg | api_test | 顶部 | 连接管理 |
| 单板阶段 | icon_pcb_32.svg | board_stage | 顶部 | 单板阶段测试 |
| 组装阶段 | icon_blackbox_test.svg | assemble_stage | 顶部 | 组装阶段测试 |
| 统计报告 | icon_report_32.svg | statistics | 顶部 | 统计报告 |
| 系统设置 | icon_settings.svg | system_settings | 顶部 | 系统参数配置、用户管理、日志查看 |
| 帮助文档 | icon_info.svg | help_docs | 底部 | 帮助文档 |

### 子菜单

#### 首页子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 欢迎页面 | 系统启动时的首页 | welcome_page.py |
| 用户管理 | 用户账户管理 | user_management_page.py |
| 项目管理 | 项目信息管理 | project_management_page.py |

#### 连接管理子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| Modbus-rtu测试 | Modbus-rtu通信测试 | modbus_rtu_test_page.py |
| API测试 | 应用程序接口测试 | api_test_page.py |
| MQTT测试 | MQTT消息队列测试 | mqtt_test_page.py |

#### 单板阶段子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 电机驱动板烧录 | 电机驱动板固件烧录 | motor_driver_burn_page.py |
| 电机驱动板测试 | 电机驱动板功能测试 | motor_driver_test_page.py |
| LED&按键板功能测试 | LED指示灯和按键功能测试 | led_key_test_page.py |
| 电机来料测试 | 电机原材料质量检测 | motor_incoming_test_page.py |
| 四手指功能测试 | 四指机械手功能测试 | four_finger_test_page.py |
| 单拇指功能测试 | 单拇指机械手功能测试 | single_thumb_test_page.py |

#### 组装阶段子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 半成品测试 | 产品半成品质量检测 | semi_finished_test_page.py |
| 老化测试 | 产品长时间稳定性测试 | aging_test_page.py |
| 整机测试 | 完整产品功能测试 | whole_machine_test_page.py |
| OTA升级 | 无线固件升级测试 | ota_upgrade_page.py |
| 整机出货检测 | 出货前最终质量检测 | whole_machine_shipment_test_page.py |

#### 统计报告子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 生产统计 | 生产数据统计分析 | production_statistics_page.py |
| 不良分析- | 产品质量不良分析 | defect_analysis_page.py |
| 报表导出 | 测试数据报表导出 | report_export_page.py |

#### 系统设置子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 测试参数配置 | 测试参数配置 | test_parameter_config_page.py |
| 用户管理 | 用户账户管理 | user_management_page.py |
| 系统日志 | 系统运行日志 | system_log_page.py |

#### 帮助文档子菜单
| 菜单名称 | 功能说明 | 页面文件 |
|---------|---------|----------|
| 测试指南 | 测试操作指南 | test_guide_page.py |
| 故障排除 | 常见故障排除 | troubleshooting_page.py |
| 系统更新 | 系统版本更新 | system_update_page.py |

## 页面路由

### 一级菜单路由

| 路由地址 | 页面组件 | 功能说明 |
|---------|---------|--------|
| home | HomePage | 首页页面 - 介绍系统功能，展示欢迎信息和快速访问入口，列出首页子菜单内容 |
| api_test | ApiTestPage | 连接管理页面 - 介绍连接管理功能，列出Modbus-rtu测试、API测试、MQTT测试等子菜单内容 |
| board_stage | BoardStagePage | 单板阶段测试页面 - 介绍单板阶段测试功能，列出电机驱动板烧录、电机驱动板测试等子菜单内容 |
| assemble_stage | AssembleStagePage | 组装阶段测试页面 - 介绍组装阶段测试功能，列出半成品测试、老化测试等子菜单内容 |
| statistics | StatisticsPage | 统计报告页面 - 介绍统计报告功能，列出生产统计、不良分析、报表导出等子菜单内容 |
| system_settings | SystemSettingsPage | 系统设置页面 - 介绍系统设置功能，列出测试参数配置、用户管理、系统日志等子菜单内容 |
| help_docs | HelpDocsPage | 帮助文档页面 - 介绍帮助文档功能，列出测试指南、故障排除、系统更新等子菜单内容 |

### 二级菜单路由

所有二级菜单页面都有对应的路由和页面实现，页面文件名称已在子菜单配置中列出。

## 功能实现

### 基础界面

- 参考 examples 里的 window 示例搭建整体窗口框架
- 使用 qfluentwidgets 组件库实现所有UI组件
- 实现主菜单与子菜单的层级展示
- 添加导航栏和状态栏

### 扩展功能

| 功能 | 位置 | 实现方式 |
|------|------|----------|
| **搜索框** | 顶部区域 | 使用 qfluentwidgets 的搜索组件，支持输入和搜索触发 |
| **主题颜色调节** | 顶部区域 | 使用 qfluentwidgets 的颜色选择器组件，支持预设主题和自定义颜色 |
| **用户信息模块** | 左下角区域 | 使用 qfluentwidgets 的用户信息组件，显示用户名、头像和登录状态 |

### 页面实现

- 所有一级菜单对应页面显示"[页面名称]+开发中"，并介绍对应功能和子菜单内容
- 所有二级菜单对应页面显示"[子菜单名称]+开发中"
- 使用 qfluentwidgets 的页面组件实现统一的页面布局

## 依赖注入实现

### 依赖注入框架

使用 `dependency-injector` 框架实现依赖注入，为应用提供以下功能：

- **单例模式**：为MQTT、Modbus-RTU、SQLite3等资源密集型服务提供单例模式创建上下文
- **工厂模式**：为用户、测试用例等需要动态创建的对象提供工厂模式注入
- **模块组织**：按功能模块组织依赖配置，提高代码可维护性

### 核心容器结构

```python
# infra/di/container.py
from dependency_injector import containers, providers
from .providers import (
    ConfigServiceProvider,
    ThemeServiceProvider,
    MQTTServiceProvider,
    ModbusServiceProvider,
    DatabaseServiceProvider,
    UserServiceProvider,
    TestCaseProvider
)

class Container(containers.DeclarativeContainer):
    """依赖注入容器"""
    # 配置服务（单例）
    config_service = ConfigServiceProvider()
    
    # 主题服务（单例）
    theme_service = ThemeServiceProvider(
        config_service=config_service
    )
    
    # 数据库服务（单例）
    database_service = DatabaseServiceProvider(
        config_service=config_service
    )
    
    # MQTT服务（单例）
    mqtt_service = MQTTServiceProvider(
        config_service=config_service
    )
    
    # Modbus服务（单例）
    modbus_service = ModbusServiceProvider(
        config_service=config_service
    )
    
    # 用户服务（工厂）
    user_service = UserServiceProvider(
        database_service=database_service
    )
    
    # 测试用例提供者（工厂）
    test_case = TestCaseProvider()
```

### 使用示例

```python
# app/viewmodel/main_viewmodel.py
from dependency_injector.wiring import inject, Provide
from infra.di.container import Container

class MainViewModel:
    """主窗口ViewModel"""
    
    @inject
    def __init__(self,
                 config_service=Provide[Container.config_service],
                 theme_service=Provide[Container.theme_service]):
        self.config_service = config_service
        self.theme_service = theme_service
        # 初始化逻辑
```

## 配置管理

### YAML配置文件

使用YAML配置文件管理应用配置，包括应用信息、主题设置、菜单配置等。

### 配置服务

创建专用配置服务类 `ConfigService`，使用 `pyyaml` 库解析YAML文件，提供配置项的获取和更新方法。

## 技术栈

| 技术/框架 | 版本 | 用途 |
|-----------|------|------|
| Python | 3.8+ | 开发语言 |
| PySide6 | 6.0+ | UI框架 |
| qfluentwidgets | 最新版 | UI组件库 |
| PyYAML | 6.0+ | 配置文件解析 |
| dependency-injector | 4.41+ | 依赖注入库 |
| QDarkStyle | 3.0+ | 主题支持（可选） |

## 依赖管理

项目依赖在 `requirements.txt` 文件中定义，包括：

- PySide6>=6.4.2
- PySideSix-Frameless-Window>=0.8.0
- darkdetect
- colorthief
- scipy
- pillow
- dependency-injector>=4.41.0

## 运行项目

1. 安装依赖：
   ```
   pip install -r requirements.txt
   ```

2. 运行应用：
   ```
   python main.py
   ```

## 开发计划

### 开发优先级

1. **搭建基础架构**：创建MVVM目录结构，实现基础框架和依赖注入容器
2. **实现菜单系统**：基于menu.md配置菜单和图标，使用qfluentwidgets组件
3. **开发页面路由**：实现页面切换和路由管理，确保一级和二级菜单都有对应界面
4. **添加扩展功能**：实现搜索框、主题调节、用户信息模块，使用qfluentwidgets组件
5. **集成配置管理**：接入YAML配置文件
6. **优化与测试**：完善功能，测试交互逻辑

### 后续规划

- 实现具体页面内容，替换"开发中"占位提示
- 增加更多自定义主题选项
- 实现用户登录和权限管理
- 集成MQTT、Modbus-RTU、SQLite3等服务
- 优化性能和用户体验
- 添加更多功能模块

## 质量保证

### 代码规范

- 遵循Python PEP8代码规范
- 使用类型注解提高代码可读性
- 编写清晰的文档和注释

### 测试策略

- 功能测试：验证所有功能正常工作
- 界面测试：确保界面美观、交互流畅
- 兼容性测试：确保在不同环境下正常运行

### 性能优化

- 合理使用PySide6的信号槽机制
- 避免不必要的UI更新
- 优化配置文件读取性能
- 合理使用依赖注入，避免过度依赖

## 风险与应对

| 风险 | 影响 | 应对措施 |
|------|------|----------|
| 图标资源缺失 | 界面美观度下降 | 参考res目录补充，或使用系统默认图标 |
| 路由系统复杂度 | 开发时间增加 | 采用简单有效的路由实现方案 |
| 配置文件格式变更 | 系统稳定性影响 | 设计灵活的配置解析机制，支持版本兼容 |
| 主题调节兼容性 | 部分组件样式异常 | 全面测试主题切换效果，确保所有组件兼容 |
| 依赖注入过度使用 | 代码复杂度增加 | 合理使用依赖注入，避免过度设计 |

## 交付标准

- 完整的MVVM架构实现
- 所有菜单和子菜单正确显示
- 页面路由系统正常工作
- 一级菜单页面显示功能介绍和子菜单内容列表
- 二级菜单页面显示"[子菜单名称]+开发中"
- 扩展功能（搜索、主题调节、用户信息）完整实现
- YAML配置文件集成完成
- 依赖注入容器实现，支持单例和工厂模式
- 代码结构清晰，符合规范
- 界面美观，交互流畅

## Skill命名规范

### 一级菜单Skill命名规则

- 格式：`testui-<菜单路由>-page`
- 示例：`testui-home-page`、`testui-api-test-page`等

### 二级菜单Skill命名规则

- 格式：`testui-<一级菜单路由>-<二级菜单名称>`
- 示例：`testui-home-welcome`、`testui-api-test-modbus-rtu`等

### Skill目录结构

所有Skill目录均位于 `.trae/skills/` 目录下，包括7个一级菜单Skill和26个二级菜单Skill，通过命名区分不同类型的Skill。