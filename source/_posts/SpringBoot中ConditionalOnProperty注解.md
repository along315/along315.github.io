---
title: SpringBoot中ConditionalOnProperty注解
date: 2024/1/8 17:45:25
tags:
    - SpringBoot
---

### 场景
我项目中使用的场景就是接入第三方服务阿里的查询身份证，测试环境不想要它调阿里的接口因为收费，我们就可以使用ConditionalOnProperty。

### 实例
```java
public interface TencentCloudService {
    Boolean verifyIdCard(String idCard, String name);
}

@Service
@ConditionalOnProperty(value = "tencent.enabled", havingValue = "false", matchIfMissing = true)
public class TencentCloudServiceMockImpl implements TencentCloudService {

    @Override
    public Boolean verifyIdCard(String idCard, String name) {
        return true;
    }

}

@Service
@ConditionalOnProperty(value = "tencent.enabled", havingValue = "true")
public class TencentCloudServiceImpl implements TencentCloudService {

    public Boolean verifyIdCard(String idCard, String name) {
        // 调用具体腾讯身份认证接口，查看是否存在
        return true;
    }

}
```

```yaml
# pro.yml腾讯云身份证校验关闭
tencent:
  enabled: true
---
# test.yml腾讯云身份证校验关闭
tencent:
  enabled: false
```

### 关键类
- @ConditionalOnX 注解是 SpringBoot 中的条件化注解的一系列变种，每个注解都针对特定的条件。这些注解用于控制 Bean 是否应该被创建，以及在满足特定条件时才会生效。以下是一些常见的 @ConditionalOnX 注解及其简要说明：
- @ConditionalOnBean： 当容器中存在指定的 Bean 时，条件才成立，可以用于控制 Bean 的创建。
- @ConditionalOnClass： 当类路径中存在指定的类时，条件才成立，可以用于控制 Bean 的创建。
- @ConditionalOnCloudPlatform： 当应用程序部署在指定的云平台时，条件才成立。
- @ConditionalOnExpression： 当给定的 SpEL 表达式的值为 true 时，条件才成立。
- @ConditionalOnJava： 当运行时的 Java 版本匹配指定的版本时，条件才成立。
- @ConditionalOnJndi： 当 JNDI 中存在指定的项时，条件才成立。
- @ConditionalOnMissingBean： 当容器中不存在指定的 Bean 时，条件才成立。
- @ConditionalOnMissingClass： 当类路径中不存在指定的类时，条件才成立。
- @ConditionalOnNotWebApplication： 当应用程序不是 Web 应用时，条件才成立。
- @ConditionalOnProperty： 当指定的属性存在且具有指定的值时，条件才成立。
- @ConditionalOnResource： 当类路径中存在指定的资源时，条件才成立。
- @ConditionalOnSingleCandidate： 当特定类型的 Bean 只有一个候选者时，条件才成立。
- @ConditionalOnWarDeployment： 当部署环境是 WAR 包时，条件才成立。
- @ConditionalOnWebApplication： 当应用程序是 Web 应用时，条件才成立

### 其他
1. nacos中NacosConfigAutoConfiguration就是根据
@ConditionalOnProperty(name = NacosConfigConstants.ENABLED, matchIfMissing = true)
注解来完成了nacos.config.enabled用来是否从nacos中心获取配置

