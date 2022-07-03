# SSP2022 服务器运行状态监控面板

监控您的服务器运行状态。

## 准备工作

- 一个Cloudflare账户
- Cloudflare Workers ID
- Cloudflare Workers API

## 开始

### 一、Fork本仓库，并修改 README.md 中第20行仓库地址为Fork后你的仓库地址


### 二、部署在Cloudflare上

[![Deploy to Cloudflare Workers](https://camo.githubusercontent.com/1f3d0b4d44a2c3f12c78bd02bae907169430e04d728006db9f97a4befa64c886/68747470733a2f2f6465706c6f792e776f726b6572732e636c6f7564666c6172652e636f6d2f627574746f6e3f706169643d74727565)](https://deploy.workers.cloudflare.com/?url=https://github.com/fangaso/ssp2022)

1. 单击按钮并按照说明进行操作
2. 输入相关信息
3. 在你的新仓库 -> 设置(Setting) -> 机密(Secrets) -> 活动(Actions) 添加如下变量：

   ```yaml
   - 名称(Name)：CF_ACCOUNT_ID
   - 值(Value)：你的 Cloudflare Workers ID
   - 名称()：CF_API_TOKEN
   - 值(Value)：你的具有 Cloudflare Workers 管理权限的API令牌
   ```

4. 在 Github Actions 中启用并开启工作流
5. 编辑 [config.yaml](./config.yaml) 配置文件

   ```yaml
   settings:
     title: '标题'
     url: 'https://status.fangaso.com' # SSP2022 调用地址
     logo: logo-192x192.png # 网站LOGO，在 /public 目录下
     daysInHistogram: 90 # 监控周期天数
     collectResponseTimes: false # 实验功能，不懂勿开

     # SSP2022 配置信息
     allmonitorsOperational: '所有系统正常运行'
     notAllmonitorsOperational: '所有系统未正常运行'
     monitorLabelOperational: '正常运行'
     monitorLabelNotOperational: '未正常运行'
     monitorLabelNoData: '无数据'
     dayInHistogramNoData: '无数据'
     dayInHistogramOperational: '全部正常'
     dayInHistogramNotOperational: '故障'

     # 监控列表
   monitors:
     - id: www-fangaso-com # 唯一ID
       name: www.fangaso.com # 名称
       description: '你的站点描述' # 为空则不显示描述
       url: 'https://.fangaso.com' # 监控URL
       method: GET # 监控模式，默认为GET，可选POST
       expectStatus: 200 # 运行状态，默认为200(HTTP 200)
       followRedirect: false # 获取跟随重定向，默认不开
       linkable: false # 标题超链接指向监控URL，默认打开
   ```

6. 部署
