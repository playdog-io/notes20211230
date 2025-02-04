## 221105

option  
期权  
option 意思是可以选择性行驶它而非像 forward（远期协议，远期交易） or futures（期货） 那样 必须 在最终交易时交换.

put option  
看跌期权

sell put option  
卖出看跌期权，那就是看涨或者更准确点说是看不跌，因为即使价格不变，你卖出后会获得费用

futures  
期货

## 230123

### ATR/平均真实波幅 指标

```
ATR指标的计算原理和代码实现

ATR指标的计算步骤可大致分为两步：

第一步：计算真实波幅（TR）。

即今日振幅（MAX((HIGH-LOW)）、今日最高与昨收差价（ABS(REF(CLOSE,1)-HIGH))），今日最低与昨收差价（ABS(REF(CLOSE,1)-LOW)）中的最大值。

TR=MAX(MAX((HIGH-LOW),ABS(REF(CLOSE,1)-HIGH)),ABS(REF(CLOSE,1)-LOW))

第二步：利用一段时间的均值计算平均真实波幅（ATR）。

参数N为K线数，一般取14。也可根据习惯的不同，使用10/20/60等值。

ATR=MA(TR,N)

```

https://xueqiu.com/8694603268/221424142

## 230131

### RSI/Relative Strength Index/相对强弱指数

#### 实际中发现 df 长度不一样算出来结果不一样，如以近 14 个单位为周期，df 长度 15 和 150 的结果却不一样。

#### pandas_ta 和 talib 中 rsi 的值也是周期越长越相近

https://zh.wikipedia.org/wiki/%E7%9B%B8%E5%B0%8D%E5%BC%B7%E5%BC%B1%E6%8C%87%E6%95%B8

相对强弱指数（英语：Relative Strength Index，縮寫：RSI），是一个借由比较价格升降运动，以表达价格强度的技术分析工具；它是以动量为基础的振荡指标，用来测量价格动向的快慢(速度)和变化(幅度)。以 RSI 之高低来决定买卖时机是根据涨久必跌，跌久必涨之原则。以 RSI 作为买卖研判时，通常会设定区域界线[1]。

根据威尔德的测量结果，当 n=14 时，指数最具代表性。他指出当某证券的 RSI 升至 70 时，代表该证券已被超买（Overbought），投资者应考虑出售该证券。相反，当证券 RSI 跌至 30 时，代表证券被超卖（Oversold），投资者应购入该证券。

当某证券的价格变动倾向（上升或下跌）越趋极端，价格变动逆转的可能性将越大。当 RSI 达 80 或 20 时，证券已被严重超买或超卖，投资者此时更应小心留意此类证券。然而，当该衍生工具市场处于利市状态（即牛市），严重超买或超卖的数值应被适当地向上调升，反之亦然。

rs = sma(u,n)/sma(d,n) 或 rs = ema(u,n)/ema(d,n)

rsi = (1-1/(1+rs))\*100%

```
add230525 例子

第一天 23.70
第二天 27.90 +4.20
第三天 26.50 -1.40
第四天 29.60 +3.10
第五天 31.10 +1.50
第六天 29.40 -1.70
第七天 25.50 -3.90
第八天 28.90 +3.40
第九天 20.50 -8.40
第十天 23.30 +2.80
（1－10 天之和）=15.00（升）+15.40（降）
15÷9=1.67 15.40÷9=1.71
前十天上升平均数=(4.20+3.10+1.50+3.40+2.80)/9=1.67
前十天下降平均数=(1.40+1.70+3.90+8.40)/9=1.71
第十天 RSI=[1.67÷（1.67+1.71)]×100=49.41
如果第十一天收市价为 25.30，则
第十一天上升平均数=(1.67× 2.10）÷9=1.72
第十一天下跌平均数=1.71×8÷9=1.52
第十一天 RSI=[1.72÷（1.72 1.52)]×100=53.09
```

### 指数移动平均/exponential moving average，EMA 或 EWMA

是以指数式递减加权的移动平均。 各数值的加权影响力随时间而指数式递减，越近期的数据加权影响力越重，但较旧的数据也给予一定的加权值。右图是一例子。

### Sharpe ratio/夏普比率

