# TestUI项目开发计划

## 1. 项目概述

### 1.1 项目目标
基于指定参考文件（menu.md、examples/window 示例），创建名为TestUI的项目，采用MVVM架构实现桌面端UI开发，需满足分层解耦、功能扩展、界面定制三大核心要求。

### 1.2 项目范围
- 搭建完整的MVVM架构框架
- 实现主菜单与子菜单的展示
- 开发基础页面路由系统
- 实现搜索、主题调节、用户信息等扩展功能
- 集成YAML配置文件管理

## 2. 架构规划

### 2.1 MVVM架构分层

| 层级 | 职责 | 实现方式 |
|------|------|----------|
| **View层** | 仅负责UI渲染（窗口、菜单、按钮等组件），无业务逻辑 | 使用qfluentwidgets提供的组件库 |
| **ViewModel层** | 处理交互逻辑（菜单切换、主题修改、搜索触发），作为View与Model的中间层 | 自定义Python类，处理信号槽 |
| **Model/Service层** | 负责数据处理（配置读取、用户信息获取） | 自定义服务类，处理数据操作 |
| **Infra层** | 封装通用能力（配置解析、主题管理、依赖注入） | 工具类和辅助模块，包括依赖注入容器 |

### 2.2 目录结构

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

### 2.3 代码规范
- 禁止将所有逻辑写入单个文件，按功能模块拆分
- 组件间通过信号槽/接口通信，避免直接依赖
- 遵循Python PEP8代码规范
- 采用类型注解提高代码可读性

## 3. 菜单与图标规划

### 3.1 主菜单配置

| 菜单名称 | 图标文件 | 路由地址 | 显示位置 | 功能说明 |
|---------|---------|---------|---------|--------|
| 首页 | icon_home.svg | home | 顶部 | 系统启动时的首页 |
| 连接管理 | icon_ch_vInput.svg | api_test | 顶部 | 连接管理 |
| 单板阶段 | icon_pcb_32.svg | board_stage | 顶部 | 单板阶段测试 |
| 组装阶段 | icon_blackbox_test.svg | assemble_stage | 顶部 | 组装阶段测试 |
| 统计报告 | icon_report_32.svg | statistics | 顶部 | 统计报告 |
| 系统设置 | icon_settings.svg | system_settings | 顶部 | 系统参数配置、用户管理、日志查看 |
| 帮助文档 | icon_info.svg | help_docs | 底部 | 帮助文档 |

### 3.2 子菜单配置

#### 首页子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 欢迎页面 |  | 系统启动时的首页 |
| 用户管理 |  | 用户账户管理 |
| 项目管理 |  | 项目信息管理 |

#### 连接管理子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| Modbus-rtu测试 |  | Modbus-rtu通信测试 |
| API测试 |  | 应用程序接口测试 |
| MQTT测试 |  | MQTT消息队列测试 |

#### 单板阶段子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 电机驱动板烧录 |  | 电机驱动板固件烧录 |
| 电机驱动板测试 |  | 电机驱动板功能测试 |
| LED&按键板功能测试 |  | LED指示灯和按键功能测试 |
| 电机来料测试 |  | 电机原材料质量检测 |
| 四手指功能测试 |  | 四指机械手功能测试 |
| 单拇指功能测试 |  | 单拇指机械手功能测试 |

#### 组装阶段子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 半成品测试 |  | 产品半成品质量检测 |
| 老化测试 |  | 产品长时间稳定性测试 |
| 整机测试 |  | 完整产品功能测试 |
| OTA升级 |  | 无线固件升级测试 |
| 整机出货检测 |  | 出货前最终质量检测 |

#### 统计报告子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 生产统计 |  | 生产数据统计分析 |
| 不良分析- |  | 产品质量不良分析 |
| 报表导出 |  | 测试数据报表导出 |

#### 系统设置子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 测试参数配置 | - | 测试参数配置 |
| 用户管理 | - | 用户账户管理 |
| 系统日志 | - | 系统运行日志 |

