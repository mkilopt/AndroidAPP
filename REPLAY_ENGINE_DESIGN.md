# Trading Trainer
# Replay Engine Design

版本：
V1.0

模块：
K线历史回放引擎


---

# 1. 模块目标


Replay Engine 是交易训练器核心模块。


目标：

让用户在不知道未来行情的情况下：

1. 查看历史K线

2. 判断交易机会

3. 模拟买入卖出

4. 设置止损止盈

5. 复盘交易结果


模拟真实交易环境。


---

# 2. 核心原则


## 隐藏未来数据


禁止：

一次加载全部K线给用户。



正确方式：


数据库：

100000根K线


↓

Replay Engine


↓

只释放：

当前可见K线



例如：


数据库：

2025-01-01

↓

2025-12-31



训练开始：


显示：

2025-01-01

前100根



未来：

不可访问



---

# 3. 核心数据结构



## Candle对象



class Candle {


int index;


DateTime time;


double open;


double high;


double low;


double close;


double volume;



}



---

# 4. Replay状态设计



ReplayState:



字段：


currentIndex

当前播放位置



visibleCount

显示多少根K线



speed

播放速度



isPlaying

是否自动播放



candles

当前显示K线



currentPrice

当前价格



---

示例：


```dart

ReplayState(

currentIndex:1000,

visibleCount:100,

speed:1,

isPlaying:false
5. Replay生命周期
创建训练

用户点击：

开始训练

流程：

选择：

品种

↓

选择：

周期

↓

选择：

时间范围

↓

创建session

↓

初始化Replay

6. 初始化流程

例如：

用户选择：

XAUUSD

5分钟

2025年1月

数据库：

50000根K线

初始化：

currentIndex=100

显示：

0-100

7. 下一根K线逻辑

用户点击：

下一根

执行：

currentIndex++

获取：

market_data[currentIndex]

加入：

visible candles

刷新图表
伪代码：


void nextCandle(){


if(currentIndex < totalLength){


currentIndex++;


updateChart();


checkPosition();


}


}
8. 自动播放

功能：

模拟真实行情流动。

参数：

1X

2X

4X

8X

逻辑：

Timer.periodic()

每隔：

500ms

增加一根K线
代码逻辑：

Timer.periodic(

duration,

(timer){


nextCandle();


}

);


9. 回放暂停

状态：

isPlaying=false

停止Timer。

10. K线显示规则

默认：

显示：

100根

用户可以调整：

50

100

200

500

11. 时间控制

支持：

上一根

下一根

跳转日期

重新开始

12. 数据读取策略

禁止：

每次读取数据库全部数据。

正确：

分页读取。

例如：

第一次：

LIMIT 500

之后：

加载下一批

SQL:

SELECT *

FROM market_data

WHERE symbol='XAUUSD'

ORDER BY datetime

LIMIT 500 OFFSET 1000;

13. 缓存设计

内存缓存：

ReplayCache

保存：

最近1000根K线

目的：

提高滑动速度。

14. 交易撮合引擎

Replay Engine 每推进一根K线：

必须调用：

TradeEngine

流程：

新K线生成

↓

检查持仓

↓

判断止损

↓

判断止盈

↓

更新订单

15. 止损止盈逻辑
多单 BUY

检查：

如果：

low <= stopLoss

则：

平仓

价格：

stopLoss

如果：

high >= takeProfit

则：

平仓

价格：

takeProfit

空单 SELL

如果：

high >= stopLoss

止损

如果：

low <= takeProfit

止盈

16. 同一根K线同时触发处理

情况：

BUY:

开仓：

2650

止损：

2640

止盈：

2660

K线：

High:

2665

Low:

2635

同时触发。

处理规则：

默认：

保守模式

认为：

先止损。

原因：

避免回测过度乐观。

17. 滑点模拟

V1:

关闭

V2:

加入：

真实成交价格：

entryPrice + slippage

例如：

滑点：

0.5美元

18. 训练模式
新手模式

允许：

提示信号

普通模式

隐藏提示

专业模式

随机开始位置

禁止暂停

19. 随机训练模式

目的：

避免用户记忆行情。

流程：

随机选择：

历史日期

隐藏未来

开始训练。

20. Replay Controller设计

文件：

replay_controller.dart

职责：

管理：

当前K线
播放状态
时间
速度
用户操作

不负责：

数据库

21. Repository设计

ReplayRepository

负责：

读取K线

保存session

恢复进度

22. Service设计

ReplayService

负责：

下一根K线

播放控制

状态管理

23. 文件结构

lib/

features/

replay/

controller/

replay_controller.dart

service/

replay_service.dart

repository/

replay_repository.dart

models/

candle_model.dart

replay_state.dart

24. 测试要求

必须测试：

测试1

10000根K线加载

结果：

不卡顿

测试2

连续播放1000根

结果：

无内存泄漏

测试3

止损测试

输入：

BUY

价格：

100

止损：

95

K线最低：

94

结果：

自动平仓

25. AI开发规则

Codex开发Replay模块时必须：

不修改数据库结构
不修改交易模块
先输出架构方案
再生成代码
每次只完成一个文件
所有状态通过Controller管理
Widget不能包含交易逻辑
26. 完成标准

Replay Engine完成后：

用户可以：

导入历史黄金数据

↓

选择日期

↓

开始回放

↓

逐根查看K线

↓

买入卖出

↓

自动计算结果

↓

保存交易记录



)
