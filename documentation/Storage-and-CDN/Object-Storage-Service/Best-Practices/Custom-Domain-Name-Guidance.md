# 自定义域名支持HTTPS访问 OSS 服务

## 常见概念

绑定自定义域名，您需要了解以下概念：

- 用户域名、自定义域名、自有域名：您在域名服务商处购买的域名。
- OSS 访问域名或 Bucket 域名：OSS 为您的 Bucket 分配的的访问域名。

## 自定义域名访问OSS

您上传文件到京东云 OSS 的 Bucket 后，可以使用OSS 访问域名或 Bucket 域名访问文件。如果您想要通过自定义域名访问这些文件，需要将自定义域名绑定到文件所在的存储空间，并添加 CNAME 记录指向存储空间对应的OSS 访问域名。参见[自定义域名服务](../Operation-Guide/Manage-Bucket/Set-Custom-Domain-Name-2.md)。

## 自定义域名支持HTTPS访问 OSS 服务

当您参照[控制台-自定义域名设置](../Operation-Guide/Manage-Bucket/Set-Custom-Domain-Name-2.md)完成域名添加后，
**您的用户域名还不支持通过 https 访问 OSS 服务，如果您需要支持 https 的访问，需要提交工单，按照要求提交资料，即可支持 https 的访问。**

## 操作指南：

* 您需要首先提交工单，输入问题描述“对象存储自定义域名支持https访问”。
* 工单中提交相应资料如下：

| 名称                 | 描述                                                         |
| :------------------- | :----------------------------------------------------------- |
| PIN（客户识别码）    | 您的用户PIN，可在登录京东云控制台后，https://uc.jdcloud.com/account/basic-info 中查询到。 |
| https证书            | 您想要支持的自有域名https证书。                              |
| OSS访问域名          | OSS访问域名 ：```<BUCKET_NAME>.s3.<REGION>.jdcloud-oss.com ``` |
| 证书过期时间         | 以便京东云在证书到期前提醒您进行续签。                       |
| 配置接入区域         | 提供需要配置的bucket所在区域，可参考下表。                   |
| 网络接入方式         | “公网接入”或“内网接入”。                                     |
| 需要配置的Bucket名称 | 需要配置的Bucket名称                                         |
| 联系电话与邮箱       | 方便证书过期前，及时通知到您                                 |

接入区域参考

| 服务域名                    | 新服务域名                    | 对应区域（Region）    |
| --------------------------- | ----------------------------- | --------------------- |
| s3.cn-north-1.jcloudcs.com  | s3.cn-north-1.jdcloud-oss.com | 华北-北京(cn-north-1) |
| s3.cn-east-1.jcloudcs.com   | s3.cn-east-1.jdcloud-oss.com  | 华东-宿迁(cn-east-1)  |
| s3.cn-east-2.jcloudcs.com   | s3.cn-east-2.jdcloud-oss.com  | 华东-上海(cn-east-2)  |
| s3.cn-south-1.jcloudcs.com  | s3.cn-south-1.jdcloud-oss.com | 华南-广州(cn-south-1) |
| oss.cn-north-1.jcloudcs.com |                               | 华北-北京(cn-north-1) |
| oss.cn-east-1.jcloudcs.com  |                               | 华东-宿迁(cn-east-1)  |
| oss.cn-east-2.jcloudcs.com  |                               | 华东-上海(cn-east-2)  |
| oss.cn-south-1.jcloudcs.com |                               | 华南-广州(cn-south-1) |



**说明**

* 请在提交证书前检查您的证书有效期，证书有效时间需要在3个月以上。若证书有效期不足3个月,您需先续签证书再提交，以便拥有稳定的服务。
* 当前仅支持与京东云对象存储新版S3域名绑定。
* 提交工单后，正常配置上线生效时间在1-2周，节假日除外，加急需求请特殊说明。
* 证书托管配置完成后，工作人员将通知您。