#### 帮助文档子菜单
| 菜单名称 | 图标文件 | 功能说明 |
|---------|---------|--------|
| 测试指南 | - | 测试操作指南 |
| 故障排除 | - | 常见故障排除 |
| 系统更新 | - | 系统版本更新 |

### 3.3 图标管理
- 图标文件统一存放在 `res/icons/` 目录
- 缺失图标参考 `res` 目录补充
- 使用 `QIcon` 加载和管理图标

## 4. 页面路由规划

### 4.1 一级菜单路由映射

| 路由地址 | 页面组件 | 功能说明 |
|---------|---------|--------|
| home | HomePage | 首页页面 - 介绍系统功能，展示欢迎信息和快速访问入口，列出首页子菜单内容 |
| api_test | ApiTestPage | 连接管理页面 - 介绍连接管理功能，列出Modbus-rtu测试、API测试、MQTT测试等子菜单内容 |
| board_stage | BoardStagePage | 单板阶段测试页面 - 介绍单板阶段测试功能，列出电机驱动板烧录、电机驱动板测试等子菜单内容 |
| assemble_stage | AssembleStagePage | 组装阶段测试页面 - 介绍组装阶段测试功能，列出半成品测试、老化测试等子菜单内容 |
| statistics | StatisticsPage | 统计报告页面 - 介绍统计报告功能，列出生产统计、不良分析、报表导出等子菜单内容 |
| system_settings | SystemSettingsPage | 系统设置页面 - 介绍系统设置功能，列出测试参数配置、用户管理、系统日志等子菜单内容 |
| help_docs | HelpDocsPage | 帮助文档页面 - 介绍帮助文档功能，列出测试指南、故障排除、系统更新等子菜单内容 |

### 4.2 二级菜单路由映射
- 首页子菜单：欢迎页面、用户管理、项目管理
- 连接管理子菜单：Modbus-rtu测试、API测试、MQTT测试
- 单板阶段子菜单：电机驱动板烧录、电机驱动板测试、LED&按键板功能测试、电机来料测试、四手指功能测试、单拇指功能测试
- 组装阶段子菜单：半成品测试、老化测试、整机测试、OTA升级、整机出货检测
- 统计报告子菜单：生产统计、不良分析-、报表导出
- 系统设置子菜单：测试参数配置、用户管理、系统日志
- 帮助文档子菜单：测试指南、故障排除、系统更新

### 4.3 路由实现
- 采用ViewModel层管理路由状态
- 使用信号槽机制实现菜单切换与页面更新
- 所有页面默认显示"[页面名称]+开发中"占位提示
- 一级和二级菜单都有对应的界面实现

## 5. 功能实现规划

### 5.1 基础界面
- 参考 examples 里的 window 示例搭建整体窗口框架
- 使用 qfluentwidgets 组件库实现所有UI组件
- 实现主菜单与子菜单的层级展示
- 添加导航栏和状态栏

### 5.2 扩展功能

| 功能 | 位置 | 实现方式 |
|------|------|----------|
| **搜索框** | 顶部区域 | 使用 qfluentwidgets 的搜索组件，支持输入和搜索触发 |
| **主题颜色调节** | 顶部区域 | 使用 qfluentwidgets 的颜色选择器组件，支持预设主题和自定义颜色 |
| **用户信息模块** | 左下角区域 | 使用 qfluentwidgets 的用户信息组件，显示用户名、头像和登录状态 |

### 5.3 交互逻辑
- 菜单点击触发页面切换
- 主题调节实时更新界面样式
- 搜索功能触发搜索逻辑
- 用户信息展示与管理

### 5.4 页面实现
- 所有一级菜单对应页面显示"[页面名称]+开发中"
- 所有二级菜单对应页面显示"[子菜单名称]+开发中"
- 使用 qfluentwidgets 的页面组件实现统一的页面布局

## 6. 依赖注入实现

### 6.1 依赖注入框架
使用 `dependency-injector` 框架实现依赖注入，为应用提供以下功能：

