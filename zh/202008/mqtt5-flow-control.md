

MQTT v5 带来了很多新的特性，我们会尽量以通俗易懂的方式展示这些特性，并探讨这些特性对开发者的影响。到目前为⽌，我们已经探讨过这些 [MQTT v5 新特性](https://www.emqx.com/zh/mqtt/mqtt5)，现在我们将继续讨论： **流量控制** 



## 流量控制

通常服务端的资源都是固定且有限的，而客户端的流量则可能是随时随地变化的。正常业务（用户集中访问、设备大量重启）、被恶意攻击、网络波动，都会导致流量出现激增，如果服务端没有对其进行任何限制，就会导致负载迅速上升，进而导致响应速度下降，影响其他业务，甚至导致系统瘫痪。

![image20200730133959150.png](https://static.emqx.net/images/52cfac4662c53ea76451ff66759e4059.png)

因此，我们需要流量控制，可以是限制发送端的发送速率，也可以是限制接收端的接收速率，但最终目的都是保证系统的稳定。常用的流控算法有滑动窗口计数法、漏桶算法以及令牌桶算法。

MQTT v3 没有规范流量控制行为，导致客户端和服务端在实现上百花齐放，进而影响了设备的接入和管理。不过现在，MQTT v5 已经引入了流量控制功能，这也是我们接下来将要探讨的内容。



## MQTT v5 中的流量控制

在 MQTT v5 中，发送端会有一个初始的发送配额，每当它发送一个 QoS 大于 0 的 PUBLISH 报文，发送配额就相应减一，而每当收到一个响应报文（PUBACK、PUBCOMP 或 PUBREC），发送配额就会加一。如果接收端没有及时响应，导致发送端的发送配额减为 0，发送端应当停止发送所有 QoS 大于 0 的 PUBLISH 报文直至发送配额恢复。我们可以将其视为变种的令牌桶算法，它们之间的区别仅仅是增加配额的方式从以固定速率增加变成了按实际收到响应报文的速率增加。

这种算法能够更加积极和充分地利用资源，因为它没有在发送速率的层面上进行限制，发送速率完全取决于对端的响应速率和网络情况，如果接收端空闲且网络良好，那么发送端可以得到比较高的发送速率，反之则会被限制到一个比较低的发送速率上。



## Receive Maximum 属性

为了支持流量控制，MQTT v5 新增了一个 Receive Maximum 属性，它存在于 CONNECT 报文与 CONNACK 报文，表示客户端或服务端愿意同时处理的 QoS 为 1 和 2 的 PUBLISH 报文最大数量，即对端可以使用的最大发送配额。如果接收端已收到但未发送响应的 QoS 大于 0 的 PUBLISH 报文数量超过 Receive Maximum 的值，接收端将断开连接避免受到更严重的影响。

![image20200730173320715.png](https://static.emqx.net/images/7fe5bd2f4190b0d9f4891b81de5246ff.png)

## 为什么没有 QoS 0 ？

也许你已经发现，前文所有提到 PUBLISH 报文的地方都使用了定语： QoS 大于 0。QoS 0 消息的特性决定了它不存在响应报文，也许是觉得 QoS 0 消息的重要性不高，接收端可以通过强制的接收速率限制来约束 QoS 0 消息，也许是其他原因，总之最后我们看到的 MQTT v5 的流量控制机制完全依赖响应报文，这就导致它的流量控制只能局限在 QoS 1,2 消息中。

聊胜于无，MQTT v5 给出了一个并不完美的解决方案，或者说仅仅只是一个建议：当发送配额减为 0 时，发送端可以选择继续发送 QoS 为 0 的 PUBLISH 报文，也可以选择暂停发送。其中暂停发送的行为逻辑是，如果 QoS 1,2 的 PUBLISH 报文的应答速度变慢，通常意味着接收端的消费能力已经下降，继续发送 QoS 0 消息只会令情况变得更糟。



## 结论

尽管 MQTT v5 的流量控制机制依然存在一些不足，但我们依然建议用户尽可能地使用它。基于响应报文的发送配额算法使得发送端能够最大程度地利用资源，Receive Maximum 使得通信双方不再需要事先协商发送配额，从而获得更高的透明度和灵活性，这在需要接入多厂商设备时是很有帮助的。