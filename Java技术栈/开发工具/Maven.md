# Maven

maven重要的是各种的配置信息。多了解每个项目的maven是怎么编写的。

maven官网：[https://maven.apache.org/](https://maven.apache.org/)，下载maven的地方。

maven仓库中心：[https://central.sonatype.com/](https://central.sonatype.com/)，每个依赖的的唯一编排。

maven教程：[https://www.runoob.com/maven/maven-tutorial.html](https://www.runoob.com/maven/maven-tutorial.html)，该教程包含maven中的内容如何编写。





**mvn dependency:tree**：显示完整的依赖树，帮助理解项目依赖结构。
**指定某一个依赖**：用 -Dincludes=groupId:artifactId，例如 
-Dincludes=ch.qos.logback:logback-classic

+ -Dverbose：显示冲突细节。
+ -DoutputFile：保存到文件。
+ -Dexcludes：排除特定依赖。

如果你想具体查看某个依赖的路径（例如 logback-classic 的引入来源），直接运行：

```java
mvn dependency:tree -Dincludes=ch.qos.logback:logback-classic
```
