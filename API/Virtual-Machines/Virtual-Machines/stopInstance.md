# stopInstance


## 描述
停止单个云主机，只能停止<b>running</b>状态的云主机，云主机没有正在进行中的任务才可停止


## 请求方式
POST

## 请求地址
https://vm.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}:stopInstance

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |地域ID|
|**instanceId**|String|True| |云主机ID|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**chargeOnStopped**|String|False| |关机模式，只支持云盘做系统盘的按配置计费云主机keepCharging：关机后继续计费；stopCharging：关机后停止计费。|


## 返回参数
无


## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
|**400**|Invalid parameter|
|**401**|Authentication failed|
|**404**|Not found|
|**500**|Internal server error|
|**503**|Service unavailable|
