# 部署

NeuVector官方提供了<resource src="NeuVector最佳部署实践文档.pdf" type="file"/>，列举了四种 HA 部署模式

<img src="deploy-0.jpg"  width="700" alt="deploy-0"/>

1. 不进行任何调度限制，Kubernetes 可以将 NeuVector 容器放置在任何节点上的部署
2. NeuVector 的 `manager`,`controller`,`scanner`,`enforce` 组件部署在 `master` 节点，`worker` 节点只部署 `enforce`
3. 与方式二类似，但是可以选择节点去充当 `master` 节点，与 2 不同的是被选择节点也可以有**工作负载**
4. NeuVector 的 master 节点不部署 `enforce`，意味着 `master` 节点不在接受**扫描**和**策略下发**，类似于公有云的情况



## 部署组件

- **Controller**： controller 负责管理 enforce 集群，可以部署在 enforce 相同的节点上，也可以部署在单独的 master 节点上，建议运行多个 controller 以实现高可用配置， **controller 通过 RAFT 协议来选举 leader**，因此，controller 的数量应为奇数，例如 3、5、7 等
- **Enforce**：enforce 应部署在由 NeuVector 监控和保护的应用程序容器的每个**主机**/**节点**上，通常以 **Daemonset** 方式部署
- **Manager**：用于显示Web 的控制台，通常**只需要一个**，manager 应部署在 controller 运行的节点上，并提供对 controller  的控制台访问权限
- **Scanner**：scanner 可以在任何地方运行，但通常在运行 controller 的节点上运行
- **Updater**：可选配置，可以在任何地方运行

<img src="deploy-1.png"  width="700" alt="deploy-1"/>
