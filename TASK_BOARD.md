Trading Trainer
TASK BOARD

版本：
V1.0

开发方式：

VS Code + Flutter + AI Assistant

项目状态

状态标记：

⬜ 未开始

🔄 开发中

✅ 已完成

⚠️ 需要修复

Sprint 1：项目基础

目标：

完成Flutter工程框架。

TASK-001
创建项目结构

状态：

⬜

目标：

建立：

lib/

├── core/

├── features/

├── shared/

└── main.dart

要求：

Material3
Riverpod
go_router

验收：

APP启动成功。

TASK-002
创建主题系统

状态：

⬜

文件：

core/theme/

完成：

Dark Theme
Trading风格颜色
字体配置

验收：

APP显示深色界面。

TASK-003
创建导航系统

状态：

⬜

页面：

Home

Replay

History

Statistics

Settings

验收：

页面可以切换。

Sprint 2：数据库

目标：

建立本地数据能力。

TASK-004
SQLite初始化

状态：

⬜

创建：

DatabaseService

表：

market_data
trade_order
trade_log
replay_session
app_settings

验收：

启动自动创建数据库。

TASK-005
创建数据Model

状态：

⬜

创建：

Candle

Order

TradeLog

ReplaySession

要求：

支持：

toMap()

fromMap()

Sprint 3：行情数据

目标：

让APP读取黄金历史行情。

TASK-006
CSV导入功能

状态：

⬜

功能：

选择CSV

↓

解析

↓

保存SQLite

验收：

导入10000根K线。

TASK-007
行情查询模块

状态：

⬜

创建：

MarketRepository

功能：

分页读取K线。

Sprint 4：K线系统

目标：

显示黄金走势。

TASK-008
K线组件

状态：

⬜

功能：

蜡烛图
缩放
拖动
TASK-009
Replay页面

状态：

⬜

显示：

K线

控制按钮

交易按钮

Sprint 5：Replay Engine

目标：

实现历史训练。

TASK-010
Replay状态

状态：

⬜

字段：

currentIndex

speed

playing

candles
TASK-011
下一根K线

状态：

⬜

功能：

next()

previous()

reset()

验收：

未来K线不可见。

TASK-012
自动播放

状态：

⬜

速度：

1x

2x

4x

Sprint 6：交易系统

目标：

模拟真实交易。

TASK-013
开仓

状态：

⬜

支持：

BUY

SELL

保存订单。

TASK-014
平仓

状态：

⬜

支持：

手动平仓。

TASK-015
止损止盈

状态：

⬜

自动检测：

SL

TP

TASK-016
盈亏计算

状态：

⬜

计算：

Profit/Loss

Sprint 7：交易日志
TASK-017

交易历史页面

状态：

⬜

显示：

时间

方向

结果

TASK-018

交易详情

状态：

⬜

显示：

K线环境

备注

截图

Sprint 8：统计
TASK-019

统计页面

状态：

⬜

显示：

胜率

盈亏比

最大回撤

Sprint 9：AI Coach
TASK-020

AI分析服务

状态：

⬜

输入：

交易记录

K线

输出：

分析报告

TASK-021

AI报告页面

状态：

⬜

显示：

评分

问题

建议

Sprint 10：测试发布
TASK-022

性能测试

状态：

⬜

测试：

50万K线。

TASK-023

Bug修复

状态：

⬜

TASK-024

生成APK

状态：

⬜

命令：

flutter build apk --release
AI执行规则

每执行一个TASK：

必须输出：

任务：

TASK-XXX


修改文件：

xxx.dart


实现内容：

xxx


测试方法：

xxx


风险：

xxx
