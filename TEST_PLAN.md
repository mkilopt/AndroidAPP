# Trading Trainer
# Test Plan

版本：
V1.0


项目：

AI交易训练器APP


测试目标：

确保APP稳定、准确、可维护。


---

# 1. 测试原则


## 1.1 每个模块独立测试


开发完成：

必须测试。


禁止：

多个模块一起修改后再测试。


---

## 1.2 核心交易逻辑必须100%测试


重点：

- Replay Engine
- Trade Engine
- 盈亏计算
- 数据加载


---

# 2. 测试环境


## Android


支持：

Android 10+

Android 11

Android 12

Android 13

Android 14


---

## Flutter


版本：

Flutter 3.x


---

## 数据规模


测试数据：

XAUUSD


数量：

500000根K线


---

# 3. 单元测试(Unit Test)

test/



---

# 4. 数据模块测试


## Test 4.1 CSV解析


输入：

正确CSV


结果：

成功解析。


测试：


```csv
datetime,open,high,low,close

2025-01-01,2650,2655,2648,2652

期待：

生成Candle对象。

Test 4.2 错误数据

输入：

datetime,null,null

结果：

返回错误。

Test 4.3 数据重复

输入：

相同时间K线。

结果：

跳过重复。

5. SQLite测试
Test 5.1 建库

启动APP。

检查：

数据库创建。

Test 5.2 建表

检查：

存在：

market_data

trade_order

trade_log

replay_session

Test 5.3 数据数量

导入：

100000根

查询：

数量一致。

6. Replay Engine测试

这是核心测试。

Test 6.1 隐藏未来数据

输入：

10000根K线

开始：

index=100

检查：

Chart只能看到：

0-100

不能访问：

101以后。

Test 6.2 下一根K线

初始：

index=100

执行：

nextCandle()

结果：

index=101

Test 6.3 上一根K线

执行：

previousCandle()

结果：

index减少。

Test 6.4 自动播放

启动：

1x

运行：

10秒

结果：

K线自动增加。

Test 6.5 暂停

点击暂停。

结果：

Timer释放。

7. Trade Engine测试

最高优先级。

Test 7.1 BUY开仓

输入：

方向：

BUY

价格：

2000

仓位：

0.1

结果：

生成订单。

Test 7.2 SELL开仓

输入：

SELL

结果：

生成订单。

Test 7.3 BUY止损

订单：

BUY

入场：

2000

止损：

1990

新K线：

Low:

1988

结果：

自动平仓。

Test 7.4 BUY止盈

订单：

BUY

入场：

2000

止盈：

2020

High:

2025

结果：

盈利。

Test 7.5 SELL止损

SELL：

2000

SL：

2010

High：

2015

结果：

止损。

Test 7.6 SELL止盈

SELL：

2000

TP：

1980

Low：

1975

结果：

盈利。

8. 盈亏计算测试
黄金计算

条件：

BUY

价格：

2000

平仓：

2010

仓位：

1 lot

结果：

盈利：

1000美元

(按照1lot=100oz)

9. 冲突测试

情况：

BUY:

Entry:

2000

SL:

1990

TP:

2010

K线：

High:

2015

Low:

1985

结果：

保守模式：

止损优先。

10. UI测试

检查：

首页

确认：

按钮正常。

Replay页面

确认：

K线显示。

按钮：

BUY

SELL

下一根

正常。

历史记录

确认：

交易显示。

11. 性能测试
Test 11.1 大数据加载

数据：

500000根K线

要求：

APP不卡死。

Test 11.2 Replay速度

连续播放：

10000根

要求：

无明显卡顿。

Test 11.3 内存

运行30分钟。

要求：

无持续增长。

12. 数据安全测试

检查：

APP关闭。

重新打开。

确认：

交易记录存在。

卸载APP：

数据清除。

符合Android规则。

13. AI Coach测试
输入测试

输入：

完整交易。

结果：

返回JSON。

异常测试

AI接口失败。

结果：

提示：

分析失败。

不能影响交易系统。

14. 回归测试

每次代码更新必须执行：

1 数据导入

2 K线显示

3 Replay

4 开仓

5 止损

6 止盈

7 日志

8 统计

15. 发布测试

发布APK前：

检查：

□ APP启动

□ 数据库创建

□ 导入数据

□ Replay

□ 模拟交易

□ 日志保存

□ AI分析

□ 横竖屏

□ Android权限

16. 自动化测试

未来加入：

Flutter Test

Integration Test

CI/CD

17. Codex测试规则

AI修改代码后：

必须输出：

修改内容
测试项目
测试结果
潜在风险

禁止：

直接修改大量代码。

18. 完成标准

测试通过：

APP达到：

稳定运行

交易计算准确

Replay真实

数据安全

性能满足要求
目录：

