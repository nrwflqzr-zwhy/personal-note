# 第一章 Maven概述

## 第一节 为什么要学习Maven？

### 1、Maven 作为依赖管理工具

#### ①jar 包的规模

随着我们使用越来越多的框架，或者框架封装程度越来越高，项目中使用的jar包也越来越多。项目中，一个模块里面用到上百个jar包是非常正常的。



比如下面的例子，我们只用到 SpringBoot、SpringCloud 框架中的三个功能：

- Nacos 服务注册发现
- Web 框架环境
- 图模板技术 Thymeleaf



最终却导入了 106 个 jar 包：

> org.springframework.security:spring-security-rsa:jar:1.0.9.RELEASE:compile
> com.netflix.ribbon: ribbon:jar:2.3.0:compile
> org.springframework.boot:spring-boot-starter-thymeleaf:jar:2.3.6.RELEASE:compile
> commons-configuration:commons-configuration:jar:1.8:compile
> org.apache.logging.log4j:log4j-api:jar:2.13.3:compile
> org.springframework:spring-beans:jar:5.2.11.RELEASE:compile
> org.springframework.cloud:spring-cloud-starter-netflix-ribbon:jar:2.2.6.RELEASE:compile
> org.apache.tomcat.embed:tomcat-embed-websocket:jar:9.0.39:compile
> com.alibaba.cloud:spring-cloud-alibaba-commons:jar:2.2.6.RELEASE:compile
> org.bouncycastle:bcprov-jdk15on:jar:1.64:compile
> org.springframework.security:spring-security-crypto:jar:5.3.5.RELEASE:compile
> org.apache.httpcomponents:httpasyncclient:jar:4.1.4:compile
> com.google.j2objc:j2objc-annotations:jar:1.3:compile
> com.fasterxml.jackson.core:jackson-databind:jar:2.11.3:compile
> io.reactivex:rxjava:jar:1.3.8:compile
> ch.qos.logback:logback-classic:jar:1.2.3:compile
> org.springframework:spring-web:jar:5.2.11.RELEASE:compile
> io.reactivex:rxnetty-servo:jar:0.4.9:runtime
> org.springframework:spring-core:jar:5.2.11.RELEASE:compile
> io.github.openfeign.form:feign-form-spring:jar:3.8.0:compile
> io.github.openfeign.form:feign-form:jar:3.8.0:compile
> com.netflix.ribbon:ribbon-loadbalancer:jar:2.3.0:compile
> org.apache.httpcomponents:httpcore:jar:4.4.13:compile
> org.thymeleaf.extras:thymeleaf-extras-java8time:jar:3.0.4.RELEASE:compile
> org.slf4j:jul-to-slf4j:jar:1.7.30:compile
> com.atguigu.demo:demo09-base-entity:jar:1.0-SNAPSHOT:compile
> org.yaml:snakeyaml:jar:1.26:compile
> org.springframework.boot:spring-boot-starter-logging:jar:2.3.6.RELEASE:compile
> io.reactivex:rxnetty-contexts:jar:0.4.9:runtime
> org.apache.httpcomponents:httpclient:jar:4.5.13:compile
> io.github.openfeign:feign-core:jar:10.10.1:compile
> org.springframework.boot:spring-boot-starter-aop:jar:2.3.6.RELEASE:compile
> org.hdrhistogram:HdrHistogram:jar:2.1.9:compile
> org.springframework:spring-context:jar:5.2.11.RELEASE:compile
> commons-lang:commons-lang:jar:2.6:compile
> io.prometheus:simpleclient:jar:0.5.0:compile
> ch.qos.logback:logback-core:jar:1.2.3:compile
> org.springframework:spring-webmvc:jar:5.2.11.RELEASE:compile
> com.sun.jersey:jersey-core:jar:1.19.1:runtime
> javax.ws.rs:jsr311-api:jar:1.1.1:runtime
> javax.inject:javax.inject:jar:1:runtime
> org.springframework.cloud:spring-cloud-openfeign-core:jar:2.2.6.RELEASE:compile
> com.netflix.ribbon:ribbon-core:jar:2.3.0:compile
> com.netflix.hystrix:hystrix-core:jar:1.5.18:compile
> com.netflix.ribbon:ribbon-transport:jar:2.3.0:runtime
> org.springframework.boot:spring-boot-starter-json:jar:2.3.6.RELEASE:compile
> org.springframework.cloud:spring-cloud-starter-openfeign:jar:2.2.6.RELEASE:compile
> com.fasterxml.jackson.module:jackson-module-parameter-names:jar:2.11.3:compile
> com.sun.jersey.contribs:jersey-apache-client4:jar:1.19.1:runtime
> io.github.openfeign:feign-hystrix:jar:10.10.1:compile
> io.github.openfeign:feign-slf4j:jar:10.10.1:compile
> com.alibaba.nacos:nacos-client:jar:1.4.2:compile
> org.apache.httpcomponents:httpcore-nio:jar:4.4.13:compile
> com.sun.jersey:jersey-client:jar:1.19.1:runtime
> org.springframework.cloud:spring-cloud-context:jar:2.2.6.RELEASE:compile
> org.glassfish:jakarta.el:jar:3.0.3:compile
> org.apache.logging.log4j:log4j-to-slf4j:jar:2.13.3:compile
> com.fasterxml.jackson.datatype:jackson-datatype-jsr310:jar:2.11.3:compile
> org.springframework.cloud:spring-cloud-commons:jar:2.2.6.RELEASE:compile
> org.aspectj:aspectjweaver:jar:1.9.6:compile
> com.alibaba.cloud:spring-cloud-starter-alibaba-nacos-discovery:jar:2.2.6.RELEASE:compile
> com.google.guava:listenablefuture:jar:9999.0-empty-to-avoid-conflict-with-guava:compile
> com.alibaba.spring:spring-context-support:jar:1.0.10:compile
> jakarta.annotation:jakarta.annotation-api:jar:1.3.5:compile
> org.bouncycastle:bcpkix-jdk15on:jar:1.64:compile
> com.netflix.netflix-commons:netflix-commons-util:jar:0.3.0:runtime
> com.fasterxml.jackson.core:jackson-annotations:jar:2.11.3:compile
> com.google.guava:guava:jar:29.0-jre:compile
> com.google.guava:failureaccess:jar:1.0.1:compile
> org.springframework.boot:spring-boot:jar:2.3.6.RELEASE:compile
> com.fasterxml.jackson.datatype:jackson-datatype-jdk8:jar:2.11.3:compile
> com.atguigu.demo:demo08-base-api:jar:1.0-SNAPSHOT:compile
> org.springframework.cloud:spring-cloud-starter-netflix-archaius:jar:2.2.6.RELEASE:compile
> org.springframework.boot:spring-boot-autoconfigure:jar:2.3.6.RELEASE:compile
> org.slf4j:slf4j-api:jar:1.7.30:compile
> commons-io:commons-io:jar:2.7:compile
> org.springframework.cloud:spring-cloud-starter:jar:2.2.6.RELEASE:compile
> org.apache.tomcat.embed:tomcat-embed-core:jar:9.0.39:compile
> io.reactivex:rxnetty:jar:0.4.9:runtime
> com.fasterxml.jackson.core:jackson-core:jar:2.11.3:compile
> com.google.code.findbugs:jsr305:jar:3.0.2:compile
> com.netflix.archaius:archaius-core:jar:0.7.6:compile
> org.springframework.boot:spring-boot-starter-web:jar:2.3.6.RELEASE:compile
> commons-codec:commons-codec:jar:1.14:compile
> com.netflix.servo:servo-core:jar:0.12.21:runtime
> com.google.errorprone:error_prone_annotations:jar:2.3.4:compile
> org.attoparser:attoparser:jar:2.0.5.RELEASE:compile
> com.atguigu.demo:demo10-base-util:jar:1.0-SNAPSHOT:compile
> org.checkerframework:checker-qual:jar:2.11.1:compile
> org.thymeleaf:thymeleaf-spring5:jar:3.0.11.RELEASE:compile
> commons-fileupload:commons-fileupload:jar:1.4:compile
> com.netflix.ribbon:ribbon-httpclient:jar:2.3.0:compile
> com.netflix.netflix-commons:netflix-statistics:jar:0.1.1:runtime
> org.unbescape:unbescape:jar:1.1.6.RELEASE:compile
> org.springframework:spring-jcl:jar:5.2.11.RELEASE:compile
> com.alibaba.nacos:nacos-common:jar:1.4.2:compile
> commons-collections:commons-collections:jar:3.2.2:runtime
> javax.persistence:persistence-api:jar:1.0:compile
> com.alibaba.nacos:nacos-api:jar:1.4.2:compile
> org.thymeleaf:thymeleaf:jar:3.0.11.RELEASE:compile
> org.springframework:spring-aop:jar:5.2.11.RELEASE:compile
> org.springframework.boot:spring-boot-starter:jar:2.3.6.RELEASE:compile
> org.springframework.boot:spring-boot-starter-tomcat:jar:2.3.6.RELEASE:compile
> org.springframework.cloud:spring-cloud-netflix-ribbon:jar:2.2.6.RELEASE:compile
> org.springframework:spring-expression:jar:5.2.11.RELEASE:compile
> org.springframework.cloud:spring-cloud-netflix-archaius:jar:2.2.6.RELEASE:compile

而如果使用 Maven 来引入这些 jar 包只需要配置三个『**依赖**』：

```xml
    <!-- Nacos 服务注册发现启动器 -->
    <dependency>
        <groupId>com.alibaba.cloud</groupId>
        <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
    </dependency>

    <!-- web启动器依赖 -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- 视图模板技术 thymeleaf -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
```



#### ②jar 包的来源

- 这个jar包所属技术的官网。官网通常是英文界面，网站的结构又不尽相同，甚至找到下载链接还发现需要通过特殊的工具下载。
- 第三方网站提供下载。问题是不规范，在使用过程中会出现各种问题。
	- jar包的名称
	- jar包的版本
	- jar包内的具体细节
- 而使用 Maven 后，依赖对应的 jar 包能够**自动下载**，方便、快捷又规范。

#### ③jar 包之间的依赖关系

框架中使用的 jar 包，不仅数量庞大，而且彼此之间存在错综复杂的依赖关系。依赖关系的复杂程度，已经上升到了完全不能靠人力手动解决的程度。另外，jar 包之间有可能产生冲突。进一步增加了我们在 jar 包使用过程中的难度。

下面是前面例子中 jar 包之间的依赖关系：

![images](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/img006.ab4f2e31.png)

而实际上 jar 包之间的依赖关系是普遍存在的，如果要由程序员手动梳理无疑会增加极高的学习成本，而这些工作又对实现业务功能毫无帮助。

而使用 Maven 则几乎不需要管理这些关系，极个别的地方调整一下即可，极大的减轻了我们的工作量。

### 2、Maven 作为构建管理工具

#### ①你没有注意过的构建

你可以不使用 Maven，但是构建必须要做。当我们使用 IDEA 进行开发时，构建是 IDEA 替我们做的。

#### ②脱离 IDE 环境仍需构建

![images](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/img010.74e515e5.png)

### 3、结论

- **管理规模庞大的 jar 包，需要专门工具。**
- **脱离 IDE 环境执行构建操作，需要专门工具。**



## 第二节 什么是 Maven？

Maven 是 Apache 软件基金会组织维护的一款专门为 Java 项目提供**构建**和**依赖**管理支持的工具。

![./images](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAVQAAABWCAYAAACQLW4KAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAN1wAADdcBQiibeAAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAACAASURBVHic7Z15mBxVuf8/3+pJCAk7CIIsCYGw7/sOoqLyE/G6o6AgXhdcogICGpAdFImIAoKoeBEFAfWqCCgosm8xQFhCgIkg4RKyTsIkM9193t8fp3qmZ9IzXXWqujPw1Od5Oj2ZrnNOdU/XW+95V5kZBQUFBQXZiVb2CRQUFBS8Weho5eSSVgVWyTCFAV02wtRoSasAq2acxsxscR7nU1BQMDJQK2SVpPcB5wHbkl0L7gHuBY43s86s55YFSZOAqcChZLtR1JgNnGRmN+YwV0FBwUomd4Eq6cPADblO6rnWzI5uwbyJkLQ9cAewfs5TzzKzSTnPWVBQsBJohQ31uBbMCfARSaNaNHcSriJ/YQpQbcGcBQUFK4FcBWpsWzwozznrGA1s3aK5h0XSh4C9WzT9sy2at6CgoM3kraHuSXZnzXBs0cK5GyKpAzinhUs83sK5CwoK2kjeAnWfnOcbzCYtnr8RxwJbtXD+QqAWFLxJyFugbpnzfINpq0CVNAb4TouX+VeL5y8oKGgTeQvUHXKebzCbtXj+wXwR2KiF8y8Cnm/h/AUFBW0kN4Ea2xp3ymu+IWjl1nsAklYDTmnxMtNGWtJCQUFBOHlqqNsBY3KcrxFbSlKL16jxFeAtLV7j0RbPX1BQ0EbyFKi75zjXUKxKG+yoktYCTmr1OhQCtaDgTUWeAnW3HOcajnbEop4MrNWGdQqBWlDwJuKNKFC3aeXkkjbAb/dbTeGQKih4k5GLQI1TQlvtkKrRag31W8C4Fq8BhUOqoOBNR14a6nbkU30pCS0TqJI2Az7XqvkHUWz3CwreZORVD7UdDqkardzyn4GvGdAOCoEKLP3xlh+xKsdSlTPH/a5U/tFakzsXrezzKigIIZfyfZIuBz6f/XQSs7aZ5XrRSdoamAGU8px3GLY0s+fatNaIZPlPtzzYqnaHVYmsKlwVrMqrmN6/xonPPriyz6+gIC15bfnbqaFCa4qknE37hGnhkAIwd6AiIpVAJSPqgKiDDRTZbQsvnNjqrLsgen86aZvlV038afdlE3/bdemkw1f2+RSMLDJv+WOHVLu//OOBR/KaTNKuwAfzmi8BbXdISRqLzzSbFD+vg7d7r4lvNePiRw8wP37MA/4NPG1m/5f/WUWTwFAEEuaqJhDAmh2UruZM7c0Z5vJfN4BfTBizvLc0BXES+Lq8kdmHlkyddNzqX3v2561cWtJb8IWH9gLeig/pWwP/t+qKH0uAV4C7gX+ZWaWV59ROJK0O7Ir/7k4ExgLr0v+9XYr/nnYCj5jZCynmvhL4bIOXuoHVgCfxZsb5wIZmVo7H7QfcHp/LRWZ2EuRjQ92e9jmkaozPeb5zia/kNtFy+2l8Eb4POALYBZ8QEfweJS3EV8b6I/CHPMwVZjapL+9NLIs6GGsyTMLJ9ugau8Xxa8CVWdfJSveV4zcUHf8r1e3EBBIYNrX7B9veOnbyU6/ktZ6k9YC31z3SFh1aKule4Gbgf8xsWV7nNhTx920H/I16sFwxvICaDzxnZnMTzLca8EngePz3N/FuWtIc4LfAjxJ8Tx/E34yOwt+sZgB/w9cp3pB+n826+JZOj0mKgEvxwhSgb43MNlRJn6X9X/rLzOyEPCaSdADwzzzmSsHHzOz6vCeVtBHwMeADwL60tqvtNOB84KZQbXv5lVssMlgzFqrzgPUAzEHvEj3cMz9aZ/0xG23NGX9fadpW9xVb7qLI/gi8rT7p2SrgKsJVoFrlG2udOOvirGtJ2hv4Kn63lFd3ivnAT4AfmtmrOc05AEkX4887yfetF9jfzB4eYq6N8TU0jsZr4Vkw4Grgm2a2YLgDJd0OvBM4zMxuj3/3PuB/6w47ysx+3UDm7WFmj0A+F1y7AvrrGZ/jXOflOFdScjNXgL8QJf0ZeAn4PrA/rW8RviteC5ghaf+0g5descX65s0NxOL49dprvUt0f8/8aGdg4tzlcw7O5WwDWHr5lh9QZPcAbxv0Ug+C2iOCA7OsI+kgSfcA9+NviHm2+lkXOA14RtKncpwXAEnvBL5G8u/baPx7HDzPapLOxmuGJ5BdmIL/Cx0PPBmb9YZj5/h5Wt3varLt9/HzDpLWxO9ob8N/Z8vAE7UBeVx07XZIQU4CVdJ78MKnnSwCEtt4hkPSjrEgvR94L60Xoo3YFrhD0vFpBnVEAxsTOqPbDJYv1N0986O9iIWKoffld6rJee2UrU7ofU2T6d/W1XgFGF0znsRPQUWBJG0l6VbgH8B+YWeamLWAX0j6U2xSyItjA8asWf+fWBOcBXyb1nT8eCtwl6Q9G70oaRN8IaTZZjav7qWaQL0Ab7I4AK+wrIZPTx8HPGlmPbUBmS5ASaNpv0MKchCocdWqc7OfSmoezeqQkhRJOhVvi31vPqeVidHAVZK+lHTA0tmjNu2eU7rLlfUigKB7+fzSXb0Lo4HatWzf3M+2CXNPnXSSiR9VlmlrjJpTzDCexF+cAm9DRWAilY1S0ihJ3wIeAw7L89wTcDjwT0mDte5QQhSqXvDOJknnAX/Af66tZDXgRknrNnitJjgHmyF2w5/rdLxzan/gM8APiM1TDNRoM2s0O9C+QPh6xkraMOMcH8Ebu9tNJoeUpHH4Lch55JeYkRffl7RHkgOr2LhqDwe9/p9oo9dfju7tflWPlrs4CEPmwKpgFWG92mn2mRNaXRayj//72tZTrBJ9F3/LW7/yuh73p8s95rVxr5QKiA8SSvw3jbWhe/B9ytrtzK2xDX5XsXaWSeKqbCEhjEdJuhl4FTiV9jmEN6FxB46aQO0zxcXyZUNgeqyBPhW/NBevsdZMCAP+9lkFapbtvhHfqQLZPHRgXAz7rIChhr8QloeuTQb7qaS34reHK2UbnIDReCdAU8wxOhaaHZXXo/0qi0ujXFm4srD4Of551Kj5q+7cfMbszPnytie7qs5yscPJqtCzOOoCuwWxP3UXvmr/CEqq3p9kfkmH4jWahlvPNrMVcHPcqTiUPQkThmviHaetbOg5FJ+NCyDVUxOO9ddmrTbJA/Fzrffbt82si35lbEACSlYNJ4tD6nR8HFdoRsxE4N7AsZ/Gx7Sl5dtmdp6kgwm3vQZpqLEx/C7Czrud7CBpZzObPtxB6lWHM8AEBhbRjYsdVPHD4tdkjKf/i90S/vPf232ZiAtVUt/6RFTdMu5ZMrvjOMHLBmVhFUMViYpBVdD1ltHlpt9DSZ8Afk6+DqesHIy3CSY21Qxir/xOpW2sgvfmX1v3u88C65jZjLrf3YkXqrUEnMuAW82spqmeDJxlZjPrJ88qUEM11NeB7+I9ZH3hMikJ0lDjO/LpAUMfwIcJAYSG8SxIE3RcI7b3/g/5CNPl+K3WAvzfYQzeuL45+W1Bj8LbnYakWparF5pY7Dm3QULVCWDjnM6rIbOP2f7TUYlLvDA1iPqeL3CyrwmNJTJvL40VspoV3IyrOGP2sDsWSV8FptLeWOekfEbSGWY2P2DsSNC0QziIOoFqZnOAOfUHmFkvdR2JzWw5/dt+zOzlRhMHC9RYMG0fOPzO+ISR9A/gQwFzTAxc+4ukr/pvwJfrnEmhrVFC7acnk22bPxf4MT7UY1ot26Oe2AyyHd5r+zmytbNpWsqxWlZVdZqoYPlA7bT2s8BWCFvKjc6Pb3+EIn5qSJj59SLDTFOjDjuWisZihkVCJZ/VVUfZRun8IaYGQNIX8E6MrFTw0SGL8MHzm5DPDXAM/u8dEj74RhWoLfOdZNFQdyR8+3Jj3c/30CaBGmdfnBqw1jW1wN04S2JCwBwQIFAlbQOcGbheGa9VX2hm3cMdGKcqPgZMlvQb4C+Edy1o5EkduF6vqvVC00GH6Bek9cIVY/3A8xiWWR/c8cCSdD0lSvEW368ru74k9rOqNjIzZPKCND5GJa+tYly6wdnPdA41f7zN/3GGU3wZ+AXwV/yNcEnd3MI7TfYFTiTb9vurkqamyaiKS1224u/yKHAfPvtoHv5T3xp/kz6MfPrWhV6/TckiULM4pB6q+znUDhrSAfXrpNculzBQCO/KirGJSQlxSF1EmCayEPiAmd2VdqCZPSDpJOCqgHWB5mFErlfL6wWocxoTec2wsZaaM88esePWEfqDRYwxA5mhSMiYFnVES1zF9pRRJ0hj7bXkz1Elm40bM6TpSNJewM8I2+bPwQvJG8ys2uiAeLc0B6+c3Cjp7cANJLiZNWB9fAD8pSnG5JnQMx9vy73WzF4a6qA41OtbeI06i0N9HUljmykZIWQ5qdAPtIeBge1PUIs/Scc6khLfIeP4s28ErHPBoMIgWQKwU2mocQhSSJypAz4aIkzruAZ/MwlhXrMDrBJ1uzpvPmXWd2UtGuTh9z9XeOnJvXcdH3guK/D8YTutT090i6uwlqsKq8QhWhXmmrNrXYXj4//Xft+XZuoqwirClaPPbfC9x15vNH+c134jYSGFPwO2NrNfDyVMG2FmdwLvwAunENLuEvMSqD8BJpjZ+cMJU/B2SzP7IjAlh3Vb4hzMIlBDNdRpNfspQBzj1dDAm4A0xaZPIX0624vA4BztZilsQzHfzGanHPPNwLWmmtlfA8cCENtZ/xU4fGazA6xs3QOEZlWbubKec2WwXuHih/WK8uLoVVfW75vNmYTp2+0xumdp6QpXYYLFwjF+VK2iU62ic22AkFWfEK09qPCTDS9++vZhlvkl6R1pDjjRzD5Tv7VPQxxZ8YWQscBuktKUr8yaIVkGPmFmn0/7fs3sPHyE0IgjSKBKGoN3YIRwX4PfhaZiJhKo8VYhJDTk1Ni7V0+oQTvVdj+21b4nYJ0X8Z0H8iA0muHxZgdUeqIuV+4Xmq5HE6ysWa53oHZqvXqhvKDjBFfWTo/tsHtm55RVdHm5K9qgX0BSE5LnmNOJVtGq9YLU1QRrLdGgYg+/HlW+OtT8ceGMdwec2olm9v3wd9bHjfiKSWkZh09cSEoWDdUBx5jZdRnmuCbDWPACPXdCNdSdCLe/NhKoocWWk2qoU0hvzJ4O/Lr+F7GQCw1dSrXdNzMH/C7lGg8B7zSzhlvRNMR1bkMD6h9rdoAzW2S9/dt7V9YGrifqdAO3/Mt6FpQWuV5NjDXWfQLPB4BpW+z5ZatyXHV5tJ1VVe7bype51VXZzCpsM3BrDwO3/prX21P60BY/nNXTaP64UlKIULzazKZmeW81YttqaFRBIiEZO6RCbLU1vmtmv8kwHuBWILFJZBALWmE/hXChmEXdb6uGKmkiPv82LWc1yLnPEqoS4pD6Ir424zp4Z9p8GmuN3XjN9G85FhbeJ143LT0k2PJHy6KFDtU7n2SwCBT/X4vLC0svV3u0a52FfQ8GRogk5tGJex4EXCzvnV+zsjSaVhrrdpUxJ+rgD67K5cI7p3zoFN6yX/LnJ6NcKrmPbX7tky8Os8wUYPWUpzab/NuWP9H8kIZsmvC4LNf/c4RHrfRhZgskLSAshLFl3TJCBWqouv/SEJXfQ99gkg6oZ5L+fT5Kf8mutOsNN2cq4hS3X2RYM4hYOz0ncPiTSYR69/+NmgM8VRrnuqNRtjsGhiryP7zWu6i0xCrq24Ka/ydEwPPIxL02EPo10GHmQ56qy9QdjZaTq55YJbqiFhNLnVffTDXv/zKcO3rTXz95x1BrSNqUsMpLZ7VAWwpVUJJ+vlm2++c2MKOFEtqyqGW93EK3/MEOqSF+HypQN5Y0ZD6wpB2AjwfM+/UhKkKFvu/XzGw4zWakMRVfqiyERDeOnZ962LlerVteWNq957WOGZVuPUpZ41xZ/+5Z0NHrytrcYu3V+kKntOTRiXul2iE8svleEXCdwYa1UiYYuIq2d5XoXEd0glVYo35rP2jL/7RVtP/mN864qclSp5Lec9wLZLEjDkVDk0QCkhZLCRWocxlkRstIqPx6qvkhYaTWUGMBlsZ4Xc9QF1voHVX4AP+hjPBnk/5Dv9HMhqrgHypQ3xAto+PiK5fhC1eEksa0MddgAxzbV5aWqIp7DeZjA4sB193ZHL6Yc+IIBoPTZbwdqMlS5ENDZ1a6XVepEpki7lEJqWSRSkTqsCgq2dJKT/SM69EaKvEthuk5Fvc8Ojr52+5jIa1xjhwZOK7VGupN9bVDsxDvokKLUOda4L2ekC3/zoSr2g0Fi5nNk7SYQYVnE7IlDQSqpN2B96ecq5fhQ5VCv0gt+wNmJS66sg++nOEHyV4pPfHNw4xXQDvU/X8f84WGVwxNM17G91dKHFv78OZ7HwB8uyaQ5aUp5msYnEu5dFOlbF6rrLUHBFQCRYZKHEJkyDimyVIfw3vJ07IBcIWk3+E/tyzV18BrmIfik0FCxw+LpPGEO6RuCxzXiE0J11BHlEDNYpAe7mJ7nrAYz6EamIUYvq8YqnhJnESQtgZAjZUuUGMtaiI+7W4i/rPeHV/PMq9UpF5SOEQMDf6stwN+j/HRgccB3hm4Cwmdgg9N2Htt4FdCpVrtUp9VCsA3EecYjFLtrZtR67lqVV+UJbaf3ofZtY1X6SNVt4JBfJbGXTdXBklMFqFKRRkY0gYdwPjAcS8OqsqfKyECNfQDfblJk7DcBGrc7CxthtFSvIlgKFp1I8mFeAs0CS8gN4l/3hqfVrgR4QVd0vB4fdJGAl4YlCM31qCB01LgK5I5EiYbGLpE2CaxMwvFHfYM+wewnowdoT+rVbWIA7zTSgZWUZmIz+381MNDZvJJ2pI3bpGQwSRx1oRe//ea2dLAsY0ILY40lB8nF9qpoTYTKqGet0ZxoSHa6ZVN7lyh7/tVM/tP4Nghib3KB8WPPfHCc2XX2kwZa9vIGamB30kbYEO9A5j60IS9P7Fn5wNDZtfcN2H/94joaGHUHrFzvxvpIrDfxbv/mlGVvv+jem315F2efahZkPxHm7z+RuLfCY4JFah5bvch3I8Tmv2XiFQCVdJYwkOHml1szwTOO0BDjdtCvyvlHIvxbQ2GY6U7pGKzw8fw/coTtRppMylNGxoYr+qF5ySgk0EVgeI6pG8FdjD0DoZIerh7wkGrR0Q/8SLS9f1eXvecgvGdWJuPjQB9ZoB6bdVhnLbr8w8mCZAPdQCNRBYnOCZUoN4TOG4oQjM1R5SGugvhDqlmbyQkXQ5gQ0lrmtniuKRZiEH+bDN7rckxoQI1s/1U0rb4dNIPEv75t4O0GuosfLZL/XvazdADxAK1r6Czf94hfn4vQwhUI7rA4Tbx3Uki6rTU+4RJ2O6xthp32TPqtNXliFsNHhZc3+z8Ja1BeDbZSOTZ4V7M4JDqJX8/wogUqGm9ZFkCeptdbE9Tr1Kk453x8wWkt2c9T5OyZZI2wteeDCFTDylJ1+EdPR9hZAvTHlLeFPfsfKDX0As1keeIcES7OaKHHBFVSvHvBj9H72g0398nHLqzQ5+Pj8ERYf7Ra0SnGzqzX0DXqu570RuHuz6DcRjGhrs9/+DsBG/hYEb23yQtzdoRhV7/03IM5ifuCRVyPc6Nq/O3jLQCNVRLe8XMXhnugLi4bWg86g8l3YavbJ+WkxM4UtrukIrrW07HJyZkbabYDh5r1AmgGY5o+iDhubojmlsnPKnWCcj4mPF3TThkhZhJI5pqRJH1C1IcwqELHPqKIxrXL2jrWpl4wSpgZ4ObSJ4K2rJCxSuBFxIIm9DroFG6eRbyTizKjXYJ1KRC5enA+Tckvd0U4C4zuznBcVluJKnviHF/+7/i4xRbRRWfMXIdcBrenPCjDPMF3Ti8NrqC8FzHES0brJ0OEqwDttp/nfDuDziig12/EI0f0TOOaIYjOqJOY+0zBECftjoddBTo07u/8GDS+rxvFoHqgP9OcFyohpq3QA09j5Y6pCCFDTVuHxJSJR+SX2wty7FtgAMmJzy2bQ4pSUcBPyS/2NBl+HJ6T+CLlszEe3OfbbANu1nS+wmLtw0ybTiih+MtN3XPexs8DBzY4LXa8874zpTcOuHwktAFcVdnRETU3z/lG2BX1JxUru6YOvvqHcL+bcb6e3Y+kKaC0VAx0Ekw/N9iuFDCPKk1Y6xFgiwDXsM7g682s6YVwggXZA81PyQVI1ZDTeOU2oXwrWdSwTIrcP4QbmzW6riOtjikJL0TXwwlizDtwguaO4B/4ouVpBES7WzvgqP0iPmg71F1wnJ/g2tBB/bl38NggdqnvRs6BqJJ9U2onBeU1wt3oKCRk6pe6B4Kbrmw76Q8/aDOu8BLwCeHSXEeccQOqZDiNK81q8QfQKhgb3k8eBqBmsUhlfTOEBo6lRYHnJXkwDjeMzQoPrGQkbQ28CvCY0kX42tx/iC04ntcODzEi7uMwIITB3Xe+fqdE97xYCxEiYXnZgZPNdJOoc/jL4A/TXh/h4im1AvK2MW1VHC5iP46SHjSL3QddVrtpft03pv2wg9pcQLwETN7IHDsymKlRbnUI2lDfKJKWhaY2ZANFfMijUDNEtietMVJuwTqVWb2ZMJj2+WQOpdwwX0v8F9mNjdwfI3QjJ/HstRhdUR/qxeo8fNooGr4thwNBGsUj/24sAn9cQI1orPBpoCNqtNYY8vqCtv+hRE2bDvoHJn9BhSmMHK0wpFyHg1Js4Vvhx1xHuFtN5KyEPh2iuND3/fLQ9R+XYG4CHYSp0AjrgPenoMwBR8GFEKmL6uj9LcG4VF7VImm1Xn2BzxXKUUAhr5Sv4mPj5/piGY7okMbOKmwFR+T9+28e2HAqYeYR/JMv2wnob3U8hZkI0JTHopEAjUurNHy1h9x2E1o6FRSzkhZHKEdN5KvExbP+DxwfMr8+eH4SOC4TF9WR3R/lWjewNCo6CBH6c6BIVUDHq/ePOHDuzqi3Ru8dqJDFw60ltaHUtUewqH/PaDzH78MPPXVAsa0opd9OxgpmuGIrviWVEPdlXBHSdoPNDRjKgkvAFekHNPSP2BcX/bTgWt8No7fzYykXQnPPsn0ZX1355+do/THQcJzW0f0SL2gHBTof5sj+nyDUKjfGdrZiMY3ELSDtdX5RhS6M4CGhVyasr6koM4DK4vYjxBiW2+FQ2pEa6hJbaitzJAazDTgvzKsNxxnpAk+l7Q5YZ5NSP6+307Y1vHfZvb3gHFD0azm51B0Ex4/3Icj+hVwbF2qqYDRoB6LS/bVvfZKt8Y+t4r1fnJQKFSvsO8J+1sDJ1WsPdR6nFgZ7JhDOm/LErb0Ir66V1p2BP6RYd0hkXQosB++5saGDFSEevEmr4XAL1LYckeEVhhnLL41YGjbOmYkFaihd4W5AZWWWhV8O4P07SayOKSSfpkOD5w/t5CbOCQmVFObnjIsqyGO6O+gThuYw3+goXuAQwd5/G9dUFrrPetWFtooyvWC85II+wLY2MHFUSCqc0xZVdhRh3XeckvG054FcTeAdLyLnAWqpHHAlcBRCYccRvLEhJGy3V/pBYqakXTLH5zDGzBm2BTVDJwat2ZOQ5ZmhEmdRAcGrnF/4LhG/AAYsjdXE3LRQt7febOrEl0+yAH1Lkd0e4P00xsqRF9eUlrt9Trb6GtG9GeHPlnvgGrwcA4dc1jnLUHdUweRNI55MJ+SFNogcwXiIi23kVyYQrJSfTVGikNqRGjKw9FUoMZ/rNCMkJAPtBXZUv80sz8FjGvHHTEkpg4GlAkNR9JxpG8VU09uF40jutoRLa8TnhN82miJMh10R2OpEl3/4iobP2uK9l2mVTrqbKPfcugsR6T6wij9NlZhqMfQce/t/FNejfHuDRy3EXBeHicgaUd8JtJ+KYYZwxdTH8wbXUMdOQIV2In2OaSIg9LzTscbrk9UQ+JSgC39IknamOSdJgezfeC4+vXfBfwk4zSPZz2PGh/qvH5Bj8Zc5ogq/bn7pY0d0UtCLIrW6J0zaoOHneNfDpWqitYuq2OeQzOMaI4RHTi4MIr1a6s3O6Jt/1/nH67J63zN7AnCO2ieKOkLoWtLGi1pMr5CVNqU8MvMLFE7kvg7GhKZMJIypEaUQN0lw/yhd6jMTo46bg4MpN6CsKaBkNzUkaol8iA+kcVbLOkYfGWlLFvPCvn+rXittM6PX+nY4N9d0Wr3OKKqI3p3lehWr2na/T0adZGT1nDygnJJNO5lIzrZEV2woic/qlWzOuTIzps+2Du7I802Nymh2q6AyyT9SNJ6iQdJq0g6Hl+7dCo+Rz8Nz5BOwRgR2/1YsIcUC0qTWJSZJAI19AOdl8GzltdFWsFXUgqhHRlSWYK81wKujrsoJEbS5pJ+A1xDWBxlPc/m1Ra4xuRZU1+oKrqlq7Ta/q+MWv+lrmi1NRyl25dEq93VHa16UE2QGhGmiO5ozKuO6K2OaPtYkM41olsc0VlGdLgR7TZ/3bXvvWSLyV96ddIGWYqZDMV1ZEtGOQF4UdINkr4k6RBJm0l6i6RNJW0laXdJn5f0a3xBk6uAzQLWWgQcYWavpxjTTv/JcIx47RSSaSehGmqWO9SwlcNTcKWZzWx+WENa1YywngX4UJbQnPAjgcck/RL4fbwFHUBsutgcn1b6KbyHOa9KVqHb3WFx6GxDnwbGL+4YN36RjbukGnXs5zPwheTLQfsq+9E5L49e79JRVp1l0oKqddwvVafjqESR3oZzP48W2wESX/3qzB/kntpsZp2SLge+nGGaVYEPx49WUQY+amZpCxCFKlR5C9QRbz+FJgJV0iqEN8PK8kZmZxhbowvfNiSUlt+ZzawsaTrZumZugS/0cpak/+CjJLrix3p4G/gaGeYfjlwjMi7c6qQdQe8xRbOBPxo6CsDEgVV0N+gQw2+rnK+PMr3Sob1ktlNVHb7ts2wvEaEInBlS9JqD95347PeaVaPPwneATxAes9xqKsDHzez2gLGFhpqCZlv+7Qm3sWV5I3ls+c8O7b8da3Xt0sz/GLhOIzbGN+87FPgAcACtE6aQs/PwmzO/93gV/cERHVBVdIRTRFURVZWOrEalV5xE34PIVSJ93qHT+mymfa8JQ4tdFP1QEXu1WJhiZgvw6cMjf3QaFwAABZtJREFUkSpwtJndlHZgXNkppNXIwhZUdnpTCNQsDqksb+R5/FY4lOfwRZpD2ZzWO6Rq/DZwnZFA7sWRT5t54TOnzbzgS45ouyp6OHYybeFMz1VVl4svXWZWer+htU1RfU6UmaK/OOm/Db1csY68zBvDYmbXAOe0Y60U9ADHmNlvAsfvHTgu1+QcSZsQFmnwn6QFivKimUANtZ9k6kUfl4LL4pE9JWPBkLal2sY23rsyrLcyaVnDsynPnPeiU7S/k35aVYRJ4x3R4lgL7bZS6XInfaWBdiqH3lNFZ6tDN58y8/xWF9vpw8ym4J19I4HngX3NLEvM7b6B40ZKQH/byyQ2E6g7Bc6bxxsJ3TI8HLK9GUSoTfM/gV0VjwWCikJnJGvKaFcuZ9GA07eZ0uGIji6r4/CKSji0j5OmOTTHEV1TdvqUQ2Oc+uNN48pS0036iquO2eOUGee3s6VOjeMIa2WeJzcAu5pZVjvmPoHj8hZkoYpdntmEiRjSPhrbEXcMnPfOwHH1PEb6xntG8j5Rw7F/4LigZmSxp/hYfMX+LLGpSXkJuBD4Od7meidh7W1ey/Ok6nGK3mb+wjwO+Bnwuqt0HK+Oyu1Iz2F25KrS+mWVx8lF60WuYyHjmHvGI2d0t+qckhCnN58k6Ul80kRoBEcI0/Ap1iHOp0aElOzsJf8dV6hi13aBKrPGGYySIvwFk9ZzuRzY1MwyXWySDiG9YL7YzL6RZd147btJL1QNOMTMgr9MkvYEbgbeFjpHE+bhtadL6hv0SfoZXktOwzLgLSljGlNx6nZnRgbXgb5u8A4jOljYvAufnHLyaducOamq6B0XPjXlslatnxVJ2wIXAO9r8VJP4yMNfmtDXdABSJpH+rJ9vzKzT+Z1DvF5/Ip0dQrAfybb5fl5JGFIrSS+0/4Qb9hOynR84HBmzSUuTXcByYKmF8XHnpR13Zjz8cInKfOBb2YRpgBm9hC+JulZ5GcCqAC34muubmpmFzbodvo1/I4gKd3A5FYKU4Aq0Z6O6IwLnjx9jlP0Ryf9l5O+B3De02c8Gxkt9d5nxcyeMrMj8KmhF5JvmNlC4HJgHzPb1sxuaIHwmELy76EBfwK+mPM5gK9hnMa59DxwbLuFKQyjofYd4JvHDZfyNQZfz/MVfL+cXN9EnF45Hp/VE+EFxBL6BX03vrpT3usKX96s2ZbNgM4cq+bX1l8H+Dheu9kXWD3h0Aq+VOF9+OIdtycJH4vf7+74VsPDsRiYkaaubCgnbn/uGhfN+FYXwNd2OP8omX0H2OviGaeFtCtZ6UgqAe/El/zbF+9sSZo6ugR/03sQuBv4S97fuUZIWgt//Y1lxWvB8DuVBfjc/cUtPI818NE39a2wB58L+F31rHZ8PxvRVKAWrHziC3FL/I1tAj7tFPq/RAvxWvIsvHBfKV+mVvGVHS6MhD0g+KVB1yVPnBLasmREIWkUXnvdFH/DjPB/22V401kXPj15drsKJBdkI7eajAWtIy7g/Ez8eKOGWAXjFH1Y2J2Y/QrpSuBNIVDjG98MWtv2p6CNhHh2Cwraxhd2+r4cmuzQRZc+8c2FVVT64o4XNTNLFBSsFAqBWjCiceiDTvrHjx8/aR6AU/Qnp+i9K/u8CgoaUQjUghHLkdufri7XPblsri9Qfqn1/n6x6z5iZZ5XQcFQFAK1YMTS5bqP7HLd/7z68ZPm13537eOnLpjvlox5+7YntSMBoqAgFYVALRixLHbdk7ts2fcH/35+dclt811X2iy6goKWUwjUghHJNlt95ohu67nn7qemzh/8Wrf1/K7XKsW2v2DEUQjUgpHKZGAF7RTg6ZlXzwdW32arzxRhfwUjikKgFow4ttnqM4cD9z098+oFwxx2J3Bwe86ooCAZhUAtGImcAFzc5JjfEdaorqCgZfx/v2CTW+S1eMcAAAAASUVORK5CYII=)

### 1、构建

Java 项目开发过程中，构建指的是使用**『原材料生产产品』**的过程。

- 原材料

	- Java 源代码

	- 基于 HTML 的 Thymeleaf 文件

	- 图片

	- 配置文件

	- ###### [#](http://heavy_code_industry.gitee.io/code_heavy_industry/pro002-maven/chapter01/verse02.html#)……

- 产品

	- 一个可以在服务器上运行的项目

构建过程包含的主要的环节：

- 清理：删除上一次构建的结果，为下一次构建做好准备
- 编译：Java 源程序编译成 *.class 字节码文件
- 测试：运行提前准备好的测试程序
- 报告：针对刚才测试的结果生成一个全面的信息
- 打包
	- Java工程：jar包
	- Web工程：war包
- 安装：把一个 Maven 工程经过打包操作生成的 jar 包或 war 包存入 Maven 仓库
- 部署
	- 部署 jar 包：把一个 jar 包部署到 Nexus 私服服务器上
	- 部署 war 包：借助相关 Maven 插件（例如 cargo），将 war 包部署到 Tomcat 服务器上

### 2、依赖

如果 A 工程里面用到了 B 工程的类、接口、配置文件等等这样的资源，那么我们就可以说 A 依赖 B。例如：

- junit-4.12 依赖 hamcrest-core-1.3
- thymeleaf-3.0.12.RELEASE 依赖 ognl-3.1.26
	- ognl-3.1.26 依赖 javassist-3.20.0-GA
- thymeleaf-3.0.12.RELEASE 依赖 attoparser-2.0.5.RELEASE
- thymeleaf-3.0.12.RELEASE 依赖 unbescape-1.1.6.RELEASE
- thymeleaf-3.0.12.RELEASE 依赖 slf4j-api-1.7.26



依赖管理中要解决的具体问题：

- jar 包的下载：使用 Maven 之后，jar 包会从规范的远程仓库下载到本地
- jar 包之间的依赖：通过依赖的传递性自动完成
- jar 包之间的冲突：通过对依赖的配置进行调整，让某些jar包不会被导入

### 3、Maven 的工作机制

![./images](https://nrwflqzr.oss-cn-beijing.aliyuncs.com/typora-img/img003.f9cc536c.png)