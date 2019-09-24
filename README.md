# Nepxion Discovery Guide
[![Total lines](https://tokei.rs/b1/github/Nepxion/Discovery?category=lines)](https://tokei.rs/b1/github/Nepxion/Discovery?category=lines)  [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg?label=license)](https://github.com/Nepxion/Discovery/blob/master/LICENSE)  [![Maven Central](https://img.shields.io/maven-central/v/com.nepxion/discovery.svg?label=maven%20central)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.nepxion%22%20AND%20discovery)  [![Javadocs](http://www.javadoc.io/badge/com.nepxion/discovery-plugin-framework.svg)](http://www.javadoc.io/doc/com.nepxion/discovery-plugin-framework)  [![Build Status](https://travis-ci.org/Nepxion/Discovery.svg?branch=master)](https://travis-ci.org/Nepxion/Discovery)  [![Codacy Badge](https://api.codacy.com/project/badge/Grade/8e39a24e1be740c58b83fb81763ba317)](https://www.codacy.com/project/HaojunRen/Discovery/dashboard?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=Nepxion/Discovery&amp;utm_campaign=Badge_Grade_Dashboard)

每一个访问路过的朋友，如果您觉得这个开源框架不错，请顺手给它点个Star吧

![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/Star2.jpg)

Nepxion Discovery Guide是Nepxion Discovery的极简指南，有助于使用者快速入门。它基于Spring Cloud Greenwich和Finchley版而制作（使用者可自行修改为Edgware版），主要功能包括：
- 基于Header传递的全链路灰度路由，网关为路由触发点。采用配置中心配置路由规则映射在网关过滤器中植入Header信息而实现，路由规则传递到全链路服务中。路由方式主要包括版本和区域的匹配路由、版本和区域的权重路由两种，除此之外，不在本文介绍内的，还包括基于机器IP地址和端口的路由
- 基于规则订阅的全链路灰度发布。采用配置中心配置灰度规则映射在全链路服务而实现，所有服务都订阅某个共享配置。发布方式主要包括版本和区域的匹配发布、版本和区域的权重发布
- 全链路服务隔离。包括注册隔离、消费端隔离和提供端服务隔离，示例仅提供基于Group隔离。除此之外，不在本文介绍内的，还包括：
    - 注册隔离：黑/白名单的IP地址的注册隔离、最大注册数限制的注册隔离
    - 消费端隔离：黑/白名单的IP地址的消费端隔离
- 全链路服务限流熔断降级权限，集成阿里巴巴Sentinel，有机整合灰度路由，扩展LimitApp的机制，通过动态的Http Header方式实现组合式防护机制，包括基于服务名、基于灰度组、基于灰度版本、基于灰度区域、基于机器地址和端口等防护机制，支持自定义任意的业务参数组合实现该功能。支持原生的流控规则、降级规则、授权规则、系统规则、热点参数流控规则
- 全链路灰度调用链。包括Header方式和日志方式，Header方式框架内部集成，日志方式通过MDC输出（需使用者自行集成）
- 同城双活多机房切换支持。它包含在“基于Header传递的全链路灰度路由”里
- 数据库灰度发布。内置简单的数据库灰度发布策略，它不在本文的介绍范围内
- 灰度路由和发布的自动化测试
- Docker容器化和Kubernetes平台的无缝支持部署

[**Nacos**] 阿里巴巴中间件部门开发的新一代集服务注册发现中心和配置中心为一体的中间件。它是构建以“服务”为中心的现代应用架构 (例如微服务范式、云原生范式) 的服务基础设施，支持几乎所有主流类型的“服务”的发现、配置和管理，更敏捷和容易地构建、交付和管理微服务平台

[**Sentinel**] 阿里巴巴中间件部门开发的新一代以流量为切入点，从流量控制、熔断降级、系统负载保护等多个维度保护服务的稳定性的分布式系统的流量防卫兵。它承接了阿里巴巴近10年的双十一大促流量的核心场景，例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等

[**Spring Cloud Alibaba**] 阿里巴巴中间件部门开发的Spring Cloud增强套件，致力于提供微服务开发的一站式解决方案。此项目包含开发分布式应用微服务的必需组件，方便开发者通过Spring Cloud编程模型轻松使用这些组件来开发分布式应用服务。依托Spring Cloud Alibaba，只需要添加一些注解和少量配置，就可以将Spring Cloud应用接入阿里微服务解决方案，通过阿里中间件来迅速搭建分布式应用系统

示例以Nacos为服务注册中心和配置中心（使用者可自行换成其它服务注册中心和配置中心），集成Spring Cloud Alibaba，通过Gateway和Zuul调用两个版本或者区域的服务，模拟网关灰度路由和服务灰度权重的功能

如果使用者需要更强大的功能，请参考[源码主页](https://github.com/Nepxion/Discovery)。规则策略很多，请使用者选择最适合自己业务场景的方式

鸣谢
- 感谢阿里巴巴中间件Nacos和Sentinel团队，尤其是Nacos负责人@于怀，Sentinel负责人@子衿，Spring Cloud Alibaba负责人@亦盏、@洛夜的技术支持
- 感谢携程Apollo团队，尤其是@宋顺，特意开发OpenApi包和技术支持
- 感谢代码贡献者，包括@WeihuaWang，@Esun，@liumapp，@terranhu，@JikaiSun，@HaoHuang，@FanYang，@Ankeway等
- 感谢为本框架进行测试验证和问题分析定位的同学，包括@CongweiXu，@fan，@阿神，@慕紫，@郝俊仁，@Windon，@李鹏，@任学会等
- 感谢为本框架提出宝贵意见和建议的同学
- 感谢使用本框架的公司和企业。不完全统计，目前社区开源项目已经被如下公司使用或者调研，为提供更好的专业级服务，请更多已经使用本框架的公司和企业联系我

平安银行 | 平安一账通 | 众安保险 | 民生银行北京分行 | 浦发信用卡 | 招商银行

太平洋保险 | 太平保险 | 东方航空 | 瑞幸咖啡 | 顺丰科技 | 悟空丰运 | 微鲸科技 

海尔消费金融 | 御家汇 | 苏州太谷 | 创软科技 | 东华软件

智慧校园 | 杭州融都科技 | 杭州天阙科技 | 杭州惠借科技 | 深圳捷顺 | 云帐房网络科技

数梦工场科技 | 冰鉴信息科技 | 轻舟科技 |  巨玩科技 | 琢创网络科技 | 上海青客

顶昂信息科技 | 上海炫贵一下智能科技 | 苏州思必驰 | 上海弘人网络科技有限公司 | 依威能源

## 目录
- [请联系我](#请联系我)
- [服务治理架构图](#服务治理架构图)
- [环境搭建](#环境搭建)
- [启动服务](#启动服务)
- [环境验证](#环境验证)
- [基于Header传递方式的网关灰度路由策略](#基于Header传递方式的网关灰度路由策略)
    - [灰度路由架构图](#灰度路由架构图)
    - [配置网关灰度路由策略](#配置网关灰度路由策略)
        - [版本匹配灰度路由策略](#版本匹配灰度路由策略)
        - [版本权重灰度路由策略](#版本权重灰度路由策略)    
        - [区域匹配灰度路由策略](#区域匹配灰度路由策略)
        - [区域权重灰度路由策略](#区域权重灰度路由策略)
    - [通过其它方式设置网关灰度路由策略](#通过其它方式设置网关灰度路由策略)
        - [通过前端传入灰度路由策略](#通过前端传入灰度路由策略)
        - [通过业务参数在网关过滤器中自定义灰度路由策略](#通过业务参数在网关过滤器中自定义灰度路由策略)
        - [通过业务参数在策略类中自定义灰度路由策略](#通过业务参数在策略类中自定义灰度路由策略)
    - [配置前端灰度&网关灰度路由组合式策略](#配置前端灰度&网关灰度路由组合式策略)    
- [基于订阅方式的全链路灰度发布规则](#基于订阅方式的全链路灰度发布规则)
    - [配置全链路灰度匹配规则](#配置全链路灰度匹配规则)
        - [版本匹配灰度规则](#版本匹配灰度规则)
        - [区域匹配灰度规则](#区域匹配灰度规则)
    - [配置全链路灰度权重规则](#配置全链路灰度权重规则)
        - [全局版本权重灰度规则](#全局版本权重灰度规则)
        - [局部版本权重灰度规则](#局部版本权重灰度规则)
        - [全局区域权重灰度规则](#全局区域权重灰度规则)
        - [局部区域权重灰度规则](#局部区域权重灰度规则)
    - [配置全链路灰度权重&灰度版本组合式规则](#配置全链路灰度权重&灰度版本组合式规则)
- [全链路服务隔离](#全链路服务隔离)
    - [注册服务隔离](#注册服务隔离)
    - [消费端服务隔离](#消费端服务隔离)
    - [提供端服务隔离](#提供端服务隔离)
- [全链路服务限流熔断降级权限](#全链路服务限流熔断降级权限)
    - [原生Sentinel注解](#原生Sentinel注解)
    - [原生Sentinel规则](#原生Sentinel规则)
        - [流控规则](#流控规则)
        - [降级规则](#降级规则)
        - [授权规则](#授权规则)
        - [系统规则](#系统规则)
        - [热点参数流控规则](#热点参数流控规则)	
    - [基于灰度路由和Sentinel-LimitApp扩展的防护机制](#基于灰度路由和Sentinel-LimitApp扩展的防护机制)
        - [基于服务名的防护机制](#基于服务名的防护机制)
        - [基于灰度组的防护机制](#基于灰度组的防护机制)
        - [基于灰度版本的防护机制](#基于灰度版本的防护机制)
        - [基于灰度区域的防护机制](#基于灰度区域的防护机制)
        - [基于机器地址和端口的防护机制](#基于机器地址和端口的防护机制)
        - [自定义业务参数的组合式防护机制](#自定义业务参数的组合式防护机制)
- [全链路灰度调用链](#全链路灰度调用链)
    - [Header输出方式](#Header输出方式)
    - [日志输出方式](#日志输出方式)
- [Docker容器化和Kubernetes平台支持](#Docker容器化和Kubernetes平台支持)
- [Star走势图](#Star走势图)

## 请联系我
微信和公众号

![Alt text](https://github.com/Nepxion/Docs/raw/master/zxing-doc/微信-1.jpg)![Alt text](https://github.com/Nepxion/Docs/raw/master/zxing-doc/公众号-1.jpg)

## 部署架构拓扑图
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/BasicTopology.jpg)

## 灰度方式区别图

![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/Difference.jpg)

## 服务治理架构图
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/Govern.jpg)

## 环境搭建
- 下载代码
    - Git clone https://github.com/Nepxion/DiscoveryGuide.git 
- 代码导入IDE
- 下载Nacos服务器
    - 从[https://github.com/alibaba/nacos/releases](https://github.com/alibaba/nacos/releases)获取nacos-server-x.x.x.zip，并解压
- 启动Nacos服务器
    - Windows环境下，运行bin目录下的startup.cmd
    - Linux环境下，运行bin目录下的startup.sh

## 启动服务 
- 在IDE中，启动四个应用服务和两个网关服务，如下： 

| 类名 | 微服务 | 服务端口 | 版本 | 区域 |
| --- | --- | --- | --- | --- |
| DiscoveryGuideServiceA1.java | A1 | 3001 | 1.0 | dev |
| DiscoveryGuideServiceA2.java | A2 | 3002 | 1.1 | qa |
| DiscoveryGuideServiceB1.java | B1 | 4001 | 1.0 | qa |
| DiscoveryGuideServiceB2.java | B2 | 4002 | 1.1 | dev |
| DiscoveryGuideGateway.java | Gateway | 5001 | 1.0 | 无 |
| DiscoveryGuideZuul.java | Zuul | 5002 | 1.0 | 无 |

注：启动不分前后次序

## 环境验证
- 导入Postman的测试脚本，[脚本地址](https://github.com/Nepxion/Discovery/raw/master/postman.json)

- 在Postman中执行目录结构下 ”Nepxion“ -> ”Discovery极简指南接口“ -> ”Gateway网关调用示例“，调用地址为[http://localhost:5001/discovery-guide-service-a/invoke/gateway](http://localhost:5001/discovery-guide-service-a/invoke/gateway)，相关的Header值已经预设，供开发者修改。测试通过Spring Cloud Gateway网关的调用结果，结果为如下格式：
```xml
gateway -> discovery-guide-service-a[192.168.0.107:3001][V=1.0][R=dev][G=discovery-guide-group] 
-> discovery-guide-service-b[192.168.0.107:4001][V=1.0][R=qa][G=discovery-guide-group]
```

- 在Postman中执行目录结构下 ”Nepxion“ -> ”Discovery极简指南接口“ -> ”Zuul网关调用示例“，调用地址为[http://localhost:5002/discovery-guide-service-a/invoke/zuul](http://localhost:5002/discovery-guide-service-a/invoke/zuul)，相关的Header值已经预设，供开发者修改。测试通过Zuul网关的调用结果，结果为如下格式：
```xml
zuul -> discovery-guide-service-a[192.168.0.107:3001][V=1.0][R=dev][G=discovery-guide-group] 
-> discovery-guide-service-b[192.168.0.107:4001][V=1.0][R=qa][G=discovery-guide-group]
```

- 上述步骤在下面每次更改规则策略的时候执行，并验证结果和规则策略的期望值是否相同

## 基于Header传递方式的网关灰度路由策略

### 灰度路由架构图

多版本灰度路由架构图
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/RouteVersion.jpg)

多区域灰度路由架构图
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/RouteRegion.jpg)

多IP和端口灰度路由架构图
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/RouteAddress.jpg)

### 配置网关灰度路由策略
在Nacos配置中心，增加网关灰度路由策略

#### 版本匹配灰度路由策略
增加Spring Cloud Gateway的基于版本匹配路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-gateway，策略内容如下，实现从Spring Cloud Gateway发起的调用都走版本为1.0的服务：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <strategy>
        <version>1.0</version>
    </strategy>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-1.jpg)

每个服务调用的版本都可以自行指定，见下面第二条。当所有服务都选同一版本的时候，可以简化成下面第一条
```xml
1. <version>1.0</version>
2. <version>{"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}</version>
```

如果上述表达式还未满足需求，也可以采用通配符（具体详细用法，参考Spring AntPathMatcher）
```xml
* - 表示调用范围为所有服务的所有版本
1.* - 表示调用范围为所有服务的1开头的所有版本
```
或者
```xml
"discovery-guide-service-b":"1.*;1.2.?"
```
表示discovery-guide-service-b服务的版本调用范围是1开头的所有版本，或者是1.2开头的所有版本（末尾必须是1个字符）

#### 版本权重灰度路由策略
增加Spring Cloud Gateway的基于版本权重路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-gateway，策略内容如下，实现从Spring Cloud Gateway发起的调用1.0版本流量调用为90%，1.1流量调用为10%：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <strategy>
        <version-weight>1.0=90;1.1=10</version-weight>
    </strategy>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-2.jpg)

每个服务调用的版本权重都可以自行指定，见下面第二条。当所有服务都选相同版本权重的时候，可以简化成下面第一条
```xml
1. <version-weight>1.0=90;1.1=10</version-weight>
2. <version-weight>{"discovery-guide-service-a":"1.0=90;1.1=10", "discovery-guide-service-b":"1.0=90;1.1=10"}</version-weight>
```

#### 区域匹配灰度路由策略
增加Zuul的基于区域匹配路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现从Zuul发起的调用都走区域为dev的服务：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <strategy>
        <region>dev</region>
    </strategy>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-3.jpg)

每个服务调用的区域都可以自行指定，见下面第二条。当所有服务都选同一区域的时候，可以简化成下面第一条
```xml
1. <region>dev</region>
2. <region>{"discovery-guide-service-a":"dev", "discovery-guide-service-b":"dev"}</region>
```

如果上述表达式还未满足需求，也可以采用通配符（具体详细用法，参考Spring AntPathMatcher）
```xml
* - 表示调用范围为所有服务的所有区域
d* - 表示调用范围为所有服务的d开头的所有区域
```
或者
```xml
"discovery-guide-service-b":"d*;q?"
```
表示discovery-guide-service-b服务的区域调用范围是d开头的所有区域，或者是q开头的所有区域（末尾必须是1个字符）

#### 区域权重灰度路由策略
增加Zuul的基于区域权重路由的灰度策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容如下，实现从Zuul发起的调用dev区域流量调用为85%，qa区域流量调用为15%：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <strategy>
        <region-weight>dev=85;qa=15</region-weight>
    </strategy>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-4.jpg)

每个服务调用的区域权重都可以自行指定，见下面第二条。当所有服务都选相同区域权重的时候，可以简化成下面第一条
```xml
1. <region-weight>dev=85;qa=15</region-weight>
2. <region-weight>{"discovery-guide-service-a":"dev=85;qa=15", "discovery-guide-service-b":"dev=85;qa=15"}</region-weight>
```

### 通过其它方式设置网关灰度路由策略
除了上面通过配置中心发布灰度规路由则外，还有如下三种方式:

#### 通过前端传入灰度路由策略
通过前端（Postman）方式传入灰度路由策略，来代替配置中心方式，传递全链路路由策略。注意：当配置中心和界面都配置后，以界面传入优先

- 版本匹配策略，Header格式如下任选一个：
```xml
1. n-d-version=1.0
2. n-d-version={"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}
```

- 版本权重策略，Header格式如下任选一个：
```xml
1. n-d-version-weight=1.0=90;1.1=10
2. n-d-version-weight={"discovery-guide-service-a":"1.0=90;1.1=10", "discovery-guide-service-b":"1.0=90;1.1=10"}
```

- 区域匹配策略，Header格式如下任选一个：
```xml
1. n-d-region=qa
2. n-d-region={"discovery-guide-service-a":"qa", "discovery-guide-service-b":"qa"}
```
- 区域权重策略，Header格式如下任选一个：
```xml
1. n-d-region-weight=dev=99;qa=1
2. n-d-region-weight={"discovery-guide-service-a":"dev=99;qa=1", "discovery-guide-service-b":"dev=99;qa=1"}
```
- 机器地址策略：
```xml
1. n-d-address={"discovery-guide-service-a":"127.0.0.1:3001", "discovery-guide-service-b":"127.0.0.1:4002"}
```

如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-5.jpg)

![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-6.jpg)

当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。需要通过如下开关做控制：
```xml
# 当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。如果下面开关为true，以网关设置为优先，否则以外界传值为优先。缺失则默认为true
spring.application.strategy.gateway.header.priority=false

# 当外界传值Header的时候，网关也设置并传递同名的Header，需要决定哪个Header传递到后边的服务去。如果下面开关为true，以网关设置为优先，否则以外界传值为优先。缺失则默认为true
spring.application.strategy.zuul.header.priority=false
``` 

#### 通过业务参数在网关过滤器中自定义灰度路由策略
通过网关过滤器传递Http Header的方式传递全链路灰度路由策略。下面代码只适用于Zuul和Spring Cloud Gateway网关，Service微服务不需要加该方式

- 内置策略解析映射到过滤器的自定义方式

增加Spring Cloud Gateway的解析策略，Group为discovery-guide-group，Data Id为discovery-guide-gateway，或者，增加Spring Cloud Gateway的解析策略，Group为discovery-guide-group，Data Id为discovery-guide-zuul，策略内容见下面XML内容，它所表达的功能逻辑：
```xml
1. 当外部调用带有的Http Header中的值a=1同时b=2
   <condition>节点中header="a=1;b=2"对应的version-id="version-route1"，找到下面
   <route>节点中id="version-route1" type="version"的那项，那么路由即为：
   {"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"}

2. 当外部调用带有的Http Header中的值a=1
   <condition>节点中header="a=1"对应的version-id="version-route2"，找到下面
   <route>中id="version-route2" type="version"的那项，那么路由即为：
   {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.1"}

3. 当外部调用带有的Http Header中的值都不命中，找到上面
   <strategy>节点中的全局缺省路由，那么路由即为：
   {"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}

4. 策略解析总共支持5种，可以单独一项使用，也可以多项叠加使用：
   1）version 版本路由
   2）region 区域路由
   3）address 机器地址路由
   4）version-weight 版本权重路由
   5）region-weight 区域权重路由
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <!-- 基于Http Header传递的策略路由，全局缺省路由 -->
    <strategy>
        <version>{"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}</version>
    </strategy>

    <!-- 基于Http Header传递的策略路由，客户定制化控制，跟业务参数绑定。如果不命中，则执行上面的全局缺省路由 -->
    <strategy-customization>
        <conditions>
            <condition id="condition1" header="a=1" version-id="version-route2"/>
            <condition id="condition2" header="a=1;b=2" version-id="version-route1"/>
        </conditions>

        <routes>
            <route id="version-route1" type="version">{"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"}</route>
            <route id="version-route2" type="version">{"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.1"}</route>
        </routes>
    </strategy-customization>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide2-7.jpg)

- 用户覆盖过滤器的自定义方式

继承GatewayStrategyRouteFilter或者ZuulStrategyRouteFilter，覆盖掉如下方法中的一个或者多个，通过@Bean方式覆盖框架内置的过滤类
```java
protected String getRouteVersion();

protected String getRouteRegion();

protected String getRouteAddress();
```

GatewayStrategyRouteFilter示例

在代码里根据不同的Header选择不同的路由路径
```java
// 适用于A/B Testing或者更根据某业务参数决定灰度路由路径。可以结合配置中心分别配置A/B两条路径，可以动态改变并通知
// 当Header中传来的用户为张三，执行一条路由路径；为李四，执行另一条路由路径
public class MyGatewayStrategyRouteFilter extends DefaultGatewayStrategyRouteFilter {
    private static final String DEFAULT_A_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.0\", \"discovery-guide-service-b\":\"1.1\"}";
    private static final String DEFAULT_B_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.1\", \"discovery-guide-service-b\":\"1.0\"}";

    @Value("${a.route.version:" + DEFAULT_A_ROUTE_VERSION + "}")
    private String aRouteVersion;

    @Value("${b.route.version:" + DEFAULT_B_ROUTE_VERSION + "}")
    private String bRouteVersion;

    @Override
    public String getRouteVersion() {
        String user = strategyContextHolder.getHeader("user");

        if (StringUtils.equals(user, "zhangsan")) {
            return aRouteVersion;
        } else if (StringUtils.equals(user, "lisi")) {
            return bRouteVersion;
        }

        return super.getRouteVersion();
    }
}
```
在配置类里@Bean方式进行过滤类创建，覆盖框架内置的过滤类
```java
@Bean
public GatewayStrategyRouteFilter gatewayStrategyRouteFilter() {
    return new MyGatewayStrategyRouteFilter();
}
```

ZuulStrategyRouteFilter示例

在代码里根据不同的Header选择不同的路由路径
```java
// 适用于A/B Testing或者更根据某业务参数决定灰度路由路径。可以结合配置中心分别配置A/B两条路径，可以动态改变并通知
// 当Header中传来的用户为张三，执行一条路由路径；为李四，执行另一条路由路径
public class MyZuulStrategyRouteFilter extends DefaultZuulStrategyRouteFilter {
    private static final String DEFAULT_A_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.0\", \"discovery-guide-service-b\":\"1.1\"}";
    private static final String DEFAULT_B_ROUTE_VERSION = "{\"discovery-guide-service-a\":\"1.1\", \"discovery-guide-service-b\":\"1.0\"}";

    @Value("${a.route.version:" + DEFAULT_A_ROUTE_VERSION + "}")
    private String aRouteVersion;

    @Value("${b.route.version:" + DEFAULT_B_ROUTE_VERSION + "}")
    private String bRouteVersion;

    @Override
    public String getRouteVersion() {
        String user = strategyContextHolder.getHeader("user");

        if (StringUtils.equals(user, "zhangsan")) {
            return aRouteVersion;
        } else if (StringUtils.equals(user, "lisi")) {
            return bRouteVersion;
        }

        return super.getRouteVersion();
    }
}
```
在配置类里@Bean方式进行过滤类创建，覆盖框架内置的过滤类
```java
@Bean
public ZuulStrategyRouteFilter zuulStrategyRouteFilter() {
    return new MyZuulStrategyRouteFilter();
}
```

#### 通过业务参数在策略类中自定义灰度路由策略
通过策略方式自定义灰度路由策略。下面代码既适用于Zuul和Spring Cloud Gateway网关，也适用于Service微服务，同时全链路中网关和服务都必须加该方式
```java
// 实现了组合策略，版本路由策略+区域路由策略+IP和端口路由策略+自定义策略
public class MyDiscoveryEnabledStrategy extends DefaultDiscoveryEnabledStrategy {
    private static final Logger LOG = LoggerFactory.getLogger(MyDiscoveryEnabledStrategy.class);

    @Override
    public boolean apply(Server server) {
        // 对Rest调用传来的Header参数（例如：mobile）做策略
        String mobile = strategyContextHolder.getHeader("mobile");
        String serviceId = pluginAdapter.getServerServiceId(server);
        String version = pluginAdapter.getServerVersion(server);
        String region = pluginAdapter.getServerRegion(server);

        LOG.info("负载均衡用户定制触发：mobile={}, serviceId={}, version={}, region={}", mobile, serviceId, version, region);

        if (StringUtils.isNotEmpty(mobile)) {
            // 手机号以移动138开头，路由到1.0版本的服务上
            if (mobile.startsWith("138") && StringUtils.equals(version, "1.0")) {
                return true;
                // 手机号以联通133开头，路由到2.0版本的服务上
            } else if (mobile.startsWith("133") && StringUtils.equals(version, "1.1")) {
                return true;
            } else {
                // 其它情况，直接拒绝请求
                return false;
            }
        }

        return true;
    }
}
```
在配置类里@Bean方式进行策略类创建
```java
@Bean
public DiscoveryEnabledStrategy discoveryEnabledStrategy() {
    return new MyDiscoveryEnabledStrategy();
}
```

### 配置前端灰度&网关灰度路由组合式策略
当前端（例如：APP）和后端微服务同时存在多个版本时，可以执行“前端灰度&网关灰度路由组合式策略”

例如：前端存在1.0和2.0版本，微服务存在1.0和2.0版本，由于存在版本不兼容的情况（前端1.0版本只能调用微服务的1.0版本，前端2.0版本只能调用微服务的2.0版本），那么前端调用网关时候，可以通过Header传递它的版本号给网关，网关根据前端版本号，去路由对应版本的微服务

该场景可以用“通过业务参数在网关过滤器中自定义灰度路由策略”的方案来解决，如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <strategy-customization>
        <conditions>
            <condition id="condition1" header="app-version=1.0" version-id="version-route1"/>
            <condition id="condition2" header="app-version=2.0" version-id="version-route2"/>
        </conditions>

        <routes>
            <route id="version-route1" type="version">{"discovery-guide-service-a":"1.0", "discovery-guide-service-b":"1.0"}</route>
            <route id="version-route2" type="version">{"discovery-guide-service-a":"1.1", "discovery-guide-service-b":"1.1"}</route>
        </routes>
    </strategy-customization>
</rule>
```

上述配置，模拟出全链路中，两条独立不受干扰的调用路径：

```xml
1. APP v1.0 -> 网关 -> A服务 v1.0 -> B服务 v1.0
2. APP v1.1 -> 网关 -> A服务 v1.1 -> B服务 v1.1
```

## 基于订阅方式的全链路灰度发布规则
在Nacos配置中心，增加全链路灰度发布规则
注意：该功能和网关灰度路由和灰度权重功能会叠加，为了不影响演示效果，请先清除网关灰度路由的策略

### 配置全链路灰度匹配规则

#### 版本匹配灰度规则
增加版本匹配的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务1.0版本只能访问b服务1.0版本，a服务1.1版本只能访问b服务1.1版本：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <version>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-version-value="1.0" provider-version-value="1.0"/>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-version-value="1.1" provider-version-value="1.1"/>
        </version>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide3-1.jpg)

#### 区域匹配灰度规则
增加区域匹配的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现dev区域的a服务只能访问dev区域的b服务，qa区域的a服务只能访问qa区域的b服务：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <region>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-region-value="dev" provider-region-value="dev"/>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-region-value="qa" provider-region-value="qa"/>
        </region>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide3-2.jpg)

### 配置全链路灰度权重规则

#### 全局版本权重灰度规则
增加全局版本权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现版本为1.0的服务提供90%的流量，版本为1.1的服务提供10%的流量：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <weight>
            <version provider-weight-value="1.0=90;1.1=10"/>
        </weight>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide4-1.jpg)

#### 局部版本权重灰度规则
增加局部版本权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务1.0版本提供90%的流量，1.1版本提供10%的流量；b服务1.0版本提供20%的流量，1.1版本提供80%的流量：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <weight>
            <service provider-service-name="discovery-guide-service-a" provider-weight-value="1.0=90;1.1=10" type="version"/>
            <service provider-service-name="discovery-guide-service-b" provider-weight-value="1.0=20;1.1=80" type="version"/>
        </weight>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide4-2.jpg)

#### 全局区域权重灰度规则
增加全局区域权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现区域为dev的服务提供90%的流量，区域为qa的服务提供10%的流量：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <weight>
            <region provider-weight-value="dev=90;qa=10"/>
        </weight>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide4-3.jpg)

#### 局部区域权重灰度规则
增加局部区域权重的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现a服务dev区域提供90%的流量，qa区域提供10%的流量；b服务dev区域提供20%的流量，qa区域提供80%的流量：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <weight>
            <service provider-service-name="discovery-guide-service-a" provider-weight-value="dev=90;qa=10" type="region"/>
            <service provider-service-name="discovery-guide-service-b" provider-weight-value="dev=20;qa=80" type="region"/>
        </weight>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide4-4.jpg)

注意：局部权重优先级高于全局权重，版本权重优先级高于区域权重

请执行Postman操作，请仔细观察服务被随机权重调用到的概率

### 配置全链路灰度权重&灰度版本组合式规则
增加组合式的灰度规则，Group为discovery-guide-group，Data Id为discovery-guide-group（全局发布，两者都是组名），规则内容如下，实现功能：
- a服务1.0版本向网关提供90%的流量，1.1版本向网关提供10%的流量
- a服务1.0版本只能访问b服务1.0版本，1.1版本只能访问b服务1.1版本

该功能的意义是，网关随机权重调用服务，而服务链路按照版本匹配方式调用

```xml
<?xml version="1.0" encoding="UTF-8"?>
<rule>
    <discovery>
        <version>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-version-value="1.0" provider-version-value="1.0"/>
            <service consumer-service-name="discovery-guide-service-a" provider-service-name="discovery-guide-service-b" consumer-version-value="1.1" provider-version-value="1.1"/>
        </version>

        <weight>
            <service consumer-service-name="discovery-guide-gateway" provider-service-name="discovery-guide-service-a" provider-weight-value="1.0=90;1.1=10" type="version"/>
            <service consumer-service-name="discovery-guide-zuul" provider-service-name="discovery-guide-service-a" provider-weight-value="1.0=90;1.1=10" type="version"/>
        </weight>
    </discovery>
</rule>
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide5-1.jpg)

图形化界面验证
- 下载[源码主页](https://github.com/Nepxion/Discovery)的工程，并导入IDE
- 启动源码工程下的discovery-springcloud-example-console/ConsoleApplication
- 启动源码工程下的discovery-console-desktop/ConsoleLauncher
- 通过admin/admin登录，点击“显示服务拓扑”按钮，将呈现如下界面
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide5-2.jpg)
- 在加入上述规则前，选中网关节点，右键点击“执行灰度路由”，在弹出路由界面中，依次加入“discovery-guide-service-a”和“discovery-guide-service-b”，点击“执行路由”按钮，将呈现如下界面
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide5-3.jpg)
- 在加入上述规则后，在路由界面中，再次点击“执行路由”按钮，将呈现如下界面
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide5-4.jpg)

## 全链路服务隔离

元数据中的Group在一定意义上代表着系统ID或者系统逻辑分组，基于Group策略意味着只有同一个系统中的服务才能调用

### 注册服务隔离
基于Group黑/白名单的策略，即当前的服务所在的Group，不在Group的黑名单或者在白名单里，才允许被注册。只需要在网关或者服务端，开启如下配置即可：
```xml
# 启动和关闭注册的服务隔离（基于Group黑/白名单的策略）。缺失则默认为false
spring.application.strategy.register.isolation.enabled=true
```
黑/白名单通过如下方式配置
```xml
spring.application.strategy.register.isolation.group.blacklist=
spring.application.strategy.register.isolation.group.whitelist=
```

### 消费端服务隔离
基于Group是否相同的策略，即消费端拿到的提供端列表，两者的Group必须相同。只需要在网关或者服务端，开启如下配置即可：
```xml
# 启动和关闭消费端的服务隔离（基于Group是否相同的策略）。缺失则默认为false
spring.application.strategy.consumer.isolation.enabled=true
```
通过修改discovery-guide-service-b的Group名为其它名称，执行Postman调用，将发现从discovery-guide-service-a无法拿到discovery-guide-service-b的任何实例。意味着在discovery-guide-service-a消费端进行了隔离

### 提供端服务隔离
基于Group是否相同的策略，即服务端被消费端调用，两者的Group必须相同，否则拒绝调用，异构系统可以通过Header方式传递n-d-service-group值进行匹配。只需要在服务端（不适用网关），开启如下配置即可：
```xml
# 启动和关闭提供端的服务隔离（基于Group是否相同的策略）。缺失则默认为false
spring.application.strategy.provider.isolation.enabled=true

# 灰度路由策略的时候，需要指定对业务RestController类的扫描路径。此项配置作用于RPC方式的调用拦截和消费端的服务隔离两项工作
spring.application.strategy.scan.packages=com.nepxion.discovery.guide.service.feign
```

在Postman调用，执行[http://localhost:4001/invoke/abc](http://localhost:4001/invoke/abc)，去调用discovery-guide-service-b服务，将出现如下异常。意味着在discovery-guide-service-b提供端进行了隔离
```xml
Reject to invoke because of isolation with different service group
```
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide6-1.jpg)
如果加上n-d-service-group=discovery-guide-group的Header，那么两者保持Group相同，则调用通过。这是解决异构系统调用微服务被隔离的一种手段
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide6-2.jpg)

## 全链路服务限流熔断降级权限

通过集成Sentinel，在服务端实现该功能

封装NacosDataSource和ApolloDataSource，支持Nacos和Apollo两个远程配置中心，零代码实现Sentinel功能。更多的远程配置中心，请参照Sentinel官方的DataSource并自行集成
```xml
1. Nacos的Key格式：Group为元数据中配置的[组名]，Data Id为[服务名]-[规则类型]
2. Apollo的Key格式：[组名]-[服务名]-[规则类型]
```

支持远程配置中心和本地规则文件的读取逻辑，即优先读取远程配置，如果不存在或者规则错误，则读取本地规则文件。动态实现远程配置中心对于规则的热刷新

支持如下开关开启该动能，默认是关闭的
```xml
spring.application.strategy.sentinel.enabled=true
```

### 原生Sentinel注解

参照下面代码，为接口方法增加@SentinelResource注解，value为sentinel-resource，blockHandler和fallback是防护其作用后需要执行的方法

```java
@RestController
@ConditionalOnProperty(name = DiscoveryConstant.SPRING_APPLICATION_NAME, havingValue = "discovery-guide-service-b")
public class BFeignImpl extends AbstractFeignImpl implements BFeign {
    private static final Logger LOG = LoggerFactory.getLogger(BFeignImpl.class);

    @Override
    @SentinelResource(value = "sentinel-resource", blockHandler = "handleBlock", fallback = "handleFallback")
    public String invoke(@PathVariable(value = "value") String value) {
        value = doInvoke(value);

        LOG.info("调用路径：{}", value);

        return value;
    }

    public String handleBlock(String value, BlockException e) {
        return value + "-> B server sentinel block, cause=" + e.getClass().getName() + ", rule=" + e.getRule() + ", limitApp=" + e.getRuleLimitApp();
    }

    public String handleFallback(String value) {
        return value + "-> B server sentinel fallback";
    }
}
```

### 原生Sentinel规则

原生Sentinel规则的用法，请参照Sentinel官方文档

#### 流控规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-flow，规则内容如下：
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "grade": 1,
        "count": 1,
        "strategy": 0,
        "refResource": null,
        "controlBehavior": 0,
        "warmUpPeriodSec": 10,
        "maxQueueingTimeMs": 500,
        "clusterMode": false,
        "clusterConfig": null
    }
]
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-1.jpg)

#### 降级规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-degrade，规则内容如下：
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "count": 2,
        "timeWindow": 10,
        "grade": 0,
        "passCount": 0
    }
]
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-2.jpg)

#### 授权规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下：
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "discovery-guide-service-a",
        "strategy": 0
    }
]
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-3.jpg)

#### 系统规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-system，规则内容如下：
```xml
[
    {
        "resource": null,
        "limitApp": null,
        "highestSystemLoad": -1.0,
        "highestCpuUsage": -1.0,
        "qps": 200.0,
        "avgRt": -1,
        "maxThread": -1
    }
]
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-4.jpg)

#### 热点参数流控规则

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-param-flow，规则内容如下：
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "default",
        "grade": 1,
        "paramIdx": 0,
        "count": 1,
        "controlBehavior": 0,
        "maxQueueingTimeMs": 0,
        "burstCount": 0,
        "durationInSec": 1,
        "paramFlowItemList": [],
        "clusterMode": false
    }
]
```
如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-5.jpg)

### 基于灰度路由和Sentinel-LimitApp扩展的防护机制

该方式对于上面5种规则都有效，这里以授权规则展开阐述

授权规则中，limitApp，如果有多个，可以通过“,”分隔。"strategy": 0 表示白名单，"strategy": 1 表示黑名单

#### 基于服务名的防护机制

修改配置项Sentinel Request Origin Key为服务名的Header名称，修改授权规则中limitApp为对应的服务名，可实现基于服务名的防护机制

配置项，该配置项默认为n-d-service-id，可以不配置
```xml
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-id
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示所有discovery-guide-service-a服务允许访问discovery-guide-service-b服务
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "discovery-guide-service-a",
        "strategy": 0
    }
]
```

#### 基于灰度组的防护机制

修改配置项Sentinel Request Origin Key为灰度组的Header名称，修改授权规则中limitApp为对应的组名，可实现基于组名的防护机制

配置项
```xml
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-group
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示隶属my-group组的所有服务都允许访问服务discovery-guide-service-b
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "my-group",
        "strategy": 0
    }
]
```

#### 基于灰度版本的防护机制

修改配置项Sentinel Request Origin Key为灰度版本的Header名称，修改授权规则中limitApp为对应的版本，可实现基于版本的防护机制

配置项
```xml
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-version
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示版本为1.0的所有服务都允许访问服务discovery-guide-service-b
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "1.0",
        "strategy": 0
    }
]
```

#### 基于灰度区域的防护机制

修改配置项Sentinel Request Origin Key为灰度区域的Header名称，修改授权规则中limitApp为对应的区域，可实现基于区域的防护机制

配置项
```xml
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-region
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示区域为dev的所有服务都允许访问服务discovery-guide-service-b
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "dev",
        "strategy": 0
    }
]
```

#### 基于机器地址和端口的防护机制

修改配置项Sentinel Request Origin Key为灰度区域的Header名称，修改授权规则中limitApp为对应的区域值，可实现基于机器地址和端口的防护机制

配置项
```xml
spring.application.strategy.service.sentinel.request.origin.key=n-d-service-address
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示地址和端口为192.168.0.88:8081和192.168.0.88:8082的服务都允许访问服务discovery-guide-service-b
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "192.168.0.88:8081,192.168.0.88:8082",
        "strategy": 0
    }
]
```

#### 自定义业务参数的组合式防护机制

通过适配类实现自定义业务参数的组合式防护机制
```java
// 版本号+用户名，实现组合式熔断
public class MyServiceSentinelRequestOriginAdapter extends AbstractServiceSentinelRequestOriginAdapter {
    @Override
    public String parseOrigin(HttpServletRequest request) {
        String version = request.getHeader(DiscoveryConstant.N_D_SERVICE_VERSION);
        String user = request.getHeader("user");

        return version + "&" + user;
    }
}
```
在配置类里@Bean方式进行适配类创建
```java
@Bean
public ServiceSentinelRequestOriginAdapter ServiceSentinelRequestOriginAdapter() {
    return new MyServiceSentinelRequestOriginAdapter();
}
```

增加服务discovery-guide-service-b的规则，Group为discovery-guide-group，Data Id为discovery-guide-service-b-sentinel-authority，规则内容如下，表示版本为1.0且传入的Http Header的user=zhangsan，同时满足这两个条件下的所有服务都允许访问服务discovery-guide-service-b
```xml
[
    {
        "resource": "sentinel-resource",
        "limitApp": "1.0&zhangsan",
        "strategy": 0
    }
]
```

运行效果

- 当传递的Http Header中user=zhangsan，当全链路调用中，API网关负载均衡discovery-guide-service-a服务到1.0版本后再去调用discovery-guide-service-b服务，最终调用成功

如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-6.jpg)

- 当传递的Http Header中user=lisi，不满足条件，最终调用在discovery-guide-service-b服务端被拒绝掉

如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-7.jpg)

- 当传递的Http Header中user=zhangsan，满足条件之一，当全链路调用中，API网关负载均衡discovery-guide-service-a服务到1.1版本后再去调用discovery-guide-service-b服务，不满足version=1.0的条件，最终调用在discovery-guide-service-b服务端被拒绝掉

如图所示
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/DiscoveryGuide7-8.jpg)

## 全链路灰度调用链

灰度调用链主要包括如下6个参数。使用者可以自行定义要传递的调用链参数，例如：traceId, spanId等；也可以自行定义要传递的业务调用链参数，例如：mobile, user等
```xml
1. n-d-service-group - 服务所属组或者应用
2. n-d-service-type - 服务类型，分为“网关”和“服务”
3. n-d-service-id - 服务ID
4. n-d-service-address - 服务地址，包括Host和Port
5. n-d-service-version - 服务版本
6. n-d-service-region - 服务所属区域
```
灰度调用链输出分为Header方式和日志方式

### Header输出方式

Header方式框架内部集成
- Spring Cloud Gateway网关端自行会传输Header值（参考Discovery源码中的AbstractGatewayStrategyRouteFilter.java）
- Zuul网关端自行会传输Header值（参考Discovery源码中的AbstractZuulStrategyRouteFilter.java）
- 服务端通过Feign和RestTemplate拦截器传输Header值（参考Discovery源码中的FeignStrategyInterceptor.java和RestTemplateStrategyInterceptor.java）

### 日志输出方式
- Spring Cloud Gateway网关

继承GatewayStrategyTracer.java，trace方法里把6个参数（参考父类里debugTraceHeader方法）或者更多通过MDC方式输出到日志
```java
public class MyGatewayStrategyTracer extends DefaultGatewayStrategyTracer {
    @Override
    public void trace(ServerWebExchange exchange) {
        super.trace(exchange);
        
        // 输出到日志
        MDC.put("traceid", "traceid=" + strategyContextHolder.getHeader("traceid"));
        ...

        MDC.put(DiscoveryConstant.N_D_SERVICE_GROUP, "服务组名=" + strategyContextHolder.getHeader(DiscoveryConstant.N_D_SERVICE_GROUP));
        ...
    }

    @Override
    public void release(ServerWebExchange exchange) {
        MDC.clear();
    }
}
```
在配置类里@Bean方式进行调用链类创建，覆盖框架内置的调用链类
```java
@Bean
@ConditionalOnProperty(value = StrategyConstant.SPRING_APPLICATION_STRATEGY_TRACE_ENABLED, matchIfMissing = false)
public GatewayStrategyTracer gatewayStrategyTracer() {
    return new MyGatewayStrategyTracer();
}
```

- Zuul网关

继承ZuulStrategyTracer.java，trace方法里把6个参数（参考父类里debugTraceHeader方法）或者更多通过MDC方式输出到日志
```java
public class MyZuulStrategyTracer extends DefaultZuulStrategyTracer {
    @Override
    public void trace(RequestContext context) {
        super.trace(context);
        
        // 输出到日志
        MDC.put("traceid", "traceid=" + strategyContextHolder.getHeader("traceid"));
        ...

        MDC.put(DiscoveryConstant.N_D_SERVICE_GROUP, "服务组名=" + strategyContextHolder.getHeader(DiscoveryConstant.N_D_SERVICE_GROUP));
        ...
    }

    @Override
    public void release(RequestContext context) {
        MDC.clear();
    }
}
```
在配置类里@Bean方式进行调用链类创建，覆盖框架内置的调用链类
```java
@Bean
@ConditionalOnProperty(value = StrategyConstant.SPRING_APPLICATION_STRATEGY_TRACE_ENABLED, matchIfMissing = false)
public ZuulStrategyTracer zuulStrategyTracer() {
    return new MyZuulStrategyTracer();
}
```

- Service服务

继承ServiceStrategyTracer.java，trace方法里把6个参数（参考父类里debugTraceLocal方法）或者更多通过MDC方式输出到日志
```java
public class MyServiceStrategyTracer extends DefaultServiceStrategyTracer {
    @Override
    public void trace(ServiceStrategyTracerInterceptor interceptor, MethodInvocation invocation) {
        super.trace(interceptor, invocation);
        
        // 输出到日志
        MDC.put("traceid", "traceid=" + strategyContextHolder.getHeader("traceid"));
        ...

        MDC.put(DiscoveryConstant.N_D_SERVICE_GROUP, "服务组名=" + pluginAdapter.getGroup());
        ...
    }

    @Override
    public void release(ServiceStrategyTracerInterceptor interceptor, MethodInvocation invocation) {
        MDC.clear();
    }
}
```
在配置类里@Bean方式进行调用链类创建，覆盖框架内置的调用链类
```java
@Bean
@ConditionalOnProperty(value = StrategyConstant.SPRING_APPLICATION_STRATEGY_TRACE_ENABLED, matchIfMissing = false)
public ServiceStrategyTracer serviceStrategyTracer() {
    return new MyServiceStrategyTracer();
}
```
请参考在IDE控制台打印的结果
![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/Tracer.jpg)

## Docker容器化和Kubernetes平台

### Docker容器化

- 搭建Windows10操作系统或者Linux操作系统下的Docker环境
    - Windows10环境下，具体步骤参考[Docker安装步骤](https://github.com/Nepxion/Thunder/blob/master/thunder-spring-boot-docker-example/README.md)
    - Linux环境请自行研究
- 全自动部署和运行Docker化的服务。在根目录下
    - 一键运行install-docker-gateway.bat或者.sh，把Spring Cloud Gateway网关全自动部署且运行起来
    - 一键运行install-docker-zuul.bat或者.sh，把Zuul网关全自动部署且运行起来
    - 一键运行install-docker-service-xx.bat或者.sh，把微服务全自动部署且运行起来。注意，必须依次运行，即等上一个部署完毕后才能执行下一个

![Alt text](https://github.com/Nepxion/Docs/raw/master/discovery-doc/Docker.jpg)

### Kubernetes平台

请自行研究

## Star走势图

[![Stargazers over time](https://starchart.cc/Nepxion/DiscoveryGuide.svg)](https://starchart.cc/Nepxion/DiscoveryGuide)