- **单例模式**：为MQTT、Modbus-RTU、SQLite3等资源密集型服务提供单例模式创建上下文
- **工厂模式**：为用户、测试用例等需要动态创建的对象提供工厂模式注入
- **模块组织**：按功能模块组织依赖配置，提高代码可维护性

### 6.2 依赖注入容器配置

#### 核心容器结构

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

#### 提供者实现

```python
# infra/di/providers.py
from dependency_injector import providers
from app.service import ConfigService, ThemeService
from app.service.mqtt_service import MQTTService
from app.service.modbus_service import ModbusService
from app.service.database_service import DatabaseService
from app.service.user_service import UserService
from app.model.test_case import TestCase

class ConfigServiceProvider(providers.Singleton):
    """配置服务提供者（单例）"""
    def __init__(self):
        super().__init__(ConfigService)

class ThemeServiceProvider(providers.Singleton):
    """主题服务提供者（单例）"""
    def __init__(self, config_service):
        super().__init__(ThemeService, config_service=config_service)

class DatabaseServiceProvider(providers.Singleton):
    """数据库服务提供者（单例）"""
    def __init__(self, config_service):
        super().__init__(DatabaseService, config_service=config_service)

class MQTTServiceProvider(providers.Singleton):
    """MQTT服务提供者（单例）"""
    def __init__(self, config_service):
        super().__init__(MQTTService, config_service=config_service)

class ModbusServiceProvider(providers.Singleton):
    """Modbus服务提供者（单例）"""
    def __init__(self, config_service):
        super().__init__(ModbusService, config_service=config_service)

class UserServiceProvider(providers.Factory):
    """用户服务提供者（工厂）"""
    def __init__(self, database_service):
        super().__init__(UserService, database_service=database_service)

class TestCaseProvider(providers.Factory):
    """测试用例提供者（工厂）"""
    def __init__(self):
        super().__init__(TestCase)
```

### 6.3 使用示例

#### 在ViewModel中使用依赖注入

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

#### 在Service中使用依赖注入

```python
# app/service/mqtt_service.py
class MQTTService:
    """MQTT服务"""
    
    def __init__(self, config_service):
        self.config_service = config_service
        self.client = None
        self._initialize()
    
    def _initialize(self):
        # 初始化MQTT客户端
        pass
    
    def publish(self, topic, message):
        # 发布消息
        pass
```

### 6.4 后续扩展

为后续规划的功能模块预留依赖注入配置：

- **设备管理模块**：为不同类型的测试设备提供统一的依赖注入接口
- **测试执行模块**：为测试流程和测试用例提供依赖注入支持
- **报告生成模块**：为不同格式的报告生成器提供依赖注入支持

## 7. 配置管理

### 7.1 YAML配置文件结构

```yaml
# app_config.yml
app:
  name: "TestUI"
  version: "1.0.0"

theme:
  default_color: "#1E88E5"
  available_colors: ["#1E88E5", "#26A69A", "#FFA726", "#EF5350"]

menu:
  main_menu:
    - name: "首页"
      icon: "icon_home.svg"
      route: "home"
      position: "top"
      description: "系统启动时的首页"
    # 其他主菜单配置...
  sub_menu:
    home:
      - name: "欢迎页面"
        description: "系统启动时的首页"
      # 其他子菜单配置...

user:
  default_name: "Admin"
  default_avatar: "default_avatar.png"

search:
  placeholder: "搜索..."
  max_results: 10
```

### 6.2 配置读取
- 创建专用配置服务类 `ConfigService`
- 使用 `pyyaml` 库解析YAML文件
- 提供配置项的获取和更新方法

## 7. 执行计划

### 7.1 开发优先级
1. **搭建基础架构**：创建MVVM目录结构，实现基础框架和依赖注入容器
2. **实现菜单系统**：基于menu.md配置菜单和图标，使用qfluentwidgets组件
3. **开发页面路由**：实现页面切换和路由管理，确保一级和二级菜单都有对应界面
4. **添加扩展功能**：实现搜索框、主题调节、用户信息模块，使用qfluentwidgets组件
5. **集成配置管理**：接入YAML配置文件
6. **优化与测试**：完善功能，测试交互逻辑

