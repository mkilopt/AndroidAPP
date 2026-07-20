Trading Trainer
Codex Prompt Library

版本：
V1.0

0. 总规则 Prompt（每次开发前发送）
你现在是 Trading Trainer 项目的高级 Flutter 工程师。

请严格遵守以下项目文档：

- Trading_Trainer_PRD.md
- PROJECT_RULES.md
- UI_SPEC.md
- DATABASE_DESIGN.md
- REPLAY_ENGINE_DESIGN.md
- TRADE_ENGINE_DESIGN.md
- AI_COACH_DESIGN.md
- DEVELOPMENT_ROADMAP.md


开发要求：

1. 使用 Flutter + Dart
2. 使用 Clean Architecture
3. 使用 Riverpod 管理状态
4. 使用 SQLite 保存本地数据
5. 不修改无关模块
6. 不重复创建文件
7. 所有业务逻辑不能写入Widget
8. 每次修改前说明方案
9. 输出修改文件列表
10. 完成后说明测试方法

当前任务：

【填写任务】

开始执行。
Phase 1 项目初始化 Prompt
Task 1. 创建Flutter项目
创建 Trading Trainer Flutter 项目。

要求：

Flutter 3.x

Material 3

Dark Theme

Riverpod

go_router


创建基础目录：

core

data

domain

presentation


不要开发业务功能。

输出：

1. 项目结构
2. 已创建文件
3. 运行方法
Task 2. 配置依赖
配置项目依赖。


需要：

flutter_riverpod

sqflite

path_provider

go_router

csv

file_picker


修改pubspec.yaml。


完成后：

执行flutter pub get。


检查依赖是否正常。
Phase 2 SQLite Prompt
Task 3. 创建数据库
开发SQLite数据库模块。


要求：

创建：

DatabaseService


功能：

初始化数据库

创建表

关闭数据库


数据库：

trading_trainer.db


根据DATABASE_DESIGN.md创建：

market_data

trade_order

trade_log

replay_session

app_settings


不要开发Repository。
Task 4. 创建数据库Model
创建数据库Model。


需要：

CandleModel

TradeOrderModel

TradeLogModel

ReplaySessionModel


要求：

包含：

fromMap()

toMap()


支持SQLite转换。
Phase 3 数据导入
Task 5 CSV导入
开发历史行情CSV导入模块。


功能：

用户选择CSV文件。

解析：

datetime

open

high

low

close

volume


保存SQLite。


要求：

显示：

成功数量

失败数量

导入时间


创建：

CSVService

MarketRepository

ImportController

ImportPage
Phase 4 K线模块
Task 6 K线显示
开发K线显示模块。


要求：

读取SQLite行情。


显示：

蜡烛图


支持：

缩放

拖动

十字光标


不要加入交易逻辑。


创建：

CandleChartWidget

ChartController

ChartRepository
Phase 5 Replay Engine
Task 7 Replay状态
开发Replay状态管理。


创建：

ReplayState


字段：

currentIndex

visibleCandles

speed

isPlaying


使用Riverpod。


不要连接交易系统。
Task 8 下一根K线
开发ReplayController。


实现：

nextCandle()

previousCandle()

reset()


要求：

隐藏未来数据。


测试：

1000根K线回放。
Task 9 自动播放
增加Replay自动播放。


支持：

1x

2x

4x

8x


要求：

Timer管理。


暂停后释放资源。
Phase 6 Trade Engine
Task 10 开仓
开发模拟交易开仓功能。


支持：

BUY

SELL


输入：

价格

仓位

止损

止盈


保存SQLite。


创建：

TradeController

TradeEngine

TradeRepository
Task 11 止损止盈
开发自动平仓逻辑。


每生成一根K线：

检查持仓。


BUY：

low <= stopLoss

high >= takeProfit


SELL：

high >= stopLoss

low <= takeProfit


自动更新订单。
Phase 7 日志统计
Task 12 交易历史页面
开发交易记录页面。


显示：

时间

方向

入场

出场

盈亏


支持：

点击查看详情。
Task 13 数据统计
开发统计页面。


计算：

交易次数

盈利次数

亏损次数

胜率

平均盈亏比

最大回撤


使用SQLite计算。
Phase 8 AI Coach
Task 14 AI接口
开发AI Coach模块。


创建：

AIService


功能：

analyzeTrade()


输入：

Trade

K线数据

交易规则


输出：

AIReport


不要写UI。
Task 15 AI评分页面
开发AI交易分析页面。


显示：

评分

等级

优点

问题

建议


数据来自AIReport。
Debug Prompt

遇到错误时：

你现在负责Debug Trading Trainer项目。


错误信息：

【复制错误】


请：

1. 分析原因

2. 指出影响文件

3. 给出修复方案

4. 输出修改代码

5. 说明测试方法


不要重构整个项目。
Code Review Prompt

完成模块后：

请作为高级Flutter架构师审查当前代码。


检查：

1. 架构是否符合Clean Architecture

2. 是否存在重复代码

3. 是否存在性能问题

4. 是否违反模块隔离

5. 是否存在SQLite风险


输出：

问题列表

优化建议

必须修改项。
发布前Prompt
请准备Trading Trainer Android发布。


检查：

Flutter build

性能

数据库

权限

APK大小

异常处理


生成：

发布检查清单。
AI开发顺序总表
1 创建Flutter项目

↓

2 SQLite

↓

3 数据导入

↓

4 K线显示

↓

5 Replay Engine

↓

6 Trade Engine

↓

7 交易日志

↓

8 统计

↓

9 AI Coach

↓

10 发布
