## 接口概述
本接口为桔牛按照极速云提供的《极速云-对外通知接口说明》V1.0创建。主要用于接收商户申请贷款流程中极速云的通知。

## 接口详情
> 说明：所有接口通过HTTPS协议提供，只支持POST请求  

### 申请审核状态通知
- 接口地址  
  https://<host>/jisu/audit_result.do
- 接口参数 

 值            | 类型   |  描述 
---            | ----   | ----  
id             | string | 消息ID
application_id | string | 申请ID 
status         | string | 审核状态（提交申请、审核通过、审核放弃、审核拒绝）
desc           | string | 状态描述（放弃或拒绝的原因） 
notify_time    | string | 通知时间（2018-04-03 13:03:44）  

- 返回  
  成功时返回success，失败时返回对应错误

### 放款出帐通知
- 接口地址  
  https://<host>/jisu/loan_notify.do
- 接口参数 

值              | 类型     | 描述
---             | ----     | ----  
id              |  string  |  消息ID
application_id  |  string  |  申请ID
form_id         |  string  |  提款ID
type            |  string  |  1:放款到银行卡 2:放款到电子账户
bank_name       |  string  |  收款卡号所属银行
bank_card       |  string  |  收款卡号
amount          |  string  |  放款金额（单位分）
notify_time     |  string  |  通知时间（2018-04-03 13:03:44）

- 返回  
  成功时返回success，失败时返回对应错误


### 还款结清通知
- 接口地址  
  https://<host>/jisu/settle_notify.do
- 接口参数 

 值            | 类型   |  描述 
---            | ----   | ----  
application_id | string | 申请ID 
amount         | string | 借款金额（单位分） 
notify_time    | string | 通知时间（2018-04-03 13:03:44）  

- 返回  
  成功时返回success，失败时返回对应错误
