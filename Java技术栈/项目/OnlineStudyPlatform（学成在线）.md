# Online Study Platform（学成在线）

垃圾项目，资料给的依赖全问题，文档写的一坨屎。直接整理里面的技术点：

1. gogs（托管的代码平台，简单部署就会了）
2. 跨域问题：这里采用的是统一配置跨域过滤器：

```java
 @Configuration
 public class GlobalCorsConfig {

  /**
   * 允许跨域调用的过滤器
   */
  @Bean
  public CorsFilter corsFilter() {
   CorsConfiguration config = new CorsConfiguration();
   //允许白名单域名进行跨域调用
   config.addAllowedOrigin("*");
   //允许跨越发送cookie
   config.setAllowCredentials(true);
   //放行全部原始头信息
   config.addAllowedHeader("*");
   //允许所有请求方法跨域调用
   config.addAllowedMethod("*");
   UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
   source.registerCorsConfiguration("/**", config);
   return new CorsFilter(source);
  }
 }
```

3. Mysql递归：这里的业务因为层数的不确定性，使用了递归：

```java
WITH [RECURSIVE]
        cte_name [(col_name [, col_name] ...)] AS (subquery)
        [, cte_name [(col_name [, col_name] ...)] AS (subquery)] ...
```

4. 统一异常处理的实现，异常返回相同的响应格式
5. 配置nacos充当注册中心和配置中心
6. 配置gateway
7. 分布式minio上传图片，上传视频（断点续传）
8. ffmpeg视频编码
9. XXL-JOB分布式调度任务
10. FreeMarker
11. 分布式事务技术方案
12. 熔断降级
13. 索引ES
14. SpringSecurity
15. OAuth2
16. 微信扫码登录
17. 支付
18. 部署































> 更新: 2024-12-31 11:31:34  
> 原文: <https://www.yuque.com/u25002409/zhab2g/od3hcwm0k7cptpxo>