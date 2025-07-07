# Aqara-P100-HA
通过Aqara 开发者平台，借助Node-RED，将门锁P100的各项状态接入家庭助理

![1210751746712804_ pic](https://github.com/user-attachments/assets/525a7f52-7ef3-4c04-8f09-641efdcba3cf)
<img width="868" alt="image" src="https://github.com/user-attachments/assets/10d1a7d2-039c-41e6-9bd1-8d348d1d102a" />

具体流程：
  1. 在Node-RED 中构建认证流程，通过 HTTP 请求向 Aqara 云平台发送凭据，获取长期访问令牌（AccessToken）
  2. 使用该令牌，调用Aqara 云API 接口，订阅门锁等设备相关资源（如开锁记录、门锁状态变更等）
  3. 配置Aqara 云平台的推送地址为Node-RED 的HTTP 端点，实现事件实时接收
  4. Node-RED 监听Aqara 云平台推送的JSON 消息，提取关键字段（如用户、时间、事件类型）并结构化处理
  5. 通过 Webhook 将整理后的事件信息，推送至Home Assistant，生成实体，用于自动化响应或消息展示

使用方法：

  0. 前置条件：拥有公网IP、域名；搭建好Home Assistant、Node-RED；注册成为Aqara 开发者并建立项目
  1. 下载并解压文件
  2. 将Node_Flow 文件夹中的AqaraP100流程.json 导入至Node-RED 中，根据说明填入相关信息
  3. 将HA_Config 文件夹中configuration.yaml 内的代码粘贴进自己Home Assistant 的同名配置文件中，注意缩进，重启HA
  4. HA 仪表盘新建一个部件，选择以YAML 编辑，将HA_Config 文件夹中dashboards.yaml 中的内容粘贴至此
