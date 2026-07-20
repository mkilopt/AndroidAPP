Trading Trainer
Development Execution Plan

版本：
V1.0

开发环境：

VS Code
Flutter
Dart
SQLite
Android
第一阶段：创建项目骨架

目标：

让APP具备基础结构。

Task 001

创建Flutter项目结构。

AI指令：

根据PROJECT_STRUCTURE.md创建Trading Trainer项目目录。

要求：

1. 使用Clean Architecture
2. 创建core目录
3. 创建features目录
4. 创建shared目录
5. 配置Material3主题
6. 配置Riverpod

暂时不要开发业务功能。

完成：

检查：

flutter run

APP启动成功。

第二阶段：基础框架开发
Task 002

开发主题系统。

文件：

core/theme/

完成：

深色交易主题
全局颜色
字体
Task 003

开发路由。

页面：

HomePage

ReplayPage

HistoryPage

StatisticsPage

SettingsPage

使用：

go_router

完成：

底部导航。

第三阶段：SQLite数据库
Task 004

创建数据库。

AI指令：

根据DATABASE_DESIGN.md创建SQLite数据库。

包括：

market_data

trade_order

trade_log

replay_session

app_settings


要求：

创建Migration机制。

测试：

启动APP自动创建数据库。

第四阶段：黄金数据导入
Task 005

开发CSV导入。

功能：

用户选择：

XAUUSD历史数据CSV

流程：

文件选择

↓

解析

↓

验证

↓

写入SQLite

测试：

导入：

10000根K线。

第五阶段：K线显示
Task 006

开发K线页面。

页面：

ReplayPage

功能：

显示：

黄金K线

支持：

缩放

拖动

暂时：

不交易。

第六阶段：Replay Engine
Task 007

开发：

ReplayState

保存：

currentIndex

speed

isPlaying

visibleCandles
Task 008

开发：

ReplayController

实现：

按钮：

下一根

上一根

播放

暂停

测试：

隐藏未来K线。

第七阶段：模拟交易
Task 009

开发：

Trade Model

创建：

Order

Position

Task 010

开发：

BUY/SELL

功能：

点击：

BUY

生成订单。

Task 011

开发：

止损止盈。

测试：

BUY:

价格：

2650

SL:

2640

TP:

2670

播放行情：

自动关闭。

第八阶段：交易日志
Task 012

开发：

交易记录页面。

显示：

时间
方向
盈亏
Task 013

交易详情。

增加：

交易理由
截图
备注
第九阶段：统计系统
Task 014

开发统计。

显示：

交易次数

胜率

盈亏比

最大回撤

第十阶段：AI Coach
Task 015

开发AI接口。

输入：

交易数据

K线环境

输出：

JSON报告。

Task 016

AI分析页面。

显示：

评分：

85

问题：

追涨

建议：

等待确认

第十一阶段：优化
Task 017

性能优化。

目标：

支持：

50万K线。

Task 018

UI优化。

Task 019

发布APK。

每次开发固定流程

在VS Code打开AI助手。

发送：

你现在开发Trading Trainer项目。

参考：

PRD.md

PROJECT_STRUCTURE.md

当前任务：

Task XXX


要求：

1. 先分析方案

2. 列修改文件

3. 生成代码

4. 不修改其他模块

5. 输出测试方法


开始。
第一版完成顺序

不要改变：

项目骨架

↓

SQLite

↓

CSV导入

↓

K线

↓

Replay

↓

交易

↓

日志

↓

统计

↓

AI

↓

发布
