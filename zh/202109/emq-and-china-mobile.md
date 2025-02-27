8 月 23 日- 25 日，2021 重庆智博会成功举办。本次智博会以「智能化:为经济赋能，为生活添彩」为主题，来自各行业的近 200 家企业在展会上展示了数字经济下的先进技术成果。


![重庆广电《第1眼新闻》](https://static.emqx.net/images/484849a4b3a4fb763d5048b32c8abc0b.png)

图源：重庆广电《第1眼新闻》

中国移动展示的车路协同 5G  时空信息平台成为了本次智博会最大的亮点之一。据重庆移动车路协同项目专家张力介绍：通过这一信息平台，所有的道路信息、交通工况信息，都可以借助路侧设备和 5G + 北斗 + V2X 网络，收集到云控中心。那么对于无人驾驶车来说，就可以 5G  超远距离感知的方式获取前方的交通信息，并据此规划调整车辆配速。对于社会车辆，也同样可以利用 5G  终端，实时收取云控平台传来交通工况信息，及时掌握路况。

![重庆广电《第1眼新闻》](https://static.emqx.net/images/15a599b5e518bb28ed9f5f9b1d0e2d78.png)

图源：重庆广电《第1眼新闻》

事实上，这一展示场景已经在重庆两江协同创新区开始了落地实践。前不久，重庆两江新区获工信部批准创建国家级车联网先导区，成为全国第四个、西部第一个国家级车联网先导区，将在龙盛片区打造 55 公里的 5G 车路协同示范路段。这一项目正是基于中国移动「5G + 北斗 + V2X 三网协同、云网融合」方案，利用全国首创的 5G  RCS 车路协同消息技术，构造起针对山地城市交通场景、社会车辆可感知的车路协同示范区。

![重庆广电《第1眼新闻》](https://static.emqx.net/images/92fdee1a604fff43b060f3d72f645ab5.png)

图源：重庆广电《第1眼新闻》

**而在这一方案中也有 EMQ 的深度参与**，提供了车路协同、北斗高精定位等超低时延消息通信服务。


## 5G+北斗+V2X 车路协同方案

### 方案概述

车路协同 V2X 的发展主要经历以下三个阶段。

![中国移动车路协同V2X智慧交通解决方案](https://static.emqx.net/images/efab423e5dc5de1f9d3cb1e6cbebd1ad.png)

图源：中国移动车路协同V2X智慧交通解决方案（http://iot.10086.cn/solution/read/id/1411）

 产业和技术的发展推动以车载信息服务为主的传统车联网，向以智能化和网联化为基础的智能辅助驾驶、自动驾驶及智能交通的下一代车联网发展，V2X 是下一代车联网的核心。

![5G北斗V2X车路协同方案.png](https://static.emqx.net/images/db44414464afd855d8dbf2e8e9318539.png)

5G + 北斗 + V2X 车路协同方案采用中国移动「人-车-路-网-云」架构搭建。基于车机端和路侧设备的感知数据，通过 MQTT、JT808、TCP 等协议将车端、路侧设施感知到的路况信息通过 5G 网络超远局里感知的方式推送到车端或 5G 终端。

### EMQ车路协同消息服务

作为实现车路协同的关键，5G + 北斗 + V2X 车路协同方案采用了 EMQ X 消息中间件进行数据消息服务。

![EMQ X 车路协同平台.png](https://static.emqx.net/images/48190ad0d0f9572d60c52f6ce112ed10.png)

搭载了 EMQ X 的车路协同平台具备了以下特点：

- 低时延

  车路协同、自动驾驶场景对消息时延相当敏感， EMQ X 基于强大的 message Routing 可以实现超低时延的消息通信，可满足车联网场景的时延要求。

- 海量连接

  EMQ X 采用分布式集群架构，支持千万级车载/路侧设备的并发接入，并支持容量的水平动态扩展能力。

- Qos消息可靠传输

  EMQ X 支持全栈的 MQTT 协议支持，通过 MQTT Qos 机制保障消息的可靠传输。

- 平台高可用

  通过高可用的分布式集群搭建，EMQ X 支持自动集群、集群脑裂监测和集群脑裂自愈合等能力，可以提供 99.99% 的 SLA 服务保证。



## 未来展望

在智博会上，张力经理表示要「通过把云和网这两层级做实做厚，拉动车、路、云、网、图，与各个层级合作伙伴一起开放共赢」。为了实现此目标，EMQ  也将紧密配合中国移动车路协同发展规划，推进双方在云端更丰富的消息推送和边缘计算等场景展开更加深入的合作，为自动驾驶、车辆协同、车联网用户提供更快、更好、更智能的消息服务，与中国移动共同全方位打造 5G 交通生态链。