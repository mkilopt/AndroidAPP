# Trading Trainer UI设计规范

版本：
V1.0

平台：
Android

技术：
Flutter Material 3


# 1. UI设计原则

目标：

模拟专业交易软件体验。

设计方向：

- 简洁
- 高信息密度
- 深色交易风格
- 操作快速
- 减少误操作


主题：

Dark Mode优先


颜色规范：

背景：

#121212


卡片：

#1E1E1E


盈利：

绿色


亏损：

红色


辅助：

灰色


---

# 2. 页面结构


BottomNavigationBar


包含：

1. 首页

2. 训练

3. 记录

4. 设置


结构：

lib/presentation/pages/


home/

replay/

history/

settings/


---

# 3. 首页 HomePage


文件：

home_page.dart


功能：

APP入口。


布局：


--------------------------------

Trading Trainer


今日训练：

0 / 10


-------------------------------


开始训练


-------------------------------


最近交易


交易次数：

120


胜率：

65%


-------------------------------


数据状态

XAUUSD

125000 candles


--------------------------------


组件：

HomeHeader

TrainingCard

RecentTradeCard

DataStatusCard


---

# 4. 数据管理页面


DataPage


功能：

管理历史行情。


页面：

--------------------------------


行情数据


XAUUSD


周期：

5分钟


数量：

250000


时间：

2020-2025


--------------------------------


按钮：

导入CSV


删除数据


--------------------------------


组件：

DataCard

ImportButton


---

# 5. 核心训练页面


ReplayPage


这是APP核心。


结构：


--------------------------------


顶部信息栏


资金

10000


时间

2025-01-01


--------------------------------


K线区域


ChartWidget


--------------------------------


交易面板


BUY

SELL


--------------------------------


Replay控制


上一根

下一根

播放

速度


--------------------------------



组件：

CandleChart

TradePanel

ReplayController

PositionCard


---

# 6. K线组件


CandleChart


要求：

支持：

- 放大
- 缩小
- 拖动
- 十字线


输入：

List<Candle>


输出：

当前价格


---

# 7. 下单组件


TradePanel


按钮：


BUY按钮


点击：

打开：

OrderDialog



OrderDialog:


字段：

方向：

BUY


价格：

自动


数量：

输入


止损：

输入


止盈：

输入



确认交易



---

# 8. 订单详情页面


TradeDetailPage



显示：


交易方向：

BUY


入场：

2650


出场：

2675


盈亏：

+250


持仓：

2小时


策略：

突破回踩


备注：

文本


截图：

图片


---

# 9. 交易历史页面


HistoryPage


显示：


--------------------------------


交易001


BUY


+250


2025-01-01



--------------------------------


交易002


SELL


-100



--------------------------------



筛选：

日期

方向

盈亏


---

# 10. 统计页面


StatisticsPage


显示卡片：


总交易：

300


胜率：

68%


盈利：

200


亏损：

100


平均盈亏比：

2.1


最大回撤：

8%



组件：

StatisticCard


---

# 11. 设置页面


SettingsPage


功能：

默认资金


默认仓位


默认周期


数据管理


关于



---

# 12. Flutter组件规范


所有页面：

xxx_page.dart


组件：

xxx_widget.dart


状态：

xxx_controller.dart


模型：

xxx_model.dart


---

# 13. UI开发要求


AI必须：

1. 使用Material3

2. 使用Responsive布局

3. 不把业务逻辑写入Widget

4. 页面只负责UI

5. Controller负责状态

6. Repository负责数据
