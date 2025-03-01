# DescribeAccountAttributes {#doc_api_Ecs_DescribeAccountAttributes .reference}

查询您在一个阿里云地域下能创建的ECS资源上限。包括您能创建的安全组数量、弹性网卡数量、按量付费vCPU核数、抢占式实例vCPU核数、专用宿主机数量、地域网络类型以及账号是否已完成实名认证。

## 接口说明 {#description .section}

[注册](https://account.alibabacloud.com/register/intl_register.htm) 了阿里云账号后，您可以在不同的阿里云地域中创建一定数量的ECS资源，更多详情，请参阅 [使用限制](~~25412~~)。

您也可以根据自己的需求 [提交工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex) 提高资源使用上限。

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeAccountAttributes)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|RegionId|String|是|cn-hangzhou|地域ID。您可以调用 [DescribeRegions](~~25609~~) 查看最新的阿里云地域列表。

 |
|Action|String|否|DescribeAccountAttributes|系统规定参数。取值：DescribeAccountAttributes

 |
|ZoneId|String|否|cn-hangzhou-b|可用区ID。

 |
|AttributeName.N|RepeatList|否|max-security-groups|查询某类资源的使用上限，N的取值范围为1~8。取值范围：

 -   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-delicated-hosts：当前地域下专用宿主机数量。
-   supported-postpaid-instance-types：当前地域下按量付费 I/O 优化实例规格。
-   real-name-authentication：账号是否完成了实名认证。

**说明：** 您只有完成了实名认证 才可以创建ECS实例。


 默认值：空

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|AccountAttributeItems| | |指定地域下账号特权的信息集合

 |
|└AttributeName|String|max-security-groups|资源的使用上限分类。可能值:

 -   instance-network-type：当前地域可选择的网络类型。
-   max-security-groups：安全组数量。
-   max-elastic-network-interfaces：当前地域下弹性网卡的数量。
-   max-postpaid-instance-vcpu-count：当前地域下按量实例的vCPU核数。
-   max-spot-instance-vcpu-count：当前地域下抢占式实例vCPU核数。
-   max-delicated-hosts：当前地域下专用宿主机数量。
-   supported-postpay-instance-types：当前地域下按量付费I/O优化实例规格。
-   real-name-authentication：账号是否完成了实名认证。

 |
|└AttributeValues| | |资源的使用上限具体数值

 |
|└Count|Integer|3|特权属性类型的数量。

 |
|└ExpiredTime|String|2019-01-01T12:30:00Z|特权到期时间， 仅存在到期时间的账号特权会返回该参数。按照 [ISO8601](~~25696~~) 标准表示，并需要使用 UTC 时间。格式为yyyy-MM-ddTHH:mm:ssZ。

 |
|└InstanceChargeType|String|PrePaid|实例计费方式

 |
|└InstanceType|String|\["ecs.g5.large"\]|实例规格

 |
|└Value|String|800|当前地域或全部地域下某类资源的使用上限具体数值。可能值:

 -   分类为 max-security-groups、max-elastic-network-interfaces、max-postpaid-instance-vcpu-count、max-delicated-hosts、max-spot-instance-vcpu-count时：返回0或正整数。
-   分类为 supported-postpay-instance-types 时：返回实例规格取值。参阅 [实例规格族](~~25378~~)。
-   分类为 real-name-authentications时：返回 yes | none | unnecessary
-   分类为 为instance-network-type 时：返回 vpc | classic

 |
|└ZoneId|String|cn-hangzhou-b|可用区ID

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E|请求 ID

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

https://ecs.aliyuncs.com/?Action=DescribeAccountAttributes
&RegionId=cn-hangzhou
&ZoneId=cn-hangzhou-b
&AttributeName.1=max-security-groups
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeAccountAttributesResponse>
    <AccountAttributeItems>
        <AccountAttributeItem>
            <AttributeName>max-security-groups</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>800</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
          <AccountAttributeItem>
            <AttributeName>instance-network-type</AttributeName>
            <AttributeValues>
                <ValueItem>
                    <Value>vpc</Value>
                    <Value>classic</Value>
                <ValueItem>
            </AttributeValues>
        </AccountAttributeItem>
     </AccountAttributeItems>
    <RequestId>675B6D89-A3EB-4987-BAF3-610591E0D019</RequestId>
</DescribeAccountAttributesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"AccountAttributeItems":{
		"AccountAttributeItem":[
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"100"
						}
					]
				},
				"AttributeName":"max-security-groups"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"2"
						}
					]
				},
				"AttributeName":"max-dedicated-hosts"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-postpaid-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"1000"
						}
					]
				},
				"AttributeName":"max-spot-instance-vcpu-count"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"5000"
						}
					]
				},
				"AttributeName":"max-elastic-network-interfaces"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"yes"
						}
					]
				},
				"AttributeName":"real-name-authentication"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"vpc"
						}
					]
				},
				"AttributeName":"instance-network-type"
			},
			{
				"AttributeValues":{
					"ValueItem":[
						{
							"Value":"ecs.f3-c16f1.4xlarge"
						},
						{
							"Value":"ecs.g5.2xlarge"
						}
					]
				},
				"AttributeName":"supported-postpaid-instance-types"
			}
		]
	},
	"RequestId":"8CE45CD5-31FB-47C2-959D-CA8144CE9F42"
}
```

## 错误码 { .section}

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|403|Invalid.Parameter|The required parameter regionId must be not null.|确实必需参数。|

[查看本产品错误码](https://error-center.aliyun.com/status/product/Ecs)

