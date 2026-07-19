Trading Trainer APP 产品需求文档（PRD）

版本：V1.0
产品名称：Trading Trainer
平台：Android
技术：Flutter + SQLite
运行方式：本地离线运行

1. 产品概述
1.1 产品定位

Trading Trainer 是一款交易训练模拟器。

目标：

通过历史真实行情，让交易者在不知道未来走势的情况下进行模拟交易训练，提高：盘感
交易执行能力
风险控制能力
交易纪律

主要训练品种：

第一阶段：

黄金 XAU/USD（伦敦金）

未来扩展：

外汇
指数
加密货币
股票

2. 产品目标
用户目标

用户可以：

导入历史行情数据
隐藏未来K线
像真实交易一样判断行情
模拟买卖
设置止损止盈
保存交易记录
复盘交易过程

3. 产品范围
V1.0 必须实现
核心功能

✅ 本地K线数据库
✅ 历史行情回放
✅ 模拟交易
✅ 止损止盈
✅ 交易日志
✅ 盈亏统计

V1.1

增加：

技术指标
交易评分
策略模板
截图复盘
交易笔记

V2.0

增加：

AI交易教练
实时行情API
多设备同步
券商连接

4. 用户流程
首次使用

流程：
打开APP

↓

导入历史行情

↓

选择交易品种

↓

选择周期

↓

开始训练

↓

进入K线回放

↓

模拟交易

↓

查看复盘报告

5. 功能需求
模块一：首页 Home
功能

展示：

开始训练
最近训练
交易统计
数据管理

页面：
--------------------

Trading Trainer

--------------------

开始训练

继续训练


历史记录


数据管理


设置

--------------------
模块二：历史数据管理
功能

用户导入：

CSV格式行情文件。

支持字段：
datetime

open

high

low

close

volume
示例：
2025-01-01 09:00

2650.5

2655

2648

2651

1000

数据处理

要求：

自动检测格式
检查重复数据
显示导入数量
显示错误数量
模块三：K线回放 Replay（核心）
产品目标

模拟真实交易环境。

功能

用户选择：

品种：
XAUUSD
周期：
15分钟

30分钟

4小时

日线

周线
选择日期：

例如：
2025-01-01

回放规则

初始：

显示100根K线。

未来数据隐藏。

用户操作：
下一根K线
显示：

下一根。

支持：

播放速度：
1X

2X

4X

8X
模块四：模拟交易
开仓

用户点击：

BUY

SELL

弹出：
方向:

BUY


价格:

自动获取当前价格


仓位:

0.1


止损:

输入


止盈:

输入
订单状态

状态：
OPEN

CLOSED
自动平仓规则

每产生一根K线：

检查：

多单：

如果：
最低价 <= 止损
平仓。

如果：
最高价 >= 止盈
平仓。

空单：

相反
模块五：交易日志

保存：

每一笔交易。

字段：
交易时间

品种

周期

方向

入场价格

出场价格

止损

止盈

盈利金额

盈利点数

持仓时间

交易备注

截图
模块六：统计分析

显示：

基础数据
总交易次数

盈利次数

亏损次数

胜率

总收益

风险数据
最大连续亏损

最大回撤

平均盈利

平均亏损

平均盈亏比
6. 数据库设计
Table 1

market_data

字段：
id

symbol

timeframe

datetime

open

high

low

close

volume
Table 2

replay_session

字段：
id

symbol

timeframe

start_time

current_index

speed

created_time
Table 3

trade_order

字段：
id

session_id

direction

entry_price

exit_price

stop_loss

take_profit

lot

profit

status

entry_time

exit_time
Table 4

trade_note

字段：
id

trade_id

content

image

score

created_time
7. 技术需求
前端

Flutter

版本：

Flutter 3.x
状态管理

使用：

Riverpod

数据库

SQLite

Flutter:
sqflite
架构

采用：

Clean Architecture

目录：
lib/

core/

data/

domain/

presentation/

features/

8. UI设计要求

风格：

类似：

TradingView

要求：

深色主题
专业交易界面
信息密度高
操作快速

颜色：

背景：

深灰

K线：

上涨：

绿色

下跌：

红色
9. 非功能需求
性能

要求：

支持：

50万根K线

打开：

3秒以内
数据安全

所有数据：

本地保存。

不上传服务器。
离线

APP无需网络：

可以：

查看数据
回放
模拟交易
查看记录
10. 后续AI扩展设计

预留接口：
AIService
输入：
交易记录

K线截图

技术指标

交易规则
输出：
交易评分

错误分析

改进建议
11. 开发阶段规划
Sprint 1

基础工程

Flutter初始化
项目结构
SQLite
Sprint 2

行情数据

CSV导入
K线数据库
Sprint 3

K线系统

K线显示
Replay
Sprint 4

交易系统

BUY
SELL
SL
TP
Sprint 5

日志系统

保存交易
统计
Sprint 6

优化

UI优化
性能优化
发布APK
