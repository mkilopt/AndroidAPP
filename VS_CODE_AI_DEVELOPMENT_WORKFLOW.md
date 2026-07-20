# Trading Trainer
# VS Code AI Development Workflow

版本：
V1.0


开发环境：

VS Code

Flutter

Dart

Codex / AI Assistant


---

# 1. 开发原则


采用：

人负责设计

AI负责编码

人负责验证


AI不能：

一次生成整个APP。


必须：

模块化开发。


---

# 2. VS Code项目打开方式


目录：

Trading_Trainer/


打开：

VS Code

↓

File

↓

Open Folder

↓

选择 Trading_Trainer


---

# 3. VS Code插件要求


必须安装：


## Flutter


作用：

Flutter开发支持。



## Dart


作用：

Dart语法支持。



## Flutter Widget Snippets


作用：

快速生成Widget。



## SQLite Viewer


作用：

查看本地数据库。



## Git（可选）


作用：

版本管理。



---

# 4. 项目初始化流程


终端执行：
进入：

cd trading_trainer


运行：

flutter run


确认：

APP正常启动。

5. AI开发流程

每次开发：

固定流程：

Step 1

告诉AI当前任务

例如：

开发Task 2.1：

创建Candle Model

参考：

DATABASE_DESIGN.md

要求：

不要开发其他模块。

Step 2

AI先分析

要求AI输出：

修改方案
文件列表
实现步骤
Step 3

AI生成代码

AI修改：

指定文件。

Step 4

人工测试

执行：

flutter run

Step 5

确认后进入下一任务。

6. AI开发提示模板

每次复制：

你现在是Trading Trainer Flutter工程师。


当前任务：

【任务名称】


参考文件：

PRD.md

PROJECT_STRUCTURE.md

DATABASE_DESIGN.md


要求：

1. 先分析

2. 列修改文件

3. 再写代码

4. 不修改无关模块

5. 保持Flutter规范

6. 完成后告诉我测试方法。


开始。

7. VS Code文件检查

开发后检查：

目录：

lib/


确认：

core

features

shared

没有混乱。

8. 每完成一个模块

执行：

格式检查：

flutter analyze


代码格式：

dart format .


测试：

flutter test

9. Debug流程

出现错误：

不要直接让AI重写。

发送：

Flutter运行错误：


【复制错误信息】


请：

1. 分析原因

2. 找出文件

3. 最小修改解决

4. 不改变架构。


10. AI修改限制

禁止AI：

❌ 删除大量代码

❌ 重构整个项目

❌ 修改数据库结构

❌ 修改核心交易逻辑

除非：

明确要求。

11. 文件备份规则

每完成一个阶段：

复制项目。

例如：

TradingTrainer_v0.1

TradingTrainer_v0.2

TradingTrainer_v0.3

12. 开发阶段检查
阶段1

Flutter运行

完成：

□ 页面显示

□ 路由正常

阶段2

数据库

完成：

□ 创建表

□ 导入数据

阶段3

Replay

完成：

□ K线显示

□ 下一根

阶段4

交易

完成：

□ BUY

□ SELL

□ SL

□ TP

13. APK生成

测试版本：

flutter build apk --debug


正式版本：

flutter build apk --release


生成：

build/app/outputs/flutter-apk/

14. AI开发最佳实践

推荐顺序：

不要说：

"帮我开发整个APP"

应该说：

"开发ReplayController"

"开发TradeEngine"

"开发CSV导入"

"测试止损逻辑"

15. 最终开发流程
PRD设计

↓

创建Flutter项目

↓

数据库

↓

行情导入

↓

K线

↓

Replay

↓

模拟交易

↓

交易日志

↓

统计

↓

AI Coach

↓

APK发布

完成目标

使用：

VS Code

Flutter

AI助手

独立完成：

Trading Trainer Android APP。


```bash
flutter create trading_trainer
