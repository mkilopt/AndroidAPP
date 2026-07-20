AI交易训练器 APP 产品需求文档（PRD）

版本：V1.0
项目名称：Trading Trainer
平台：Android
技术架构：Flutter + SQLite
运行方式：本地离线

1. 产品定位
1.1 产品名称

Trading Trainer

1.2 产品目标

打造一个用于训练交易者盘感、执行纪律和交易系统的模拟训练工具。

通过：

历史行情回放
隐藏未来K线
模拟真实交易
自动计算盈亏
交易复盘分析

帮助用户形成交易规则执行能力。

2. 用户画像

目标用户：

初级交易者

需求：

学习如何找进场点
训练止损纪律
避免情绪交易
中级交易者

需求：

测试交易系统
统计策略胜率
优化交易规则
专业交易者

需求：

快速复盘大量历史行情
验证交易模型
3. 产品范围
V1.0功能

必须实现：

✅ 黄金历史数据导入

✅ K线显示

✅ 历史行情回放

✅ 模拟交易

✅ 止损止盈

✅ 交易日志

✅ 盈亏统计

V2.0功能

未来：

AI交易分析
自动评分
策略模板
技术指标
多品种
V3.0功能

未来：

实时行情API
券商账户连接
云同步
社区
4. 技术架构
4.1 技术选型

Flutter：

Flutter 3.x
Dart
Material 3

状态管理：

Riverpod

数据库：

SQLite

sqflite

本地存储：

shared_preferences

文件：

file_picker

CSV：

csv package
5. 软件架构

采用：

Clean Architecture

结构：

lib/

core/

database/

network/

utils/


data/

models/

repositories/


domain/

entities/

usecases/


presentation/


pages/

widgets/

controllers/

6. 数据库设计
6.1 行情表

表名：

market_data

字段：

字段	类型
id	INTEGER
symbol	TEXT
timeframe	TEXT
datetime	TEXT
open	REAL
high	REAL
low	REAL
close	REAL
volume	REAL

示例：

XAUUSD

5m

2025-01-01 09:00

2650

2655

2648

2652

1000
6.2 回放记录表

表名：

replay_session

字段：

id

symbol

timeframe

start_time

current_index

speed

status

created_at

6.3 模拟订单

表：

trade_order

字段：

id

direction

entry_price

exit_price

stop_loss

take_profit

lot

profit

open_time

close_time

status

6.4 交易日志

表：

trade_log

字段：

id

trade_id

strategy

reason

emotion

image

score

comment

created_at

7. 页面设计
7.1 首页 Home

功能：

进入训练

查看记录

数据管理

布局：

-----------------

Trading Trainer


开始训练


历史记录


数据管理


设置


-----------------

7.2 数据管理页

功能：

导入历史行情。

显示：

当前数据

XAUUSD

数量:

250000

时间:

2020-2025

7.3 K线训练页（核心）

布局：


-------------------

K线区域


-------------------


时间:

2025-01-01


资金:

10000


-------------------


BUY

SELL


下一根K线


自动播放


-------------------

持仓

方向:

BUY

价格:

2650

止损:

2640

止盈:

2670

-------------------

8. Replay引擎设计
原理

加载：

100000根K线

初始化：

显示：

前100根

用户点击：

下一根

显示：

第101根

循环。

伪代码：

currentIndex++


load candle[currentIndex]


refresh chart


自动播放：

Timer


↓

currentIndex++


↓

update UI

9. 模拟交易系统
开仓

用户输入：

方向

BUY

SELL


价格


仓位


止损


止盈


保存：

trade_order

平仓判断

每根K线:

BUY:

if low <= stopLoss

close


if high >= takeProfit

close


SELL:

if high >= stopLoss

close


if low <= takeProfit

close

10. 盈亏计算

公式：

多单：

(close-entry)*lot

空单：

(entry-close)*lot

11. 交易统计

显示：

总交易次数

盈利次数

亏损次数

胜率

平均盈利

平均亏损

盈亏比

最大回撤

12. AI交易教练设计（预留）

输入：

交易记录

K线截图

交易规则

结果


AI输出：

交易评分:

85


优点:

顺势

位置合理


问题:

止损太近


建议:

等待确认K线

13. 开发规则（给AI）

AI开发必须遵守：

代码规则
不允许一次生成整个项目
每次只开发一个模块
修改代码前说明影响范围
保持已有功能正常
不重复创建文件
所有数据库操作集中管理
14. 开发顺序
Sprint 1

项目初始化

完成：

Flutter

目录

主题

Sprint 2

SQLite

完成：

数据库

Model

Repository

Sprint 3

CSV导入

Sprint 4

K线显示

Sprint 5

Replay Engine

Sprint 6

模拟交易

Sprint 7

交易日志

Sprint 8

统计分析

Sprint 9

AI分析接口

15. Codex启动指令

每次开发前发送：

你现在是本项目Flutter高级工程师。

请严格遵守 Trading_Trainer_PRD.md。

当前任务：

【填写任务】

要求：

1. 先分析设计方案
2. 输出修改文件列表
3. 再生成代码
4. 不修改无关模块
5. 保持Clean Architecture

开始执行。
16. MVP完成标准

APP可以做到：

用户：

导入黄金历史K线

↓

开始训练

↓

隐藏未来行情

↓

判断买卖

↓

设置止损止盈

↓

自动计算结果

↓

查看交易统计

完成即为第一版。
