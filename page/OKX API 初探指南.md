# OKX API 初探指南

![Loading]()

![Loading]()

## 目录

1. What is the OKX API?
2. What is OKX?
3. Is OKX API free?
4. 为什么使用 OKX API？
5. 为什么不使用 OKX API？
6. OKX API 在哪些国家可用？
7. OKX API 的替代方案有哪些？
8. OKX API 支持哪些客户端？
9. 如何入门 OKX API？
10. 如何通过 OKX API 获取交易对信息？
11. 如何通过 OKX API 获取价格数据？
12. 如何通过 OKX API 获取历史数据？
13. 如何使用 OKX API 获取技术指标（如 20 SMA）？
14. 如何通过 OKX API 获取 Order Book 数据？
15. 如何通过 OKX API 获取交易数据？
16. 如何区分使用市价单和限价单下单？
17. 如何在 ETH 达到特定价格时执行 BTC 交易？
18. 如何在 BTC 5 分钟内波动 5% 时执行 ETH 交易？
19. 如何取消订单？
20. Full code

---

## What is the OKX API?

OKX API 是一种允许交易者通过编写代码在 OKX 平台上自动进行加密货币交易的接口方法。

---

## What is OKX?

OKX 是一家线上加密货币交易平台，支持交易超过 250 种币和代币。该平台自带云服务，并提供现货、杠杆及期货交易功能。

---

🚀 与 OKX 一起开启您的加密货币之旅！零手续费交易，使用最先进的 Web3 功能，加入数百万全球交易者的行列。新用户可获得高达 100 USDT 的独家欢迎奖金！今天就与世界领先的数字资产平台一起开始您的交易冒险吧。

