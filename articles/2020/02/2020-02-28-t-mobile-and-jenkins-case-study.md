---
title: "T-Mobile 和 Jenkins 案例研究"
description: "聊聊 POET Pipeline 对流水线的改变以及给您带来的巨大的价值"
date: 2020-02-28
original: "https://jenkins.io/blog/2020/02/10/t-mobile-case-study/"
tags:
- Jenkins
- T-Mobile
keywords:
- T-Mobile
- Pipeline
- POET Pipeline
author: Alyssa Tong and Ravi Sharma
translator: wenjunzhangp
poster: "t-mobile-and-jenkins.png"
---

![t-mobile-and-jenkins](t-mobile-and-jenkins.png)

## Jenkins 在 T-Mobile 节省数千小时和数百万美元

大多数人都知道 T-Mobile 是无线服务提供商。毕竟，我们拥有国际化的业务，并且是美国第三大移动运营商。但是我们还是一家技术公司，提供的新产品包括 TVision 家庭电视服务，T-Mobile Money 个人银行产品以及 SyncUp Drive 车辆监控和路边辅助设备。

在幕后，T-Mobile 还是开源社区的领导者。我们已经在 GitHub 上共享了 35+ 个代码存储库（包括我们的 POET 流水线框架自动化库），以通过采用健壮和智能的做法来加快 CI/CD 周期，从而帮助其他组织支持内部和外部客户。

我是 T-Mobile 系统可靠性工程（SRE）部门的高级系统可靠性工程师。我们的团队成功地将 POET 实施的第一阶段推广到了 30 多个团队。这是一个巨大的成功，并且计划使用结合在  Kubernetes 集群上运行的 Jenkins 和 CloudBees Core 的稳定、可靠的 CI/CD 流水线，将其扩展到我们的 350 个开发团队和 5,000 个活跃用户。

## 更少的插件，更多的 Master

我们从构建简化的基于容器的流水线基础结构开始，该基础结构可以集中管理并易于适应开发方法。结果使我们的开发团队有更多的精力专注于开发和测试应用程序，而不是维护 Jenkins 环境。

然后，我们将在 master 中使用的 Jenkins 插件的数量从 200 个减少到了 4 个。有超过 1,000 种此类附加组件，包括构建工具，测试实用程序和云集成资源。它们是扩展平台的绝佳方法，但它们也是 Jenkins 的致命弱点，因为它们可能引起冲突。

接下来，我们从一个单一的 Master 给我们所有的 Jenkins slave 提供动力变成了多个 Master，现在拥有 30 个流水线引擎，每个引擎为大约 10 个团队提供动力。此设置减少了 CPU 负载和其他瓶颈，同时允许  T-Mobile 的 DevOps 团队继续享受水平扩展的优势。

## 在两分钟内启动 Jenkins 流水线

这项工作的成果是，我的 SRE 团队现在可以在大约两分钟的时间内从 Docker 镜像启动 Jenkins 主机，对其进行测试并将其推广到我们的生产环境。然后，各个团队可以自定义其 CI/CD 流水线，以满足特定项目的需求。我们允许这些团队扩展平台，但我们将加载项列表限制为 16 个核心插件。这些插件是在 Docker 容器中预先配置的，每个团队都以相同的 CI/CD 流水线开始，然后可以在文件夹级别根据自己的喜好对其进行设置。

这种简化且集中的方式来部署我们的流水线，使 SRE 团队能够将所有事情付诸行动，然后再加以解决。但这只是故事的一半。当我们的开发团队拥有简化的 CI/CD 流水线时，真正的魅力就会展现出来。他们不再需要担心底层的 Jenkins 技术，而可以将注意力转移到采用其解决方案上。

POET 流水线最大程度地减少了对 Jenkins Groovy 代码的需求，该代码繁琐，容易出错并且难以集成到第三方库中。相反，一切都从位于流水线源代码中的流水线定义文件开始，并创建步骤容器以执行构建，部署和其他流水线功能。

我们在 POET 流水线中引入 40 个通用容器，因此我们的开发人员不必从头开始。当然，他们必须知道如何创建 Docker 容器以及如何编写 YAML 文件以扩展流水线功能。通过简化基础架构，减少插件数量并消除对 Groovy 的需求，我们使开发人员可以自由定义自己的流水线，而不必依赖集中的管理团队。

## 我们的开发人员不再是基础架构工程师

为了进一步增强我们的开发人员的能力，我们编写了全面的 POET Pipeline 文档，包括易于理解的帮助文件，教程和视频，以进行自学成才和自助服务。这种宝贵的资源还释放了我们的流水线管理团队和开发人员的精力，使其可以专注于创新。

本文档是我们采用的“以客户为中心”方法的一部分。我们将内部开发团队视为客户，而 POET Pipeline 是我们的产品。您能想象 T-Mobile 要求订户在每次通话时重建智能手机吗？还是让他们在发送短信之前与 CSR 对话？那我们为什么要要求我们的开发商兼任基础设施工程师呢？

## 减少停机时间

除了使开发人员满意并简化管理任务之外，我们简化的 POET Pipeline 框架还大大减少了停机时间。我们的插件繁重的、单主机的 Jenkins 环境占用了 CPU 周期，引起了各种配置难题，并且不断下降。

在任何给定的一周内，我们必须重新启动 Jenkins 两到三次。有时，我们的构建会对我们的环境造成很大的压力，以至于我们不得不在一夜之间重新启动它，并在团队无法工作时重置所有内容。借助 POET Pipeline，我们将停机时间减少到每年一次此类事件。

## 扩大我们的成功

通过消除每个开发团队对流水线专家的需求，由于与 Jenkins 和 CloudBees Core 的合作，我们还节省了大量人工和成本。如果您将一个典型的工作年数定为 2,000 个小时，再乘以 350 个团队，那么您要计算的是数十万个小时和数千万美元。现在，我们可以将这些资源重新定向到构建收益产品中，从而更好地为 T-Mobile 的外部客户提供服务。

这些数字很大，但不要让他们以为 POET 流水线不适合您。我们可能有数百个团队和数千名开发人员，但是 Jenkins 具有可扩展性，任何规模的组织都可以使用我们开发的工具。因此，我们选择与 GitHub 上的开源社区共享流水线。

## 与世界一起创新

创新不是凭空发生的。通过将我们的代码发布给其他人使用和修改，我们正在帮助世界各地的开发人员将重点从管理流水线转移到构建更好的应用程序。反过来，我们将从更广泛的社区的智慧应用于我们的内部项目中受益。

每个人都获得了一定的成果，但真正的赢家是 T-Mobile 的客户。他们可以期待提供新的和改进的产品，因为我们将花费更少的时间来管理流水线框架，而将更多的时间用于简化和改善生活的产品和服务上。