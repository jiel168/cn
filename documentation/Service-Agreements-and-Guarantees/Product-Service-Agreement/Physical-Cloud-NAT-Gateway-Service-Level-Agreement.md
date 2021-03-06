**1.服务范围**

本服务等级协议（Service Level Agreement，以下简称 “SLA”）规定了京东云向客户提供物理云NAT网关（Physical Cloud NAT Gateway）的服务可用性等级指标及赔偿方案，京东云的其他服务器产品不在本服务等级协议覆盖范围内。

**2.服务等级指标**

**2.1服务功能**

物理云NAT网关能够让VPC内的云物理服务器提供网络地址转换，访问Internet或使云物理服务器提供互联网服务。专用于云物理服务器的NAT网关。NAT网关具体功能请详见京东云在官网上提供的详细说明文档、技术文档及帮助文档。NAT网关所有可能影响用户的功能性变更都将向用户公告。

**2.2服务可用性**

服务周期：一个服务周期为一个自然月，如不满一个月不计算为一个服务周期。

服务周期分钟数：指按照一个服务周期内实际总天数×24（小时）×60（分钟）计算所得的分钟时长。

服务器周期不可用分钟数：当某一分钟内，物理云NAT网关出方向所有数据包都被京东云出口网关设备丢弃时，则视为该物理云NAT网关该分钟内服务不可用。在一个服务周期内单用户的单个物理云NAT网关不可用分钟数累计分钟时长即为服务周期不可用分钟数。

服务可用性计算公式：（一个服务周期内单用户单地域所有可用区内所有服务器的服务周期分钟数之和 － 一个服务周期内单用户单地域所有多可用区内所有服务器的服务周期不可用分钟数之和）/（一个服务周期内单用户单地域所有可用区内所有服务器的服务周期分钟数之和）× 100%。

服务可用性承诺：一个服务周期内单用户单地域的服务可用性不低于99.9%。

（地域：指的是京东云的Region概念；可用区：指的是京东云的AZ概念。）

**2.3故障恢复能力**

京东云为付费用户的云服务提供7×24小时的运行维护，并以在线工单和电话报障等方式提供技术支持，具备完善的故障监控、自动告警、快速定位、快速恢复等一系列故障应急响应机制。

**2.4网络接入性能**

用户在开通京东云物理云NAT网关服务时，物理云NAT网关和物理云公网IP进行绑定，用户可自主选择公网出口带宽。京东云提供BGP接入，保障用户的网络接入质量。

**2.5服务计量准确性**

京东云物理云NAT网关具备准确、透明的计量计费系统，京东云根据用户选择的物理云NAT网关规格据实结算，实时扣费，具体计费标准以京东云官网公布的有效的计费模式与价格为准。用户的原始计费日志默认最少保留1年备查。

**3.服务赔偿条款**

**3.1** **赔偿范围**   

因京东云设备故障、设计缺陷或操作不当导致用户所购买的物理云NAT网关服务无法正常使用，京东云将对不可用时间进行赔偿，但不包括以下原因所导致的服务不可用时间：

（1）京东云预先通知用户后进行系统维护所引起的，包括割接、维修、升级和模拟故障演练；

（2）任何京东云所属设备以外的网络、设备故障或配置调整引起的；

（3）用户的应用程序或数据信息受到黑客攻击而引起的；

（4）用户维护不当或保密不当致使数据、口令、密码等丢失或泄漏所引起的；

（5）用户自行升级操作系统所引起的；

（6）用户的应用程序或安装活动所引起的；

（7）用户的疏忽或由用户授权的操作所引起的；

（8）不可抗力以及意外事件引起的；

（9）由于客户违反《京东云服务协议》导致的物理云NAT网关被暂停或终止，包括但不限于由于订单过期或者账号欠费导致物理云NAT网关被暂停服务或被释放等；

（10）其他非京东云原因所造成的不可用；

**3.2** **赔偿方案**

故障时间=不可用时间。

包年包月的物理云NAT网关以服务时长补偿的方式，按不可用时间的100倍赔偿。

说明：

京东云通过赠送代金券的方式进行赔偿，赠送代金券仅支持购买物理云NAT网关产品，赔偿总额不超过当月用户就该物理云NAT网关已支付的月度服务费用（不含赠送余额或代金券抵扣的费用）。

**4.其他**

京东云有权根据变化适时对本服务等级协议部分服务指标作出调整，并及时在京东云官网 [www.jdcloud.com](http://www.jdcloud.com/) 发布公告或发送邮件或书面通知向用户提示修改内容。如您不同意京东云对本服务等级协议所做的修改，您有权停止使用物理云NAT网关服务，如您继续使用物理云NAT网关服务，则视为您接受修改后的服务等级协议。