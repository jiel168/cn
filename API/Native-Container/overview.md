# 原生容器


## 简介
原生容器相关接口


### 版本
v1


## API
|接口名称|请求方式|功能描述|
|---|---|---|
|**associateElasticIp**|POST|容器绑定弹性公网 IP，绑定的是主网卡、主内网IP对应的弹性IP. <br>一台云主机只能绑定一个弹性公网 IP(主网卡)，若主网卡已存在弹性公网IP，会返回错误。<br>如果是黑名单中的用户，会返回错误。<br>|
|**createContainers**|POST|创建一台或多台指定配置容器<br>- 创建容器需要通过实名认证<br>- 镜像<br>  \- 容器的镜像通过镜像名称来确定<br>  \- nginx:tag, mysql/mysql-server:tag这样命名的镜像表示docker hub官方镜像<br>  \- container-registry/image:tag这样命名的镜像表示私有仓储的镜像<br>  \- 私有仓储必须兼容docker registry认证机制，并通过secret来保存机密信息<br>- hostname规范<br>  \- 支持两种方式：以标签方式书写或以完整主机名方式书写<br>  \- 标签规范<br>    \- 0-9，a-z(不分大小写)和-（减号），其他的都是无效的字符串<br>    \- 不能以减号开始，也不能以减号结尾<br>    \- 最小1个字符，最大63个字符<br>  \- 完整的主机名由一系列标签与点连接组成<br>    \- 标签与标签之间使用“.”(点)进行连接<br>    \- 不能以“.”(点)开始，也不能以“.”(点)结尾<br>    \- 整个主机名（包括标签以及分隔点“.”）最多有63个ASCII字符<br>- 网络配置<br>  \- 指定主网卡配置信息<br>    \- 必须指定vpcId、subnetId、securityGroupIds<br>    \- 可以指定elasticIp规格来约束创建的弹性IP，带宽取值范围[1-200]Mbps，步进1Mbps<br>    \- 可以指定网卡的主IP(primaryIpAddress)和辅助IP(secondaryIpAddresses)，此时maxCount只能为1<br>    \- 可以指定希望的辅助IP个数(secondaryIpAddressCount)让系统自动创建内网IP<br>    \- 可以设置网卡的自动删除autoDelete属性，指明是否删除实例时自动删除网卡<br>    \- 安全组securityGroup需与子网Subnet在同一个私有网络VPC内<br>    \- 每个容器至多指定5个安全组<br>    \- 主网卡deviceIndex设置为0<br>- 存储<br>  \- volume分为root volume和data volume，root volume的挂载目录是/，data volume的挂载目录可以随意指定<br>  \- volume的底层存储介质当前只支持cloud类别，也就是云硬盘<br>  \- 云盘类型为 ssd.io1 时，用户可以指定 iops，其他类型云盘无效，对已经存在的云盘无效，具体规则如下<br>    \- 步长 10<br>    \- 范围 [200，min(32000，size*50)]<br>    \- 默认值 size*30<br>  \- root volume<br>    \- 云硬盘类型可以选择hdd.std1、ssd.gp1、ssd.io1<br>    \- 磁盘大小<br>      \- 所有类型：范围[10,100]GB，步长为10G<br>    \- 自动删除<br>      \- 默认自动删除<br>    \- 可以选择已存在的云硬盘<br>  \- data volume<br>    \- data volume当前只能选择cloud类别<br>    \- 云硬盘类型可以选择hdd.std1、ssd.gp1、ssd.io1<br>    \- 磁盘大小<br>      \- 所有类型：范围[20,2000]GB，步长为10G<br>    \- 自动删除<br>      \- 默认自动删除<br>    \- 可以选择已存在的云硬盘<br>    \- 可以从快照创建磁盘<br>    \- 单个容器可以挂载7个data volume<br>- 容器日志<br>  \- default：默认在本地分配10MB的存储空间，自动rotate<br>- 其他<br>  \- 创建完成后，容器状态为running<br>  \- maxCount为最大努力，不保证一定能达到maxCount<br>|
|**createSecret**|POST|创建一个 secret，用于存放镜像仓库认证信息。<br>|
|**deleteContainer**|DELETE|容器状态必须为 stopped、running 或 error状态。 <br>按量付费的实例，如不主动删除将一直运行，不再使用的实例，可通过本接口主动停用。<br>只能支持主动删除按配置计费类型的实例。包年包月过期的容器也可以删除，其它的情况还请发工单系统。计费状态异常的容器无法删除。<br>|
|**deleteSecret**|DELETE|删除单个 secret<br>|
|**describeContainer**|GET|查询一台原生容器的详细信息<br>|
|**describeContainers**|GET|批量查询原生容器的详细信息<br>此接口支持分页查询，默认每页20条。<br>|
|**describeInstanceTypes**|GET|查询实例规格信息列表<br>|
|**describeQuota**|GET|查询资源的配额，支持：原生容器 pod 和 secret.<br>|
|**describeSecret**|GET|查询单个 secret 详情<br>|
|**describeSecrets**|GET|查询 secret 列表。<br> <br>此接口支持分页查询，默认每页20条。<br>|
|**disassociateElasticIp**|POST|容器解绑公网 IP，解绑的是主网卡、主内网 IP 对应的弹性 IP.<br>|
|**execCreate**|POST|创建exec<br>|
|**execGetExitCode**|GET|获取exec退出码<br>|
|**getLogs**|GET|查询单个容器日志<br>|
|**modifyContainerAttribute**|PATCH|修改容器的 名称 和 描述。<br>name 和 description 必须要指定一个<br>|
|**rebuildContainer**|POST|重置原生容器，对已有原生容器使用新的镜像重置。<br>原容器 id 不变，不涉及计费变动，暂不支持修改实例类型，不会改变原生容器所在的物理节点，也不支持修改已经使用的系统盘和数据盘以及网络相关参数。<br>- 镜像<br>    \- 容器的镜像通过镜像名称来确定<br>    \- nginx:tag 或 mysql/mysql-server:tag 这样命名的镜像表示 docker hub 官方镜像<br>    \- container-registry/image:tag 这样命名的镜像表示私有仓储的镜像<br>    \- 私有仓储必须兼容 docker registry 认证机制，并通过 secret 来保存机密信息<br>- 其他<br>    \- rebuild 之前容器必须处于关闭状态<br>    \- rebuild 完成后，容器仍为关闭状态<br>|
|**resizeContainer**|POST|调整原生容器实例类型配置。<br>- 原生容器状态为停止;<br>- 支持升配、降配；**不支持原有规格**<br>- 计费类型不变<br>    \- 包年包月：需要计算配置差价，如果所选配置价格高，需要补齐到期前的差价，到期时间不变；如果所选配置价格低，需要延长到期时间<br>    \- 按配置：按照所选规格，进行计费<br>|
|**resizeTTY**|POST|调整TTY大小<br>|
|**startContainer**|POST|启动处于关闭状态的单个容器，处在任务执行中的容器无法启动。<br>容器实例或其绑定的云盘已欠费时，容器将无法正常启动。<br>|
|**stopContainer**|POST|停止处于运行状态的单个实例，处于任务执行中的容器无法启动。<br>|
