# Trading Trainer 数据库设计

版本：
V1.0


数据库：

SQLite


Flutter:

sqflite



# 1. 数据库文件


名称：

trading_trainer.db


位置：

Application Documents


---

# 2. 表设计


## 表1：行情数据


名称：

market_data


SQL:


CREATE TABLE market_data (

id INTEGER PRIMARY KEY AUTOINCREMENT,


symbol TEXT NOT NULL,


timeframe TEXT NOT NULL,


datetime TEXT NOT NULL,


open REAL,


high REAL,


low REAL,


close REAL,


volume REAL


);



用途：

保存黄金历史K线。



---

# 表2：训练记录


名称：

replay_session



SQL:


CREATE TABLE replay_session (


id INTEGER PRIMARY KEY AUTOINCREMENT,


symbol TEXT,


timeframe TEXT,


start_index INTEGER,


current_index INTEGER,


speed REAL,


status TEXT,


created_at TEXT


);



用途：

保存当前训练进度。



---

# 表3：模拟订单


名称：

trade_order



SQL:


CREATE TABLE trade_order (


id INTEGER PRIMARY KEY AUTOINCREMENT,


session_id INTEGER,


direction TEXT,


entry_price REAL,


exit_price REAL,


stop_loss REAL,


take_profit REAL,


lot REAL,


profit REAL,


open_time TEXT,


close_time TEXT,


status TEXT


);



direction:

BUY

SELL


status:

OPEN

CLOSED



---

# 表4：交易日志


名称：

trade_log



SQL:


CREATE TABLE trade_log (


id INTEGER PRIMARY KEY AUTOINCREMENT,


trade_id INTEGER,


strategy TEXT,


reason TEXT,


emotion TEXT,


image_path TEXT,


score INTEGER,


comment TEXT,


created_at TEXT


);



---

# 表5：用户设置


名称：

app_settings



SQL:


CREATE TABLE app_settings (


id INTEGER PRIMARY KEY,


key TEXT,


value TEXT


);



保存：

默认资金

默认仓位

默认周期



---

# 3. Flutter Model设计



## CandleModel


文件：

candle_model.dart



字段:


int id;

String symbol;

String timeframe;

DateTime datetime;

double open;

double high;

double low;

double close;

double volume;




---

## TradeOrderModel


字段:



int id;


String direction;


double entryPrice;


double exitPrice;


double stopLoss;


double takeProfit;


double lot;


double profit;


String status;




---

## ReplaySessionModel



字段:



int id;


String symbol;


String timeframe;


int currentIndex;


double speed;


String status;



---

# 4. Repository设计



结构:



repositories/


MarketRepository


TradeRepository


ReplayRepository


SettingsRepository



---

# 5. 数据流程



## K线读取



SQLite


↓

MarketRepository


↓

ReplayController


↓

CandleChart



---


## 下单流程



用户点击BUY


↓

TradeController


↓

TradeRepository


↓

SQLite


↓

更新UI



---


## 平仓流程



下一根K线


↓

TradeEngine


↓

检查：

止损

止盈


↓

更新订单



---

# 6. 索引优化



创建：


CREATE INDEX idx_market_time


ON market_data(datetime);



目的：

快速加载历史行情。



---

# 7. 数据量设计



支持：

500000根K线



单品种：

XAUUSD



周期：

1m

5m

15m

1H



---

# 8. AI扩展字段预留



trade_log:

增加：


ai_score


ai_analysis


ai_suggestion



用于：

AI交易教练。

