Trading Trainer
Data Source Design

版本：
V1.0

模块：

历史行情数据系统

1. 模块目标

建立统一行情数据层。

支持：

黄金 XAUUSD
历史K线
多周期
本地SQLite存储
Replay Engine调用
2. 数据架构

整体流程：

行情来源

↓

CSV文件

↓

数据解析

↓

数据清洗

↓

SQLite

↓

MarketRepository

↓

Replay Engine

↓

K线显示

3. 第一版数据范围

V1支持：

品种：

XAUUSD

周期：

1分钟

5分钟

15分钟

1小时

4小时

日线

数据字段：

必须包含：

字段	说明
datetime	时间
open	开盘
high	最高
low	最低
close	收盘
volume	成交量
4. 标准CSV格式

文件：

XAUUSD_5M.csv

格式：

datetime,open,high,low,close,volume

2025-01-01 09:00,
2650.20,
2652.10,
2648.50,
2651.30,
1250

5. 数据来源方案
方案A：MT5历史数据（推荐）

适合：

黄金交易者。

流程：

MT5

↓

历史中心

↓

导出CSV

↓

APP导入


优点：

数据真实
免费
支持多个周期
方案B：TradingView导出

适合：

快速测试。

流程：

TradingView

↓

导出数据

↓

CSV

↓

APP导入

方案C：行情API（未来）

例如：

实时行情：

API

↓

APP

↓

SQLite缓存


V1不使用。

6. 数据清洗规则

导入时检查：

6.1 时间格式

统一：

YYYY-MM-DD HH:mm:ss

例如：

2025-01-01 09:00:00
6.2 空数据

禁止：

open=null

处理：

跳过。

6.3 K线异常

检查：

最高价：

必须 >=

开盘

收盘

最低价：

必须 <=

开盘

收盘

错误：

记录日志。

7. 数据库存储

对应：

market_data

字段：

CREATE TABLE market_data(

id INTEGER PRIMARY KEY,

symbol TEXT,

timeframe TEXT,

datetime TEXT,

open REAL,

high REAL,

low REAL,

close REAL,

volume REAL

);

8. 数据索引

必须创建：

CREATE INDEX idx_market_datetime

ON market_data(datetime);


目的：

快速Replay。

9. 数据加载策略

禁止：

一次加载全部。

错误：

50万K线

↓

全部进入内存


可能：

内存不足。

正确：

分页。

例如：

第一次：

500根

下一次：

500根

10. 数据缓存

创建：

MarketCache

保存：

最近：

1000根K线

作用：

提高滚动速度。

11. 数据管理页面需求

页面：

DataManagementPage

显示：

当前数据


品种:

XAUUSD


周期:

5分钟


数量:

350000


时间范围:

2020-2025


按钮：

导入CSV

删除数据

刷新统计

12. 导入流程

用户：

点击导入

↓

选择文件

↓

读取CSV

↓

验证格式

↓

显示预览

↓

确认

↓

写入SQLite

↓

完成

13. 导入预览

显示前10条：

例如：

时间              开      高

2025-01-01       2650

2025-01-01       2651


用户确认后导入。

14. 数据Repository设计

文件：

market_repository.dart

职责：

负责：

查询K线
分页加载
保存行情
删除数据

禁止：

处理UI。

15. 数据Service设计

文件：

market_data_service.dart

职责：

CSV解析
数据验证
格式转换
16. API扩展设计（未来）

未来支持：

实时行情。

架构：

MarketProvider


├── LocalProvider

SQLite


├── CSVProvider

文件


└── ApiProvider

实时API

17. 多品种扩展

未来支持：

XAUUSD

EURUSD

GBPUSD

BTCUSD

US30

NASDAQ


数据库已经预留：

symbol字段。

18. 性能目标

支持：

单品种：

500000根K线

要求：

首次加载：

<2秒

Replay：

60FPS

SQLite：

查询稳定。

19. 测试要求
测试1

导入：

10万K线

结果：

成功。

测试2

导入：

50万K线

结果：

APP不卡顿。

测试3

错误CSV

结果：

提示错误原因。

20. Codex开发规则

开发数据模块：

必须：

不修改Replay逻辑
不修改交易逻辑
Repository隔离
所有数据异常必须处理
导入过程不能阻塞UI
21. 完成标准

完成后：

用户可以：

获取黄金历史数据

↓

导入APP

↓

查看K线

↓

开始Replay训练

↓

模拟交易
