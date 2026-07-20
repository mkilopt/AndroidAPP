# Trading Trainer
# Flutter Project Structure Design

版本：
V1.0


技术：

Flutter

Dart

Riverpod

SQLite

Clean Architecture



---

# 1. 架构原则


采用：

Feature First + Clean Architecture
Presentation

↓

Domain

↓

Data

↓

External



---

# 2. 总目录结构



trading_trainer/

├── android/

├── ios/

├── assets/

│
├── lib/

│
├── core/

│
├── features/

│
├── shared/

│
├── main.dart

└── pubspec.yaml



---

# 3. Core核心层


目录：


lib/core/



作用：

全局基础能力。


结构：



core/

├── database/

├── router/

├── theme/

├── constants/

├── utils/

├── errors/

└── services/



---

# 4. Database数据库模块


目录：



core/database/



文件：



database_service.dart

database_tables.dart

database_migration.dart



职责：


负责：

- SQLite初始化
- 数据库升级
- 表创建


禁止：

写业务逻辑。



---

# 5. Theme主题模块


目录：



core/theme/



文件：



app_theme.dart

color_scheme.dart

text_theme.dart



负责：

- 深色主题
- 字体
- 全局样式



---

# 6. Router路由模块


目录：



core/router/



文件：



app_router.dart

route_names.dart



页面：


/

home

/replay

/trade

/history

/settings



---

# 7. Features业务模块


核心业务全部放：


features/



结构：


features/

├── home/

├── market/

├── replay/

├── trade/

├── history/

├── statistics/

├── ai_coach/

└── settings/



---

# 8. Home模块


目录：



features/home/



结构：



home/

├── presentation/

│ ├── pages/

│ ├── widgets/

│ └── controllers/

├── domain/

└── data/



---

# 9. Market行情模块


负责：

历史行情。


目录：


features/market/



结构：


market/

data/

├── models/

candle_model.dart

├── repositories/

market_repository_impl.dart

├── services/

csv_service.dart

domain/

entities/

candle.dart

repositories/

market_repository.dart

presentation/

pages/

widgets/

controllers/



---

# 10. Replay模块


核心模块。


目录：


features/replay/



结构：



replay/

domain/

entities/

replay_state.dart

services/

replay_engine.dart

data/

repositories/

replay_repository_impl.dart

presentation/

pages/

replay_page.dart

widgets/

candle_chart.dart

replay_controller.dart



---

# 11. Trade模块


模拟交易。


目录：



features/trade/



结构：



trade/

domain/

entities/

order.dart

position.dart

services/

trade_engine.dart

data/

models/

repositories/

trade_repository_impl.dart

presentation/

pages/

widgets/

controllers/



---

# 12. AI Coach模块


目录：



features/ai_coach/



结构：



ai_coach/

domain/

entities/

ai_report.dart

data/

services/

ai_service.dart

presentation/

pages/

widgets/



---

# 13. History模块


交易日志。


目录：


features/history/



负责：

- 历史交易
- 交易详情
- 复盘记录



---

# 14. Statistics模块


统计分析。


目录：


features/statistics/



负责：

计算：

- 胜率
- 盈亏比
- 最大回撤
- 收益曲线


---

# 15. Shared共享组件


目录：



shared/



用于：

多个模块共用。


结构：



shared/

widgets/

app_button.dart

app_card.dart

loading.dart

extensions/

helpers/



---

# 16. 文件命名规范


## 页面



xxx_page.dart



例如：


replay_page.dart



---

## Widget



xxx_widget.dart



例如：


trade_panel_widget.dart



---

## Controller



xxx_controller.dart



---

## Service



xxx_service.dart



---

## Repository



xxx_repository.dart



---

## Model



xxx_model.dart



---

# 17. 状态管理规范


使用：

Riverpod



规则：


Widget

↓

Controller

↓

Service

↓

Repository

↓

Database


---

禁止：

Widget直接访问SQLite。


错误：

```dart
database.query()


正确：

controller.loadData()

18. Dependency规则

模块依赖：

允许：

Presentation

↓

Domain

↓

Data


禁止：

Data

↓

Presentation

19. AI开发规则

Codex修改代码时：

必须：

说明修改文件
不跨模块修改
不删除已有功能
保持命名规范
添加测试
20. 新功能添加流程

例如：

增加策略训练。

步骤：

创建feature

features/strategy/


建立：

domain

建立：

data

建立：

presentation

添加router

添加测试

21. 性能规范

禁止：

大量Widget重建。

要求：

使用：

ConsumerWidget

Provider

22. 完成标准

工程结构满足：

✓ 易维护

✓ 可扩展

✓ 支持AI开发

✓ 支持未来联网

✓ 支持商业版本


结构：