https://zh.wikipedia.org/wiki/%E5%A4%8F%E6%99%AE%E6%AF%94%E7%8E%87

假设目前投资一个预期回报率为 12%，波动率为 10%的投资组合。无风险利率是 5%。夏普比率就是：(0.12-0.05)/0.1=0.7

## 230528 交易中常说的 delta 是什么意思

在金融交易中，"Delta"是一个衍生品和期权交易中的术语，用来衡量标的资产价格变化对衍生品或期权价格的影响。更具体地说，它衡量的是衍生品价格或期权价格对标的资产价格每变动一个单位时的变化量。

例如，如果一个期权的 Delta 是 0.5，那么如果标的资产价格上升 1 单位，期权的价格就会上升 0.5 单位；如果标的资产价格下降 1 单位，期权的价格就会下降 0.5 单位。

Delta 也被用来衡量一个投资组合的市场风险。例如，一个有正 Delta 的投资组合预计会在市场上升时获益，而在市场下跌时损失。相反，一个有负 Delta 的投资组合预计会在市场下跌时获益，而在市场上升时损失。

此外，Delta 还被用来计算"Delta 对冲"策略，这是一种旨在减小标的资产价格变动对投资组合价值影响的策略。简单来说，如果一个投资组合的 Delta 是正的，投资者可以通过卖出相应 Delta 量的标的资产来对冲风险。同样地，如果一个投资组合的 Delta 是负的，投资者可以通过购买相应 Delta 量的标的资产来对冲风险。

## 230530 蒙特卡洛模拟

```
蒙特卡洛模拟（Monte Carlo Simulation）是一种计算数学期望的统计方法，这种方法利用随机数（或更普遍地说，伪随机数）来解决许多计算问题的数学方法。其命名来自于摩纳哥的蒙特卡洛，那里有许多赌场游戏，而赌博本质上就是一种随机过程。

蒙特卡洛模拟的基本思想是利用大量的随机抽样来模拟或模拟复杂的概率过程。然后，通过分析抽样结果来计算出某种特定情况的概率，或者更一般地说，计算出某个随机变量的数学期望。这种方法在金融工程、物理、计算生物学、工程、环境科学和许多其他领域都有广泛的应用。

蒙特卡洛模拟的一个关键特点是其能够处理复杂的概率分布和随机过程，这在许多其他的数值方法中是难以实现的。然而，它的一个缺点是需要大量的计算资源，因为需要进行大量的随机抽样和计算
```

```
一个最简单的蒙特卡洛模拟的例子就是用来估计圆周率π的值。

这个模拟的方法是这样的：

在一个边长为1的正方形内随机撒点。
计算这些点落在正方形内接的四分之一圆内的比例（即那些离正方形中心距离小于0.5的点）。
这个比例乘以4就是π的近似值。
这个模拟的数学原理是基于圆的面积公式和正方形的面积公式。正方形的面积是1（边长乘以边长），四分之一圆的面积是π/4（π乘以半径的平方，这里半径为0.5）。因此，落在四分之一圆内的点的比例应该接近π/4，所以乘以4就得到了π的近似值。

这个模拟的精度取决于我们撒的点的数量：点越多，模拟的结果就越接近真实的π值。这是因为随机模拟的结果通常会在真实值附近波动，但是随着试验次数的增加，这些波动会越来越小，结果会越来越稳定。这就是大数定律的一个应用。
```

### 230615 tqqq 是什么

TQQQ 是 ProShares UltraPro QQQ 的交易代码，这是一个交易所交易基金（ETF）。它旨在实现纳斯达克 100 指数（NASDAQ-100 Index）的三倍日常表现。换句话说，如果纳斯达克 100 指数在一天内上涨 1%，那么理论上 TQQQ 应该上涨 3%。

需要注意的是，这种杠杆 ETF 是用于短期交易的工具，而不是长期投资的工具。因为它们是基于每日的指数表现，所以长期持有可能会导致与预期的三倍收益有所偏离。这种差异是由于所谓的"复利效应"或"波动率腐蚀"造成的。

此外，TQQQ 等杠杆 ETF 具有更高的风险性，因为其价格变动可能会比未加杠杆的 ETF 更大。因此，投资者在考虑投资此类产品时应谨慎，理解这些产品的性质和风险。