👉 OKX 新人限时优惠，最高可领取 100 USDT 奖励 ： [OKX活动页面](https://bit.ly/OKXe) | [国内镜像地址（免翻墙）](https://bit.ly/okX)

---

## Is OKX API free?

注册并试用 OKX API 完全免费，费用仅在实际交易时产生。OKX 的费用结构比大多数其他加密货币交易平台要复杂。  
主要影响费用的因素有用户类型（普通用户或 VIP 用户）以及持有 OKB（OKX 原生代币）的数量。

对于普通用户，现货交易费用基于持有 OKB 的总量；  
而 VIP 用户则根据按月交易量（以 USD 计）分为 7 个等级，均采用 maker/taker 费用模式。  
此外，期货市场的费用结构与现货市场略有不同，下方展示了两种用户的费用表格示例。

---

## 为什么不使用 OKX API？

- 部分用户反馈客服响应不及时
- 提现转账存在一定限制

---

## OKX API 在哪些国家可用？

OKX 致力于全球化服务，但由于某些严格的法规和司法管辖问题，以下国家/地区无法使用该平台：
  
Hong Kong, Cuba, Iran, North Korea, Crimea, Sudan, Malaysia, Syria, United States (包括所有美国领土), Bangladesh, Bolivia, Ecuador, 和 Kyrgyzstan。

---

## OKX API 的替代方案有哪些？

对于部分用户而言，其他交易平台可能更贴合个人需求。您可以根据自己的交易习惯选择合适的平台替代 OKX。

---

## OKX API 支持哪些客户端？

OKX API 目前支持多种编程语言及客户端，便于交易者根据各自的需求选择最适合的开发环境。

---

## 如何入门 OKX API？

要开始使用 OKX API 并部署交易策略，首先需要前往官网获取 API Key。  
点击注册：https://bit.ly/OKXe  
注册流程简单：输入您的邮箱、设置密码，并按照邮件提示输入 6 位验证码。完成后，进入个人资料区域，选择 API 进行进一步设置。  
接着，启用 2FA（例如使用手机验证或 Google Authenticator），进入 API 区域并点击 “+Create V5 API Key” 按钮。  
您可以在创建时指定 API Key 权限、名称等。最后，系统会生成 API Key 和 Secret Key，请妥善保管以备后用。

---

## 如何通过 OKX API 获取交易对信息？

获取交易对信息可使用 tickers 接口，需指定所需的交易市场类型（如 Spot、Swap、Futures 或 Option）。  
下面的示例代码演示如何导入相关库并获取现货市场的全部交易对，然后用 pandas 整理数据：

python
import requests
import pandas as pd

url = 'https://www.okx.com'
tickers = pd.DataFrame(requests.get(url + '/api/v5/market/tickers?instType=SPOT').json()['data'])
tickers = tickers.drop('instType', axis=1)
print(tickers.tail().T)


该示例显示现货市场共有 505 个交易对，如需其它市场数据，只需将“SPOT”替换为对应市场类型（例如 “FUTURES”）。

---

## 如何通过 OKX API 获取价格数据？

使用指定的 instrument id（交易对代码和所属交易市场）即可获取价格数据。  
以下示例展示如何获取 BTC-USD-SWAP 的价格数据：

python
ticker = requests.get(url + '/api/v5/market/ticker?instId=BTC-USD-SWAP').json()
print(ticker)


返回数据中包含最新成交价格、买卖盘价格、开盘价以及其他交易信息。

---

## 如何通过 OKX API 获取历史数据？

获取历史数据时，您需根据需求选择合适的接口。主要有以下四种：
  
- **Get Candlesticks** – 获取最新 1440 条按指定周期分组的蜡烛图数据
- **Get Candlesticks History (top currencies only)** – 获取热门币种近年历史蜡烛图数据
- **Get Index Candlesticks** – 获取指数蜡烛图数据
- **Get Mark Price Candlesticks** – 获取标记价格的蜡烛图数据

下面以第二种接口为例，获取 BTC-USDT-SWAP 的历史数据并整理为 pandas DataFrame：

python
historical = pd.DataFrame(requests.get(url + '/api/v5/market/history-candles?instId=BTC-USDT-SWAP').json()['data'])
print(historical)


数据初步返回后，由于字段标记并不直观，建议根据官方文档重新命名列并转换 Unix 时间：

python
historical.columns = ["Date", "Open", "High", "Low", "Close", "Vol", "volCcy"]
historical['Date'] = pd.to_datetime(historical['Date'], unit='ms')
historical.set_index('Date', inplace=True)
historical.sort_values(by='Date', inplace=True)
print(historical)


如此整理过的数据便于后续技术指标计算与图表展示。

---

## 如何使用 OKX API 获取技术指标（如 20 SMA）？

虽然 OKX API 不直接提供技术指标数据，但可以利用 pandas 或 btalib 库自行计算。例如，下面的示例展示如何计算并绘制简单移动平均线（20 SMA）：

python
historical['20 SMA'] = historical['Close'].rolling(20).mean()
print(historical.tail())


利用 plotly 绘制蜡烛图和 20 SMA 指标图：

python
import plotly.graph_objects as go

fig = go.Figure(data=[
    go.Candlestick(x=historical.index,
                   open=historical['Open'],
                   high=historical['High'],
                   low=historical['Low'],
                   close=historical['Close']),
    go.Scatter(x=historical.index, y=historical['20 SMA'], line=dict(color='purple', width=1))
])
fig.show()


---

## 如何通过 OKX API 获取 Order Book 数据？

通过 Get Order Book 接口，指定交易对和订单深度参数即可获得订单簿数据，其中数据分为买单（bid）和卖单（ask）部分。

python
book = requests.get(url + '/api/v5/market/books?instId=BTC-USD-SWAP&sz=10').json()
print(book['data'])


若要将买单和卖单分别整理成 DataFrame，可执行如下步骤：

python
ask = pd.DataFrame(book['data'][0]['asks'])
bid = pd.DataFrame(book['data'][0]['bids'])
print(ask)


数据的每一行依次表示：
- 价格
- 该价格的数量
- 涉及清算订单数量
- 该价格的订单数

下面将 bid 和 ask 数据合并，并对相关字段重新命名：

python
bid.pop(2)
ask.pop(2)
df = pd.merge(bid, ask, left_index=True, right_index=True)
df = df.rename({"0_x": "Bid Price", "1_x": "Bid Size", "3_x": "Bid Amount",
                "0_y": "Ask Price", "1_y": "Ask Size", "3_y": "Ask Amount"}, axis='columns')
print(df.head())


---

## 如何通过 OKX API 获取交易数据？

利用 Get Trades 接口可以获取最近的交易数据。例如，以下代码获取 BTC-USDT 的交易记录：

python
trades = requests.get(url + '/api/v5/market/trades?instId=BTC-USDT').json()
print(trades['data'])


返回结果中包含交易方向、成交量、成交价格及交易时间等信息。

---

## 如何区分使用市价单和限价单下单？

市价单与限价单在下单时除了价格参数略有不同外，最大的区别在于 `sz` 参数的含义。  
对于市价单，`sz` 参数代表买入时以第二种货币计量的数量，而限价单时则以目标币种计算。  
因此，在设计交易策略时，需要特别注意 `sz` 参数的定义。

---

## 如何在 ETH 达到特定价格时执行 BTC 交易？

此示例演示如何构建一个基于价格触发的交易逻辑：当 ETH 达到设定价格（例如 3000 美元）时，执行 BTC 市价单交易。  
实现思路是首先构建订单框架，然后进入循环不断检查 ETH 价格；若达到预设条件，则执行市价单。  
为确保交易安全，下单后程序还会暂停几秒钟，再次确认订单是否已全部成交。  
（此处的示例代码依赖于 OKX 官方的 Python SDK，需参考 SDK 文档进行开发。）

---

## 如何在 BTC 5 分钟内波动 5% 时执行 ETH 交易？

策略核心在于实时监控 BTC 与 ETH 的价格变化。当检测到 BTC 在过去 5 分钟内波动达到或超过 5% 时，程序将执行 ETH 交易。  
流程包括：
1. 定时获取 BTC 和 ETH 当前价格；
2. 计算过去 5 分钟的百分比变化；
3. 若变化未达到 5%，程序休眠 5 分钟后重新检查；
4. 一旦达到或超过 5%，执行交易，并稍作等待后确认订单成交情况。  
具体代码实现需要根据实际需求进行调整。

---

## 如何取消订单？

取消订单操作通过 Cancel Order 接口完成。以下代码摘自 SDK 文档，展示了取消订单的基本方法：

python
# 示例代码（请参考官方 SDK 文档以获取最新实现）
response = requests.post(url + '/api/v5/trade/cancel-order', data={
    "instId": "BTC-USDT",
    "ordId": "请输入订单号"
})
print(response.json())


---

## Full code

以上各部分代码组合即为 OKX API 的完整应用示例。您可以根据实际交易需求进一步修改和完善代码，实现自动化交易策略。


**总结：**  
本文以简洁明了的方式介绍了 OKX API，从基本概念、功能接口、数据获取到示例代码演示，帮助读者快速上手。通过合理的代码示例和图表展示，您可以全面了解如何利用 OKX API 实现自动化交易策略。