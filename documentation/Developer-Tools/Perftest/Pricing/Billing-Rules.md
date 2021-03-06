# 计费规则

性能测试服务支持按需购买套餐包的付费方式。需购买大于压测任务的最大并发数的套餐包，方可使用性能测试服务执行压测任务，测试任务执行时会按照设置的并发数和压测时长进行VUM的预扣，如任务未成功发起或者中途被手工取消，会根据实际消耗进行VUM的退还，确保仅在任务正常执行时计算VUM消耗。

### 套餐包购买和使用说明：

采用预付费模式，一次性支付，实时生效。

暂不支持续订、退订。套餐包到期后，未使用的VUM会被清零，请注意套餐包的到期时间。

套餐包可多类型、重复购买，在有效期内叠加使用。VUM扣除时只考虑套餐包的有效期和是否满足最大并发数。

举例：

您先后购买了2个入门包，某压测场景2000并发执行90分钟，压测执行时需要预扣18万VUM，会从先过期的套餐包扣除10万VUM，剩下的套餐包扣除8万VUM。

您先购买了1个入门包，后购买了1个专业包，某压测场景1万并发执行90分钟，压测执行时需要预扣90万VUM，会从满足最大并发数条件的专业包中进行VUM的扣除。