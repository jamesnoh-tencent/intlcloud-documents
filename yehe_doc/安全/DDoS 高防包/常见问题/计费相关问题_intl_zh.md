### 想要中止高防包服务怎么办？

DDoS 高防包服务为后付费模式。当您想要结束该服务请务必 [提交工单](https://console.cloud.tencent.com/workorder/category)至客服申请销毁资源，若资源未销毁，可能会持续产生费用。

- 当月申请资源销毁后本月各项费用不变（包年包月项的费用照常支付，按天按量计费项根据实际资源销毁时产生费用为准进行支付），资源销毁后该资源防护服务立即终止，次月资源不再计费。

- 整个销毁流程需要1-3个工作日完成，具体时长以实际操作时间为准（销毁期间可能会陆续产生防护费用）。



### 受防护的 IP 一天之内遭受多次攻击，怎么计算防护次数的消耗？

DDoS 高防包的全力防护服务：当检测到实例中防护IP的攻击流量≥10Gbps时且半小时后不再有攻击流量，则认为本次攻击结束，扣除1次全力防护，或如果攻击持续进行着且超过半个小时，则直到本次攻击全部结束后才扣除1次全力防护。

### DDoS 高防包的全力防护和 DDoS 高防 IP 的弹性防护计费方式有什么区别？
当遭受攻击时，自动调用该高防包实例所在地域的腾讯云最大DDoS防护能力提供全力防护。全力防护服务包含在高防包中，不额外产生弹性防护费用。
DDoS 高防 IP 服务的弹性防护计费按照当日产生最大攻击流量对应弹性防护区间带宽进行计费。

