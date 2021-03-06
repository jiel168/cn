# 云数据库RDS


## 简介
目前RDS OpenAPI支持云数据库 MySQL、Percona、MariaDB、SQL Server、PostgreSQL


### 版本
v1


## API
|接口名称|请求方式|功能描述|
|---|---|---|
|**alterTableWithOnlineDDL**|POST|通过 PT-OSC 服务来处理 DDL 命令, 避免锁表。此接口暂是对部分用户开放|
|**clearBinlogs**|POST|清理本地的binlog并释放空间。 系统只会清理已经备份到存储的binlog，不会影响MySQL实例的备份恢复<br>- 仅支持MySQL|
|**copyParameterGroup**|POST|拷贝参数组|
|**createAccount**|POST|创建数据库账号，用户可以使用客户端，应用程序等通过该账号和密码登录RDS数据库实例。<br>为便于管理和恢复，RDS对账号进行了限制，数据库账号只能通过控制台或者OpenAPI进行创建、删除账号以及对账号授权等，用户不能通过SQL语句对账号进行相关操作。|
|**createAudit**|POST|开启SQL Server的数据库审计功能，目前支持实例级的数据库审计。用户可以根据需要开启、关闭审计、自定义审计策略，并下载审计文件。审计文件为原生的SQL Server审计文件，缺省保存6个月。<br>- 仅支持SQL Server|
|**createBackup**|POST|创建一个RDS实例全量备份，可以对整个实例或者部分数据库（仅SQL Server支持）进行全量备份。同一时间点，只能有一个正在运行的备份任务|
|**createBackupSynchronicity**|POST|创建一个跨地域备份同步服务。|
|**createDatabase**|POST|创建一个数据库。 为了实例的管理和数据恢复，RDS对用户权限进行了限制，用户仅能通过控制台或本接口创建数据库|
|**createInstance**|POST|创建一个RDS实例，用户可以使用相应的数据库客户端或者应用程序通过域名和端口链接到该RDS实例上，进行操作。|
|**createInstanceByTime**|POST|根据源实例备份创建一个新实例，并通过追加日志的方式，将新实例的数据恢复到跟源实例指定时间点的数据状态一样。<br>例如根据实例A在“2018-06-18 23:00:00”时间点创建一个实例B，就是新建一个实例B，该实例B的数据跟实例A在“2018-06-18 23:00:00”这个时间点的数据完全一致。<br>对于SQL Server，主备切换后30分钟内，不支持按时间点恢复/创建，例如在10:05分用户进行了主备切换，那么10:05 ~ 10:35这个时间段不能进行按时间点恢复/创建。|
|**createInstanceByTimeInCrossRegion**|POST|根据跨地域备份同步服务时间点创建实例。|
|**createInstanceFromBackup**|POST|根据源实例全量备份创建一个新实例，新实例的数据跟源实例在创建备份时的数据状态一样。<br>例如根据源实例A的一个全量备份“mybak”新建一个实例B，该备份是在“‘2018-8-18 03:23:54”创建的。那么新建实例B的数据状态跟实例A‘2018-8-18 03:23:54’的状态一致|
|**createParameterGroup**|POST|创建一个参数组<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**createROInstance**|POST|创建MySQL的只读实例<br> \- 仅支持MySQL<br> \- 创建的只读实例跟主实例在同一个VPC同一个子网中<br> * 只读实例只支持按配置计费|
|**createSuperAccount**|POST|创建数据库账号，用户可以使用客户端，应用程序等通过该账号和密码登录RDS数据库实例。<br>为便于管理和恢复，RDS对账号进行了限制，数据库账号只能通过控制台或者OpenAPI进行创建、删除账号以及对账号授权等，用户不能通过SQL语句对账号进行相关操作。|
|**deleteAccount**|DELETE|删除数据库账号，账号删除后不可恢复，用户无法再使用该账号登录RDS实例|
|**deleteAudit**|DELETE|关闭数据库审计。关闭数据库审计后，以前生成的审计结果文件并不会被立即删除。审计结果文件会过期后由系统自动删除，过期时间缺省为6个月<br>- 仅支持SQL Server|
|**deleteBackup**|DELETE|删除RDS实例备份，仅允许删除用户生成的备份，系统自动备份不允许删除。|
|**deleteBackupSynchronicity**|DELETE|删除一个跨地域备份同步服务。|
|**deleteDatabase**|DELETE|从RDS实例中删除数据库。为便于管理和数据恢复，RDS对用户权限进行了控制，用户仅能通过控制台或本接口删除数据库<br>敏感操作，可开启<a href="https://docs.jdcloud.com/cn/security-operation-protection/operation-protection">MFA操作保护</a>|
|**deleteImportFile**|DELETE|删除用户通过单库上云工具上传的数据库备份文件<br>- 仅支持SQL Server|
|**deleteInstance**|DELETE|删除一个RDS实例或者MySQL/PostgreSQL的只读实例。删除MySQL/PostgreSQL主实例时，会同时将对应的MySQL/PostgreSQL只读实例也删除<br>敏感操作，可开启<a href="https://docs.jdcloud.com/cn/security-operation-protection/operation-protection">MFA操作保护</a>|
|**deleteParameterGroup**|DELETE|删除参数组<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**describeAccountPrivilege**|GET|查看RDS实例的账号的权限信息 \- 仅支持 MySQL，Percona，MariaDB|
|**describeAccounts**|GET|查看某个RDS实例下所有账号信息，包括账号名称、对各个数据库的访问权限信息等|
|**describeActiveQueryPerformance**|GET|根据用户定义的查询条件，获取正在执行中的SQL执行的性能信息。用户可以根据这些信息查找与SQL执行相关的性能瓶颈，并进行优化。<br>- 仅支持SQL Server|
|**describeAudit**|GET|查看当前实例已开启的审计选项。如当前实例未开启审计，则返回空<br>- 仅支持SQL Server|
|**describeAuditDownloadURL**|GET|获取某个审计文件的下载链接，同时支持内链和外链，链接的有效时间为24小时<br>- 仅支持SQL Server|
|**describeAuditFiles**|GET|获取当前实例下的所有审计结果文件的列表<br>- 仅支持SQL Server|
|**describeAuditOptions**|GET|获取当前系统所支持的各种数据库版本的审计选项及相应的推荐选项<br>- 仅支持SQL Server|
|**describeAuditResult**|GET|仅支持查看MySQL实例的审计内容<br>- 仅支持 MySQL 5.6, MySQL 5.7, Percona, MariaDB, PostgreSQL|
|**describeAzs**|GET|查看指定地域下各种RDS数据库支持的可用区，不同类型的RDS支持的可用区不一样|
|**describeBackupDownloadURL**|GET|获取整个备份或备份中单个文件的下载链接。<br>- 当输入参数中有文件名时，获取该文件的下载链接。<br>- 输入参数中无文件名时，获取整个备份的下载链接。<br>由于备份机制的差异，使用该接口下载备份时，SQL Server必须输入文件名，每个文件逐一下载，不支持下载整个备份。SQL Server备份中的文件名（不包括后缀）即为备份的数据库名。例如文件名为my_test_db.bak，表示该文件是my_test_db数据库的备份。<br>MySQL可下载整个备份集，但不支持单个文件的下载。|
|**describeBackupPolicy**|GET|查看RDS实例备份策略。根据数据库类型的不同，支持的备份策略也略有差异，具体请看返回参数中的详细说明|
|**describeBackupSynchronicities**|GET|查询跨地域备份同步服务列表。|
|**describeBackups**|GET|查看该RDS实例下所有备份的详细信息，返回的备份列表按照备份开始时间（backupStartTime）降序排列。|
|**describeBinlogDownloadURL**|GET|获取MySQL实例的binlog的下载链接<br>- 仅支持 MySQL, Percona, MariaDB|
|**describeBinlogs**|GET|获取MySQL实例中binlog的详细信息<br>- 仅支持 MySQL, Percona, MariaDB|
|**describeDatabases**|GET|获取当前实例的所有数据库详细信息的列表|
|**describeErrorLog**|GET|查询PostgreSQL实例的错误日志的概要信息。<br>- 仅支持PostgreSQL|
|**describeErrorLogs**|GET|获取SQL Server 错误日志及下载信息<br>- 仅支持SQL Server|
|**describeImportFiles**|GET|获取用户通过单库上云工具上传到该实例上的文件列表<br>- 仅支持SQL Server|
|**describeIndexPerformance**|GET|根据用户定义的查询条件，获取索引性能的统计信息，并提供缺失索引及索引创建建议。用户可以根据这些信息查找与索引相关的性能瓶颈，并进行优化。<br>- 仅支持SQL Server|
|**describeInstanceAttributes**|GET|查询RDS实例（MySQL、SQL Server等）的详细信息以及MySQL/PostgreSQL只读实例详细信息|
|**describeInstances**|GET|获取当前账号下所有RDS实例及MySQL/PostgreSQL只读实例的概要信息，例如实例类型，版本，计费信息等|
|**describeIntercept**|GET|查看当前实例已开启的安全模式。如果开启数据库的高安全模式，会返回配置信息<br>- 仅支持MySQL|
|**describeInterceptResult**|GET|查看开启高安全模式后，当前实例的 SQL 拦截记录<br>- 仅支持MySQL|
|**describeLatestRestoreTime**|GET|获取SQL Server实例按时间点恢复/创建时，可恢复到的最后的一个时间点<br>- 仅支持SQL Server|
|**describeLogDownloadURL**|POST|根据日志文件的下载链接过期时间，生成日志文件下载地址 仅支持 PostgreSQL, MySQL, Percona, MariaDB|
|**describeLogs**|GET|获取日志文件列表<br>- 仅支持PostgreSQL, MySQL, Percona, MariaDB|
|**describeParameterGroupAttachedInstances**|GET|查看参数组绑定的云数据库实例<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**describeParameterGroupParameters**|GET|查看参数组的参数<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**describeParameterGroups**|GET|获取当前账号下所有的参数组列表<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**describeParameterModifyRecords**|GET|查看参数的修改历史<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**describeParameters**|GET|查看SQL Server实例的配置参数<br>- 仅支持SQL Server|
|**describePrivilege**|GET|查看云数据库 RDS 的权限信息 \- 仅支持 MySQL，Percona，MariaDB|
|**describeQueryPerformance**|GET|根据用户定义的查询条件，获取SQL执行的性能统计信息，例如慢SQL等。用户可以根据这些信息查找与SQL执行相关的性能瓶颈，并进行优化。<br>- 仅支持SQL Server|
|**describeSSL**|GET|查看当前实例已开启加密连接。|
|**describeSlowLogAttributes**|GET|查询MySQL实例的慢日志的详细信息。<br>- 仅支持MySQL|
|**describeSlowLogs**|GET|查询MySQL实例的慢日志的概要信息。<br>- 仅支持MySQL|
|**describeTables**|GET|获取当前实例的指定库的表列表信息 \- 仅支持 MySQL，Percona，MariaDB|
|**describeTde**|GET|查看当前实例是否开启TDE|
|**describeWhiteList**|GET|查看RDS实例当前白名单。白名单是允许访问当前实例的IP/IP段列表，缺省情况下，白名单对本VPC开放。如果用户开启了外网访问的功能，还需要对外网的IP配置白名单。|
|**disableAudit**|POST|仅支持MySQL实例关闭数据库审计<br>- 仅支持 MySQL 5.6, MySQL 5.7, Percona, MariaDB, PostgreSQL|
|**disableIntercept**|POST|关闭数据库的高安全模式<br>- 仅支持MySQL|
|**disableInternetAccess**|POST|关闭RDS实例的外网访问功能。关闭后，用户无法通过Internet访问RDS，但可以在京东云内网通过内网域名访问|
|**enableAudit**|POST|仅支持MySQL实例开启数据库审计<br>- 仅支持 MySQL 5.6, MySQL 5.7, Percona, MariaDB, PostgreSQL|
|**enableIntercept**|POST|开启数据库的高安全模式<br>- 仅支持MySQL|
|**enableInternetAccess**|POST|开启RDS实例的外网访问功能。开启后，用户可以通过internet访问RDS实例|
|**enableSSL**|POST|开启数据库的加密连接, 同时会重启数据库实例|
|**enableTde**|POST|开启数据库的TDE功能|
|**exchangeInstanceDns**|POST|交换两个实例的域名，包括内网域名和外网域名。如果一个实例有外网域名，一个没有，则不允许交换。<br>- 仅支持SQL Server|
|**failoverInstance**|POST|对RDS实例进行主备切换。<br>注意：如果实例正在进行备份，那么主备切换将会终止备份操作。可以查看备份策略中的备份开始时间确认是否有备份正在运行。如果确实需要在实例备份时进行主备切换，建议切换完成 后，手工进行一次实例的全备<br>对于SQL Server，主备切换后30分钟内，不支持按时间点恢复/创建，例如在10:05分用户进行了主备切换，那么10:05 ~ 10:35这个时间段不能进行按时间点恢复/创建。<br>- 仅支持SQL Server|
|**getUploadKey**|POST|获取单库上云工具上传文件的需要的Key。单库上云工具需要正确的key值方能连接到京东云<br>- 仅支持SQL Server|
|**grantAccountPrivilege**|POST|授予账号的数据库细粒度的访问权限 \- 仅支持 MySQL，Percona，MariaDB|
|**grantPrivilege**|POST|授予账号的数据库访问权限，即该账号对数据库拥有什么权限。一个账号可以对多个数据库具有访问权限。<br>为便于管理，RDS对权限进行了归类，目前提供以下两种权限<br>- ro：只读权限，用户只能读取数据库中的数据，不能进行创建、插入、删除、更改等操作。<br>- rw：读写权限，用户可以对数据库进行增删改查等操作|
|**modifyAudit**|POST|修改当前的审计选项。当前已有审计选项可以通过describeAudit获得，支持的全部选项可以通过getAuditOptions获得。<br>- 仅支持SQL Server|
|**modifyBackupPolicy**|POST|修改RDS实例备份策略，目前仅支持用户修改“自动备份开始时间窗口”这个参数，其他参数暂不开放修改|
|**modifyConnectionMode**|POST|修改MySQL实例的连接模式：标准模式(standard) 和高安全模式(security).<br>- **标准模式**：响应时间短，但没有 SQL 审计和拦截的能力。<br>- **高安全模式**：具备一定的 SQL注入拦截能力（通过分析表达式、关键系统函数等来实现防御 SQL 注入攻击），并可开启 SQL 审计，但会增加一定的响应时间。<br>- 仅支持MySQL|
|**modifyInstanceAz**|POST|修改实例的可用区，例如将实例的可用区从单可用区调整为多可用区|
|**modifyInstanceName**|POST|修改实例名称，可支持中文，实例名的具体规则可参见帮助中心文档:[名称及密码限制](../../documentation/Database-and-Cache-Service/RDS/Introduction/Restrictions/SQLServer-Restrictions.md)|
|**modifyInstanceSpec**|POST|实例扩容，支持升级实例的CPU，内存及磁盘。|
|**modifyParameterGroup**|PUT|修改RDS实例的参数组<br>- 仅支持MySQL|
|**modifyParameterGroupAttribute**|PUT|修改参数组名称，描述<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**modifyParameterGroupParameters**|PUT|修改参数组的参数<br>- 仅支持MySQL，Percona，MariaDB，PostgreSQL|
|**modifyParameters**|PUT|修改SQL Server实例的配置参数，目前支持以下参数:max_worker_threads,max_degree_of_parallelism,max_server_memory_(MB)。 部分参数修改后，需要重启才能生效，具体可以参考微软的相关文档。<br>- 仅支持SQL Server|
|**modifyWhiteList**|PUT|修改允许访问实例的IP白名单。白名单是允许访问当前实例的IP/IP段列表，缺省情况下，白名单对本VPC开放。如果用户开启了外网访问的功能，还需要对外网的IP配置白名单。|
|**rebootInstance**|POST|重启RDS实例，例如修改了一些配置参数后，需要重启实例才能生效。可以结合主备切换的功能，轮流重启备机，降低对业务的影响<br>**注意：如果实例正在进行备份，那么重启主实例将会终止备份操作。** 可以查看备份策略中的备份开始时间确认是否有备份正在运行。如果确实需要在实例备份时重启主实例，建议重启后，手工进行一次实例的全备。|
|**resetPassword**|POST|重置数据库账号密码。如果用户忘记账号的密码，可以使用该接口重置指定账号密码。密码重置后，以前的密码将无法使用，必须使用重置后的新密码登录或连接数据库实例。|
|**restoreDatabaseFromBackup**|POST|从备份中恢复单个数据库，支持从其他实例（但必须是同一个账号下的实例）备份中恢复。例如可以从生产环境的数据库实例的备份恢复到测试环境的数据库中。<br>- 仅支持SQL Server|
|**restoreDatabaseFromFile**|POST|从用户通过单库上云工具上传到云上的备份文件中恢复单个数据库<br>- 仅支持SQL Server|
|**restoreDatabaseFromOSS**|POST|从上传到OSS的备份文件中恢复单个数据库<br>- 仅支持SQL Server|
|**restoreInstance**|POST|使用实例的全量备份覆盖恢复当前实例|
|**restoreInstanceByTime**|POST|根据时间点，选择单表恢复当前实例<br>- 仅支持MySQL|
|**revokePrivilege**|POST|取消该账号对某个数据库的所有权限。权限取消后，该账号将不能访问此数据库。取消账号对某个数据库的访问权限，不影响该账号对其他数据库的访问权限|
|**setImportFileShared**|POST|设置或取消上传文件是否共享给同一账号下的其他实例。缺省情况下，文件仅在上传的实例上可见并可导入，其他实例不可见不可导入。如果需要该文件在其他实例上也可导入，可将此文件设置为共享<br>- 仅支持SQL Server|
|**updateLogDownloadURLInternal**|POST|设置日志文件的下载链接过期时间，重新生成 PostgreSQL 的日志文件下载地址|
