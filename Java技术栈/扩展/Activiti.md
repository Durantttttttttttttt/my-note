
官网地址：[Activiti官方网址](https://www.activiti.org/)

# 基本使用
通常使用Activiti包含的几个步骤：
- 部署Activiti：Activiti包含一堆的Jar包，因此需要把业务系统和Activiti的环境集成在一起进行部署
- 定义流程：使用Activiti的建模工具定义业务流程.bpmn文件
- 部署流程定义：使用Activiti提供的API将流程定义内容存储起来，在Activiti执行过程汇总可以查询定义的内容。Activiti是通过数据库来存储业务流程的。
- 启动流程实例：流程实例也叫ProcessInstance。启动一个流程实例表示开始一次业务流程的运作，例如员工提交请假申请后，就可以开启一个流程实例，从而推动后续的审批等操作
- 用户查询待办任务：因为现在系统的业务流程都交给了Activiti管理，通过Activiti就可以查询当前流程执行到哪个步骤了，当前用户要查询需要办理哪些任务就可以通过Activiti，开发人员不需要自己编写SQL进行查询
- 用户办理任务：用户查询到自己的待办任务后，就可以办理某个业务，如果这个业务办理完成后还需要其他用户办理，Activiti可以帮我们把工作流程继续往后面的流程推动
- 流程结束：当任务办理完成没有下一个任务节点后，这个流程实例完成了

代码示例：[Activiti基本使用示例](./file/activiti-demo.zip)

# BusinessKey
businessKey属于是业务系统的一个扩展，可以在创建流程定义的时候附带上去，然后在任务阶段可以查询出来，关联业务系统

# 流程的挂起和激活
流程的挂起和激活

# 流程变量
流程变量：流程中使用的变量，使用场景：比如一些判断条件控制执行分支等
流程变量分为：
- Global，作用于整个流程实例
- Local，作用域当前执行实例

# 网关
网关：
- 排它网关，通过条件计算走哪个流程
- 并行网关，所有的流程分支都要走
- 包含网关，默认的流程要走，判断的条件成立也要走，全部通过之后才继续往下走
- 事件网关

# 任务分配
任务分配：
- 个人任务管理：分配任务责任人，通过Assignee进行分配
- 组任务分配：给组分配多个责任人，只要任何一个责任人完成了任务，就完成当前任务



# Activiti与Spring整合


# Activiti与SpringBoot整合
参考： [Activiti与SpringBoot整合](https://blog.csdn.net/weixin_49561506/article/details/130791619)

这个更详细：[Activiti与SpringBoot整合](https://www.cnblogs.com/chenyanbin/p/activiti.html#%E6%B7%BB%E5%8A%A0%E5%AE%A1%E6%89%B9%E4%BA%BA%E6%84%8F%E8%A7%81)