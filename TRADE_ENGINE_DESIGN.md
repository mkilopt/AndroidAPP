Trading Trainer
Trade Engine Design

版本：
V1.0

模块：
模拟交易撮合引擎

1. 模块目标

Trade Engine 模拟真实交易环境。

用户在历史行情中：

看到机会

↓

决定交易

↓

提交订单

↓

系统模拟成交

↓

管理仓位

↓

计算结果

↓

生成交易记录

2. 设计原则
2.1 不预测行情

Trade Engine 不负责：

判断涨跌
推荐买卖
自动交易

只负责：

执行用户决定。

2.2 交易规则透明

所有计算必须可追踪：

例如：

为什么止损？

为什么盈利？

什么时候成交？

必须保存记录。

3. 核心对象设计
3.1 Order订单

文件：

order_model.dart

结构：

class Order {

int id;


String symbol;


String direction;


double volume;


double entryPrice;


double stopLoss;


double takeProfit;


DateTime openTime;


String status;


}

direction:

BUY

SELL

status:

OPEN

CLOSED

CANCELLED
4. Position持仓设计

文件：

position_model.dart

结构：

class Position {


int id;


int orderId;


String direction;


double openPrice;


double currentPrice;


double floatingProfit;


double volume;


}

作用：

保存当前未平仓交易。

5. 开仓流程

用户点击：

BUY

流程：

TradePanel

↓

TradeController

↓

TradeService

↓

TradeEngine

↓

SQLite

6. 开仓规则
BUY

成交价格：

当前K线收盘价

例如：

当前：

2350

用户点击BUY

成交：

2350

SELL

成交：

当前价格。

7. 开仓检查

开仓前检查：

资金

例如：

账户：

10000美元

风险：

2%

允许：

200美元

仓位

计算：

风险金额 ÷ 止损距离
8. 持仓管理

每出现新K线：

Replay Engine调用：

TradeEngine.onNewCandle()

流程：

新K线

↓

读取持仓

↓

检查止损

↓

检查止盈

↓

更新浮盈

↓

保存状态

9. 止损规则
BUY

如果：

Low <= StopLoss

执行：

Close Position


成交：

StopLoss价格。

SELL

如果：

High >= StopLoss

执行：

平仓。

10. 止盈规则
BUY

如果：

High >= TakeProfit

平仓。

SELL

如果：

Low <= TakeProfit

平仓。

11. 盈亏计算
BUY

公式：

Profit =
(exitPrice - entryPrice)
× volume

SELL

公式：

Profit =
(entryPrice - exitPrice)
× volume

12. 点值计算

黄金：

XAUUSD

默认：

1 lot = 100 ounces


示例：

买入：

0.1 lot

黄金上涨：

10美元

盈利：

10 × 100 × 0.1

=100美元

13. 手续费设计

V1：

关闭

V2加入：

字段：

commission

swap

spread

14. 滑点设计

V1:

无滑点

V2:

增加：

slippage

例如：

BUY:

实际成交：

2350.3

15. 同K线冲突处理

情况：

BUY

止盈：

2360

止损：

2340

当前K线：

High：

2365

Low：

2335

两个都触发。

默认规则：

保守模式：

先触发止损

原因：

避免模拟结果过于理想。

16. 账户资金系统

Account Model

字段：

balance

equity

margin

availableMargin


示例：

初始：

10000美元

盈利：

+500

余额：

10500

17. 风险管理

用户设置：

风险比例：

例如：

2%

系统计算：

最大亏损：

balance × 2%

18. 交易记录生成

平仓后自动创建：

trade_log

内容：

交易时间

方向

入场

出场

盈亏

持仓时间

19. Trade Engine 文件结构
features/


trade/


models/

order_model.dart

position_model.dart


controller/

trade_controller.dart


service/

trade_engine.dart


repository/

trade_repository.dart


20. 核心接口设计
开仓
openTrade(OrderRequest request)

平仓
closeTrade(positionId)

新K线通知
onNewCandle(Candle candle)

获取当前持仓
getPositions()

统计交易
getStatistics()

21. Trade Engine 与 Replay关系

架构：

                 K线数据

                    |

                    ↓


              Replay Engine


                    |

                    ↓


             Trade Engine


                    |

        ---------------------

        |                   |

     Position           Account


                    |

                    ↓


              SQLite


22. 单元测试要求

必须测试：

测试1 开仓

输入：

BUY

价格：

2000

结果：

生成订单。

测试2 止损

BUY:

2000

止损：

1990

K线：

Low=1988

结果：

自动平仓。

测试3 盈利

BUY:

2000

止盈：

2020

High：

2025

结果：

盈利。

测试4 空单

SELL:

2000

价格下降：

1980

结果：

盈利。

23. AI开发规则

Codex开发Trade Engine：

必须：

不写UI
不直接操作数据库
使用Repository
所有交易逻辑集中在TradeEngine
所有计算必须有测试
修改前说明影响范围
24. 完成标准

Trade Engine完成后：

用户可以：

✅ 开多

✅ 开空

✅ 设置止损

✅ 设置止盈

✅ 自动平仓

✅ 查看盈亏

✅ 保存交易记录

✅ 统计交易结果
