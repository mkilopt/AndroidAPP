# Trading Trainer
# Development Roadmap

版本：
V1.0

开发方式：
AI辅助开发（Codex / Cursor）


---

# 0. 总体开发阶段


项目分为：

Phase 0 项目初始化

Phase 1 基础架构

Phase 2 数据系统

Phase 3 K线系统

Phase 4 Replay系统

Phase 5 交易系统

Phase 6 统计系统

Phase 7 AI教练

Phase 8 优化发布



---

# Phase 0
# 项目初始化


目标：

创建Flutter工程。


---

## Task 0.1 创建项目
创建Flutter项目。

要求：

Flutter 3.x

Material3

Dark Theme

Riverpod

Clean Architecture

创建基础目录。

不要开发业务功能。

输出：

目录结构。



完成标准：

✓ APP运行

✓ 页面显示

✓ 项目结构完成


---

# Phase 1
# 基础架构


目标：

建立代码基础。


---

## Task 1.1


开发：

主题系统


文件：



core/theme/



完成：

- 深色主题
- 字体
- 全局颜色


---

## Task 1.2


开发：

路由系统


使用：

go_router


页面：

Home

Replay

History

Settings



---

## Task 1.3


开发：

SQLite基础服务



文件：


core/database/



完成：

- 创建数据库
- 打开数据库
- Migration


---

# Phase 2
# 行情数据系统


目标：

让APP可以读取黄金历史行情。



---

## Task 2.1


创建：

Candle Model



字段：


datetime

open

high

low

close

volume




---

## Task 2.2


创建：

market_data表



完成：

SQL

Migration



---

## Task 2.3


开发CSV导入


功能：


选择文件

↓

解析

↓

保存SQLite



测试：

导入10万根K线。



---

# Phase 3
# K线图系统


目标：

显示黄金行情。



---

## Task 3.1


接入K线组件


要求：

支持：

缩放

拖动

十字线



---

## Task 3.2


开发：

ChartRepository



功能：

读取K线。



---

## Task 3.3


开发：

ChartController



负责：

管理显示数据。



---

# Phase 4
# Replay Engine


目标：

实现历史回放。



---

## Task 4.1


开发：

ReplayState



保存：

当前K线位置

播放状态

速度



---

## Task 4.2


开发：

ReplayController



功能：

下一根K线

上一根K线

暂停

播放



---

## Task 4.3


开发：

ReplayService



功能：

加载历史数据

控制时间



---

## Task 4.4


完成：

隐藏未来K线测试。



测试：

10000根K线。



---

# Phase 5
# Trade Engine


目标：

实现模拟交易。


---

## Task 5.1


创建：

Order Model



---

## Task 5.2


创建：

Trade数据库表



---

## Task 5.3


开发：

开仓功能


支持：

BUY

SELL



---

## Task 5.4


开发：

止损止盈



测试：


BUY:

2350


SL:

2340


TP:

2370



---

## Task 5.5


开发：

盈亏计算



---

# Phase 6
# 交易日志系统


目标：

保存训练过程。


---

## Task 6.1


交易记录页面



显示：

时间

方向

盈利



---

## Task 6.2


交易详情



显示：

K线截图

交易理由

备注



---

## Task 6.3


统计系统



计算：

交易次数

胜率

盈亏比

最大回撤



---

# Phase 7
# AI Coach


目标：

AI交易复盘。


---

## Task 7.1


创建：

AI Service



接口：



analyzeTrade()




---

## Task 7.2


设计：

AI Prompt模板



---

## Task 7.3


生成：

交易评分



输出：


评分

问题

建议



---

# Phase 8
# 产品优化


---

## Task 8.1


性能优化



目标：


加载50万K线不卡顿。


---

## Task 8.2


UI优化



优化：

交易体验

动画

交互



---

## Task 8.3


Android发布



完成：

APK

签名

测试



---

# 每次给Codex的开发模板



你现在是Trading Trainer项目工程师。

请严格遵守：

PRD.md

UI_SPEC.md

DATABASE_DESIGN.md

REPLAY_ENGINE_DESIGN.md

TRADE_ENGINE_DESIGN.md

AI_COACH_DESIGN.md

当前任务：

【填写Task编号】

执行要求：

先分析方案
列出修改文件
再生成代码
不修改无关模块
保持Clean Architecture
完成后告诉我测试方法

开始。



---

# 项目完成验收标准


## 功能验收


用户可以：


导入黄金历史数据

↓

选择日期

↓

开始回放

↓

逐根查看K线

↓

模拟交易

↓

设置止损止盈

↓

自动计算盈亏

↓

保存交易日志

↓

AI分析交易



---

# 第一版发布目标


APK大小：

<100MB


启动：

<3秒


支持：

Android 10+


数据：

50万K线


运行：

完全离线


Codex Prompt:

