---
layout:     post
title:      java类读取properties
subtitle:   通过@value读取properties注意点
date:       2018-10-15
author:     charles
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - 后端
    - JAVA
    - properties
---

# 前言
通过@value读取properties注意点

- applicationContext文件读取文件需要配置成为多文件读取方式

  ```xml
  <bean id="propertyConfigurer" class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
          <property name="locations">
              <list>
                  <!-- jdbc配置 -->
                  <value>classpath:config/jdbc.properties</value>
                  <!-- 通用配置 -->
                  <value>classpath:config/appConfig.properties</value>
              </list>
          </property>
      </bean>

  ```

- 需要将java配置到service.impl中，就是需要spring service层级能够扫描到

  ```java
  @Component("commonConfig")
  public class CommonConfig {

      @Value("${config.isaKey}")
      private String isaKey;

      @Value("${config.doubankey}")
      private String doubanKey;

      @Value("${config.juheKey}")
      private String juheKey;

      @Value("${config.oneUuid}")
      private String oneUuid;

      public String getIsaKey() {
          return isaKey;
      }

      public String getDoubanKey() {
          return doubanKey;
      }

      public String getJuheKey() {
          return juheKey;
      }

      public String getOneUuid() {
          return oneUuid;
      }
  }
  ```