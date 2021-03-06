# 按增强95消峰计费
本文将详细介绍按增强95计费模式的共享带宽包的计费规则。目前增强95消峰计费处于灰度中，如需使用请[提交工单](https://ticket.jdcloud.com/applyorder/submit)申请权限。



### 详细介绍

- 按增强95消峰计费月度总费用包含保底带宽费用和超保底带宽费用

- 若超保底带宽费用小于等于0，则每天仅收取保底带宽费用，若超保底带宽费用大于0，则需收取超保底带宽费用，并在下个月初根据每天共享带宽包实际使用流量出账单

- 选择按增强95消峰计费模式至少需要使用完一个完整的自然月，最早支持在完整自然月的下个月初出完账单之后删除

### 计费公式

- 每个带宽包月度总费用 = 月总保底带宽费用 + 超保底带宽费用


#### 保底带宽费用

- 保底带宽 = 带宽上限 x 保底带宽百分比
```
按用量计费模式的共享带宽包不支持调整保底带宽百分比，目前支持的百分比为20%（保底带宽单价 = 超保底带宽单价）
```
- 月总保底带宽费用 = 保底带宽1 × 实例对应保底带宽存在天数1x 增强95保底带宽日单价1 + 保底带宽2 × 实例对应保底带宽存在天数2x 增强95保底带宽日单价2 + ...+ 保底带宽n × 实例对应保底带宽存在天数nx 增强95保底带宽日单价n

```
说明：
- 一个完整的自然月里，对共享带宽包进行多次变配操作，不同的共享带宽上限对应不同的保底带宽1、保底带宽2、...、保底带宽n
- 不同带宽上限带宽日单价：增强95保底带宽日单价1、增强95保底带宽日单价2、……增强95保底带宽日单价n
- 每次变配后实例存在的时间：例对应保底带宽存在天数1、实例对应保底带宽存在天数2、……实例对应保底带宽存在天数n

```

- 月平均保底带宽 = （保底带宽1 × 实例对应保底带宽存在天数1+保底带宽2 × 实例对应保底带宽存在天数2……+保底带宽n × 实例对应保底带宽存在天数n）÷实例对应计费周期存在天数


#### 超保底带宽费用

- 月平均超保底带宽 = MAX（0,(月平均峰值 – 月平均保底带宽））

- 超保底带宽费用 = 月平均超保底带宽 × 增强95超保底带宽日单价 × 实例对应计费周期存在天数

```
说明：当前保底带宽单价与超保底带宽单价相同，因此当月平均峰值大于月平均保底带宽时，
每个带宽包月度总费用 = 月平均峰值 x 增强95消峰日单价 x 实例对应计费周期存在天数，即月平均超保底带宽大于0，则收取超保底带宽费用；
当月平均峰值小于月平均保底带宽时，每个带宽包月度总费用 = 月平均保底带宽 x 增强95消峰日单价 x 实例对应计费周期存在天数
```

#### 月平均峰值

月平均峰值带宽计算方法如下：

- 日峰值：以5分钟为粒度采样，采集入方向和出方向的流量，分别计算入方向和出方向在5分钟内的带宽平均值，取入方向和出方向中较大的带宽平均值作为采样点带宽值。每天得到全部采样点后，按从高到低排序，去掉前4个最高的采样点，取第5峰采样点为日峰值（如果当天采样点不足5个，以排序后的最后一个为日峰值）

- 月平均峰值：月底将日峰值从高到底排序，取前5个最高的日峰值，计算其均值得到月平均峰值(如当月最高日峰值不足5个，则月平均峰值为所有最高日峰值的平均值)

下图为1个完整自然月Top5峰值计费采样和计算方法说明。


 ![增强95图](../../../../../image/Networking/Shared-Bandwidth-Package/Enhanced-95.png)


### 计费实例

假设您够买了1个按增强95消峰计费模式的共享带宽包，带宽上限为30Gbps，计费周期为1个月（按30天计算），保底带宽百分比为20%，则保底带宽为6Gbps，假设期间未进行变配，按照上述消峰方法消峰后月平均带宽峰值为7.506Gbps，共享带宽包的总费用为（7.506-6）\*1000* 100.80+6\*1000\*100.8=756604.8元（超保底带宽单价 = 保底带宽单价，价格详情请参考[价格总览](../Price-Overview.md)）。

### 变配计费规则

- 按用量计费模式支持实时调节共享带宽上限，并立刻生效，调整完共享带宽上限后，保底带宽会随之变化

- 升配/降配 ：以天为粒度计算，每天的保底带宽取当天设置过最大带宽上限对应的保底带宽；例如：一天中进行过带宽上限调整: 1000Mbit/s -> 3000Mbit/s -> 2000Mbit/s，则当天的保底带宽为3000Mbit/s\*20%=600Mbit/s

- 实例对应计费周期存在天数：计费周期时间（单位：秒）/（24\*60\*60），实例存在天数小数部分取小数点后2位，其他小数位直接舍弃


### 账单说明

- 账单周期：保底带宽费用及超保底带宽费用按月出账单，可提供精确到天的费用明细

- 出账时间：通常为当前计费周期结束的下个自然月1日。例如：3月1日会生成2月份完整月（2020-02-01 00:00:00 至 2020-02-29 23:59:59）的超保底带宽计费账单

- 结算时间：账单生成后会自动从您的账户余额中扣除费用以结算账单。请确保结算时账户的余额充足，以免出现欠费问题



注意：实际使用天数和共享带宽中是否有业务流量无关，如果创建后不使用也会计算实际使用天数。

## 相关参考
- [价格总览](../Price-Overview.md)
- [计费概述](../Billing-Overview.md)
- [计费规则](../Billed-Rules.md)
- [续费流程](../Renew-Process.md)
- [购买流程](../Purchase-Process.md)
- [常见问题](../../FAQ/FAQ.md)
