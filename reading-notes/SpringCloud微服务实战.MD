## 基础知识

### 微服务的优势
1. 服务独立部署，相互之间影响较小。
2. 可以为每个服务性能进行评估，以确定其瓶颈。

### 微服务的劣势
1. 由于服务的拆分，运维和测试将变得更为复杂。
2. 分布式系统带来复杂性(分布式事务、网络不稳定)

## 微服务构建SpringBoot

### SpringBoot的优势
1. 使用大量的自动化配置来简化Spring原有样板化的配置
2. 使用模块化的starter来定义引用，使依赖管理更简单
3. 内置容器，使部署启动更轻便

### SpringBoot文件加载顺序
1. 在命令行中传入的参数
2. 操作系统的环境变量
3. 位于当前应用jar包之外，针对不同profile环境的配置文件内容
4. 位于当前应用jar包之内，针对不同profile环境的配置文件内容
5. 位于当前应用jar包之外的application.properties和yaml配置内容
6. 位于当前应用jar包之内的application.properties和yaml配置内容

### 应用配置类
/autoconfig 用来获取应用的自动化配置报告，列出了每个候选项是否满足自动化配置的各个先决条件，所以它可以帮我们找出一些自动化配置没有生效的具体原因。positiveMatches中返回的是条件匹配成功的自动化配置。negativeMatches中返回的是条件匹配不成功的自动化配置。


## 服务治理Spring Cloud Eureka
### 服务提供者

### 服务消费者


### 服务注册中心

## 客户端负载均衡Spring Cloud Ribbon


## 服务容错保护Spring Cloud Hystrix


## 声明式服务调用Spring Cloud Feign


## API网关服务Spring Cloud Zuul


## 分布式配置中心Spring Cloud Config


## 消息总线Spring Coud Bus


## 消息驱动的微服务Spring Cloud Stream


## 分布式服务跟踪Spring Cloud Sleuth
