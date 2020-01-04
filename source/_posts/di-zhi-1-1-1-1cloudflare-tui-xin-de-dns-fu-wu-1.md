---
title: 地址 1.1.1.1，Cloudflare 推新的 DNS 服务
url: 517.html
id: 517
categories:
  - 文章页
  - 资讯
date: 2018-04-04 18:30:17
tags:
  - 资讯
---

2018.4.1 Cloudflare 宣布正式推出 1.1.1.1 公共 DNS 服务，号称任何人都可以使用它可以加快互联网访问速度并并保持连接私密性。Cloudflare 声称它将是“互联网上速度最快，隐私优先的消费者 DNS 服务”，此前类似的免费公共服务 OpenDNS 与 Google DNS 都已经服役了很长时间。 ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180404182640.png) Cloudflare 与 APNIC 合作通过 1.1.1.1 和 1.0.0.1 两个 IP 提供 DNS 服务。并且，本身作为互联网服务供应商的 Cloudflare 本身还利用了自己的长处，分析和研究垃圾流量，以保证 DNS 解析数据的准确。 ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180404182836.png) Cloudflare 的 DNS 将支持 DNS-over-TLS 和 DNS-over-HTTPS，全球平均响应时间为 14ms，而 OpenDNS 为 20ms，Google 的 DNS 为 34ms。 ![](http://47.100.4.8/wp-content/uploads/2018/04/QQ图片20180404182853.png) DNS 的全名为网域名称系统（domain name system），可将网域名称转成 IP 位址，它就像是个网络目录，协助使用者通过网域名称找到相对应的地址。 Cloudflare 在 1.1.1.1 网站上说明，DNS 通常非常缓慢且缺乏安全性，有些 DNS 供应商甚至会销售使用者网络浏览的资料，并用以发送目标式广告。而 1.1.1.1 将以使用者的隐私为主，既不会记录使用者的 IP 位址，也不会销售使用者资料，或是利用这些资料发送广告。 此外，Cloudflare 也希望 1.1.1.1 成为全球最快的 DNS 目录，根据 DNSPerf 的 DNS 监控数据，1.1.1.1 解析网域名称的速度比第二名的 DigitalOcean 快了 53%。 Cloudflare 指出，网络上的每件事几乎都是始于 DNS 请求，因此，选择一个最快的 DNS 目录基本上将加速使用者使用任何网络。 1.1.1.1 这个 IP 位址属于 APNIC 所有，容易记忆的程度可媲美 Google 的 8.8.8.8 或是 IBM 的 9.9.9.9，此外，强调隐私保护与速度也都让该服务备受期待。如果您有兴趣启用 Cloudflare 的新 DNS，您可以在 https://1.1.1.1 找到所有信息。   转自：ITHOME +  Cloudflare