### 7.2 详细执行步骤

| 步骤 | 任务 | 完成标准 |
|------|------|----------|
| 1 | 创建项目目录结构 | 目录结构符合架构设计，包含依赖注入相关目录 |
| 2 | 配置依赖项 | 在requirements.txt中添加qfluentwidgets和dependency-injector等依赖 |
| 3 | 实现依赖注入容器 | 创建DI容器，配置服务和组件的依赖关系 |
| 4 | 实现主窗口框架 | 参考examples/window示例，使用qfluentwidgets组件创建主窗口 |
| 5 | 开发菜单组件 | 使用qfluentwidgets实现主菜单和子菜单，正确显示图标 |
| 6 | 实现页面路由 | 菜单点击能切换对应页面，一级和二级菜单都有对应界面 |
| 7 | 实现页面和子页面 | 所有页面显示"[页面名称]+开发中"，使用qfluentwidgets组件 |
| 8 | 添加扩展功能组件 | 搜索框、主题调节、用户信息模块正常工作，使用qfluentwidgets组件 |
| 9 | 集成YAML配置 | 配置文件能够正确读取和应用 |
| 10 | 实现ViewModel逻辑 | 组件间交互正常，逻辑清晰，使用依赖注入管理依赖 |
| 11 | 测试与优化 | 功能完整，界面美观，交互流畅 |

## 8. 技术栈

| 技术/框架 | 版本 | 用途 |
|-----------|------|------|
| Python | 3.8+ | 开发语言 |
| PySide6 | 6.0+ | UI框架 |
| qfluentwidgets | 最新版 | UI组件库 |
| PyYAML | 6.0+ | 配置文件解析 |
| dependency-injector | 4.41+ | 依赖注入库 |
| QDarkStyle | 3.0+ | 主题支持（可选） |

## 9. 资源需求

### 9.1 图标资源
- 主菜单图标：参考menu.md中指定的图标文件
- 子菜单图标：部分需要补充
- 功能图标：搜索、主题调节等功能需要的图标

### 9.2 参考资源
- examples/window 示例：窗口框架参考
- res目录：图标和样式参考
- menu.md：菜单结构参考

## 10. 质量保证

### 10.1 代码规范
- 遵循Python PEP8代码规范
- 使用类型注解提高代码可读性
- 编写清晰的文档和注释

### 10.2 测试策略
- 功能测试：验证所有功能正常工作
- 界面测试：确保界面美观、交互流畅
- 兼容性测试：确保在不同环境下正常运行

### 10.3 性能优化
- 合理使用PySide6的信号槽机制
- 避免不必要的UI更新
- 优化配置文件读取性能

## 11. 风险与应对

| 风险 | 影响 | 应对措施 |
|------|------|----------|
| 图标资源缺失 | 界面美观度下降 | 参考res目录补充，或使用系统默认图标 |
| 路由系统复杂度 | 开发时间增加 | 采用简单有效的路由实现方案 |
| 配置文件格式变更 | 系统稳定性影响 | 设计灵活的配置解析机制，支持版本兼容 |
| 主题调节兼容性 | 部分组件样式异常 | 全面测试主题切换效果，确保所有组件兼容 |

## 12. 交付标准

- 完整的MVVM架构实现
- 所有菜单和子菜单正确显示
- 页面路由系统正常工作
- 扩展功能（搜索、主题调节、用户信息）完整实现
- YAML配置文件集成完成
- 代码结构清晰，符合规范
- 界面美观，交互流畅

## 13. 后续规划

- 实现具体页面内容，替换“开发中”占位提示
- 增加更多自定义主题选项
- 实现用户登录和权限管理
- 优化性能和用户体验
- 添加更多功能模块

## 14. Skill命名规范

### 14.1 一级菜单Skill命名规则

