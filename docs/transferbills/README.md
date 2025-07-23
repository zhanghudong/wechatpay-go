# 微信支付 API v3 Go SDK - transferbills

* 场景及业务流程：
    商户可通过该产品实现向单个用户微信零钱进行转账的操作。转账后可能需要用户确认才能到账（状态为WAIT_USER_CONFIRM），也可能直接到账。可用于红包奖励、佣金结算、退款补偿等场景。
    [https://pay.weixin.qq.com/wiki/doc/apiv3/open/pay/chapter4_3_1.shtml](https://pay.weixin.qq.com/wiki/doc/apiv3/open/pay/chapter4_3_1.shtml)
* 接入步骤：
    * 商户在微信支付商户平台开通"转账到零钱"产品权限，并配置相关参数。
    * 调用转账接口，向指定用户微信零钱发起转账。
    * 调用查询接口，可获取到转账详情及当前状态。
    * 可调用撤销接口，在用户确认前撤销转账。
    * 可配置异步通知，接收转账状态变更通知。

## 总览
本 SDK 由 WechatPay APIv3 SDK 生成器生成。生成器基于 [OpenAPI Generator](https://openapi-generator.tech) 构建。

- API 版本: 1.0.0

## 接口列表

所有URI均基于微信支付 API 地址：*https://api.mch.weixin.qq.com*

服务名 | 方法名 | HTTP 请求 | 描述
------------ | ------------- | ------------- | -------------
*TransferBillsApi* | [**CreateTransferBill**](TransferBillsApi.md#createtransferbill) | **Post** /v3/transfer/bills | 发起商家转账到用户零钱
*TransferBillsApi* | [**GetTransferBillByOutBillNo**](TransferBillsApi.md#gettransferbillbyoutbillno) | **Get** /v3/transfer/bills/out-bill-no/{out_bill_no} | 通过商户订单号查询转账单
*TransferBillsApi* | [**GetTransferBillByTransferBillNo**](TransferBillsApi.md#gettransferbillbytransferbillno) | **Get** /v3/transfer/bills/transfer-bill-no/{transfer_bill_no} | 通过微信转账单号查询转账单
*TransferBillsApi* | [**CancelTransferBill**](TransferBillsApi.md#canceltransferbill) | **Post** /v3/transfer/bills/out-bill-no/{out_bill_no}/cancel | 撤销转账

## 通知处理

转账状态变更时，微信支付会向商户配置的通知地址推送通知。详见：
- [转账状态通知处理](NotifyHandling.md)

## 类型列表

### 请求参数类型
 - [CreateTransferBillRequest](CreateTransferBillRequest.md) - 发起转账请求参数
 - [GetTransferBillByOutBillNoRequest](GetTransferBillByOutBillNoRequest.md) - 通过商户订单号查询请求参数
 - [GetTransferBillByTransferBillNoRequest](GetTransferBillByTransferBillNoRequest.md) - 通过微信转账单号查询请求参数
 - [CancelTransferBillRequest](CancelTransferBillRequest.md) - 撤销转账请求参数

### 响应结果类型
 - [CreateTransferBillResponse](CreateTransferBillResponse.md) - 发起转账响应结果
 - [GetTransferBillResponse](GetTransferBillResponse.md) - 查询转账单响应结果
 - [CancelTransferBillResponse](CancelTransferBillResponse.md) - 撤销转账响应结果

### 通知相关类型
 - [TransferNotifyContent](TransferNotifyContent.md) - 转账通知内容
 - [TransferState](TransferState.md) - 转账状态枚举
 - [EventType](EventType.md) - 事件类型枚举

### 辅助类型
 - [TransferSceneReportInfo](TransferSceneReportInfo.md) - 转账场景信息

## 核心特性

### 🔒 安全加密
- 支持收款方姓名RSA/AES-GCM加密
- 敏感信息自动加密处理
- 符合微信支付安全规范

### 📋 场景信息上报
- 必填的转账场景信息上报
- 支持自定义场景类型和内容
- 满足监管合规要求

### 🔔 异步通知
- 转账状态变更实时通知
- 完善的通知验证机制
- 兼容现有通知处理框架

### 🎯 精准查询
- 支持商户订单号查询
- 支持微信转账单号查询
- 状态实时同步

### ⚡ 快速撤销
- 用户确认前可撤销转账
- 避免误操作造成损失
- 提升用户体验

## 使用建议

### 转账状态处理
- **WAIT_USER_CONFIRM**：转账需要用户确认，24小时内有效
- **SUCCESS**：转账成功，资金已到账
- **PROCESSING**：转账处理中
- **FAIL**：转账失败

### 错误处理
- 妥善处理转账失败情况
- 建议实现重试机制
- 记录详细的操作日志

### 通知处理
- 建议使用异步通知获取最终状态
- 实现幂等性处理避免重复操作
- 验证通知签名确保安全性

### 资金安全
- 转账前进行金额校验
- 实现转账限额控制
- 建立完善的对账机制