- 格式：`testui-<菜单路由>-page`
- 示例：`testui-home-page`、`testui-api-test-page`等

### 14.2 二级菜单Skill命名规则

- 格式：`testui-<一级菜单路由>-<二级菜单名称>`
- 示例：`testui-home-welcome`、`testui-api-test-modbus-rtu`等

### 14.3 Skill目录结构

所有Skill目录均位于 `.trae/skills/` 目录下，包括7个一级菜单Skill和26个二级菜单Skill，通过命名区分不同类型的Skill。

### 14.4 命名规范文档

详细的Skill命名规范请参考 `.trae/skills/SKILL_NAMING_SPEC.md` 文件。

## 15. 提示词参考指南

### 15.1 优先参考文件

在后续的AI交互中，请优先参考以下文件：

1. **TestUI_plan.md**：项目开发计划的核心文件，包含架构设计、菜单配置、页面路由、功能实现等详细规划
2. **README.md**：项目说明文档，提供项目概述、架构设计、菜单配置、页面实现等内容
3. **.trae/skills/** 目录下的相关Skill文件：每个页面的详细开发指南

### 15.2 如何找到对应的Skill

要找到对应的Skill文件进行AI执行，请按照以下步骤：

1. **确定任务类型**：
   - 如果是项目整体开发或架构相关任务，请使用 `testui-dev` Skill
   - 如果是特定页面开发任务，请找到对应的页面Skill

2. **一级菜单页面Skill查找**：
   - 格式：`testui-<菜单路由>-page`
   - 示例：首页页面使用 `testui-home-page` Skill

3. **二级菜单页面Skill查找**：
   - 格式：`testui-<一级菜单路由>-<二级菜单名称>`
   - 示例：首页-欢迎页面使用 `testui-home-welcome` Skill

4. **Skill文件位置**：
   - 所有Skill文件均位于 `.trae/skills/` 目录下
   - 每个Skill目录包含 `SKILL.md` 文件，定义了该Skill的具体内容和执行步骤

### 15.3 构建项目的参考流程

1. **项目初始化**：
   - 参考 `README.md` 中的依赖管理部分，安装项目依赖
   - 参考 `TestUI_plan.md` 中的目录结构部分，创建项目目录结构

2. **架构搭建**：
   - 参考 `TestUI_plan.md` 中的MVVM架构分层部分，实现各层组件
   - 参考 `testui-dev` Skill，了解项目整体开发流程

3. **页面开发**：
   - 对于一级菜单页面，参考对应的 `testui-<菜单路由>-page` Skill
   - 对于二级菜单页面，参考对应的 `testui-<一级菜单路由>-<二级菜单名称>` Skill

4. **功能实现**：
   - 参考 `TestUI_plan.md` 中的功能实现规划部分，实现各项功能
   - 参考 `README.md` 中的技术栈部分，使用指定的技术和框架

5. **测试与优化**：
   - 参考 `TestUI_plan.md` 中的质量保证部分，进行功能测试和性能优化

### 15.4 提示词示例

**示例1：开发首页页面**
```
请根据TestUI项目的需求，开发首页页面。

参考文件：
- TestUI_plan.md：了解页面路由和功能需求
- .trae/skills/testui-home-page/SKILL.md：首页页面的详细开发指南
- README.md：了解项目整体架构和技术栈

实现要求：
- 使用qfluentwidgets组件库
- 显示"首页页面+开发中"的提示
- 介绍系统功能和首页子菜单内容
```

**示例2：开发连接管理-Modbus-rtu测试页面**
```
请根据TestUI项目的需求，开发连接管理-Modbus-rtu测试页面。

参考文件：
- TestUI_plan.md：了解页面路由和功能需求
- .trae/skills/testui-api-test-modbus-rtu/SKILL.md：Modbus-rtu测试页面的详细开发指南
- README.md：了解项目整体架构和技术栈

实现要求：
- 使用qfluentwidgets组件库
- 显示"Modbus-rtu测试+开发中"的提示
- 实现Modbus-rtu通信测试的基础界面
```