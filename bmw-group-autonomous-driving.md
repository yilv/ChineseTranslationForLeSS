# 致谢
我们想要向宝马集团致谢，感谢他们给我们机会去学习、成长，并分析一个在高度竞争且挑战的环境中极有吸引力的LeSS巨型案例。我们也想感谢所有参与到这场宝马集团的旅程的LeSS的培训师和教练们。

我们真诚的感谢我们的导师[Mark Bregenzer](https://less.works/profiles/mark-bregenzer)和[Viktor Grgic](https://less.works/profiles/viktor-grgic), 他们从最一开始就陪伴着我们。而且我们要特别的感谢Viktor Grgic，因为他对于经验报告的反馈和改写以及随时随地的讨论。

[Craig Larman](https://less.works/profiles/craig-larman)，感谢你在不停的改写和辅导我们时的无限耐心。[Bas Vodde](https://less.works/profiles/bas-vodde)，感谢你的支持和不停的回答我们的问题，以及一路的支持。

还要非常感谢我们的同事和朋友的支持！
而且，最重要的是，感谢我们的家人，是他们在这段旅程中给了我们无尽的精神上的支持。

对于我们来说这是一场持续的、深入的且变革性的学习经历。

# 介绍
宝马集团决定经历一场重要的变革，为了组织能够交付最高的客户价值、比竞争对手更快的学习速度，以及创建一个容易适应的组织以确保前两个目标的实现。目前依然是在旅程中。

本篇报告是关于在宝马集团自动驾驶部门深入实践探索LeSS导入。它包括了从2016年年中到2019年10月的实践，目前LeSS导入仍旧在进行中。

本报告的作者是[Konstantin Ribel](https://less.works/profiles/konstantin-ribel)和[Michael Mai](https://less.works/profiles/michael-mai)。由于法律原因，涉及到的人并没有使用真实姓名。

报告基于变革的多个角度组织如下：  
1. 时间线角度   
2. 技术角度   
你可以从任何喜欢的角度开始！

# 背景
在宝马集团作为汽车设计师和制造商的旅程中，其致力于通过3级自动驾驶 (AD) 提供更多安全性、舒适性、灵活性和质量（见[图1](#fig001)）。在通往AD的道路上要克服许多挑战，也许最重要的是AD其固有的复杂性。

<a name="fig001"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig001.png" alt="Autonomous Driving Levels">
  <figcaption>Figure 1: Autonomous Driving Levels.</figcaption>
</figure>

为了创造像AD这样复杂和软件密集型的系统，宝马集团必须从一家拥有100年历史的机械工程和制造技术公司转变为一家软件公司，并将AD视为一项复杂的软件研发计划。这听起来像是一场革命和范式转变。的确就是这样！

作为早期的一步，BMW集团召集了所有参与AD的人员，并将他们集中在*一个*地点 - BMW自动驾驶园区。为什么？因为他们预计，如果涉及*多个*地点，成功解决如此困难的问题 - 结合范式转变 - 将更加困难。

然后，宝马集团做了一件出乎意料的事情：他们深入改变了传统的组织设计，转向一种为大团队更容易学习和适应来优化的组织设计。为此，他们从LeSS中获得了灵感。

到目前为止，这个旅程充满了失败和痛苦，但也充满了积极的影响，例如部门之间的协作更加紧密、减少库存和团队之间的交接。对团队自管理的更高关注和频繁的回顾，导致团队设计和拥有他们自己的流程。对技术卓越性的高度重视导致了更好的软件设计、更简洁的代码和更具适应性的技术堆栈。

# 时间线角度
三个代词*我*、*我们*和*他们*在时间线角度中提供了不同的视角。先从作者的个人经历开始 - *我*和*我们*。然后过渡到*他们*，对许多情况呈现外部观点，提供更客观的观察，然后再是根因分析和建议措施。

## 这一切是如何开始的
在2015年成功推出新车后，我（Konstantin Ribel）正在寻找新的挑战。当时，高度自动驾驶项目刚刚开始。我在2016年初加入了这个项目。

我的主要任务之一是创建一个高效的工作模式来开发我们复杂的AD开放平台，该平台涉及宝马集团、合作伙伴和供应商。对于一个标准复杂度的高级驾驶辅助系统（ADAS）的电子控制单元（ECU），我们通常用一个团队对接*一个*供应商来开发它。对于AD开放平台及其多处理器硬件设计，我们估计复杂度要高5-10倍，需要*多个*供应商和合作伙伴。我们进一步发现，如果我们以线性方式扩大规模，仅是用于供应商的项目管理接口，我们可能就需要增加10-15倍的人员（参见[图2](#fig002)）。我意识到必须改变一些东西来改进。

<a name="fig002"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig002.png" alt="ECU schematic">
  <figcaption>Figure 2: ECU schematic.</figcaption>
</figure>

在寻找解决方案时，我阅读了几本Scrum和敏捷开发书籍。然后我被推荐与敏捷教练和LeSS培训师Mark Bregenzer交谈。我遇到了Mark并解释了我们的情况。他的回答是：“你需要的人比你想象的要少得多。你需要改变组织结构。” 会议结束后，Mark建议我参加Craig Larman的[认证LeSS实践者](https://less.works/courses/less-practitioner)（CLP）课程。

我于2016年6月在柏林参加了CLP课程。在CLP课程的第二天，我意识到我在工作中的所有角色都体现了精益浪费 - “没有增加价值但消耗资源的时刻或行动” [[1](#references), p. 58]。谁希望自己的工作是一种浪费？我很沮丧。课程结束后，我意识到我想减少我工作环境中的精益浪费，我确信我的同事也会想要这样。

当我回到办公室时，我试图说服我的line manager的上司（“Paul”）应该在我们的部门采用LeSS。最初，我并没有成功。我们对这在我们的环境中如何永远不会工作存在争议。这对我来说是一次非常令人失望的经历。然而，我记得Craig在CLP课程中经常重复以下说法：“[在引入变革时]像政治家一样思考和行动，而不是像工程师一样。” 我意识到我需要采取不同的行动，并停止强推这个话题。

让我们从不同的角度来看这个故事。

<a name="fig003"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig003.png" alt="The bigger picture">
  <figcaption>Figure 3: The bigger picture.</figcaption>
</figure>

2015年9月至2016年3月期间，我们试图为未来的ADAS系统（包括AD）建立一个组织单元。多个部门的主管齐心协力完成了这项任务。2016年4月1日，来自不同组织单位的多个部门为自动驾驶与ADAS合并组成了新的部门 - ADD（自动驾驶部门）。

在ADD启动后不久，我们发现在现有设置中，除其他问题外，部门、组和角色之间的大量协调开销和交接使我们放慢了速度。 对于具有许多不确定性和未知数的复杂产品（例如AD）来说，这是一个薄弱的起点。为了改善这种情况，ADD执行委员会在2016年6月至2016年12月期间就新的工作模式和组织设置进行了工作。

在此期间，Craig Larman在现场教授我们的开发人员遗留代码的测试驱动开发。我邀请Paul在2016年11月末与Craig会面。他接受了这个提议。Carig和Paul谈了大约20分钟。见过Craig的人都知道他可以多么坦率和尖锐。在他们交谈时，我不知道让他们互相交谈是否是个好主意。除了其它话题，Criag还向Paul介绍了[Larman的组织行为法则](https://www.craiglarman.com/wiki/index.php?title=Larman%27s_Laws_of_Organizational_Behavior)，并与他分享了英语谚语“在自己的土地上，你永远不是先知”。谈话越深入，我就越不确定谈话的结果会如何。当Paul和我离开房间时，Paul说：“这是我经历过的最好的推销。” 成功了！Paul成为高管级别里第一个与我志同道合的人。变革的势头开始上升。

在2017年1月份，一个所谓的迁移团队成立了，而我是其中一员。为了代表整个组织体系，这个团队由不同层次的经理和员工组成。这样的团队使我们可以在不同的抽象层次上讨论想法。我们继续完善ADD执行小组前一年提出的工作模式。我们讨论了不同的用例、日常情况以及如果我们采用这种工作模型它们会是什么样子。我们一直在努力提出改善我们所面临情况的建议。

与此同时，Paul说服ADD高管与Craig Larman一起举办为期4天的研讨会，主题是大规模敏捷开发的系统思维和组织设计，也称为[认证LeSS高管](https://less.works/courses/less-executive.html)（CLE）课程。我们想要确保所有高管的参加，但是由于他们的时间安排，该活动不得不在几个月后举行。为了在那之前能动起来，2017年4月，我与Mark Bregenzer组织了一个为期一天的介绍研讨会。

<a name="fig004"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig004.png" alt="Mark Bregenzer is debriefing a systems thinking exercise">
  <figcaption>Figure 4: Mark Bregenzer is debriefing a systems thinking exercise.</figcaption>
</figure>

<a name="fig005"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig005.png" alt="Executives are learning and exercising systems thinking">
  <figcaption>Figure 5: Executives are learning and exercising systems thinking.</figcaption>
</figure>

Mark介绍的内容激发了参与者的灵感。很明显，我们需要朝着这个方向前进。这个最初的研讨会创造了下一个重要的转变动力。

在这时，ADD高管确信，要真正改变行为和组织的工作模式，他们需要改变组织*结构*。

**开始阶段的复盘总结**   

* 像政治家一样思考和行动，而不是像工程师一样   
* 在不同的组织层级中获得盟友并对齐你们共同的目标 - 真正的改变只有作为一个群体才有可能，既自上而下又自下而上。 LeSS指南：[三个采用原则](https://less.works/less/adoption/three-principles) [[3](#references), p. 55-59]   
* 培训所有高级管理人员和董事，尤其是那些拥有真正决策权的人 [[3](#references), p. 57]   
* “在自己的土地上，你永远不是先知。” 聘请在敏捷开发的大规模组织设计方面经验丰富的外部专家。这位专家 - 一位出色的培训师和一位出色的教练 - 将专注于*为什么*这么做，并将在你的LeSS导入中产生积极影响。有关此主题的更多信息，请参阅《大规模Scrum》[[3](#references), p. 3] 一书中“教授为什么”的部分   
*（LeSS指南：启动）

## 准备阶段
### 认识到组织变革是必要的

> LeSS导入涉及到大型组织和许多根深蒂固的假设组织应该如何工作的想法。成功导入LeSS需要挑战这些假设并简化组织结构，而这一切也都是伴随着在大团队中存在的‘政治’和‘丢脸’。LeSS导入需要每个人都朝着共同的目标前进。[[3](#references), p. 54]

我们的起点是一个常见的层次结构（见[图6](#fig006)）。

<a name="fig006"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig006.png" alt="Typical hierarchy">
  <figcaption>Figure 6: Typical hierarchy.</figcaption>
</figure>

ADD从原先部门继承了超过15个不同角色，这些角色定义了接口用以清晰地描述某人工作的开始和结束。通过这种设置，我们曾经成功地向客户交付了许多优质汽车。然而，它却是精益思维中浪费的沃土，例如交接、协调开销都造成浪费。由于浪费抑制了复杂产品开发 - 尤其是大规模产品开发 - 的适应性，因此我们有强烈的动力去改变。

这一阶段于2017年5月开始，紧跟在与Mark Bregenzer为期一天的介绍研讨会之后。在这一时间点上，针对以下问题的答案都是开放的：

1. 我们想怎么工作？
2. 我们将采用哪种工作模式？
3. 如果它是基于Scrum的，我们会使用哪个规模化框架？

为了回答这些问题，我们需要包括整个组织系统，这就意味着包括来自宝马集团其他部门的所有利益相关者。我们成立了两个团队。现有的迁移团队太大，因此我们将其缩小。第二个团队是高管团队，成员最多为10人，如[图7](#fig007)所示。

通过这种设置，我们让高度参与产品开发的人员和具有深远决策权的经理都参与进来。它使我们能够验证想法并快速做出决定。

<a name="fig007"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig007.png" alt="Teams covering the whole organizational system. Stakeholders and interface partners not shown.">
  <figcaption>Figure 7: Teams covering the whole organizational system. Stakeholders and interface partners not shown.</figcaption>
</figure>

此外还有Mark Bregenzer，他挑战我们对组织结构的假设，并就’为什么’辅导我们。我们全职投入在这项工作上。

团队和Mark在*发散-合并*的周期中工作。迁移团队和高管团队代表探讨了以下问题的答案：我们希望如何工作？在多团队设置中，两个团队就可能的解决方案背后的基本原理进行了辩论。代表们依据解决方案制定了组织设计。然后，整个ADD委员会（C-1和C-2级别）和执行团队评审了两个团队的提案，即“我们想如何工作？”的答案以及对应的组织设计。

两个团队密切合作，以使他们的想法可以快速反馈并且迭代时间较短。

<a name="fig008"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig008.png" alt="Close cross-team collaboration across functions and hierarchies.">
  <figcaption>Figure 8: Close cross-team collaboration across functions and hierarchies.</figcaption>
</figure>

几周后，在两个团队都获得了很多见解之后，组织设计的优化目标变得明显。首先，世界上没有人确切知道如何做可以量产的自动驾驶汽车。因此，学习‘What’以及‘How’变得至关重要。这也就要求组织成为一个*学习型组织*。

其次，更快的反馈循环可以改善学习。由于还没有人制造出（SAE3级及更高级别的）自动驾驶汽车，因此任何成功的希望都必须是从‘现实中学习’、‘调整产品待办列表’并‘处理最高优先级的项目’中得来的。这意味着短周期时间、早期集成和在公共道路上行驶的原型车。换句话说，使用反馈循环来学习，然后决定下一步做什么。因此，始终处理新发现的最关键事项的能力需要一个适应性强的组织。

以上这些发现得出了如下优化目标：

1. 比竞争对手学得更快的能力
2. 基于学习，致力于和交付最高客户价值的能力
3. 易于适应的组织，以确保 (1) 和 (2)

有必要消除浪费以实现优化目标。首先，需要减少协调开销。例如，识别具有经验和专业知识的合适人员来进行聚焦的讨论，尤其是排除中层管理人员，以避免‘个人战术职业游戏’干扰这些讨论（通常会增加开销）。

其次，需要清除交接浪费，尤其是在组件团队、单一职能‘筒仓‘和个人职责之间。指导目标是：增加职能部门之间的共同责任。

我们详尽分析了在我们的领域中使用LeSS是否可以实现所有这些。对于此分析，我们邀请了不属于迁移和高管团队的人员，他们具有不同的角色和用例。我们让这些人挑战LeSS工作模型，并彻底讨论了他们的用例，例如缺陷处理和在安全关键软件和共享公共代码的背景下获得公共道路的驾驶批准。讨论的重点是我们如何用LeSS来实现用例的结果。

我们不停寻找没法实现的用例，但最终我们没有找到。

除了LeSS之外，执行团队还有其它关于如何实现结果的方案。只有*一个*需要对组织*结构*进行更改 - 艰难方式。其它的方案只需要改变*实践* - 简单方式。高管们已经了解到，仅仅改变实践而不重组组织设计的方式并不会改变任何事情。一些高管称这些尝试只是贴了不同标签的“老调重弹”。

相比之下，LeSS 需要对组织结构进行深刻的改变 - 这是一种更难的方式，但更有可能支持我们达到目标。在2017年6月我们决定采用LeSS。

<a name="fig009"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig009.png" alt="Easy vs. hard way. On the right: a climbing wall with an overhang.">
  <figcaption>Figure 9: Easy vs. hard way. On the right: a climbing wall with an overhang.</figcaption>
</figure>

### 产品定义
AD由客户需求和法律要求驱动，新技术和无缝连接正在为实现需求而铺平道路。技术挑战是巨大的，例如建立数据中心、训练AI算法、虚拟测试和验证、从头开始开发新传感器、将非汽车高性能硬件引入汽车并使其符合汽车使用要求，以及复杂的系统架构等等。

<a name="fig010"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig010.png" alt="Technological challenges">
  <figcaption>Figure 10: Technological challenges.</figcaption>
</figure>

#### 在这次LeSS导入中产品是什么？
> 产品定义决定了你的产品待办列表的范围，以及谁会是好的产品负责人。采用LeSS时，产品定义决定了你可以预期的组织变革程度以及需要参与的人员。[[3](#references), p. 157]

客户很可能会认为AD就是一种移动服务，涵盖范围从智能手机应用程序、移动网络、汽车、传感器、算法、执行器、轮胎到道路基础设施。这个清单很长但这只是从技术角度来看的清单。如果从法律的角度来看，则需要处理保险问题、道路清关、法律变更等。为了满足这个产品定义，则需要多方参与，除了宝马集团，还包括各国政府、保险公司、供应商、服务提供商等等。客户的观点可能是正确的，但同时，没法从这样的规模开始导入LeSS。

有一些因素会限制产品的定义：

1. LeSS导入的组织边界；
2. 能够参与进来的各方

这两个因素将产品定义限制在以宝马集团为主的具有自动驾驶功能的汽车上。该产品定义需要与宝马集团内的其他部门以及未采用LeSS的供应商合作。

[图11](#fig011)概述了宝马集团的组织结构。研发的每个部门都有其专门的高级副总裁。ADD高级副总裁支持这次LeSS导入，这也自然限制了LeSS导入在ADD的组织范围内。因此，与ADD之外的其他部门和各方的现有接口和工作模型需要保持不变。

<a name="fig011"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig011.png" alt="Boundaries for the change">
  <figcaption>Figure 11: Boundaries for the change.</figcaption>
</figure>

> 大多数产品开发都是按项目组织的 - 每个新产品发布就是一个新项目。组织通过管理项目来管理产品开发…… [[1](#references), p. 236]

这句话完美地描述了宝马集团的情况。我们以 ACC（[主动巡航控制](https://www.youtube.com/watch?v=rvWCJbYtq7Q)）为例。宝马集团于2000年发布了其第一个版本的ACC。随着每一次发布，ACC获得新的改进可以处理越来越多的交通情况。通过多个版本的产品增强使其成为产品开发案例。

在继续之前有个术语需要定义一下。

**开始生产 (Start of Production - SOP)**：作为一个重要的里程碑，涉及更新或新的汽车模型，其生产将在此版本之后开始。此外，技术栈（硬件和软件）也会被更新。

尽管是长期的产品，但SoP仍以项目来组织。

ADD有两个大项目，SoP2018和SoP2021。为了确保SoP2018的稳定交付，相关人员被排除在LeSS采用之外。他们可以在发布后加入LeSS组织。因此，他们的组织设置基本保持不变。

该决定还将SoP2018产品范围排除在可能的产品定义之外。

因此，LeSS导入的产品定义变成了SoP2021的发布范围，不包括SoP2018。主要是SAE Level 2上的ADAS功能和SAE Level 3上的AD。它涉及传感器、计算硬件和软件的开发。它还需要与没有采用LeSS的ADD以外的部门和供应商合作。

此外，AD应作为单独的自动驾驶平台 (ADP) 提供给其他汽车OEM。

### 从一开始就建立完整的LeSS组织架构
LeSS要求小型的、端到端的、自我管理的团队为实现共同目标而进行协调，同时分担实现该目标的责任。我们的起始位置与预期的位置相去甚远（参见[认识到组织变革是必要的](#the-way-to-the-insight-that-organizational-change-is-necessary)一章）。此外，我们数十年来形成的思维方式支持单一职能团队、英雄主义、组件团队，并且只有一条需要从技术转向管理的职业通道。我们担心如果不改变奖励制度，人们就不会改变。因此，我们面临这样一个问题：“如果人们合作时，他们个人的情况会变得更糟，他们为什么要合作？” [[6](#src006)]。

它使我们认识到我们需要创建一种组织设计，以培养一种文化“……在这种文化中，合作变得对个人有用”[[6](#src006)]。 你可以在[文化跟随结构](https://less.works/less/structure/index.html)指南中找到有关此主题的更多信息。

我们遵循[LeSS规则](https://less.works/less/rules/index.html)“……‘从一开始’就建立完整的LeSS结构”。我们以典型的LeSS巨型组织结构图为指导设计了新的组织结构（参见[图12](#fig012)）。

<a name="fig012"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig012.png" alt="Organizational structure for LeSS Huge">
  <figcaption>Figure 12: Organizational structure for LeSS Huge.</figcaption>
</figure>

迁移团队和高管团队在审视以前的组织结构并应用[系统思维](https://less.works/less/principles/systems-thinking.html)将组织往“学习和适应”的目标转向上都发挥了重要作用。

我们担心，随着时间的推移，任何跨职能和基于团队的组织都会不可避免地回归到单一职能团队的旧范式。根深蒂固的宝马文化和结构与理想的文化和结构截然不同，它曾经（并且仍然）是一股强大的力量，再次证实了我们的担忧。我们决定通过立即对结构进行重大更改来解决这个问题（参见[图13](#fig013)）。我们采用这种方法来对抗回归旧习惯的趋势。以下段落解释了结构的每个部分。

<a name="fig013"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig013.png" alt="New organizational setup">
  <figcaption>Figure 13: New organizational setup.</figcaption>
</figure>

#### 第一步：设立开发部门（多个特性团队和一个管理团队）
首先我们完全去除了一个层级，即Team Leader的角色（C-4级别，参见[图14](#fig014)），结果是留下的Line Manager每个人都要负责大约60名产品开发人员。这随之创造了一些机会来组建跨职能和跨组件的团队。

<a name="fig014"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig014.png" alt="Role of team leaders removed.">
  <figcaption>Figure 14: Role of team leaders removed.</figcaption>
</figure>

如何建立特性团队成员与Line Manager的汇报关系（这在宝马集团是必需的）？我们考虑了两种选项。

##### 选项1：特性团队成员都有同一个Line Manager
一个选项是为每位line manager安排八个团队（一个[需求领域](https://less.works/less/less-huge/requirement-areas)）。

好处？除了局部优化以外我们想不出任何其它的。

缺点？需求领域的概念需要*灵活性*。它们必须*易于*设置和解散。将团队从一个需求区域重新分配到另一个需求区域必须*方便*。选项1会带来一定程度的组织僵化。如果需求领域是一个组织单位，向一位Line Manager报告，那么比如将团队从一个需求领域重新分配到另一个需求领域，或解散需求领域，都将需要正式的组织变更。

当考虑到时间和规模时，此选项的其它缺点：

当接近发布日期时，交付压力会增加。此时，旧的行为模式可能会复活。管理者会肩负起对他团队绩效负责的重担，从而导致指挥-控制的行为模式的复活。在这种情况下，管理者可能会关注团队而不是*团队的系统*。这随之会导致经理干扰团队和他们的Scrum Master所关注的方面。

此外，在之前的设置中，未来的Line Manager是C-3级别的单职能经理（例如架构组经理），C-4级别的Team Leader向他们报告。因此，他们很可能倾向于（1）他们最初的单一职能活动和（2）建立一个非正式的team leader层（即使team leader的*官方*职位被取消）。他们为什么要这样做，为什么这是一个问题？

首先，请注意升职仍将由经理驱动。在宝马集团攀登职业阶梯需要在某些时候展示管理技能。因此，更多地关注经理的专业（例如架构师）的员工可能会获得更多的青睐，甚至得到经理的非正式支持，以让他们在团队中扮演更积极的“领导”角色。这可能会在一个表面上自我管理的团队中创建一个非正式的层次结构，并“……破坏团队的共同责任和凝聚力”。 [[3](#references), p. 63]

##### 选项2：特性团队成员有不同的Line Manager
第二个选项的主要目标是在根据需要更改需求领域时具有高度的灵活性。

我们考虑团队中的开发人员有不同的Line Managers（参见[图13](#fig013)）。通过这种设置，每个Line Manager将有大约60名产品开发人员分布在多个团队中。

好处？组织结构高度灵活，无需更改正式组织结构即可轻松更改需求领域。

此外，这种设置预计会迫使Line Mangers在全球范围内进行优化。怎么做到的呢？此选择使得各个Line Managers对团队的权力趋向*均等*。这可能会降低管理者利用他们对特定“我的团队”的权力在本地进行优化的效果。它将创建一个环境，Line Manager们能以一致的行为面对团队。——“文化遵循结构”模式的积极应用。

缺点？我们没有看到明显的，但的确是有一些悬而未决的问题。以前，组织结构图反映了单一职能组和个性化的职责，这使得为问题找到负责人很容易。由于跨职能团队和分担责任，这些信息在组织结构图中不再可见。保留在传统组织架构中的其他宝马集团部门将如何与ADD进行沟通？

此外，当责任分担并且组织结构与产品架构分离时，如何升级问题以及向谁升级问题？

现有的LeSS指南可以解决这些问题, 例如致力于诸如与相关部门合作之类长期主题的*领头羊团队*[[3](#references), p. 308]。由于ADD之前没有经历过这些做法，很难想象它们会如何工作。

我们选择让这些问题保持开放，并使用检查和调整来回答它们。

这些优势对我们来说非常重要，因此我们决定从这个选项2开始。

#### 第二步 – 创建一个PO团队
谁应该是产品负责人？如[根据开发类型来找到产品负责人](https://less.works/less/framework/product-owner.html#FindaProductOwnerGivenYourTypeofDevelopment)指南中所述 [[3](#references), p. 173]，寻找PO的第一步是了解你的*开发类型*。

一方面，我们的产品（AD）是更大的产品（汽车）的一部分。从这个意义上说，它就像内部组件开发。另一方面，客户需要额外付费以在汽车配置中添加AD功能。

关键点在于，最初由ADD负责人设定的产品愿景是将AD作为单独的自动驾驶平台 (ADP) 提供给其他汽车OEM。 从这方面来看，它本身就是一个外部产品。

对于外部产品，LeSS指南[谁应该是产品负责人？](https://less.works/less/framework/product-owner.html#FindaProductOwnerGivenYourTypeofDevelopment)[[3](#references), p. 173] 建议在产品管理部门寻找PO，例如产品管理负责人。此外，该指南定义：

> 作为PO（产品负责人），你拥有独立的权力来做出重要的业务决策，选择和更改内容、发布日期、优先级、愿景等。当然，PO需要与利益相关者合作，但真正的PO拥有最终决策权。[[3](#references), p. 175, 添加了强调]

有几个因素限制了PO的选择。

宝马集团拥有（并且仍然拥有）范围广泛的产品，包括复杂的系统。其中的开发和维护涉及数万人。该公司的结构反映了汽车的子系统，多年来这些子系统的复杂性和分散性逐渐增加，尤其随着每个子系统中软件的重要性日益增加。

因此，任何人都无法的独立的制定*或改变*重要的商业决策，即使是CEO也不成。相反，所有重要的商业决策都是在委员会中共同做出的。由此，我们知道未来的PO的独立决策权会受到一定的限制。

从ADD中选择PO有两个理由：(1) 向其他汽车OEM提供ADP的愿景；(2) ADD正在采用LeSS，而不是在整个宝马集团范围内采用。

先前存在的部门负责人已经负责所有ADAS和AD*客户产品*；他还掌握了开发它们的预算并有权决定如何使用它。在独立决策权的意义上，他不拥有最终的决策权，但的确拥有很多权力。当然，他需要与利益相关者保持一致，并在做出决策时考虑整个宝马集团的产品系列。因此，这个人成为了PO。APO则是从ADD的不同部分招募的。

不幸的是，正如稍后将探讨的那样，“很多”权限不足以建立一个结构合理且优先排序的产品待办列表。

无论怎样，PO和APO组成了PO团队。

#### 第三步：建立一个能力和教练部门
> 软件是由人创造的。改进人就改进了产品。 [[3](#references), p. 111]

*坚持不懈的*培训和辅导对于在任何方面达到精通以改进产品都是必要的。为了践行这个观点，我们创建了一个能力和教练部门，如[LeSS巨型组织结构](https://less.works/less/less-huge/organizational-structure)指南 [[3](#references), p. 111]所描述的。它由Scrum Master、技术教练和与流程相关的员工（例如行业标准化专家）组成。

为什么Scrum Master在这个部门？Scrum Master的职责是教授Scrum（和LeSS）以及如何利用它获得价值，指导团队、PO/APO、Line Manager以及应用它的整个组织，最后也是同样重要的一点是，作一面*镜子*。这种教练，尤其是在充当镜子时，要求每个人都与Scrum Master处于同一角度去思考。当个人以前的职业道路和等级会影响不同角色和他们层级的看法时，这一点就更加重要了。

宝马集团的典型情况是，工资级别越高，这个人在层级中的地位也越高。Grade通常取决于经验和展示的技能。大多数 Scrum Master的Grade低于APO和line manager。这导致了两个问题：

1. Scrum Master 在指导时将如何看待和接触更高级别的APO和line manager？
2. APO和line manager如何看待“经验不足”（基于他们的Grade）Scrum Master？

让我们也将 IPA（个人绩效评估）添加到教练的角度。一个人的Line Manager进行年度IPA，这会影响到一个人的Grade和薪水。此外，line manager决定他们使用哪些数据进行绩效评估。

考虑以下假设情况。假设几个团队和他们的Scrum Master有相同的line manager。Scrum Master观察到Line Manager的行为助长了自我管理的反模式。Scrum Master会做什么？

1. Scrum Master是会不偏不倚地充当Line Manager的一面镜子，并让这种行为变得透明，冒着伤害自尊和冒着负面IPA的风险。或者？ …
2. Scrum Master会接受这种行为，或者为了自己更好的IPA结果而支持这种行为？

在讨论新的流程和组织结构，尤其是能力和教练部门时，我们推断大多数Scrum Master会有偏见，会选择第二个选项。但我们想创造一个环境，让Scrum Master可以尽可能地无所畏惧和不偏不倚。

此外，考虑到上述情况，宝马集团的员工不习惯在没有事先咨询Line Manager的情况下直接与高层管理人员交谈。因此，高层管理人员从Scrum Master那里获得过滤信息而不是真实情况的风险被认为是有害的。

为了解决这些问题并创造一个让Scrum Master可以尽可能自由地开展工作的环境，我们明确希望Scrum Master拥有与团队成员不同的line manager。这个决定导致我们将Scrum Master安排在能力和教练部门。

#### 结果
最终的组织结构图如[图15](#fig#015)所示。

<a name="fig015"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig015.png" alt="Resulting organizational structure">
  <figcaption>Figure 15: Resulting organizational structure.</figcaption>
</figure>

ADD内有三个主要部门。PO、APO及其支持人员组成了产品负责人部门。所有产品开发人员和line manager都在开发部门。能力和教练部门包含所有Scrum Master、技术教练和其他行业标准化专家。

这三个部门共同输送组成了需求领域：来自PO部门的APO、来自开发部门的团队以及来自能力和教练部门的Scrum Master。

## A New Age—the First Requirement Area—Begins
The first of the [Three Adoption Principles](https://less.works/less/adoption/three-principles) [[3](#references), p. 55]—*Deep and Narrow over Broad and Shallow*—describes that LeSS should preferably be adopted in one product group well, instead of applying LeSS in many groups poorly. In case of LeSS Huge, LeSS adoptions should start with one [Requirement Area](https://less.works/less/less-huge/requirement-areas.html) and reach a good state before further scaling.

Since this is a LeSS Huge case, ADD followed the principle described above, and the LeSS adoption started with one Requirement Area.

[Figure 16](#fig016) gives a visual scheme of the Requirement Areas’ scope as the LeSS adoption grew. The X-axis represents the cross-functionality of the teams. It shows the level of difficulty. The actions on the right are not a composition of the ones on the left. Developing on a rapid prototyping platform and testing in a car is simpler than integrating and testing the same software on the target platform and in a car. Expanding the scope to multiple ECUs increases the complexity and difficulty a team has to face. Including the co-creation of mobility as a service means working on the whole system, which is impractical, at least today.

The Y-axis shows the product scope, which ranges from a single component to a customer problem.

<a name="fig016"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig016.png" alt="Scope of the LeSS organization over time">
  <figcaption>Figure 16: Scope of the LeSS organization over time.</figcaption>
</figure>

The starting point was component-based development on a rapid prototyping platform (step 1 in [Figure 16](#fig016)), far away from the full product scope.

The focus area of the first Requirement Area needed to include the next step towards cross-functional Feature Teams. It was the following:

1.	develop a build system sufficient for scaling and adding further Requirement Areas
2.	simple [Dynamic Cruise Control](https://www.youtube.com/watch?v=1-dNIPy9SxE) (DCC) as it involved only a few SW components

Step 1 in [Figure 16](#fig016).

### Prerequisites and Constraints
Another principle of the [Three Adoption Principles](https://less.works/less/adoption/three-principles) [[3](#references), p. 55] is to use volunteers.

> Use volunteers! True volunteering is a powerful way of engaging people’s minds and hearts. [[3](#references), p. 58]

The intention was to start small with volunteers.

At this point, managers’ education consisted of the 1-day introduction to LeSS, [Craig’s Readings Preparing for LeSS for Executives](http://www.craiglarman.com/wiki/index.php?title=Readings_Preparing_for_LeSS_for_Executives), and coaching by Mark Bregenzer. [Certified LeSS Executive](https://less.works/courses/less-executive) (CLE) courses took place later, together with [Certified LeSS Practitioner](https://less.works/courses/less-practitioner) (CLP) courses of the first Requirement Area’s participants.

Setting up the first Requirement Area was constrained as follows.

1.	The size of the first Requirement Area should have been around 70 people.
2.	The transitioning process to the first Requirement Area had to start at the beginning of August, which meant during the summer school holidays.
3.	Functional managers of existing functional/component teams were required to temporarily live a double role when transitioning into the LeSS organization. Those would be (1) a line manager in a LeSS organization and (2) a functional manager in the previous organization. This setup would ensure that employees not yet joining the LeSS organization remain with their functional manager.

#### Parallel Organization
Constraint #1 and the size of ADD (around 800 people) led us to have a parallel organization as described in the respective guide [[3](#references), p. 74]. Looking at [Figure 16](#fig016) makes it clear that the scope of the build system and simple DCC (step 2) would be in the LeSS organization. Everything else (steps 3, 4, and 5) would need to remain in the former organizational structure to ensure stable delivery and stable interfaces to the outside of ADD and BMW Group. [Figure 17](#fig017) visualizes the notion of LeSS, non-LeSS organization, and people working for SoP 2018.

<a name="fig017"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig017.png" alt="LeSS, non-LeSS organization and the SoP 2018 project">
  <figcaption>Figure 17: LeSS, non-LeSS organization and the SoP 2018 project.</figcaption>
</figure>

The parallel organization and the concept of “only volunteers should join the first Requirement Area” resulted in the third constraint.

#### Fake Volunteers
As mentioned in the section [Product Definition](#product-definition), ADD had two major milestones, SoP 2018 and SoP 2021. The people working on SoP 2018 remained in the former organization to ensure the release; they could not join the LeSS organization. Consequently, nearly all product developers, who delivered a car to series production at least once in their life, were not available for the first Requirement Area. This thinking in projects and, as a repercussion, still organizing people around work restricted the pool of available people with the required skills for successful product development in this context. See [Organize by Customer Value](https://less.works/less/structure/organizing_by_customer_value) [[3](#references), p. 78] for more information on the topic of organizing people around work vs. work around people.

Further, the beginning of August was also the beginning of the summer school holidays in Bavaria, Germany (see constraint #2). At this time, people with families were on their summer holidays, which reduced the pool of available people even further. The resulting pool of possible volunteers consisted mainly of long-term researchers who never developed a car to the production stage, people who freshly joined ADD, and few experienced key players.

The shortage of available people, combined with the demand to start the LeSS adoption with eight teams in the first Requirement Area, led to forcing people to become “volunteers.” The order of actions before the first Requirement Area amplified this effect. First, people from the group of potential volunteers volunteered—in some cases, with a little push. Second, after managers provided a list of “volunteers,” they immediately started with CLP classes to educate people on LeSS and give them an idea of what it means to work in a LeSS organization.

Observations during CLP classes showed that some “volunteers” were poorly informed and had little understanding of what it means to work in a LeSS organization. It was the time when the “volunteers” understood what they volunteered for. Some people did not like what they learned. They did not want to be part of the first Requirement Area and became prisoners of the system.

The guide [Getting Started](https://less.works/less/adoption/getting-started.html) [[3](#references), p. 59], advises the opposite order—step 0: educate everyone *first*, before volunteering. That wasn’t done.

### After the Start—Revisit Parallel Organization
Before the LeSS adoption at the BMW Group, managers were usually involved in deciding what the actual work was and how to do it. Further, they conducted individual performance appraisals (IPA) and other line manager related tasks, for example, escalations with vendors and organizational changes. Let’s define this type of manager as a traditional manager.

In LeSS, a [Product Owner](https://less.works/less/framework/product-owner.html) is responsible for the vision of a product and optimizing its impact by prioritizing the Product Backlog—the *What*. The teams, and *only the teams*, decide the *How* of turning the features or needs into a product. The work of both roles is overlapping intentionally. They should support each other.

The existing paradigm at ADD—having clear lines of responsibility—led to the understanding that the duties or tasks of those roles are mutually exclusive. It became: a Product Owner decides on the What, and teams decide on the How.

Regular Scrum, and LeSS in this regard, don’t define the role of a line manager. What should line managers do?

> ... the role of management changes significantly from managing the work to creating the conditions for teams to thrive ... [[1](#references), p. 241].

In other words, their role is to improve the value-delivery capability of the organizational system.

ADD defined the responsibilities for the LeSS organization precisely this way. The Product Owner department was responsible for the *what*. The line managers’ roles in the Development department was to improve the delivery capability of the organizational system, and the teams decided on the *how*.

Constraint #3 (see [Prerequisites and Constraints](#prerequisites-and-constraints)) specified that a manager transitioning from a traditional manager to a line manager in the new organization would temporarily need to have a double role. The first would be their previous role as a traditional manager. The second would be their new line manager role. This dual role situation would persist as long as the prior group’s subordinates remained in the non-LeSS organization. In other words, a manager who is part of the LeSS organization would still carry out traditional management, deciding on the what and how, in the non-LeSS organization.

The double role setup would violate the distinction of product ownership, line management in LeSS, and traditional management. The concerns about the boundary violation of the roles and organizations led to a rejection of constraint #3. Consequently, the remaining people in the non-LeSS organization became manager free, and no one coordinated the what and the how for them—an unusual situation for those people.

Further, most key players with full system knowledge, if available, transited to the first Requirement Area.

The sum of those circumstances made the rest of the ADD organization strongly dependent on the LeSS organization and they could not deliver without the people in the LeSS organization anymore.

Simultaneously the LeSS organization focused on increasing its delivery capability as a Requirement Area. But, the delivery capability of the entire group working for SoP 2021 decreased, and interfaces to the rest of the BMW Group weakened. Why? Mainly because approximately 250 people in the non-LeSS organization lacked an understandable structure and were lost. Many people stopped doing whatever they were responsible for.

Further, some people of the LeSS organization focused so much on the Requirement Area that they dropped communication and interfaces to the rest of the organization. The pressure for finding a solution increased rapidly, and the lead coach (the first LeSS coach and trainer in this LeSS adoption) became heavily involved in helping to find one. Additional LeSS coaches were engaged in continuing coaching of the first Requirement Area.

The people of the non-LeSS organization needed to work with their colleagues from the LeSS organization. Usually, because someone needed help on topic X, and the topic X expert was in the first Requirement Area. But both groups had significantly different ways of working. “We want to do X in our cross-functional team” vs. “we want to split X across several single-function teams.” Explanations of why the people in the LeSS organization wanted to approach and solve things in different ways led to heated discussions and a higher tension between both groups. Both groups did not speak the same language any longer.

Based on this insight, the CLP classes took place independently of the actual transition into the LeSS organization. The entire ADD received CLP classes within one year. However, by the time the people transitioned into a LeSS organization, their knowledge from CLP classes faded, which created further difficulties in the new Requirement Areas.

## Adding More Requirement Areas
Activities such as getting the LeSS organization up and running, creating a solution for the people in the non-LeSS organization, clarifying which legacy code should be part of future development, and many other issues absorbed lots of time and energy. Therefore, progress was rather slow.

There was eagerness for expanding the LeSS organization and starting a second Requirement Area. A few factors motivated it. First, there was a strong desire to become better. It seemed that transitioning people from the almost structureless non-LeSS organization to the LeSS organization would resolve some issues and soothe the pain. Second, the majority of people from the non-LeSS organization who participated in a CLP course were self-motivated to join the LeSS organization as fast as possible. Third, the ADD needed to demonstrate features to their stakeholders and the press. Thus, it was natural that the Senior VP of ADD wanted to see and experience feature increments in the car.

It is worth noting that it is necessary to fulfil some conditions to keep a LeSS organization healthy, especially when adding teams. Those are:

1. A common structure for the Product Backlog of all teams and Requirement Areas
2. A working build system which ensures fast feedback

At this stage, the Product Backlog of the first Requirement Area started mutating to a multi-level, tree-like requirements set, introducing dependencies between items, which obscured the overview of work to be done, the direction to go, and burdened prioritization already for only one Requirement Area. The Product Backlog started to deviate from the most Product Backlog related guides, especially from *Don’t “Manage Dependencies” but Minimize Constraints* [[3](#references), p. 198] and *Three Levels Max* [[3](#references), p. 222].

Before the LeSS adoption two “project groups” had created prototype code for some aspects of autonomous driving; the two sets of experimental code contained lots of duplication and inconsistencies across them. To “speed” things up (another *quick fix*), the entire legacy code from these two bases was merged to the new master branch, with little automated testing, leaving the feature and code coverage at an insufficient level (for more details see [Merging Repositories](#merging-repositories)). Consequently, shared code ownership became significantly more difficult. The build system and infrastructure were not ready for this structure and load. The whole system became slow, and feedback times increased significantly. As a consequence, trunk-based development with fast feedback cycles became impossible (more on this topic in the [Technology View](#technology-view) chapter).

The second Requirement Area kicked off with a broken backlog and build system. And the scope for the LeSS organization expanded to *all* software components and sensors, yet still being developed on only the rapid prototyping platform (step 3 in [Figure 16](#fig016)).

To expand from one Requirement Area to many while sustaining transparency about item priorities in the Product Backlog, it must have a common structure for all Requirement Areas. It enables the PO to better grasp what’s going on, and to prioritize and change teams between Requirement Areas—a quality of *organizational adaptiveness*. But, the tool, which was used as an electronic Product Backlog, and the people using it, created obstacles. Combined with the obscure multi-level, tree-like requirements set in the Product Backlog, its structures between Requirement Areas (existing and planned) began to diverge at about this time—a *local optimization*. See also *Guide: Tools for Large Product Backlogs* [[3](#references), p. 210].

Unfortunately, even with these clear weaknesses in place, adding new Requirement Areas continued for the next few months (see [Figure 18](#fig018)).

<a name="fig018"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig018.png" alt="Requirement Area ramp up over time">
  <figcaption>Figure 18: Requirement Area ramp up over time.</figcaption>
</figure>

With each step, the scope of the LeSS organization expanded. Adding four Requirement Areas expanded the scope to step 4 represented in [Figure 16](#fig016). With all nine Requirement Areas, the scope reached its maximum, the entire context of ADD (step 5 in [Figure 16](#fig016)), yet myriad weaknesses underlay this too-rapid expansion.

Numerous experiments were necessary to find a meaningful scope for each Requirement Area. It took several restructurings, inspect & adapt cycles. During those restructurings, the flexibility of a LeSS structured organization became visible. Since Requirement Areas were *not* part of an organizational chart or unit, the restructuring process was quick. The fastest restructuring of Requirement Areas (inception until complete implementation), happened within one week.

That was the good news: an adaptive organization. But the bad news was that a key driver for this frequent restructuring was expanding too fast.

Although a LeSS Huge organizational structure allows such flexibility, it is intended to accommodate changing priorities in the customer-centric view, and it comes with some *switching costs*. Due to interrupting evolved inter-team relationships and established collaboration within one Requirement Area, and the non-trivial domain learning required for teams moving to a new area, *frequent* restructuring of Requirement Areas has issues.

## Retrospective On The Timeline View
> Adjusting organizational structure is relatively easy, but changing mindset takes time, discussion, introspection, and learning. [[1](#references), p. 229]

The BMW Group’s LeSS adoption can be visualized with the help of the Satir change model. [Figure 19](#fig019) shows the journey to the current state and how it could look like in the future.

<a name="fig019"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig019.png" alt="Journey of BMW Group’s LeSS adoption. Based on the Satir change model.">
  <figcaption>Figure 19: Journey of BMW Group’s LeSS adoption. Based on the <a href="https://stevenmsmith.com/ar-satir-change-model/">Satir change model</a>.</figcaption>
</figure>

The journey consists of 5 phases. This retrospective view elaborates on the Chaos phase only.

After introducing LeSS, ADD entered this phase quickly! Cognitive biases and the system all humans are in influence our mental models and, therefore, our behavior. Craft mistakes and active sabotage were its effects, leading to the situations described in this report.

The question is: Could the magnitude of the chaos have been minimized or even avoided?

Probably, it could have! And so perhaps you the reader can benefit from some lessons learned. This retrospective view, covering two years after the original steps towards LeSS, exposes causes of the painful dynamics and proposes ways to prevent or minimize them.

**The Product Development System**
Let’s elaborate on what the product development system is, using Jay Galbraith’s organizational design framework—the Star Model™ (see [Figure 20](#fig020)).

<a name="fig020"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig020.png" alt="Jay Galbraith’s organizational design framework, called the Star Model. This version is from 1998.">
  <figcaption>Figure 20: Jay Galbraith’s organizational design framework, called the Star Model. This version is from 1998.</figcaption>
</figure>

Craig Larman and Bas Vodde observed in their book *Scaling Lean & Agile Development* that a Scrum or LeSS adoption directly alters the *processes* and *structural* elements. In ADD’s case, precisely those elements were focused on when preparing for the LeSS adoption.

Structure and processes are only *two* parts of an organization’s design, and often too many efforts are spent on just them and too little on the other elements.

> Structure is usually overemphasized because it affects status and power... [14, p. 4]

The Star Model elements are highly interwoven and have influential forces on one another, which *together* influence the behavior, culture, and performance of the organization. Therefore, alignment between *all elements is crucial* for an organization to be effective. Otherwise, the organizational capability *decreases*. Galbraith put it this way:

> For an organization to be effective, *all the policies* (elements in the Star Model™) must be aligned and interacting harmoniously with one another. [14, p. 5, explanation in parenthesis added, emphasis added]

This retrospective analysis is structured using the Star Model elements.

### Strategy & Task
> Effective team self-management is impossible unless someone in authority sets the direction for the team’s work. [12, p. 62]

Despite a LeSS introduction and decision to manage *product* development as product development, the reality felt like *project* development.

The BMW Group had (and still has) a Product Management department, which accommodates people who plan and manage the entire life-cycle, from idea to development to maintenance, of all vehicles that the BMW Group offers. This department sets up *modular systems contracts* with other departments that develop car parts. Such a contract usually covers a set of different vehicles, their release dates, general scope, budget, and aims at high reuse of the components/systems the departments develop.

Before the LeSS adoption, such a modular system contract (an actual document) was signed between the ADD and Product Management departments.

The traditional automotive industry still does long-delayed integration rather than frequent. Therefore, there was (and still is) a BMW Group-wide general car project timeline, which defined fixed integration steps and other milestones across all involved departments on the way to the start of production so that they can synchronize their work on a slow cycle.

[Figure 21](#fig021) illustrates the setup between the modular system contract, the general car project timeline, and ADD.

<a name="fig021"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig021.png" alt="ADD-external constraints which should influence the Product Backlog.">
  <figcaption>Figure 21: ADD-external constraints which should influence the Product Backlog.</figcaption>
</figure>

Over decades managers conveyed the message that “we need to deliver *everything* and on time,” meaning the contract’s scope, by the release date agreed upon. The message turned into a mantra, spread and believed in by many people, not just managers. Consequently, the desire to deliver everything was high, and the message continued to spread. Further, this ethos arose in the context of creating *electro-mechanical components* such as a braking system; which are *infinitely* less complex, less variable, and less research-oriented than the profoundly hard job of creating AD software.

Interestingly, the people conveying this message ignored the evidence that, at least in the last decade, the product group *never* delivered “everything” on one given deadline. There usually was an intensive work mode (like a task force), where someone deprioritized less important topics to focus on the mission-critical ones.

Further, the scope described in the modular system contract was, to a degree, negotiable. What was that degree? All the features a customer could experience in the latest car model must also be available in a new model. Therefore, the scope of existing features was a must-have. However, the content of new features was negotiable.

Despite the evidence, those circumstances diminished the acceptance of reducing-the-scope discussions (at least at an early stage), leading to no prioritization because “everything was crucial.” The resulting behavior was “we need everything.” Wishful thinking! Of course, if everything is equally important, everything is equally unimportant. Only one year before the release, deprioritization started—meaning re-negotiations of the scope and date. Such late re-negotiations were—and still are—common and in line with other BMW Group projects; therefore, they were expected.

Another aspect led to an unprioritized so-called “Product Backlog” (so-called since, per definition, a real Product Backlog would be prioritized, providing a clear direction). Most not-really-APOs “APOs” were project managers who had also previously been developers.

The first Requirement Area started with such “APOs” acting as a fake PO because it was only one Requirement Area, and the person who later became the PO was not fully available. Sometime after starting the first Requirement Area, both “APOs” rejected coaching, especially on setting up a real Product Backlog. Why?

To start with, the learnings emerging during the initial coaching sessions were undoubtedly uncomfortable. For example, accepting that the idea of *managing the product complexity* by splitting it into small parts is an illusion and that instead, empirical control, learning from product experience feedback, and prioritization are a better approach.

And some “APOs” in high power positions refused LeSS coaching from people they saw under their status level—basically all coaches we engaged.

The resulting lack of PO/APO and Product Backlog competence led to a “Product Backlog” full of technical tasks on multiple abstraction layers and many dependencies between them, which was the main impediment for the PO to prioritize the Backlog.

**Key point**: Most “APOs” could not keep the whole product focus and derive valuable items for the next Sprints. Instead, they tried to split everything into small parts—a decades-of-practice habit and a fear response of forgetting something.

Those circumstances were very convenient for the teams because technical tasks narrowed their focus to just one or two components but didn’t motivate them to learn the customer language, nor to learn across a broader set of components and skills to increase their learning and *adaptiveness*. In consequence, the so-called “Product Backlog” consisted mainly of technical tasks instead of customer-centric items. The result was two other anti-patterns. (1) Re-prioritization on the product level became difficult—in fact, close to impossible—because technical tasks naturally depended more on each other. And (2) collaboration and coordination opportunities between teams when finding technical solutions for customer-centric problems were hard to find. Why? Because technical tasks typically reflect only a small part of the whole system, for example, one component, but customer-centric items usually span multiple system elements.

Both anti-patterns led to overloaded so-called “APOs.” Some of them acted as single-team “POs,” prioritizing specific team backlogs in their Requirement Area, which reinforced and amplified the downward spiral from a product-requirement to technical-task perspective.

The result? Lack of whole-product focus and prioritization, leading to high busyness and *output* of completed technical tasks, but very low output of completed customer features, and thus no useful *outcome*. This typhoon of technical tasks made it impossible for the PO to have a meaningful whole-product overview, to order the so-called “Product Backlog,” which disempowered him and made him dependent on the technically involved “APOs”—he had to believe what the “APOs” told him.

Why didn’t the PO clean up this mess? Why didn’t he enforce a real Product Backlog enabling him to order it? One cause is the lack of time for the job as PO. The person playing the PO role had many other duties; for example, VP of a department, project manager of a project external but adjacent to ADD, and most importantly, he was occupied with the SoP 2018 release. And there are very likely other reasons that remain invisible to us.

It begs the questions of why a “free” PO was not chosen and why we thought an overburdened person could effectively learn and do a complicated new approach?

No-one, at least to my knowledge (Konstantin here), questioned whether or not this person should become PO. He was considered a perfect fit for the PO role by people on all hierarchy levels. Why? Because before the LeSS adoption, he was the VP of the customer offerings department and re-prioritization was in his job’s nature.

Having time to live out the PO role was not considered an issue because he could have delegated other activities to his staff and free himself up.

Therefore, the better questions are: Why did he become overburdened, and why didn’t he receive PO coaching?

To start with, the PO lapsed into a traditional management paradigm. He delegated most of the PO tasks and trusted that his staff would execute them properly.

Further, he knew about the problem of technical tasks “Product Backlog.” But, he decided to support his so-called “APOs” mainly because the “APOs” saw the lead coach as someone who never delivered a car to production, which degraded the coach in the “APO’s” and PO’s eyes. Therefore, the PO trusted his “APOs” more.

> ... the failure to establish a compelling direction runs two significant risks: that team members will pursue whatever purposes they *personally prefer*, but *without any common focus*; or that they gradually will fade into the woodwork ... [12, p. 80, emphasis added]

How could this situation be resolved?

> The key is to identify who has the legitimate authority for direction setting and then to make sure that that person or group exercises it *competently*, *convincingly*, and *without apology*. Team performance greatly depends on how well this is done. [12, p. 63, emphasis added]

A better approach would have been to free up the PO of other duties, which have little to do with product ownership. Further, replace the so-called APOs with real ones who focus on the product instead of technical solutions.

Further, de-escalation and mediation sessions would probably have been helpful to re-establish PO and APO coaching.

Moreover, a Product Backlog (PB) transformation from SW component-centric and technical tasks to customer-centric features would enable the *PB’s prioritization* and allow teams to solve real customer problems.

*Whole product focus* is crucial! Inviting users, paying customers, and subject-matter experts to the Product Backlog Refinement (PBR) sessions would have helped establish a *customer* language, gain *whole product focus*, and deliver the ADD product incrementally with evolving customer features rather than completing technical tasks.

How to involve customers in PBR and comply with information-protection policies? It is worth realizing that many of BMW Group employees are also *customers*. They drive BMW cars and experience the product themselves. The only constraint would be to involve those who don’t understand the technical details and only speak the customer language—for example, people from HR, legal, or procurement.

### Structure
> The job of managers is to build an environment in which teams continuously deliver and continuously improve. [[3](#references), p. 69]
> Managers’ role is to improve the product development system by practicing Go See, encouraging Stop & Fix, and “experiments over conformance.” [[3](#references), p. 115]

The starting structure allowed a high degree of organizational adaptiveness, which we experienced when reforming Requirement Areas. Since Requirement Areas were *not* part of an organizational chart or unit, the restructuring process was quick.

The ADD used this benefit to frequently change Requirement Areas, mainly caused by a too-fast expansion of the LeSS organization (see also [Adding More Requirement Areas](#adding-more-requirement-areas)). Why did the LeSS organization expand too fast?

One cause lies in the BMW Group’s traditional career paths, where good hands-on engineers at the top of their technical career became mediocre managers. Consequently, the *sunshine to bad-weather managers* ratio was high, decreasing the managers’ capability to structure and manage the non-LeSS organization, subsequently leading it to an unhealthy state, which became one strong force to bring the people into the LeSS organization faster.

Another cause—likely related to the previous—was the non-LeSS group’s inability to work independently from the LeSS organization due to a lack of experts, who mainly were in the SoP 2018 project and the LeSS organization. This situation is a consequence of thinking in and organizing people around projects instead of products.

Despite the thoughtful groundwork of organizational structure and striving for self-managing teams and collaboration in communities of practice, people perceived self-management, particularly in communities, as ineffective. This was because of a vast amount of unskillful decisions and weak decision-making, due in part to the lack of experience and ability in decision-making amongst developers (since this was previously done by people in specialist roles and managers) and also in part to the lack of experience and skill amongst the Scrum Masters, who did not effectively coach the teams or communities in participatory decision-making protocols.

As a *quick fix*, for this and related reasons, senior managers revived C-4 level managers and specialist roles around two years after starting the first Requirement Area. Further, the organizational structure fossilized such that Requirement Areas became official organizational units, which leads to *rigid hard-to-eliminate* groups instead of adaptive birth/grow/shrink/die Requirement Areas, which are essential within LeSS Huge. Further, official organizational groups reinforce the silo problems. Unfortunately, this insight was either never present or forgotten at ADD, which led to ignoring the guide [LeSS Huge Organization](https://less.works/less/less-huge/organizational-structure).

> Avoid having the Requirements Areas be equal to the organizational structure as it leads to them being difficult to change. [[3](#references), p. 110]

Let’s elaborate on why many decisions were unskillful, and decision-making was ineffective.

When changing from manager-led to self-managing teams and communities, managers’ and sometimes Scrum Masters’ thinking was, “Either the teams/communities are self-managing, or I need to step in, breaking the self-management.”

**Key point**: This was a *false dichotomy*. Instead, it should have been: “I need to *help them become self-managing.*”

Driven by the fear of breaking self-management, managers left the teams and communities mostly to themselves. Since they had to make decisions, the most inadequate and naive decision protocol became their default, *majority voting*, another *quick fix* not seen, and even worse, supported by junior Scrum Masters. The experienced people were a small minority and were outvoted most times. Therefore, most decisions were unskillful and ineffective.

**Key point**: We failed to establish a skill hierarchy (without specialist roles) and introduce adequate decision-making protocols, such as a quorum of skilled and experienced people makes decisions.

The situation became similar to the one described by Jo Freeman in her article *The Tyranny of Structurelessness* [15].

> ... the movement generates much motion and few results. Unfortunately, the consequences of all this motion are not as innocuous as the results’ and their victim is the movement itself. [15]

How could a specialist-role-free skill hierarchy look like?

First, make transparent who has beginner, intermediate, advanced, or expert skills and their fields. Second, ensure that people with advanced and expert skills form a quorum for decision-making and introduce participatory decision-making protocols, such as the Decider/Resolution from [The Core Protocols](https://thecoreprotocols.org/) [19].

Third, make the differences between the skill levels transparent so that people know how to advance. Fourth, help people gaining advanced and expert skills. Moving from beginner to intermediate can usually be done by acquiring knowledge. Moving from intermediate to advanced and then to an expert level takes time, where the knowledge gets enriched by the experience.

### Processes
#### Do Continuous Improvement Towards Perfection... *Continuously*
We wanted to follow the [Deep and Narrow over Broad and Shallow](https://less.works/less/adoption/three-principles) [[3](#references), p. 55] adoption principle and adopt LeSS step-by-step, one Requirement Area slowly after another. The contract engaging coaches defined a fixed-price package of bringing 70 people into the LeSS organization at a time.

The emphasis on complying with the contract was strong, especially in the beginning. Otherwise, there would be less “value” for the same money—a *contract game*. This dynamic led to the... *prerequisite of having 70 people in the first Requirement Area*! Combined with the demand of starting the LeSS adoption at the beginning of summer holidays, and therefore little availability of people, this led to *forced* “volunteering” (see also [Prerequisites and Constraints](#prerequisites-and-constraints) and [Fake Volunteers](#fake-volunteers)). Thus, most Requirement Areas started with this number of people.

The contract also contained a project plan—a Gantt chart describing when the LeSS adoption starts and ends. This project plan, based on ignorance of skillful change and improvement, aimed to comply with the purchasing processes and BMW Groups’ policies. Behind the scenes, of course, there was no intention by those understanding adaptiveness for it to be used as an actual project plan.

But of course Murphy’s law came true: senior managers discovered this project plan, and then ADD followed it, mainly because it indicated an end date of a *continuous* change. Consequently, and this plan is only one cause, the LeSS organization expanded mostly according to plan rather than according to what made sense! See also [Adding More Requirement Areas](#adding-more-requirement-areas) and [Structure](#structure).

**Key point**: Continuous Improvement Towards Perfection was seen and run as a project instead of *continuously*.

#### Avoid Making Departments or Individuals Responsible For a Special Thing
Whenever an existing process needed adaptation or compliance with industry standards required a new one, most of the time the PO team and the development department delegated these tasks and withdrew themselves (see [Figure 15](#fig015)). Why?

One cause is that people were used to working this way. Another is that the important idea of those who use and live the processes *make* the processes was, to a large extent, not lived.

**Key Point**: In LeSS, *teams* are responsible for their processes. It is a direct consequence of having self-managing teams. See *Guide: Understand Taylor and Fayol* [[3](#references), p. 115].

One of the differences between self-managing and manager-led teams is the responsibility for their processes. Self-managing teams *own* their processes. Since this understanding was lacking at the BMW Group and due to organizational size and dependencies external to ADD, most people *rented* the processes rather than owned them.

Let’s take a look at the reasons why people did not take responsibility for their processes.

During the first two years of the LeSS adoption, people had doubts about their ability to align with LeSS principles and rules when changing existing or designing new processes. To resolve this situation, Scrum Masters coached [LeSS principles](https://less.works/less/principles/index.html) and helped to create or improve processes. It is a healthy dynamic.

During the preparation phase, before the LeSS adoption, this dynamic was foreseen. To ensure alignment with LeSS and industry standards, the *Competence and Coaching* department, which consisted of Scrum Masters and industry-standardization experts, became the official body responsible for processes.

Why did the Scrum Masters allow themselves to get involved in something so obvious that they should not? Due to little Scrum experience in the entire ADD, there was a deeply engraved understanding that Scrum is somewhat a process. As a corollary, there were *no masters of Scrum*. Instead, there were junior Scrum Masters who did not foresee the dysfunctions the “responsible for processes” label would create.

The official “responsible for processes” label created a mental barrier in people’s minds. People sought approval from the Competence and Coaching department for any changes in any process. After some time, this turned into handing problems over to the Competence and Coaching department and expecting them to drive their resolution.

As a *quick fix*, the Competence and Coaching department was split into two—(1) A unit of industry-standardization experts and (2) a homogeneous Scrum Master organizational unit. Two functional groups, each with their single-function line manager. This was an example of the “default organizational problem-solving technique. (1) Discover a problem—the blah-blah problem. (2) Create new role—the blah-blah manager. (3) Assign problem to new role.” [[3](#references), p. 120]

In the long run, one negative and unforeseen side-effect was that the industry-standardization experts unit ended up creating various unskillful processes for the teams since they had little hands-on experience nor insights. In retrospect, with more focus on the experiment *Avoid...Adoption with top-down management support* [[2](#references), p. 374], we might have been able to anticipate this since it warns of this very problem.

In conclusion, making an organizational unit responsible for processes is counterproductive for human workers in about any context. It is a manifestation of the very basic tayloristic approach of separating work between people who plan and people who mindlessly execute the plan.

**Key Point**: In fact, “responsible for anything” labels create bottlenecks, delays, hand-offs, various other wasteful dynamics, and, most important, the ownership problem. That is when the psychological connection between the role or group responsible for X and other people owning X gets broken.

The Competence and Coaching department received the “responsible for processes” label for people from other departments to know whom to seek advice from when changing processes. However, this label created an unwanted dynamic.

A more effective means to the same end would be to (1) allow the industry-standardization experts to join teams to gain hands-on experience, and (2) have regular team members be centrally involved in creating the processes.

### Rewards
During preparation for the LeSS adoption, coaches strongly emphasized the importance of changing the rewards system (including the salary model) to support the other elements of the product development system.

Specifically, subjective *manager-driven* promotions and manager-based *individual* performance appraisals (IPAs) needed significant changes to support *self-managing* teams. Why?

Manager-driven promotions drive the desire for manager-based IPAs, yet the manager (appraiser) virtually never has the insightful information to skillfully appraise. And then there are biases—conscious and otherwise. Combined with long cycle times (in this case 12 months!) between IPAs, the feedback becomes *superficial* and *unrelated* to the individual’s specific behavior. Hence, the feedback quality for the individual’s betterment is highly questionable.

Further, since manager-driven promotions are *subjective*, people start to believe that promotions are less related to performance but more related to having the “right” relationships and an ingratiating personality. Jeffrey Pfeffer described this dynamic in his worth-reading *Harvard Business Review* article *Six Dangerous Myths About Pay*.

This leads to individualism, heroism, and other dysfunctions in an intended self-managing *teamwork* environment.

At ADD, C-3 level managers, together with the HR department, had the aspiration to change the existing IPA to support teamwork and make the rules for individual career advancements transparent. But they failed.

This situation wasn’t a problem until...

...The next cycle of IPAs. Since nothing changed, people still expected their line managers to conduct their IPA. But! ...The elimination of the C-4 level managers increased the span of each C-3 line manager to about 60 employees, who now had many IPAs while at the same time having even less sight and insight.

This dynamic made the already-subjective IPAs even more subjective. Later, an employee satisfaction survey confirmed people’s frustration with this situation and their managers. Urgent improvement was necessary.

As a *quick fix* senior managers revived managers on the C-4 level to decrease the span and generate a false feeling of objectiveness in the next IPA cycle. Back to the status quo!

**Conclusion**

When introducing a significant change, such as a LeSS adoption, and changing only the structure and processes, but not reward policies and other elements, the change will fail. It’s a system!

> The Star Model™ suggests that the reward system must be congruent
with the structure and processes to influence the strategic direction. Reward
systems are effective only when they form a consistent package in
combination with the other design choices (elements in the Star Model™). [14, p. 4, explanation in parenthesis added]

If upper managers don’t exercise systems thinking, then the system will “revert to mean” simply because everybody knows it. Only changing parts of the system and having high expectations causes pain. It forms the opinion, “We have tried X, it does not work,” and leads to reactive responses, which usually result in *quick-fix reactions*.

**What could be an alternative?**

A shared objective is necessary before evaluating alternatives. If the goal is employees’ short-term compliance, then behavioral manipulation is probably the best approach. In this case, it is senseless to work towards self-managing teams because both aims contradict each other.

The next paragraphs assume a shared agreement on the goal of having self-managing teams. To elaborate alternatives, the practices of *individual performance appraisal* and *promotions* need some deconstruction.

**Individual performance appraisal:**

The common two purposes of a performance appraisal are:

1. feedback for betterment (improvement and development, e.g., adding new strengths or adding to existing strengths), and
2. input for promotion.

Feedback for betterment is supposed to be a two-way conversation, conducted frequently rather than annually, and it is utterly divorced from promotions.

> Providing feedback that employees can use to do a better job ought never to be confused or combined with controlling them by offering (or withholding) rewards. [17, p. 185]
>
> It seems foolish to have a manager serving in the self-conflicting role as a counselor (helping a man to improve his performance) when, at the same time, he is presiding as a judge over the same employee’s salary... [18]

In a Scrum environment, the team members and their Scrum Master—who are working closely together and understand in detail each other’s work—have the opportunity to give feedback to each other *every* Sprint Retrospective. Since this is standard practice, the value of this purpose in IPAs vanishes.

What is left are promotions.

**Promotion (and Rewards)**: a decision (by another party) for someone to be categorized in a new role classification that is considered “higher” and a desirable step. It *usually* includes a raise in *one* of the following: salary, power, visibility, prestige, influence, decision authority, recognition, etc.

What is usually interesting to people is not a promotion per se, but what comes with it, and promotions usually offer different types of *rewards*. Frederick Herzberg categorized some of them in his *Harvard Business Review* article “One More Time: How Do You Motivate Employees?” into two categories: (1) *hygiene factors* and (2) *intrinsic motivators* [16]. According to Herzberg, a bad implementation of the hygiene factors leads to job dissatisfaction. However, getting those right does not lead to job satisfaction. Instead, it leads to *no job dissatisfaction*. Intrinsic motivators are the ones which lead to job satisfaction.

In this context, *salary is just a hygiene factor*. Therefore, it is useful to treat it as *compensation*, not as a performance contingent reward. With that in mind, the entire practice of manager-driven and -influenced salary adjustments become ineffective and can be removed.

> Do your best to make sure they (employees) don’t feel exploited. Then do *everything in your power to help them put money out of their minds*. [17, p. 182, explanation added in parenthesis]

Note that the *non-monetary* rewards (e.g., decision authority, recognition) associated with promotions are more likely to act as intrinsic motivators.

Dr. Richard Hackman (who was a leading expert on teams, at Harvard university) mentions three conditions for rewards to work. (1) “team members must *understand* what it is that is wanted and rewarded.” (2) “There must be trustworthy *indicators* of the degree to which the desired outcome actually have been achieved.” (3) “... members must perceive that they have *leverage* on the attainment of those outcomes, that their collective behavior directly shapes the outcomes that trigger the rewards.” [12, p. 138-139].

*Formulaic-criteria promotions* could help to achieve all three points. They would also indicate the Product Developer (PD) level.

What could be the formulaic criteria? In a LeSS context, the criteria must help increase the adaptiveness of the organizational system. For example, to go from PD_n to PD_n+1, the employee has to indicate level X in *four* different skill areas, showing they are adaptive. This way, formulaic-criteria promotions become more objective, transparent, and clear to everybody.

How to assess the employees then? As in any assessment, the assessor must be more experienced than the person being assessed. Therefore, it could be done by internal widely-recognized experts or an expert panel, or by an external body, such as a group that evaluates and certifies expertise in a skill. Further, feedback from peers could also be used.

**What to do if the HR policies remain unchanged?**

Just like in ADD’s case, managers couldn’t change HR policies or remove the IPA. The book *Scaling Lean and Agile Development* contains two experiments in this regard.

1. *Try...Discuss with your team how to do appraisals* [[1](#references), p. 275]
2. *Try...Fill in the forms* [[1](#references), p. 275]

In step one, managers and the teams need to discuss the dysfunctions manager-based individual performance appraisals and manager-driven promotions create. After they reached a shared understanding and understood that the process is unskillful and wasteful, they must *agree* on how to handle the unchanged HR policies in the future.

In step two, after recognizing the process is a waste, they do the process with the *least effort and attention* and then go quickly back to the useful work: *shipping the product*.

### People
Basic systems thinking—and the Star Model’s interwoven nature (see [Figure 20](#fig020))—shows that people need a holistic appropriate organizational design to succeed.

**Key point**: Peoples’ attitudes and the other Star Model elements need to fit together for the organization to be effective.

The team members were coming from a traditional organization, manager-led and organized in single-function groups and component teams. The LeSS adoption required people who *want* to work cross-component in *shared code* and cross-functional solving customer problems—a quite different attitude.

Many people had difficulties working this way, regardless of whether they wanted this or not. Over time, most teams reverted to a component-team-like setup. Let’s explore the driving forces behind this phenomenon.

One strong cause was the technical-tasks list of work, incorrectly called a “Product Backlog”. See [Strategy & Tasks](#strategy--task).

Another cause was the peoples’ desire to narrow their focus to fewer, ideally one software component. There were at least two reasons for that:

**Reason one:**

Before the LeSS adoption, ADD estimated (based on software components) the additional number of people required to develop AD. How much more complex will each software component become, and how many more people will we need to cope with that? This implies that the dominant mental model about organizational structure was based on components instead of customer-centric features.

Hiring efforts before the LeSS adoption attracted many new people with a component-thinking attitude since people with specific expertise in specific algorithmic fields were looked for. Further, most new-hires came from universities or their first jobs and had little to no product development experience, especially working in shared code.

With the LeSS introduction, the *initial* customer-centric end-to-end Product Backlog items rarely covered peoples’ existing expertise. The fear of losing their competencies and the illusion of losing their market value made the people demand to work only on “items” (i.e., single-specialist tasks) covering their specialization, especially since this was why ADD hired them in the first place.

The traditional-management need of utilizing people in their specialization, combined with some manager’s unwillingness to help their subordinates resolve their issues, led to accepting the peoples’ demands and creating work (tasks rather than customer features) designed for their single specialty—another *quick fix*.

A more useful approach would have been to take only real volunteers into the LeSS organization. Further, help each person individually resolve the issues they had, mainly a widespread false dichotomy of “Either I do what I like and good at (single specialization), or I’m a generic feature team member.” In the worst case of not wanting to work in such an environment, managers should have assisted individuals in finding another position.

**Reason two:**

The learnings from Certified LeSS Practitioner courses motivated many people to work cross-component and cross-functional. However, the lack of software craftsmanship before the LeSS adoption accumulated so much technical debt that it blocked simultaneous working in a shared code manner.

The problem was further exacerbated by having so many new teams involved, and more or less at the same time. It became impossible to adopt software craftsmanship with so many people involved, while dealing with dirty code.

For example, low test coverage and high coupling between components left people in the dark about whether their changes broke another part of the system. People had to rely on component experts’ judgments on whether their changes would break something. Consequently, people were reluctant when changing the parts that they were not experts in.

Therefore, people could not handle the technical stack’s wide scope effectively and requested a focus reduction. These effects became evident, especially as the LeSS organization expanded—another effect of too-fast expansion.

**Key point**: Large technical debt, too-rapid expansion of the LeSS organization, and little software craftsmanship skills lead over time to component teams—a reinforcing downward spiral.

At that time, technical coaching was available en mas at ADD. Unfortunately, many teams did not use it. The perception teams had on problems they have was different from the one coaches had about them. For example, it was unclear to the teams how learning TDD (whose value is appreciated in the longer term) would solve their *short-term* current and short-term future challenges, such as designing the application for modularity (different sensor characteristics during application-life-time) or security and safety goals provability (e.g., no hard turn while driving fast). Coaches missed the opportunity to help teams solve their problems and use them as a vehicle to improve the teams’ technical excellence.

Those who used technical coaching improved their software craftsmanship skills. Unfortunately, the positive effects of improved software craftsmanship skills have a long delay until they become visible in a huge codebase. Considering the LeSS organization’s too-fast expansion, the technical coaching had little impact at that time.

### Conclusion
The product development system’s parts are interwoven and highly influential on each other. It’s a system! ADD failed to understand that.

This section will examine some of the symptoms and their influences. In addition to what we present below, we wonder if there were deeper forces at play that we haven’t been able to see. Common deeper forces of organizational dysfunction include personal relationship favoritism, sabotaging changes that challenge the status quo of manager positions (so that reverting to the status quo becomes an option), and so much more.

One crucial observation at ADD is that many (described so far) issues were correctly foreseen. Still, many chosen “solutions” avoided (in reality, just postponed) the problems instead of confronting directly and solving them.

One cause of this effect was minimal systems thinking. Mainly due to—often self-inflicted—time pressure, rapid jumping from problem to solution space, being convinced that the causes of problems at hand were obvious. Consequently, leading to more problems, time pressure, and less systems thinking—a reinforcing loop.

Another cause was the many sunshine managers—a delayed effect of lacking a technical career path—who did not understand and therefore did not warn about or explain any consequence when people disregarded agreements and guidelines or bluntly ignored agreed-upon tasks. Active sabotaging had little to no consequences (for saboteurs), resulting in more dysfunctions. One result was a too-fast expansion of the LeSS organization—an overarching symptom and cause of many other harmful effects.

The retrospective on the timeline view results in five symptomatic categories.

1. Unmet prerequisites for scaling adaptive product development
2. Too-fast expansion to many Requirement Areas
3. Missing understanding of and motivation for Go See
4. Missing motivation for teamwork
5. Missing focus on technical enabling and excellence

<a name="unmet-prerequisites-for-scaling-adaptive-product-development"></a>
**Unmet Prerequisites for Scaling Adaptive Product Development**

In the beginning, the organization feared that a profound change would disturb the delivery capability of SoP 2018. Combined with *treating products as projects*, it increased the distance between the people involved in SoP 2018 and SoP 2021. The project structure forced the delivery of SoP 2018. Therefore, we started the LeSS adoption, although most people experienced in production-ready car development were unavailable. The technologies, design approach, complexity, organizational design, and ways of working between SoP 2018 and SoP 2021 was utterly different. Therefore, it is very uncertain that involving SoP 2018 people into the first Requirement Area would make the LeSS adoption less painful. However, their experience from really shipping, and the required focus on whole-product overview when a group is getting close to delivery, would have been invaluable in the SoP 2021 non-LeSS organization, especially at the early stage.

The forced “volunteers” led to dysfunctions in the first Requirement Area. The creation of a positive showcase for further scaling was not possible. However, due to running continuous improvement as a *project* (thus, with an *end*) instead of *continuously*, ADD still executed the “scale-up” plan.

More significantly, the importance of a rock-solid build system and continuous integration as behavior was underestimated and ignored because of inexperience in large-scale agile software development and weak software craftsmanship.

The modular-system contract between ADD and the Product Management department and the “we need to deliver everything” ethos led to no prioritization and lower acceptance of reducing-the-scope discussions. The failed PO/APO coaching resulted in a so-called Product Backlog consisting of technical tasks.

Both resulted in a lack of whole-product focus and prioritization, leading to high busyness and *output* of completed technical tasks, but very low output of completed customer features, and thus no useful *outcome*. This typhoon of technical tasks made it impossible for the PO to have a meaningful whole-product overview, to order the so-called “Product Backlog,” which disempowered him and made him dependent on the technically-involved “APOs”—he had to believe what the “APOs” told him.

Further, managers and a vast number of junior Scrum Masters failed to establish effective decision-making protocols in communities of practice and teams.

<a name="missing-understanding-of-and-motivation-for-go-see"></a>
**Missing Understanding of and Motivation for Go See**

First, the Go See practice was misunderstood or not understood at all. Go See in software development means observing the *code* and the people’s experiences in the moment while hands-on creating the code and grasping the situation, positive and negative, from that.

It isn’t “Go See in the building where product developers work.” It is, for example, sitting in the back of the room while a team is doing mob programming and grasping the situation by observing the developers in that context and the code they are creating.

**Key Point**: The heart of “gemba” in software development is... the *source code*.

See also the respective guides, *Guide: Go See* [[3](#references), p. 125], and *Guide: Managers as Teachers and Learners* [[3](#references), p. 128].

Second, the area of concern for managers was too broad; it defused their efforts and limited their motivation for practicing Go See. Individual, incentivized targets and the individual performance appraisal (IPA) for managers supported this behavior; it did not include teams’ feedback. Instead, it was done solely by their line manager.

**Missing Motivation for Teamwork**

One cause for the missing motivation for teamwork was the unchanged and opaque IPA, in some cases combined with specific persons’ bonuses attached to specific goals or achievements. It promoted individualism instead of teamwork on any level.

**Missing focus on technical enabling and excellence**

The attention gap for technical enabling and excellence led to negative reinforcing loops. The deployment to the actual target platform, or at least an emulated environment, was undervalued mainly due to decades of early software component development and late integration. Instead, ADD used a (not suitable for production) rapid-prototyping platform for a long time. Consequently, the software evolved towards only being suitable for the rapid-prototyping platform, hiding design flaws and undermining the *whole product focus*.

#### What Should Have Happened To Keep the Magnitude of the Chaos Phase Bounded?
First and foremost, ensure that *continuous improvement* was understood and established as such—no fixed end of “completing the change!” *Continuous improvement towards perfection* is a *life long* undertaking. At ADD, this part might have been rationally understood. However, since *culture follows structure*, peoples’ behavior showed the opposite.

Second, set up a stable parallel organization. Have one Product Backlog for both organizations. It would motivate one code base and prevent separation in code. Further, it would influence the entire product group to work on the highest customer value.

Build up the LeSS organization with real volunteers, expand it slowly and carefully, and only when the preconditions are in place, including a prioritized common Product Backlog for all teams and Requirement Areas, and a working build system which ensures fast feedback.

Crucially, follow the standard advice in LeSS Huge to incrementally expand one Requirement Area at a time.

Remove complexity by treating products as what they are—products. Treating them still as projects leads to organizing people around just tasks and creates further dysfunctions. This approach would have brought the people from SoP 2018 and SoP 2021 closer together. People would have been able to benefit from each other’s experiences. It would also enable one common Product Backlog for the entire product group.

To keep the pace and magnitude of change bound to a manageable level, starting with SoP 2018 would have been a wiser choice. Within SoP 2018, the number of knowns—for example, target platform, processes, build pipeline—was much higher. Those circumstances would have made it easier to move from single-function and component teams towards feature teams. Further, the SoP 2018 setup change would be confined to one Requirement Area, focusing on the transition towards feature teams, avoiding premature expansion of the LeSS organization.

The individual performance appraisal should have been removed or changed to minimize its negative impact and to support teamwork and self-management. An in-depth education, including Scrum basics, would have laid a more solid ground for the adoption.

## Summary and Positive Effects
With the start of the LeSS adoption, the amount of euphoria was high, and so too were the expectations on the whole new organization. Time passed, it became visible that expectations were far from being met, and the euphoria turned into pain. Where did this pain come from?

> ...in a larger product group (say, 500 people) adopting large-scale Scrum, systemic weaknesses are exposed in the organizational design—in structure, processes, rewards, people, and tasks. [[1](#references), p. 290]

Indeed, so did the weaknesses of the prior organizational design at ADD, which led to this situation. It is naive to expect that after decades of building up organizational and technical debt, suddenly overnight, the behavior of a rock-solid build system and continuous integration would be in place. Paying off those debts will take years, and the practices and technical agility will improve gradually.

Technical agility constrains organizational agility—or phrased in reverse “[Organizational Agility is constrained by Technical Agility](https://less.works/less/technical-excellence/index.html).” Therefore, the highly flexible organizational structure there was at ADD, provided only limited benefits. Instead, the gap between how ADD wanted to work and how the technical infrastructure and product code base allowed it to work was the pain. Some changes had to be reverted, and some adapted to get the organization going again (see [Figure 22](#fig022)).

<a name="fig022"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig022.png" alt="Technical agility constrains organizational agility.">
  <figcaption>Figure 22: Technical agility constrains organizational agility.</figcaption>
</figure>

> **Do not expect this to go fast; it will take years or perhaps decades**—in fact, forever, considering the pillar of continuous improvement. A good sense of humor, an informal supportive community of practice, and patience is especially helpful in organizational improvement. Celebrate small steps forward. Especially in the work of organizational redesign, we encourage our clients to **keep in mind systems thinking and the dynamic of local optimization**. [[1](#references), p. 284, emphasis added]

#### Learnings and Positive Effects
A key purpose of LeSS is to make already-existing issues visible again. Hence, when the euphoria settled and the product focus increased, the issues and failures described in this report became visible. Then, to correct the errors and make up for what ADD lost so far, the introduction of inevitable changes began.

Despite the dysfunctions and pain ADD was in, these have led to positive effects and learnings.

An important learning is that *whole product focus* and an *inspiring product vision* are crucial for successful adaptive development.

##### Collaboration Between Departments
Established cross-area events, such as reviews, Product Backlog refinements, and retrospectives, led to better collaboration between departments. Further, fewer roles and a higher degree of cross-functional teams reduced hand-overs and politics between departments—less “we vs. them” thinking.

Multiple departments, even those adjacent to ADD, are working based on the same principles. Therefore, there are fewer escalations at the department borders necessary.

##### Higher Focus on Self-Managing Teams and Frequent Retrospectives
Since the LeSS introduction, there is a sharper focus on *teams* rather than individuals, while demanding and supporting self-management. By far, more decisions are made by teams today compared to earlier, leading to less hand-off and information scatter.

Further, retrospectives, inspections, and adaptations occur each Sprint, which hardly ever happened before the LeSS adoption. Meaning root-causes are being analyzed and fixed much more frequently.

##### Technical Excellence
The attention to technical excellence increased significantly with the start of the LeSS adoption. It led to a higher focus on virtualization and automation.

Coaching on technical excellence increased the awareness of its importance and implications. It led to modern C++, clean(er) code, TDD, etc. Merging the research with the development group amplified the progress on technical excellence. Further, cross-team collaboration improved shared code ownership.

There is also more try, inspect, and adapt to learn from the real product environment instead of finding a “solution” to a problem without writing any code.

##### ADD Learned to Drive the LeSS Adoption Themselves
When an external coach is engaged to help a company adopt LeSS, the coach usually takes the driving person’s role. On the positive side, this approach leads to fewer failures in the beginning. On the contrary, as soon as the coach leaves, the company must learn to continue alone, which could be hard without a coach.

In this case, BMW Groups’ internal people took the driving person’s role. The coach focused very much on enabling the internal employees to make the adoption themselves. Doing so led to some failures due to still limited internal experience, which the ADD learned from. This way, the product group can still pursue the LeSS adoption themselves even after all external coaches’ engagement ended.

ADD got used to real adaptations. Therefore, it is easier to initiate changes when necessary.

From this point on, the change must be continuous and sustainable, made in small steps, going towards the initial optimizing goals.

Two steps forward, one step back, still brings you ahead!

## Outlook
During the writing period of this report, further adaptations took place at ADD. Teams of a Requirement Area and their dedicated line manager are one organizational unit now. Line managers have a much narrower scope of concern and can focus on teams of one Requirement Area. APOs and Scrum Masters remain in other separate organizational units.

Prioritization is starting to happen. The product focus is increasing fast, allowing everyone to inspect and adapt based on product-related issues.

It seems that ADD is entering the fourth phase of the Satir change model—the integration phase. Overlaying the Satir change model pattern with [Shu-Ha-Ri](https://www.makigami.info/continuous-improvement-tools/shuhari-japanese-learning-system/) stages gives a better understanding of why it is happening this way, and how the future could look like (see [Figure 23](#fig023)).

<a name="fig023"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig023.png" alt="Journey of BMW Group’s LeSS adoption overlaid with Shu-Ha-Ri stages. Based on the Satir change model.">
  <figcaption>Figure 23: Journey of BMW Group’s LeSS adoption overlaid with <a href="https://www.makigami.info/continuous-improvement-tools/shuhari-japanese-learning-system/">Shu-Ha-Ri</a> stages. Based on the <a href="https://stevenmsmith.com/ar-satir-change-model/">Satir change model</a>.</figcaption>
</figure>

Facing the blunt reality, and understanding and living out the rules and practices help enter the *integration phase*, which also correlates with the *Ha* stage. In the Ha stage, people in an organization must reflect on the meaning and purpose of everything that they learned. Therefore, they come to a deeper understanding of the art—in this case, large-scale adaptive development—than pure repetitive practice can allow.

It is too early to draw any conclusions from the recent adaptations. They need close observation and analysis over time. The results of this could be the next volume of this report.

# 技术角度
在这一部分中，探讨了几个技术方面：哪些进展顺利，哪些不足，以及下一次需要学习什么。为了更好地理解起点，这里简要介绍了转型开始之前的技术情况。以下章节将提供更多详细信息。

## 转型之前
宝马集团在转型之前几十年就开始探索ADAS。在博士研究、外包和其他学术研究等众多不相关联的研究项目中，探索路线有所不同。在大多数情况下，项目计划和功能描述将这些路线链接起来，但在实际设计和代码中却有很大的脱节。这导致了各种各样的代码库和工具。

顺便说一句，作为一名技术教练，我（[Michael Mai](https://less.works/profiles/michael-mai)）发现，当软件开发被视为多个项目而不是一个产品时，这是一种常见的模式。

学术项目经常使用Matlab和Simulink。宝马集团雇佣的外包商使用Matlab或C。这使得协作复杂化，也解释了代码库中一些分歧的概念。

值得注意的是，关于实现至少Level 3的自动驾驶的高难度目标，宝马并没有关注现代机器学习方法，这与该领域最有成就的领导者（如Waymo、Tesla）采取的以机器学习为中心的方法形成鲜明对比。相反，宝马集团继续探索和应用传统的控制方法，如基于公式的指令式编程，就像之前在巡航控制里相对简单的驾驶控制问题中使用那样。

宝马集团将一些研发工作集中在三个大的内部团队：SoP 2018、SoP 2021高阶自动驾驶（HAD）和SoP 2021全自动驾驶（FAD）。这些团队在车规级产品开发方面有不同的知识、经验和参与程度。此外，这些团队在不同的时间加入到转型中（参见[图24]（#fig024））。另请参见[图17]（#fig017）和[假志愿者]（#fake-volunteers）。

<a name="fig024"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig024.png" alt="Joining of groups">
  <figcaption>Figure 24: Joining of groups.</figcaption>
</figure>

SoP 2021团队主要由研究人员和大学刚毕业的新员工组成，他们紧密合作，形成了LeSS转型的起始种子。因此，*他们中经验丰富的软件开发人员很少，车载产品开发的经验有限，并且只具备ADAS中分隔的领域知识*。

在准备ADD计划时，管理层认为团队中增加的大学刚毕业的新员工可以将现代软件开发技能以及现代整洁和设计良好的代码引入代码库 - 这是管理人员缺乏软件开发技能的另一个迹象。鉴于这些新的非顶级加入者（来自大学或者行业中）能够贡献的经验有限，这次团队扩张是徒劳的。[人员]（#People）章节探讨了其他原因。

缺乏经验的SoP 2021团队做出的基础架构决策是直接使用基于机器人研究的消息中间件平台[ROS](https://www.ros.org/). ROS被用于许多机器人技术的研究论文，但它的设计理念与汽车平台并不兼容。

由于（1）分为HAD和FAD项目组，以及（2）他们被分成多个组件团队（这是管理人员从构建物理组件中所熟悉的传统模式），以及（3）缺乏软件开发和大规模协调的技能，*在这些团队创建的多个代码库中，软件概念和设计基本上没有一致性。这些项目组的不同代码库仅在ROS消息级别上有交互*。

由于项目目标的差异，概念和软件的“一致性”被评为较低优先级 - 尽管它是交付一个真正产品的关键。这是管理层和开发人员缺乏大规模复杂软件开发经验的另一个迹象。因此，HAD和FAD的代码库差异很大。除此之外，这两个项目组独立组建了各自的*组件团队*，正如宝马管理人员之前在相对次要和较小的软件项目所提倡的那样。在开发一个高难度的研究密集型端到端自动驾驶机器人时，需要大量基于学习的反馈和改变，宝马管理人员天真地没有意识到由此带来的风险以及缺乏学习和适应性。这些原因导致了几乎没有一致性。

SoP 2018组是具有产品开发经验的资深*传统*工程团队（参见[扩展适应性产品开发的未满足先决条件](#unmet-prerequisites-for-scaling-adaptive-product-development)以了解为什么该团队存在，以及为什么LeSS转型一开始时没有将该团队纳入）。由于他们的部署目标受限的工具链，他们不得不使用受限的C++子集，并且他们主要是一群传统的C程序员。他们在诸如面向对象设计（OOD）这些基于较新行业标准的现代大规模软件密集型设计方法上几乎没有经验。缺乏OOD技能这一因素促成了不将SoP 2018的代码库融合到新产品代码库的决策。请注意，如果没有这项技能，开发人员就无法在一个新的系统中有效地设计现代C++代码，新系统比他们以前做的任何事情都要复杂和不同。

不同的小组在交流和思考中，对共享软件的设计和想法很挣扎。他们不同的过去、目标和代码库并不支持联合开发。然而，管理层的目标是将这些小组联合起来，尽管他们存在差异。为什么？（1）他们是宝马集团的员工，应该能参与开发新产品，（2）错误地评估进一步开发将需要大量增加员工（详见[人员](#People)），（3）将十年研究成果放到一个产品中 - 要求不只是研究人员，（4）弥合研究间的差距，获得洞见，并将洞见应用于客户产品。

说到第（2）点，“大项目需要大团队”，宝马的大多数管理层都有机械和电气工程和制造业的背景，他们错误地将软件研发视为一个生产问题，而不是研发问题，*在生产过程中，更多的人意味着进展更快*。但是，*在软件研发中，增加大量的人而不是合适的人，会恶化问题和阻碍进展*。因此，这是自董事会层向下的另一个缺乏现代和大规模复杂软件管理专业知识的迹象。

以下章节重点讨论组织、政治和人的障碍以及导致这一有挑战的技术环境的系统动态。还包括并讨论了解决这种情况的一些想法和尝试性建议。


## 一个产品、一个仓库、一个分支
在LeSS转型之前，有150多个代码仓库和数百个分支。如前文所述，各组以项目制和组件团队的方式工作严重影响了代码库的设计和仓库结构。

管理层和开发人员缺乏现代大规模开发经验的另一个迹象是，他们没有意识到当不同的团队必须合到一起并交付一个共同的产品时，众多仓库和分支会导致许多问题。以前多个项目和组件团队的模式由于延迟集成也就延迟看到了这一问题。

幸运的是，新的ADD部门早期行动之一就是对产品进行定义。单一产品的定义开始使各小组形成一体，并为一个仓库和一个分支创造了动机。导致决定一个仓库和一个分支的主要需求是：

* 将工作重点放在产品上
  * 否则里程碑将受到威胁
* 法律要求和修正案的持续实施
  * 否则产品的销售不合法
* 业务和用户体验需求的持续实施
  * 否则产品卖不出去

选择的版本控制工具是[GIT](https://git-scm.com/)，“一个分支”就是指“主分支”。仅工作在主分支（相当于许多工具中的*主干*）上的实践被称为[主干开发](https://paulhammant.com/2013/04/05/what-is-trunk-based-development/).

然而，仍然存在一个主要的延迟集成问题：之前，两个组*分别*关注L3和L4级自动驾驶。考虑商业风险管理，L3级功能首先需要可靠，因为愿景是至少提供L3级自动驾驶，因此它在产品待办列表排序上有着更高的管理关注度和影响力。尽管如此，许多管理者意识到，如果L4级开发被抛弃，在市场L4级竞争上就将输给竞争对手。因此，*两者被并行跟进*。我将在合适的章节中探讨这些对立的心态，及其对集成 - 并且在更广泛程度上对产品开发 - 的有害影响。

#### 内部合作伙伴与偏离单分支规则
ADD单一产品定义带来的仓库和分支合并所产生的活力也推动了其与宝马集团内部其他部门的分离。

这种分离显示出管理者希望彼此区别开来。从其他管理者的角度来看，ADD管理者创建了一个超级部门，该部门吞噬其他部门 - 也就是这些管理者的部门。部门缩减通常是为了产品和高层的利益，但很少是为了这些部门（中层）管理着的利益。因此，一个/更广泛的产品定义的附带结果是，其他部门的经理需要区分自己，例如通过在其部门*局部优化*以有理由继续存在。

例如，负责人机界面（HMI：车机屏幕、HUD抬头显示、方向盘、广播按钮等）开发的部门认为，他们也有其他车型项目的客户。因此，他们的管理层主张（1）集中设计是“最优的”（当然，实际上是一个*局部*优化），（2）分离设计团队并加入ADD团队会破坏他们的多个人机界面*项目*，以及（3）如果设计团队分散，则每个项目的时间计划都会有风险。不用说，这个传统的人机界面和设计部门与宝马集团的许多其他部门一样，组建起来的目的是控制供应商的设计、用户体验研究以及相关软件和硬件。

宝马集团组织车型开发、车型制造和车型项目的方式也被各部门用来声称他们独立于ADD的产品愿景。潜台词是，任何“超级”部门都不应改变或挑战已经存在的（局部优化）现状。

由于整个系统部门间协作的组织设计是董事管理层的责任，而且董事管理层显然不理解现有系统对于ADD的成功是存在问题的（因此没有改进），这说明董事管理层也不具备管理大型复杂软件的知识和技能。他们可能继续将问题视作是需要他们传统的供应商管理模式。

#### 研究合作者与偏离单分支规则
将研究结果集成到产品和产品代码中对于ADD来说很重要，因此ADD维护了几个这样的研究项目。

管理者决定这些项目使用单独的仓库，因此集成的时间很晚。管理者决定这样做的一些原因是：（1）研究成果是否纳入到产品中有高度不确定性，（2）有一些非宝马集团的研究人员参与；因此，管理层限制了无关宝马集团代码的数量，（3）研究代码中的软件设计和代码质量差得令人无法接受，（4）研究人员使用不同的编程语言。

较晚集成的一些后果是：（1）不同的概念，（2）对后续算法、数据结构和评估的影响，以及（3）对研究代码解决问题的理解及细节存在很大差异，这导致了在集成以及对软件设计修改有很大挑战。

#### 外部合作伙伴与偏离单分支规则
在宝马集团，一种常见的方法是为每个合作伙伴（取决于合同协作级别）将代码库分割成多个片段（一个片段=一个仓库）。ADD管理采用了这种幼稚的方法。这带来的问题有：（1）它强调符合现有（传统）合同模型，（2）因此，它局部优化于合同，而非产品成功或端到端协作，（3）为了优化于传统的合作伙伴-合同模式，有效集成和协作受到影响，以及（4）需要适应性协作和频繁集成才能取得成功的整体解决方案受到严重损害。所有这一切都表明，缺乏现代大规模适应性开发实践经验，缺乏对这一举措的复杂性、所需的协作和集成以及仓库管理实践的理解，高级管理层更关心“好”的合同而不是工作软件。

#### “非车上”的功能与偏离单分支规则
尽管现在有“一个产品”的定义，但由于管理层和开发人员缺乏洞察力和经验，他们继续延迟集成，并为各种组件和“项目”创建多个仓库或分支。

例如，数据中心和数据检索相关组件长期未与常规产品开发进行集成。这影响了数据中心和处理集群的数据检索和再处理能力。由于未集成，用于验证或仿真的大量数据处理无法进行，因为存在不兼容数据或无效数据（较晚集成导致集群处理存在过时代码）。

只有在这个问题非常明显之后，开发人员和管理人员才开始整合代码和人员。然而，将员工转移来处理这些自我造成的创伤 - 又一个速效方案 - 阻碍了管理层思考人员的合适组织和根本原因，因此，ADD的员工规模甚至增加了更多。

#### 平台和供应商特定代码与偏离单分支规则
高层的愿景是，ADD是一个可以提供给众多车企主机厂的平台。考虑高研发难度，以及宝马及员工以前并未有相关经验，这其实是投资者和管理层的一厢情愿。

无论如何，一厢情愿的想法还是赢得了胜利。管理层决定将平台依赖（=供应商特定）代码和平台独立代码拆分到各自的代码仓库，因为管理层和开发人员不了解或不具备在架构上分离代码而只保留一个仓库的软件技能。这样拆分造成了包括ADD在内的所有参与主机厂更为复杂的开发和延迟集成问题。

#### 仓促合并仓库

第一个需求领域是从2021要发布代码库的一个子集开始；它也只包括第一批[假志愿者](#fake-volunteers)。甚至在转型开始之前，管理层就决定了人员升级，也被称为组织切换。管理层明确表示，任何员工在完全加入转型后，以前有效的东西现在也应该有效，否则这些员工应该留在旧的组织架构中。这导致了多个几乎没有对齐的仓库（代码库）的仓促合并。除了催促开发，管理层将如何实现这一目标的具体方法交给了开发人员。

由于这一管理指示和催促“加快”，出现了瞬间大爆炸 - 先将所有仓库同时合入一个仓库中，之后再整改对齐。该方式是基于复制旧构建系统中的步骤，然后将构建工件拼接在一起。这种“拼接大爆炸”方法并没有为统一软件设计或不一致的概念创造出时间或者兴趣，而只是推迟了这些关键问题。这将在以后导致许多问题，呈现了经典的常由管理团队推动的”快即是慢“的动态。

## 软件设计和架构

首先，一些广义的背景和影响：

如前所述，大多数开发人员都是ADD的研究人员。这影响了他们对软件设计的选择。起源于个人英雄主义的环境，例如获得博士学位，他们对开发的自然掌握是孤立的。这导致了大合并之前有许多仓库。

另一个影响因素是：作为大公司的一部分会影响思维方式。其中一种是由于*沉没成本*而坚持弱解决方案。

更多的上下文：（1）代码库需可维护20年以上，（2）法规要求影响更新周期，（3）传感器的变化性，（4）不同主机厂之间协议和语义元素的可变性，以及（5）正在进行的研究和实验。

### 基于规则编码还是机器学习？专业知识和招聘动态
ADP自动驾驶平台的一般架构方法是*基于规则编码*。特别是与其他重要的供应商及他们宣称的成功、失败以及他们越来越关注接近“100%”的ML（“AI”）自动驾驶方法相比：为什么ADD坚持传统的方案？

大多数开发人员的起始是做研究。他们（德国）的学术经验倾向于深入地工作在某个假设上，并注重个人的卓越。这培养了毅力和奉献精神，但也造成了思想狭隘。这导致*减少了*解决自动驾驶挑战的选项。有些选项是机器学习或者规则编码与机器学习的组合。

为什么管理层没有更严格地质疑当前的方法，尤其是因为全球行业领导者越来越公开强调，他们学到的一个关键教训是关注端到端的机器学习？首先，大多数管理者都被自己（德国）的学术生涯蒙蔽了双眼或带有偏见。

其次，他们对研究人员有过度的信任。只有少数管理人员具有大型、复杂和自适应软件开发的经验，也只有少数人具备学习这种经验的必要背景和技能，大多数*不愿意真正访问实际工作地点，查看代码并了解软件细节中的真实情况*（参见[对Go-see的理解和动机缺失](#missing-understanding-of-and-motivation-for-go-see)）。这些因素加起来导致了相信员工，特别是那些拥有*学位*的员工，是在实际创建大型复杂软件和自动驾驶设计方面的专家。由于缺乏和不愿质疑他们的“专家”，他们只是附和。没有质疑现状和“专家”，或是去调查外部有经验的专家在做的工作。

第三，一些管理者确实怀疑过所选择的路径是否正确，但没有设法挑战内部权威或他们的同级管理者、认真探索替代方案。导致他们没有对怀疑采取后续行动的原因是多方面的，没法在此进行全面讨论，因此主要是猜测。但管理者不对现状拉响警报，以避免争议或损害他们未来的职业前景，是商业上的一种常见模式。

第四，想想管理者是否曾经想过采用机器学习的方式。哪些员工能够进行产品的实现，以及对时间线有什么影响？没有人有这样的技能和经验，而且”要花的时间太久了“。早期的技术教练之一克雷格·拉曼（Craig Larman）认识到人才的缺乏，很早就向高级管理层建议了一项风险缓解战略，启动第二个平行计划，由花钱可以雇佣到的最优秀的全球专家组成，包括机器学习专家，但遭到拒绝。

考虑到许多开发人员都是来自一个崇尚英雄主义的学术环境的研究人员，他们的论文中绝大多数都是基于规则编码的解决方案，相比花精力探索机器学习架构的截然不同方法，拒绝替代方案要容易得多。

为什么拒绝替代方案对开发人员来说很容易？研究人员因为专业知识而得到认可。建立足够的专业知识来质疑一个常见的方法需要时间、机会和奉献精神……这些在公司里的竞争环境中很难找到，尤其是在命令与控制的组织结构中以及不崇尚探索替代方案的个人奖金系统中。允许一个另类的外部观点几乎等同于承认自己不是“专家” - 这是大多数学者所避免的。

为什么ADD只考虑他们的“专家”（研究人员）意见，而不考虑更具现代技能的软件开发人员的意见？在传统工程领域成熟且成功的公司将自己视为专家。去询问顶尖的外部人员挑战了他们的自我认知。

管理者的典型思维是：待的时间长的员工为长期产品提供坚实的论据，因为他们必须坚持长远的决策。这种想法是被误导的，因为决策与员工时间长短之间的联系是错误的。员工通常有其它强烈的理由留下来，例如家人、朋友、当地关系和公司附带福利。如果预算和管理人员允许，*外部人员也会选择留下来*，外部人员因而比内部人员更能体现明智的战略。

为什么ADD没有雇佣最顶尖的软件开发人员？顶级开发人员倾向于（1）自我管理的工作（管理人员的干预非常有限），（2）与其他优秀开发人员密切合作，（3）有目的地工作，（4）为了被认可而工作，以及（5）不愿意为传统和软件技能不强的管理人员工作。

将软件*设计*方法与招聘过程进行类比会有一种意想不到的效果。宝马集团拥有完善的人员配置和招聘流程。通过*宝马集团的董事管理决策*将自动驾驶开发作为紧密相连的部门运营，ADD继承了这些招聘流程。

招聘过程中的基本组成部分包括与将来可能共事的同事进行面试和编程。面试官和编程题目的选择在如何增强或削弱软件工程和软件设计方法的多样性方面起着重要作用。想象一下，一名候选人被一名具有资深传统、非OOD和非机器学习思维的宝马员工面试。任何具有很强OOD或机器学习技能的候选人都会提出*对立的*设计建议。此外，如果编程题目是为了测试基本编程技能，而在大规模设计或应用OOD或机器学习上没有挑战，那么候选人会得到这样的印象：ADD没有足够的挑战，也不是一个能在里面成长的地方。

现在，ADD确实有一些研究人员在机器学习和相关基础设施方面有一定的学术关注。他们也被聚集在一个机器学习社区中。但要想有所作为，他们需要有充分的证据（来自数据）。产生强有力的“证据”需要大量的时间和精力，但持怀疑态度的管理者无法提供支持。

最后，在德国，关于基于规则编码vs机器学习算法的整个讨论被尚未明确的法规所掩盖。不清楚是否允许机器学习做出驾驶车辆的决定。在目前的情况下，宝马集团经理的方式是遵循传统方法，因为担心不明确的法律后果。

### 模块化软件和集成 - 刻意与巧合设计
在[一个产品、一个仓库、一个分支](#one-product-one-repository-one-branch)之前的许多独立代码库复杂化了协同组件的创建，并延迟了集成。由此产生的集成噩梦通过许多修改、修复和临时操作得以解决。大多数这些“修复”在集成阶段一完成就被抛弃了 - 大多数开发人员忽视了这些“修复”，因为它们对组件的核心能力并没有什么贡献。

集成挑战的根本原因之一是不同的概念、想法和软件设计，而这又是在转型之前的体系所造成的。在仓促合并仓库的过程中，这些问题都没有得到解决（请参见[仓促合并的仓库](#a-rushed-merging-of-repositories)）。

为什么*管理者*没有解决设计问题？他们的主要关注点是让所有开发人员再次进入直接的专业（和职能）控制，这意味着关注将断开和不同的代码连接起来，而不是和谐一致的设计和概念。此外，这些管理者由于现代大型软件开发经验有限，对解决这些难题有些过度自信。

为什么*开发人员*没有解决设计问题？ADD的大多数开发人员的指导原则是他们的组件，因为正如所讨论的，他们大多按组件团队而组建，没有合作创建有紧密结合大规模产品的经验。

### Not Asking the Right Questions 没有提出正确的问题
宝马集团过去将其大部分软件开发外包。ADD是宝马公司第一个现代化且真正大规模的开发。因此，*ADD提出方向性的问题以驱动良好的长期软件设计的经验和能力都很有限*。

为什么设计好的软件产品需要提出好的方向性问题？这些问题引发并界定了产品的当前和未来使用、当前和未来的灵活性、当前和将来的挑战。拙劣的问题分散了时间和精力。通常，只有通过经验、领域洞察力、多样性、足够的预见性和对市场的把握，才能将好的问题与拙劣或没有帮助的问题区分开来。

哪些系统动态会导致ADD提不出好的方向性问题？非常强调*外包软件相关的工作*造成了这种能力的缺失。宝马集团试图分析问题领域，将问题分解为子问题，并将其交给供应商。这带来的影响是：（1）通过将问题空间分割成更小的块，失去对原始问题跟踪的风险是巨大的（特别是当自动驾驶的成熟整体解决方案实际上还没有找到），（2）丧失了从“更底层”领域来解决原始问题的机会，（3）拆分导致次优解决方案，（4）拆分导致狭隘思维模式。

## Green Build 绿色构建
A “green build” is a combination of (1) completed integration, (2) completed automated code quality checks without any faults, and (3) all completion of all prescribed tests (unittest, integration tests, integrated tests, (sub)system tests) without detecting any faults. The “green build” indicator is therefore an expression of the organization’s ability to produce a product continuously and therefore its capability of generating strong and salient feedback for learning and adapting, and... potential revenue.
“绿色构建”是（1）完成的集成，（2）完成的自动化代码质量检查，没有任何错误，以及（3）完成的所有规定的测试（单元测试、集成测试、集成试验、（子）系统测试），没有任何错误。因此，“绿色构建”指标是组织持续开发产品的能力、以及为学习和适应提供强大且重要反馈的能力，和潜在收入的表现。

#### Build System Before the Change 转型前的构建系统
Before the beginning of the adoption, the groups were organized for independent work ([Figure 24](#fig024)) which was reflected in their code bases as well as their build systems. They simply stitched build artefacts together which only occasionally worked due to integration issues.
在开始转型之前，各个组是按独立的工作所组织起来（[图24]（#fig024）），这反映在他们的代码库和构建系统中。他们只是简单地将构建工件缝合在一起，由于集成问题，这些构建工件偶尔运行。

**Key point**: Not every component-build or piecewise-build leads to agile end-to-end development discipline with short feedback.  **关键点**：并不是按组件构建或分段构建就会导致敏捷端到端开发的反馈链路短。

With the rushed merging of code repositories ([Merging Repositories](#a-rushed-merging-of-repositories)) the build system had to be subsequently changed. Revealing inconsistencies in build processes, tools, and infrastructure.
随着代码库的仓促合并（[合并仓库]（#仓库仓促合并）），构建系统随之必须进行更改。这显示出构建过程、工具和基础设施的不一致性。

### Evolving the Build System 升级构建系统
Another sign of the lack of skill was the difficulty of getting a new effective build system in place. It took several external experts and veterans of software-based product development to get across that “never change a running system”, which is deeply ingrained in some BMW Group’s managers, is one of the surest (if not fastest) way to *get stuck* also applies to build systems.
缺乏技能的另一个迹象是难以建立新的有效构建系统。几位外部专家和软件开发的资深人士了解到，“不要对能运行的系统进行改动”在宝马集团的一些管理人员中根深蒂固，这是最明显（如果不是最快的话）的导致工作“卡住”的方法之一，构建系统也是如此。

*The crucial part of a good build system: it provides fast feedback on the integration of the product*. Even if multi-stage build techniques are applied. *一个好的构建系统的关键是：它能提供关于产品集成的快速反馈*。即使是用了多阶段构建。

Why did the PO, APO, and management stick to the old insufficient build system? Partially due to the habit of management at BMW Group that views everything as a project. The tendency of thinking projects implies thinking in terms of: a start, an end, and nothing in between. This thinking discourages frequent feedback, and therefore encourages thinking of a fast integrated feedback as waste.
为什么PO、APO和管理层坚持旧的非充分构建系统？部分原因是宝马集团的管理层习惯将一切都视为一个项目。按项目方式意味着从以下方面进行思考：开始、结束，中间没有任何东西。这种想法不鼓励频繁反馈，因此快速集成反馈的想法被视为浪费。

Why hadn’t there been any movement from the developers to improve the build system? Here are several aspects at play: (1) The personal incentivization plan (IPA) didn’t favor such activities unless a manager had been convinced prior, (2) the work of the developers was optimized for working in isolation, (3) the developers had been tasked with details rather than a product, (4) they hadn’t been developers for the most parts, but researchers with focus on their research topic, and (5) there had been very few developers that had experienced the pleasure of fast integrated feedback from a good build system. In addition to that (6) exchange with other groups was mostly on research topics and not on product development topics.
为什么开发人员没有采取任何行动来改进构建系统？有几个方面：（1）个人激励计划（IPA）不支持此类活动，除非事先说服了管理者，（2）开发人员被按照独立工作进行优化，（3）开发人员被分配的是任务细节而不是产品需求，（4）大多数都不是真正开发人员，而是关注在学术问题上的科研人员（5）只有极少数开发人员体验过好的构建系统带来快速集成反馈的乐趣。除此之外，（6）与其他小组的交流主要是在科研主题上，而不是产品开发相关。

Why hadn’t there been more guiding conditions to align on integrated product development by management? Foremost, management at BMW Group thinks in terms of departments, not in products. Even vehicle projects are thought of (1) projects and (2) which department is working on. Only with several [LeSS for Executive](https://less.works/courses/less-executive) trainings this started to change at ADD. The vice president of ADD started several months after the start of the adoption, insisting on reviewing the Sprint result in the vehicle—this got the “Build and Integration” Community started and searching for better alternatives to the old build system.
为什么管理层在集成产品开发方面没有更多的指导呢？首先，宝马集团的管理层从部门而不是产品的角度思考问题。即使是车型项目也被认为是（1）项目和（2）哪个部门正在做。在几个管理者参加过LeSS for Executive(https://less.works/courses/less-executive)培训后，ADD开始改变。在转型开始几个月后开始，ADD的副主管持续Review车上Sprint的成果，这使得“构建和集成”社区开始开展，并寻找替代旧构建系统的更优方案。

One interfacing department tasked by upper management with integrating code to the vehicle was experimenting with [Bazel](https://bazel.build/), so Bazel was the prime candidate to replace the old build system.
负责将代码集成到车辆的一个接口部门正在尝试[Bazel](https://bazel.build/)因此，Bazel是替换旧构建系统的主要候选。

#### Under the Radar 在雷达下（未被注意到）
The proof of concept was done under the radar, meaning it hadn’t been on the Product Backlog. Why was it needed to do it this way?
概念验证是在雷达下完成的，这意味着它不在产品待办列表中。为什么要这样做？

In a healthy Scrum and LeSS environment, the Product Backlog consists of improvements and items to be implemented. The process of getting anything into the Product Backlog at that time was heavily influenced by the previous working model, meaning: project requirements, project managers, and very special non-development individual contributed items.
在一个健康的Scrum和LeSS的环境中，产品待办事项由改进和需要实现的条目组成。当时，将什么内容纳入产品待办列表的过程受到以前工作模式的严重影响，即：项目需求、项目经理和非常特殊的非开发项的个人条目。

Also, in a healthy Scrum and LeSS environment, there is no need to discuss technical details with PO, APO, or managers apart from implications regarding features and the product. So, no need for Product Backlog so-called ‘items’ for refactoring or experimenting with technical details.
此外，在一个健康的Scrum和LeSS的环境中，除了功能和产品之外，不需要与PO、APO或经理讨论技术细节。因此，产品代办列表中无需建立所谓的重构或者带技术细节的实验条目。

Why did the teams seek approval from their APO for this kind of technical work? In a research-heavy environment, the need for qualified data to prove a point or starting an approach is high by peers, APOs, and management. Generating qualified data is time consuming, in the case of evaluating an alternative build tool, its potential and weaknesses, it requires forking and migrating a relevant piece of the code base. This is nothing that can be done with one hour a week of playing around, but takes a significant fraction of the team's capacity. When talking about “a significant fraction” the BMW Group’s company culture calls for approval from “higher” authority. In a Large-Scale Scrum environment, the (A)PO appears like such a higher authority, even as this (A)PO should not be concerned with technical details.
为什么团队要寻求APO对此类技术工作的批准？在重科研的环境中，同行、APO和管理层都非常需要合格的数据来证明一个观点或开始一种方法。产出合格的数据非常耗时，在评估替代构建工具的可行性和缺点时，需要fork开分支和迁移代码库的相关部分。这不是一周一个小时就能完成的事情，而需要花团队的很大一部分时间。当需要花“很大一部分”时，宝马集团的公司文化是需要“更高”管理层的批准。在大规模Scrum环境中，（a）PO看起来像是一个更高的管理层，即使这个（a）PO不应该涉及技术细节。

What is the consequence of having such research and exploration tasks solely on the team’s Sprint Backlog without reference to the transparency of the Product Backlog? Normally, small research and refactoring tasks resided only in the Sprint Backlog (rather than the Product Backlog) without any hassle, because they would just create lots of minor noise for the PO or APO in the context of large-scale development, which has so many of these minor tasks every Sprint, forever. On the other hand, as explored in the LeSS guide “Handling Special Items” [[3](#references), p. 207], *big* “engineering improvement” or research tasks that involve *major* investment decisions or that *beneficially educate* the PO or APOs, or that lead to *useful conflict* discussions with the teams, are worth putting into the Product Backlog. The difference here is (1) magnitude of change, (2) familiarity with the change, and (3) implication on company processes. Changes in this area are not common and therefore require additional learning from anyone working on this item. Bypassing the Product Backlog shortened the normal learning, validation, and improvement mechanism. The consequence of this “avoid the walking and talking to APO” and putting this task into the Product Backlog, are delays, disappointments, frustrations, and magnified confusion.
将这些研究和探索任务单独放在团队的Sprint待办列表中，而不是放在产品代办列表中去体现透明度，会产生什么后果？通常，小型研究和重构任务只存在于Sprint待办事项（而不是产品待办事项）中，没有任何麻烦，因为在大规模开发的背景下，它们只会给PO或APO带来许多小噪声，因为大规模开发在每次Sprint中永远都有些小任务。另一方面，如LeSS指南“处理特殊条目”[[3]（#references），第207页]中所述，*大型“技术优化”或涉及*重大*投资决策或*有学习收益*的研究型任务，或能够给团队创造*有益冲突*讨论的条目，都值得纳入产品待办事项列表。这里的区别在于（1）变化的幅度，（2）对变化的熟悉程度，以及（3）对公司流程的影响。这部分的变化并不常见，因此需要从从事这一部分的人那里得到更多的学习。绕过产品代办列表缩短了正常的学习、验证和改进机制。这种“避免与APO交谈”并将这些任务放入产品待办列表的结果是带来延迟、失望、沮丧和更大的混乱。

Why did the team think it is a good idea to put this experiment under the radar instead of putting it into the Product Backlog? ADD’s PO and APO have a heavy focus on incremental features rather than the product-as-a-whole. Is there a difference? *In terms of the product, there is no difference; in terms of a product’s feature catalog that had been agreed upon with the upper management, the board, marketing, and other departments, there is a great difference between features and the product*. In other words: the APOs in ADD at that time did a local optimization for outputting features in isolation, but not features in a viable product... that can be viably built with a good build system.
为什么团队认为把这个实验放在雷达下、而不是放在产品待办列表中是个好主意？ADD的PO和APO重点关注增量功能，而不是整体产品。这两者有区别吗？就产品而言，没有区别；就与上层管理层、董事会、市场营销部和其他部门约定的产品功能清单而言，功能与产品之间存在很大差异。换句话说：当时ADD中的APO进行了局部优化，以单独输出功能，但不是可以通过良好的构建系统进行构建的可行产品中的功能。

The difference plays out here in a way that at that time, almost no “special items” were present in the Product Backlog. And the process of getting potential items for the Product Backlog was designed only for *feature*-related items. So, the fear of the development team was, if they started the walk to the APO for this particular experimentation item, they would be postponed until after SoP and therefore postponed... for about *two years*. Another classic “faster is slower” dynamic, aggravated by management without an understanding of modern build systems or modern building of large-scale software, when the aim is adaptiveness.
不同之处在于，当时产品待办列表中几乎没有“特殊条目”。产品待办列表中增加潜在条目的过程仅针对*功能*相关条目而设计。因此，开发团队担心的是，如果他们开始为这个特定的实验条目与APO进行讨论，这些实验条目会被推到SoP之后考虑，大约是当时的两年之后。另一个经典的“快即是慢”情形，由于管理层不了解现代构建系统或大规模软件的现代构建，当目标需要适应性时，这种情况会加剧。

This situation also highlights the entanglement of technical transition and organization, insufficiently utilizing the idea of Communities, and the miss-practice of utilizing teams up-to 100% (see “Avoid...Fake queue reduction by increased multitasking or utilization rates” [[1](#references), p. 99]). Later, Scrum Masters with the support of the teams, pushed that Communities contribute Product Backlog items and eventually are heard by PO and APO about their opinion on ordering regarding other Product Backlog items.
这种情况还突出了技术变革和组织之间的牵扯，没有充分利用社区的理念，以及将团队使用率达到100%的错误做法（见“避免...通过增加并行任务或利用率带来虚假的等待队列减少”[[1]（#references），第99页]）。后来，Scrum Masters在团队的支持下，通过推动社区来贡献产品待办列表，PO和APO听取了他们的意见并与其他产品待办条目进行排序。

#### "Rogue” Unofficial Group “流氓”非正式团体
After presenting the promising results of an experimental build system to APOs individually, interest was raised, but due to an initial estimate of 2-3 Sprints to complete the migration, no Product Backlog item was created and there was no Product Backlog refinement to improve the estimate. To the credit of the APO, they believed their developers; but they didn’t confirm the understanding of the developers regarding scope, process-integration, influence on the working environment, migration effort, and central infrastructure—despite the obvious too-small estimation.
在分别向APO展示了一个实验性构建系统充满希望的结果后，大家的兴趣提升了，但由于初步估计需要2-3次Sprint才能完成迁移，因此没有创建代办条目和进行代办列表梳理来改进估算。APO相信他们的开发人员，尽管估算明显偏低，他们没跟开发人员确认对范围、流程集成、对运行环境的影响、迁移工作量和整体基础设施的理解。

As a result, no APO maintained the build-system experiment in focus. As a consequence, there hadn’t been any team dedicated to this experiment. Only some developers from different teams joined and worked on this topic. This time with keep-me-informed by some APOs.
因此，没有APO将构建系统实验当成重点。结果，没有任何团队专注在构建系统实验。只有来自不同团队的一些开发人员加入进行相关工作。这一次，一些APO说随时将情况告知他们。

#### Management Push 管理层推动
The accumulation of shortcomings reached at some time “real” management attention. Management finally acknowledged more decisive support, which led to the creation of three temporary groups with dedicated focus:
问题的积累在某个时候引起了“真正”管理层的关注。管理层最终认可了投入更多关键支持，这引发成立了三个专注于以下方面的临时小组：

* Complete migration from catkin and cmake to Bazel 从catkin和cmake完全迁移到Bazel
* Improve build speed 提升构建速度
* Stabilize build reliability 将构建的可靠性稳定下来

**Key point**: Avoid creating new (temporary) structures; prefere providing clear focus and abilities to inquire support for existing teams. **关键点**：避免创建新的（临时）架构；给现有团队提供重点关注和能力，以及支持。

By assigning these tasks to temporary groups instead of permanent feature teams, management constrained their organization to learn. In a healthy LeSS environment, experts would be invited by the tasked feature team to work on the new topic and learn from the expert to the extent that the feature team can then maintain the system or even improve it on their own. Experts may be external or internal [Travelers](https://less.works/less/framework/coordination-and-integration#Travelerstoexploitandbreakbottlenecksandcreateskill).
通过将这些任务分配给临时工作组而不是长期特性团队，管理层限制了组织的学习。在一个健康的LeSS环境中，遇到新课题时特性团队将邀请专家加入，并向专家学习，以便特性团队能够维护系统，甚至自己改进系统。专家可以是外部专家也可以是内部专家[旅行者](https://less.works/less/framework/coordination-and-integration#Travelerstoexploitandbreakbottlenecksandcreateskill).

Why did management staff those temporary groups with members from a variety of feature teams? APOs are committed by their IPA to certain feature completion delivery at the end of a release, if complete feature teams would be committed to improve the build issues, the associated APOs would fail on their personal incentivization plan.
为什么管理层要为这些临时小组配备来自各个功能团队的成员？APO通过他们的个人绩效来承诺在发布时能交付哪些功能，如果某个功能团队花精力改善构建问题，那么这个团队的APO将无法完成其个人绩效计划。

Also, the behavior of forming temporary groups reveals the mental pattern of classical project management of “throwing experts at the problem to solve it,” which only solves the issue in the short term. LeSS, on the other hand, advises the route of *setting the right conditions for those issues to be fixed long-term*.
此外，组建临时工作组的行为也体现出了经典项目管理的思维模式，即“让专家来解决问题”，这只能解决短期问题。相反，LeSS建议采取“为长期问题的解决创造相应条件”的路线。

#### It Is Not My Build System 这不是我的构建系统
One fascinating dynamic was that most developers did not consider contributing to solve build system issues. The reasons for that lie mostly in the organizational system in place before. Before, there was strong separation of responsibilities and accountabilities. Team A is responsible for road modeling, team B from braking, and so on, and also Team Z for the build scripts; and even a complete department dedicated to build-related issues. This enforced the mindset of “it is not my job”.
一个有趣的动态是，大多数开发人员之前都没有想过为解决构建问题做出贡献。其原因主要在于之前的组织体系。在此之前，责任和义务有着很强的割裂。团队A负责道路建模，团队B负责制动，团队Z负责构建脚本等等；甚至有一个专门辅助构建相关问题的部门。这强化了“这不是我的工作”的思维。

Therefore, it is remarkable that developers started consenting to their coworker’s proposals in that area. *It reflects a change in company culture: accepting peer-generated proposals is essential*.
因此，值得注意的是，开发人员开始接受其同事的建议*这反映了公司文化的转变：接受同行提出的建议至关重要*。

From a LeSS point of view: this demonstrates the difficulty in taking ownership in a company’s culture not yet fully transformed. The adoption of communities as a utility to self-manage on a multi-team level was (and still is) in progress.
从LeSS的角度来看：这表明了在尚未完全转变的公司文化中承担责任感的困难。将社区作为在多团队层面上进行自我管理的做法已经（并且仍在）在进行中。

### Lack of Manager Support for a Green Build Solution 缺乏管理者对绿色构建解决方案的支持
Given that the build is neither a product feature nor a technical detail within the product, who is responsible and why didn’t they act? Managers are responsible to create an environment that empowers teams to build the product and take accountability on removal of impediments that surpass the powers of the teams—therefore managers are accountable for the build.
鉴于构建既不是产品特性，也不是产品中的技术细节，那么谁是负责人以及为什么他们不采取行动？经理有责任创造这样的环境，让团队有能力构建产品，并负责移出团队能力范围外的障碍，因此，经理对构建负责。

In the past many BMW Group’s managers outsourced this responsibility and therefore lost insights and ability to improve the build system. Some ADD’s managers cared enough for the build and struggled with scheduling tasks. Why? ADD is new to the concept of self-management of teams, therefore it faced confusions on how to handle such situations. Challenges such as (1) who is responsible for detecting issues with the build system, (2) where to report those issues, (3) who is responsible for proposing and finalizing solutions, and (4) how to get any solution implemented.
过去，许多宝马集团的经理将此责任外包，因此失去了改进构建系统的洞察和能力。一些ADD的管理人员对构建非常关心，但在安排任务上却很艰难。为什么会这样？ADD刚接触团队自管理的理念，因此在如何处理此类情况方面面临困惑。挑战包括（1）谁负责检查构建系统的问题，（2）在哪里报告这些问题，（3）谁负责提出并最终确定解决方案，以及（4）如何实现解决方案。

The struggle originates in the old organizational systems, its formal structure, and the company culture it had cultivated. Traditionally managers would be assigned, in the new model enthusiasts are to sense and respond on their own. LeSS advocates the structural element of “Communities” to support the self-management on cross-team level. The “Build and Integration” Community was founded a few weeks after the beginning of the adoption. Still, the company culture was slowly changing which resulted in several other consequences, more on this in chapter [Communities](#communities).
这种艰难源于旧的组织制度、架构和它所培养的公司文化。传统上，管理者是被指派的，在新的模式中，感兴趣的人会自己察觉并做出反应。LeSS倡导“社区”的结构元素，以支持跨团队层面的自管理。“构建和集成”社区是在转型开始后几周成立的。尽管如此，公司文化的转变仍在缓慢，这导致了其他一些后果，更多内容见第[社区]章（#社区）。

### Component Build and Code Structure is Coupled to Builds 组件构建和代码结构与构建耦合
Another core aspect of a Green Build is the actual code, its structure, and usage by tests. In an environment that continuously modifies the code base, a strong emphasis rests on its structure, readability hence understandability, and ease to evolve. Following the struggles of the code base’s origin, neither the structure, nor the understandability, nor the ease to evolve is a given at ADD.
绿色构建的另一个关键在于实际代码、其结构和测试使用。在一个不断修改代码库的环境中，需要重点关注其结构、可读性、易懂性和易修改性。在初始代码库的之后，ADD既没有给出结构，也没有给出可理解性，也没有提供易于修改的特性。

The highly-coupled components created by component teams with weak skill to collaborate and evolve a good overarching design, complicated the creation of true unit test, true component test, and true component builds. The consequence led to long-running and error-prone builds and tests. Several technical approaches to fix this situation had been tried, but failed as they didn’t tackle the root cause.
组件团队创建的高度耦合组件不易于协作和良好总体设计的演进，这让创建真正的单元测试、真正的组件测试和真正的组件构建的变得复杂。结果导致了长期运行且容易出错的构建和测试。已经尝试过几种技术方法来解决这种情况，但都失败了，因为它们没有解决根本原因。

Why was there more focus on components, rather than collaboration or the overall product? The answers vary but are typically (1) classical motivation, and (2) research-like focus and mastery in single topics which materialize as components.
为什么更多地关注组件，而不是协作或整体产品？答案各不相同，但通常是（1）经典动机，以及（2）专注在科研类主题和对单个主题的精通，这些主题变成了组件。

Why hadn’t management requested focus on collaborative components and the product? Managers didn’t directly prohibit needed deep changes, but the context they provided left little room for deliberation processes, re-designing the code base, and tests. Another classic of “faster is slower” dynamic, aggravated by management without an understanding of modern build systems or modern building of large-scale software, when the aim is adaptiveness.
为什么管理层没有要求关注组件协作和产品？管理者并没有直接禁止必要的深度更改，但他们提供的环境几乎没有给流程、重新设计代码库和测试留下空间。另一个经典的“快即是慢”动态模式，在目标是适应性的情况下，由于管理层不了解现代构建系统或大规模软件的构建，这种动态模式变得更严重。

Would a technical-complexity-control manager have prevented or solved this situation? The question in itself reveals a deep misunderstanding of the system dynamics: Technology (usage of technology for implementing a thought) is only one part of the dynamic; people, organization, and processes are the major parts. Thus, *the framing of the question already diverges from an appropriate solution*. Aside: the question also reveals a confession, that they (1) lack Go See, and (2) lack experience in modern large-scale adaptive development.
如果是懂技术且能管理复杂状况的经理会阻止或解决这种情况吗？这个问题本身揭示了对系统动态的严重误解：技术（使用技术实现某个想法）只是动态的一部分；人员、组织和流程是主要部分。因此，*问这个问题已经偏离了合适的解决方案*。此外：这个问题也揭示了，他们（1）缺乏Go See实地观察，（2）缺乏现代大规模适应性开发的经验。

### Long-Living Branches 长期存在的分支
<a name="fig025"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig025.png" alt="Dynamics of a Green Build is influenced by developers' ability to integrate and test changes fast and frequently.">
  <figcaption>Figure 25: Dynamics of a Green Build is influenced by developers' ability to integrate and test changes fast and frequently.</figcaption>
</figure>

ADD’s developers with their limited experience in large-scale development and limited experience in skillfully designing large-scale software systems struggled working on one branch. Their past working structure fostered working on separate code bases (and repositories). The [rushed merge](#a-rushed-merging-of-repositories) didn’t change the fundamental developer’s experience so they continued to struggle working on one branch with hundreds of teams.
ADD的开发人员在大规模开发方面经验有限，而且在熟练设计大规模软件系统方面经验也有限，因此他们在单分支上开发很艰难。他们过去的工作结构促使了在各自单独的代码库（和仓库）上工作。[仓促合并]（#a-rushed-merging-of-repositories）并没有改变开发人员的基础经验，因此数百个团队继续在一个分支上艰难工作。

This inability to collaborate effectively on one branch leads to many long-living branches. Why? First, the old system fostered single-minded excellence in components which resulted in isolated code bases. The closest resemblance with isolated coded bases in a mono-repository are long-living branches. Secondly, most developers are actual researchers and no programmers. This leads to missing skills in design, coding, incremental developing software, and effective communication and collaboration in and via code.
无法在一个分支上有效协作导致了长期存在的分支。为什么？首先，旧系统养成了在组件上个体卓越，导致了代码库的孤立。与一个仓库内多个孤立代码库最相似的是长期分支。其次，大多数开发人员实际都是的科研人员，而不是程序员。这导致在设计、编码、增量开发软件以及通过代码进行有效沟通与协作方面缺乏技能。

The lack of sufficient modern experienced developers resulted in a systematic inability to self-educate on how to develop incrementally on a large code base with one branch.
由于缺乏足够的经验丰富的现代化开发人员，无法系统化地自我训练如何在单分支的大型代码库上进行增量开发。

<a name="fig026"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig026.png" alt="All subsequent merges of long-living branches to master incur a high likelihood of severe merge conflicts.">
  <figcaption>Figure 26: All subsequent merges of long-living branches to master incur a high likelihood of severe merge conflicts.</figcaption>
</figure>

The resulting huge and complex patches while merging those long-living branches to master (see [Figure 26](#fig026)), led to challenges for the already highly-loaded build system. Why? The previously discussed lack of component builds and tests led to whole system clean rebuilds and retests each time. Due to the group’s prior focus on components instead of units, many tests incurred running verification tests with time-consuming simulation.
在将这些长期分支合并到主分支时，产生了巨大而复杂的补丁（参见[图26]（#fig026）），这给已经高负荷的构建系统带来了挑战。为什么？前面讨论了缺乏组件构建和测试，导致了每次都要进行整个系统的重新构建和重新测试。由于小组先前关注的是组件而不是单元，因此许多测试都需要运行验证测试，这些验证测试需要跑耗时很长的仿真。

The long running builds were also one reason for long-living branches. Why? Due to cycle-times of 4-8h on avg. from push to red/green, many teams adopted the malpractice of accumulating many commits on their long-living branch and then trying to punch a merge to master-branch once a Sprint. A disaster, of course.
长期运行的构建也是长期分支存在的原因之一。为什么？由于从push到red/green的平均周期为4-8小时，许多团队采取了一种弊端方式，即在其长期分支上积攒了许多commit提交，然后每个Sprint完成时将他们一起合并到主分支。这显然是一场灾难。

One consequence of those complex big-batch once-a-Sprint merges were frequent red builds. Why? As soon as several long-living branches in a poorly-designed software system are merged, hard-to-avoid/resolve conflicts occur as the inconsistent design of the components is exposed. Each merge conflict requires manual correction and re-merging to master, which triggers the same pattern again, with just one commit less.
这些复杂的大批量一次性Sprint合并的后果之一是频繁出现红色构建。为什么？当几个长期分支合并到设计粗糙的软件系统中，就很难避免/解决冲突，因为组件的设计不一致暴露出来。每次合并冲突都需要手工修改并重新合并到主分支，这将再次触发相同的情况，只是commit少了一次。

#### Extensive Conformity Checks 大量的一致性检查
The not-owning-the-product mindset of many developers (driven from component teams and management behaviors) led to the system of builds enforcing extensive verification for conformity and testing its viability. Therefore, conformity rules ([Figure 27](#fig027)) and good development practice for large development on product level haven't been followed. This resulted in manager’s quick-fixing of the system, by introducing mandatory automated build steps for conformity and rule compliance for each build. Why for each build? Traditional management thinking is calling for *assigning responsibility for failure*, therefore each failure needs to be pin-pointed to one single individual.
许多开发人员不具备产品思维模式（在组件团队和管理行为的影响下），导致构建系统被迫执行大量的一致性验证及可行性测试。因此，没有遵循产品级大规模开发的一致性规则（[图27]（#fig027））和良好开发实践。这导致管理者通过为每次构建引入强制性自动构建步骤来检查一致性和合规性，以能够快速修复系统。为什么每次构建要这么做？传统的管理思想要求“为失败分配责任”，因此每个失败都需要具体到一个人。

BMW Group’s culture is to avoid “failures” (in builds and in other ways) and view them as a problem, rather than a culture of experimentation to fail fast and then to learn and adapt from “failures”.
宝马集团的文化是避免“失败”（在构建以及其他方面），并将其视为一个问题，而不是进行实验及快速失败，然后从“失败”中学习。

<a name="fig027"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig027.png" alt="Dynamics of build and test cycle times to team’s following standards.">
  <figcaption>Figure 27: Dynamics of build and test cycle times to team’s following standards.</figcaption>
</figure>

### Organizational Wizardry 组织“魔法”
#### The Quick-Fix Build Sheriff Reaction 权宜之计-构建警长
One management reaction to the build problems was to introduce a rotating *build sheriff* (manager) role. The quick-fix of adding this role led to increasing distance and offloading of responsibility to that role. Why?
管理层对构建问题的一种应对是引入一个轮换的“构建警长”（经理）角色。增加此角色的权宜之计导致了该角色责任的距离增加及压力减小。为什么？

Caring about the result of a team’s commit in a build is influenced by the duration of the build, and by who is responsible for problems. So, with the long build cycle and the build sheriff role, the caring and in turn the felt responsibility for the result decreased.
构建的时长及谁对问题负责会影响团队对commit结果的关心。因此，随着构建周期的延长和构建警长的角色，对结果的关心以及对结果的责任感也随之降低。

The decreased responsibility for build results resulted in quickly degrading builds. This was the opposite effect to that intended by the naive intervention of assigning a build manager to the task.
构建结果责任的降低导致了构建的质量快速下降。这与预想的分配一个构建警长的天真预期恰好相反。

The effect of reduced responsibility became only apparent with growing numbers of teams. As long as there had been only about 8 teams, the not-bad social connectedness between the teams prevented this dynamic. But with more teams, the weaker social connectedness and the discussed dynamic became apparent.
随着团队数量的增加，责任降低带来的影响才变得明显。当不到8个团队时，团队之间良好的连接能防止这样的状况发生。但随着团队数量的增加，连接变弱那么责任降低带来的影响就变得明显了。

Neither managers nor developers learnt that putting a manager (or a tool) between responsibility and the teams degrades the process of taking ownership and responsibility for the whole product.
无论是经理还是开发人员都没有认识到，将警长/经理（或工具）置于责任和团队之间会降低整个产品的主人翁精神和责任。

#### Highlight Blame and the Dynamics which Follows 指责和随之而来的动态
The line between transparency and blame is thin and easily crossed with a build monitor that highlights the particular team that pushed last before a failed build. The official phrase was “Stop and Fix assigned Team”—the designated team that broke the build (based on green-red transition on the build monitor) which lasted until the build was green again. The intent was for transparency and reducing the load of email received every day. Unofficially, all developers who cared for the build were annoyed that a broken build wasn’t fixed ASAP and wished for more public pressure to fix the broken builds.
透明性和指责之间的界限很薄，并且很容易与构建显示器一起发挥作用，显示器能显示在构建失败之前最后提交代码的是哪个特定团队。正式说法是“停止并修复”，即破坏构建的那个团队（基于构建监视器上的由绿到红转换），该团队一直修复到构建再次变绿。其目的是为了提高透明度，减少每天收到的电子邮件数量。非正式下，所有关心构建的开发人员都会对一个损坏的构建没有尽快修复感到恼火，并希望能有更多的公众压力来修复损坏的构建。

The blame-casting doesn’t work on root cause (missing whole product focus), it only highlights the complexity of the system, delayed feedback from the build system, developers’ focus on components rather than the product, insufficient software design, and missing meaningful component builds and tests.
推卸责任并不能解决根本原因（缺少对整个产品的关注），只突出了系统的复杂性、延迟了构建系统的反馈、开发人员关注在组件上而不是产品、软件设计不足以及缺少重要的组件构建和测试。

The blame-casting induced an interesting other dynamic: as soon as the first team “A” (unintentionally) triggered a green-to-red transition, other teams increased their merge and push frequency. Why? First, due to long and sometimes non-linear merge processes of the auto-merge procedures on the build system, team A may not be responsible for the transition to red. Regardless, by setting the blame on team A, other teams *pushed their commits, concealed within team A’s blame*. They didn’t fear being held responsible for a potential build degradation, as the build was already red. *This contributed to the practice of delaying pushes until the first team had been assigned the blame*.
推卸责任引发了另一个有趣的动态：当第一个团队“A”（无意中）触发了从绿色变到红色时，其他团队在此时增加了合并和推送的频率。为什么？首先，由于构建系统上自动合并的过程很长，有时甚至是非线性的，团队A可能不是造成导致变成红色的原因。不管怎样，通过将责任归咎于团队A，其他团队*提交代码，并在团队A被指责时被掩盖住*。他们并不害怕承担构建可能出现降级的责任，因为构建此时已经是红色的。*这导致了延迟提交代码的做法，直到某个团队开始被指责*。

By introducing a technical system to assign blame, the dynamics led to an even more occluded situation. *At times, those liberated phases of ignoring build status led to amazing collaboration across teams and code-wise integration; at other times, the whole system simply choked*.
通过引入一种技术体系来分配指责，这种动态导致了一种更加封闭的局面*在不在乎构建状态的开放阶段，跨团队间的协作和代码级集成是惊人的；在关注构建状态的时候，整个系统都是阻塞的。

The naive call from traditional management to simply “stop the line” until the build is restored was rarely heard. ADD’s managers quickly realized that stopping all work would only degrade the situation as changes accumulate on long-living branches. In addition, prohibiting hundreds of teams to work is prohibitively expensive. The corollary to Toyota’s “stop the line” philosophy: *fix the root cause*, was not realized by ADD’s managers or developers.
传统管理层发出“暂停工作”直到构建恢复的天真呼吁，却很少有人听。ADD的经理们很快意识到，暂停一切工作只会使情况恶化，因为长期分支上积攒了代码变更。此外，让数百个团队停下工作的成本高得令人望而却步。丰田“暂停生产线”理念的推论是：“修复根本原因”，ADD的经理和开发人员并没有意识到这一点。

### Don’t Focus on Not-Red—Focus on Green 不要关注非红色，关注绿色
All of the above experiments, processes, and technical aids focus on “not-red”; all of them failed. Why did they fail? They did not focus on the one thing that matters; rather, they focused on avoiding weaknesses.
所有上述实验、流程和技术支援都关注于“非红色”；但都失败了。为什么他们失败了？他们没有关注在重要的事情；相反，他们专注于避免短处。

Why didn’t ADD strengthen “caring” and foster “ownership for the product” within the employees more?
为什么ADD没有更多地加强对员工的“关心”和“对产品的责任感”？

Among other reasons, there are several major systemic root causes: (1) the C-level chosen organization setup of ADD as a department within BMW Group incurred several constraints (e.g., company mindset of outsourcing and its ramifications, company culture “excellence in details (component) not the whole (product)”, procurement processes, vendor collaboration paradigms, HR policies), (2) the staff composition, the resulting attitude, and conformity to company culture, and (3) unchanged policies in HR and vendor-collaboration on all levels.
在众多原因中，有几个关键的系统性原因：（1）ADD作为宝马集团内部一个部门，董事层在设计组织时受到局限（例如，公司外包理念及其影响、公司文化“注重细节（组件）而非整体（产品）”、采购流程、供应商合作模式、人力资源政策），（2）员工组成、由此产生的态度和跟公司文化的匹配性，以及（3）各级人力资源和供应商合作政策不变。

The unchanged HR policy of personalized bonus system with focus on components and specialties contradicts the required skills of large-scale, adaptive products. *Modern product development of large, complex, and adaptive systems is no longer a matter of excellence on single-focus execution but a multi-learn/skill of quick adaptation on the product level goals*. The HR managers, which are in a separate reporting line than ADD, discarded all arguments for a bonus system based on product success; they measured and rewarded local optimizations by individual managers and developers, not global optimization.
保持不变的人力资源政策依然是以组件和专业为重点的个人奖金体系，这与大规模、适应性产品所需的技能相矛盾。*大型、复杂和自适应系统的现代产品开发的关键不再是个体优秀，而是针对产品目标进行快速适应的学习/技能*。HR经理属于ADD外的独立汇报线，他们放弃了产品成功为基准的奖金制度；他们通过度量及奖励个体经理与员工进行局部优化，而不是全局优化。

The unchanged vendor-collaboration policies led to the same uninsightful execution of thrown-over-the-wall tasks. ADD didn’t acknowledge the possibilities of the changes in procurement processes, and instead just introduced a new middleman role to try to quick-fix the unskillful collaborations.
保持不变的供应商合作策略导致了同样无意识地将任务传递过去就不管了。ADD没有意识到采购流程改变的可能性，而是引入了一个新的中间人角色，来试图快速修复合作不熟练。

The by-design tight control from C-level managers posed another constraint. The choice to operate ADD as a department within BMW Group, would have still left options. For example, different wage agreements, independent HR policies, and more liberal processes. But the C-level managers discouraged this level of change in their organization.
董事层的严格管控造成了另一个局限。ADD被作为宝马集团内的一个部门来运营，但仍有其他不同的方式。例如，可以有不同的工资体系、独立的人力资源政策和更自由的流程。但是，董事层不允许在他们的组织内做这种层级的改变。

## Communities 社区
### Mandated and Mandatory Communities 强制和必要的社区
Following “the past is part of the present” many teams demanded formal procedures for cross-team decisions. This reflects that behavioral changes in large organizations are influenced by structural changes ([Larman’s Law #5](https://www.craiglarman.com/wiki/index.php?title=Larman%27s_Laws_of_Organizational_Behavior)), but unlike the structural changes, behavioral changes aren't realized immediately. This (temporary) need gave rise to the idea of “mandated communities” and “mandatory communities”. Both contradicting the idea of volunteering and definition of Communities. To explain: mandated communities can make decisions for the whole development group (which contradicts “Communities cannot make decisions for the teams, but they can produce something that the teams decide to adopt” [[3](#references), p. 296]); mandatory communities are mandatory to attend for representatives of all development teams (which contradicts “Participation in Communities is completely voluntary” [[3](#references), p. 295]).
依照“过去亦是现在的一部分”，许多团队要求制定正式的跨团队决策流程。这反映出大型组织的行为变化受到组织结构变化的影响（[Larman定律#5](https://www.craiglarman.com/wiki/index.php?title=Larman%27s_Laws_of_Organizational_Behavior))但与组织结构变化不同的是，行为变化不会立刻体现出来。这种（暂时的）需求产生了“强制社区”和“必要社区“的概念。这两者都与自愿的理念和社区的定义相矛盾。解释：强制社区可以做出整个开发团队的决策（这与“社区不能为团队做出决策，但他们可以产出东西由团队决策采用”[[3]（#参考），p.296]相矛盾）；强制社区要求所有开发团队必须有代表参加（这与“社区参与是完全自愿的”[[3]（#参考文献），第295页]相矛盾）。

Why does volunteering have significance in Communities? (1) the openness for sharing and learning, high-value collaboration and contribution is higher in a volunteering (or at least not-forced) setup than a forced setup, and (2) volunteering members are more motivated to share and explain recommendations, and are more invested in adjusting recommendations to actual teams and use. The corollary is: if management feels the need to revert to a forced setup, the investments in compliance checks (e.g., conformity builds), process-supported compliance boards, explicit proclamation of new standards, etc. increase.
为什么自愿参加在社区中具有重要意义？（1） 在自愿参加（或至少不是强制）环境中，分享和学习、高价值协作和贡献的开放度高于强制环境，并且（2）自愿的成员更愿意分享和解释建议，更愿意根据实际团队和使用情况调整建议。由此得出的结论是：如果管理层认为有必要回到强制的方式，那么一致性检查（如构建一致）、流程的合规委员会、新标准的明确公告等方面的投入就会增加。

Please note the difference between community and Community. 请注意社区(community)和团体(Community)是有区别的。

Examples of mandated community: *software architecture* community and *build and integration* community; example of mandatory community: *simulation* community.
强制性社区示例：*软件架构*社区和*构建和集成*社区；必要性社区示例：仿真社区。

To make the voting in mandated communities “meaningful”, the concept of “core member” and quorum was introduced. To make the community meetings “meaningful”, an appointed facilitator was nominated, and prepared agendas on fixed schedules were sent out in advance. And to make the communities “consequential and meaningful” a manager was formally appointed but never present. The structure of these “communities” reflected much of the old BMW Group’s classic working group, with one change: no classical manager present. Developers' adherence to the decisions was meager in the first years.
为了使强制社区的投票“有意义”，引入了“核心成员”和法定人数的概念。为了使社区会议“有意义”，一位主持人被推选出来，并提前发送了按固定时间表制定的议程。为了使社区“具有重要性和意义”，正式任命了一名经理，但从未到场。这些“社区”的结构在很大程度上反映了宝马集团旧的的经典工作方式，只有一个不同：没有经理在场。在最初的几年里，开发人员对决策的遵守程度很低。

Why was the developers’ adherence meager? The abrupt shift from the self-management to the power-driven model with “mandated communities” conflicted with the slowly evolving adoption of self-management within the teams. The more the teams realized the freedom, responsibility, and accountability of self-management teams, the larger the resentments grew towards the command-driven “mandated communities”.
为什么开发者的遵守程度很低？因为突然从自我管理转变到权力驱动模式，强制社区与团队内部慢慢进化为自我管理相冲突。团队越是意识到自我管理团队的自由、责任和义务，对命令式的“授权社区”的不满就越大。

What led to the de-focusing of many developers from communities? Communities were increasingly perceived as places for formal discussions and decision-making rather than learning and achieving cross-team (functional) agreements. The lack of holistic product guidance by PO and APOs contributed to this perception. During forming and reforming of Requirement Areas, teams moved from one Area to another. On occasions, a community had members primarily from one Area. This directed topics inadvertently towards one Area’s focus, which complicated the acceptance of communities as places for cross-team and cross-Area learning and coordination. The *quick-fix of mandatory attendance* for mandated communities fixed only the issue of representation, not the root cause of missing the whole product focus in many developers.
是什么导致许多开发人员渐渐离开社区？社区越来越被视为正式讨论和决策的场所，而不是学习和达成跨团队（职能）约定的场所。PO和APO缺乏全面产品指引也导致了这个情况。在需求领域的形成和改进过程中，团队从一个需求领域转移到另一个领域。有时，某个社区的成员的大多数来自一个需求领域。这无意中把话题引向了该领域，这使得社区作为跨团队和跨领域学习与协作的场所变得更难。强制社区的“强制参加这个快速解决方案”只解决了有人参加的问题，而没有解决根因-许多开发人员拳法对整体产品的关注。

One important secondary aspect of communities and their decisions is the ISO 9001. The process-standard ISO 9001 was adopted by BMW Group for the whole group decades ago. The basic idea of the standard is to document important process decisions and demands following these decisions. ADD’s “Coaching and Standards department” mistakenly assumed that “mandated communities” produce these kinds of decisions. Therefore, the pure existence of “mandated communities” complicated the process of quality and process improvements at ADD.
社区及其决策的带来的间接结果之一是ISO 9001。几十年前，宝马集团为整个集团采用了ISO 9001过程标准。该标准的基本思想是记录重要的过程决策和相关需求。ADD的“培训与规范部门”错误地认为“强制社区”会做出此类决策。因此，“强制社区”的存在使ADD的质量和流程改进过程变得复杂。

Why did ADD’s “Coaching and Standards department” make this mistake? The (by design) close similarity of managed communities with BMW Group’s traditional working groups and its formal power to decide played an important role; from an external not-LeSS-informed auditor perspective, these structures are relabeled manager-driven working groups with the lack of joining managers. Therefore, the pure existence and definition of “mandated communities” and BMW Group’s demand for ISO compliance, led to the process: some decisions of mandated communities are relevant for ISO process changes and therefore needs to be documented, tracked, and followed-up differently.
为什么ADD的“培训与规范部门”犯了这个错误？社区与宝马集团传统工作组的相似性及其正式决策权在其中作用很大；从外部不了解LeSS的审计师角度来看，这些结构被重新定义为管理驱动的工作组，除了经理经理加入。因此，“强制社区”的存在和定义以及宝马集团对ISO合规性的要求导致了这一过程：授权社区的一些决策与ISO过程变更相关，因此需要以不同的方式记录、跟踪和跟进。

How did this mistake complicate the process of quality and process improvement? There are many aspects of how this complicated improvements: (1) the added “paper” process increased the disconnection from idea to effect (similar to the delay-feedback effect), (2) the increased distance from improvement idea to actual improvement disconnected potential contributors, and (3) the formal process discouraged improvement experiments. All this despite the effort of the “Coaching and Standards department” to make this lightweight and as unobtrusive as possible—the pure possibility and knowledge of these processes discourage many developers from proposing improvements.
这个错误是如何使质量和流程改进过程复杂化的？复杂化的改进有很多方面：（1）增加的“纸面”过程增强了想法与效果之间的脱节（类似于延迟反馈效应），（2）改进想法与实际改进之间的距离增加，使潜在贡献者退出，以及（3）正式的过程不利于进行改进实验。尽管“培训与规范部门”努力使其尽可能轻量级和不引人注目，但这些过程本事和知识阻止了许多开发人员提出改进建议。

For a better frame of reference: only a fraction of the decisions and processes produced by mandated communities are relevant for ISO; improvement experiments from Retrospective and Overall Retrospective are typically not relevant for ISO process changes. For example, mandatory information in commit messages and its format, mandatory data types to represent physical units, definitions and tools for testing, folder layout and file naming conventions.
为了获得更好的参考：只有一小部分由强制社区制定的决策和流程与ISO相关；回顾会和整体回顾会的改进实验通常与ISO中的流程变更无关。例如，commit提交消息及其格式中的必填信息、物理单元的必填数据类型、测试工具、文件夹布局和文件命名约定。

### Inflation of Communities 社区的膨胀
ADD inherited from BMW Group many HR policies, especially those for bonuses and career advancements. Some of these policies influenced the number and quality of communities.
ADD继承了宝马集团的许多人力资源政策，尤其是奖金和职业发展政策。其中一些政策影响了社区的数量和质量。

[Figure 28](#fig028) displays a not-so-obvious conflict between product, organization, and employee value.
[图28]（#fig028）显示了产品、组织和员工价值之间不太明显的冲突。

<a name="fig028"></a>
<figure>
  <img src="/img/case-studies/bmw-group-ad/fig028.png" alt="The Dynamics of Inflation of Communities.">
  <figcaption>Figure 28: The Dynamics of Inflation of Communities.</figcaption>
</figure>

Some additional context to understand the dynamics of [Figure 28](#fig028): in BMW Group, working groups and study groups are common. Those materialize on topics of concern and interest for the company. Typically, the facilitators are managers (or on the manager career track). So, being a facilitator has an influence on career advancement, personal bonuses, and salary level.
[图28]的一些额外背景（#fig028）：在宝马集团，工作小组和研究小组是常见的。这些都体现在公司关心和感兴趣的话题上。通常，推动者是经理（或在管理路线上的人）。因此，作为一名推动者对职业发展、个人奖金和工资水平都有影响。

Within LeSS, Communities are emergent structures for learning and coordinating with by-design low barriers for creating, changing, and removing Communities. This unrestricted process in combination *with unchanged HR policies*, appraisal procedures, career advancement models, and personal bonus systems, started a dynamic leading to more and more “communities”.
在LeSS中，社区是学习和协调的新兴结构，创建、更改和删除社区的障碍都很小。这种不受限制的过程加上*不变的人力资源政策*、工作评估流程、职业发展模式和个人奖金制度，开启了一个动态的过程，导致出现越来越多的“社区”。

Why? As HR did not provide any change on career paths or bonus system some developers tried to map the old ways to the new ways. They identified communities as something close to working groups, which had been essential check-points in the old model for their career advancement.
为什么？由于HR没有对职业发展或奖金制度做出任何改变，一些开发人员试图将旧方法映射到新方法。他们将社区视为类似工作组的东西，工作组是旧模式中职业发展的重要检查点。

### The Quick-Fix of “Expert Teams” 权宜之计 - “专家团队”
ADD does not include all aspects of the product, for example, hardware architecture. So, special attention to the interfaces from the non-traditional ADD structures to the traditional BMW Group structure is required.
ADD中并不包括产品的所有层面，例如硬件架构。因此，需要特别关注非传统的ADD组织结构与传统宝马集团组织结构之间的接口。

#### Hardware-related Architecture 硬件相关架构
Handling the aspect of hardware-related architecture started in the first Requirement Area with two architects from the old architecture team joining two separate regular feature teams—essentially leading teams. It was planned to form a regular Community to support learning across teams and Areas.
硬件相关架构方面的工作从第一个需求领域开始，来自旧架构团队的两名架构师分别加入了两个独立且比较领先的功能团队。计划是成立一个社区，以支持跨团队和区域的学习。

This approach (architect as team members) failed in this early stage due to several aspects: (1) the items for the feature teams in the early Sprints didn’t touch hardware-related architecture, and (2) the architect team members were still heavily involved in the BMW Group’s architecture group.
这种方法（架构师作为团队成员）在早期阶段失败了，原因有几个方面：（1）功能团队在早期Sprint中没有涉及硬件相关架构，（2）作为功能团队成员的架构师仍然大量参与宝马集团的架构团队工作中。

Why hadn’t there been hardware-related architecture items for these leading teams in the first Sprints? ADD started with vehicle prototypes and simulations before the adoption. Some details were unclear, but the big decisions were made, so the fake PO (real PO joined later) prioritized non-hardware-architecture topics, for example, software architecture-related topics and other features.
为什么在早期的Sprint中，这些领先的团队没有硬件相关的架构工作项？在转型前，ADD是从车辆原型和仿真开始。一些细节尚不清楚，但重大决定已经做决策了，因此伪PO（真正的PO后来才加入）优先考虑非硬件架构的主题，例如软件架构相关和其他功能。

Why were the architect team members occupied if no relevant items were processed by their team? Within the BMW Group, the architecture group is a network of precursors, events, and decisions—it’s a slowly moving normative, partially political body. So, for ADD as a department to stay connected to corporate’s mainstream, close ties in the form of members joining and actively contributing is essential. This led to the architect team members spending only a fraction of their time in their actual ADD team.
那么在团队没有相关事项的情况下，为什么架构师团队成员还很忙？在宝马集团内部，架构组是一个先驱、事件和决策的网络。因此，ADD作为与整个公司关联在一起的一个部门，有成员加入和积极贡献的密切联系至关重要。这导致架构师团队成员在实际的ADD团队中只花费了一小部分时间。

ADD’s management soon placed hardware-related architecture responsibility to a dedicated “architecture expert team”. This team received added responsibility to explicitly connect with teams for sharing and learning. To clarify: this team didn’t have any obligation to implement features or work on the Product Backlog, just focusing on “hardware-related architecture”.
ADD管理层很快将与硬件相关的架构责任交给了一个专门的“架构专家团队”。该团队的额外责任是与各团队建立连接进行分享和学习。澄清一下：这个团队没有义务实现特性或处理产品待办项，只关注“硬件相关架构”。

To contrast this with software-related architecture (i.e., software design): here, more developers involved themselves voluntarily from the start. They formed the “Software Architecture Community” which quickly transformed into a mandated community. Only after years, some core members of this mandated community were moved into the new “software architecture expert team”. This was a quick-fix for increased manager’s awareness of lacking software design capabilities in the teams and flaws in Product Backlog ordering.
与软件相关架构（例如软件设计）相比：在软件这边，更多的开发人员从一开始就自愿参与。他们成立了“软件架构社区”，但很快转变为一个强制社区。几年后，这个强制社区的一些核心成员被调入了新的“软件架构专家团队”。这个短期快速修复的权宜之计管理者意识到了团队中缺乏软件设计能力，以及产品代办列表排序存在不足。

One of the consequences was that most feature teams underestimated hardware-related change requests and pushed the deadlines of approval processes hard. Which then led to the gratifying learning that during Product Backlog Refinement items need skimming if hardware-related changes are needed and needs appropriate planning.
其后果之一是，大多数功能团队低估了与硬件相关的变更请求，并很艰难地赶上审批流程的截止日期。这导致了令人满意的学习成果，即在产品代办列表梳理时，如果涉及硬件的变更，则只需要略读该条目，并制定需要合适的计划。

#### Dependability 可靠性
Another “expert team” case is Dependability. Dependability in ADD’s context is safety, security, durability, maintainability, and (partially) compliance to regulatory requirements.
The content of dependability is essential for the product and should therefore be part of the Definition of Done and part of the Product Backlog Refinement. Due to the history of project thinking, component thinking, management accountability, and traditional management thinking, a dedicated group focusing on dependability existed before the start of the adoption.
另一个“专家团队”的案例是可靠性。ADD环境中的可靠性是指安全性、安全性、耐久性、可维护性和（部分）符合监管要求。
可靠性对产品至关重要，因此应成为“DoD完成的定义”的一部分，也是“产品代办列表”的一部分。由于项目思维、组件思维、管理责任制和传统管理思维的历史，在转型之前，就存在一个专注于可靠性的专门小组。

The dependability group joined late; about the time of SoP 2018 people joining. Before that, the developers considered “normal” due diligence and (softer) aspects of their Definition of Done. With the dependability group joining, the Definition of Done was revised with a gradually more complete Done.
可靠性小组的加入较晚；差不多在SoP 2018的人员加入的时候。在此之前，开发人员考虑了“常规”必需项的和“完成的定义”的（软性）部分。随着可靠性小组的加入，完成的定义被修改为一个逐渐完整的“完成”。

The tasks within the dependability group before joining the adoption focused heavily among other things on tasking and coordinating suppliers for audits and studies, definition of safety goals, definition of low-level hardware requirements, coordination with regulators, and integration of regulations into safety goals. In the classical vehicle projects, those safety goals are then passed to the development managers to be considered for planning, execution and testing.
在转型之前，可靠性小组的任务主要是分配任务和协调供应商，进行审计和研究、定义安全目标、定义低级别硬件要求、与监管机构协调以及将法规整合到安全目标中。在经典的车型项目中，这些安全目标随后被传递给开发经理，由开发经理进行规划、执行和测试。

Most of the dependability groups activity before was “aside” normal team activity, therefore this aside-characteristic was first preserved. The intention is to gradually expand teams’ capability and realization of the real Done. Until this is achieved, the dependability group is part of the “undone” activity.
之前大多数可靠性小组的活动都是在正常团队活动“之外”，因此这“之外”的特点首先被保留下来。目的是逐步提升团队的能力，和实现真正的“完成”。在实现这一点之前，可信性组是“未完成”活动的一部分。

After joining, the dependability group stayed apart as a separate group. Like the “architecture expert team”, they received the additional duty to work closely with APO and teams during Product Backlog Refinements. Depending on the APO realization of the need, this approach only barely improved the teams’ realization of the real Done for the product.
在加入后，可靠性小组作为一个单独的小组。与“架构专家团队”一样，他们额外承担了与APO和团队密切合作来进行产品代办列表梳理的职责。由于APO对需求的认知不同，这种方法只能勉强提高团队对产品真正完成的认知。

To clarify: “Dependability Expert Team” members joined on occasion Product Backlog Refinements events and contributed to the understanding of the real Done and all the little details this requires. The automated testing suites were adjusted for inspection by “Dependability Expert Team” members, other experts, and stakeholders.
澄清一下：“可靠性专家团队”成员偶尔会参加产品代办列表梳理，帮助贡献以理解真正的“完成”和所需的小细节。自动化测试套件经过调整，以供“可靠性专家团队”成员、其他专家和利益相关者检查。

# Abbreviations 缩写

| 缩写词 | 含义                                                                                                                                     |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------|
| ACC           | [Active Cruise Control自适应巡航]                                                                         |
| AD            | Autonomous Driving 自动驾驶                                                                                                 |
| ADAS          | [Advanced Driver-Assistance Systems 辅助驾驶，L2级]
| ADD           | Automated and Autonomous Driving Department  自动驾驶部门                                                                                                |
| ADP           | Autonomous Driving Platform 自动驾驶平台                                                                                                          |
| AI            | Artificial Intelligence  人工智能                                                                                                                    |
| ASIL          | [Automotive Safety Integrity Level汽车安全完整性等级]                                        |
| CLP           | Certified LeSS Practitioner  认证的LeSS实践者                                                                                                               |
| DCC           | [Dynamic Cruise Control 动态巡航]                                   |
| ECU           | Electronic Control Unit  电子控制单元                                                                                                                   |
| E2E           | End-to-End  端到端                                                                                                                            |
| GHE           | Git Hub Enterprise. A self-hosted version of Git Hub. Git Hub公司。 Git Hub自托管                                                                                      |
| IPA           | Individual Performance Appraisal 个人表现评估                                                                                                           |
| ML            | Machine Learning 机器学习                                                                                                                           |
| PO            | Product Owner    产品负责人                                                                                                                           |
| SCM           | Software Configuration Management   软件配置管理                                                                                                        |
| SoP           | Start of Production  量产                                                                                                                       |
| SWP           | Software Partner   软件合作方                                                                                                                         |
| TDD           | Test Driven Development  测试驱动开发                                                                                                                   |
| VP            | Vice President   副总裁                                                                                                                           |


# References

| Ref-No | Reference                                                                                                                                                                                                                                                                                           |
|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [1]    | C. Larman and B. Vodde, Scaling Lean & Agile Development, Addison-Wesley, 2008. For logged-in CLPs available as [PDF](https://less.works/books/scaling-lean-and-agile-development.pdf).                                                                                                             |
| [2]    | C. Larman and B. Vodde, Practices for Scaling Lean & Agile Development, Addison-Wesley, 2010. For logged-in CLPs available as [PDF](https://less.works/books/practices-or-scaling-lean-and-agile-development.pdf).                                                                                  |
| [3]    | C. Larman and B. Vodde, Large-Scale Scrum, Addison-Wesley, 2016. For logged-in CLPs available as [PDF](https://less.works/books/less.pdf).                                                                                                                                                          |
| [4]    | C. Larman and B. Vodde, Go See, 2019, <https://less.works/less/management/go-see.html>                                                                                                                                                                                                              |
| [5]    | B. Vodde, Politics!, 2019, <https://less.works/attachable/materials/916>                                                                                                                                                                                                                            |
| [6]    | [How too many rules at work keep you from getting things done](https://www.ted.com/talks/yves_morieux_how_too_many_rules_at_work_keep_you_from_getting_things_done). TED Talk, 2015.                                                                                                                |
| [7]    | C. Larman, Applying UML and Patterns, Prentice Hall, 3rd edition, 2004.                                                                                                                                                                                                                             |
| [8]    | C. Larman and B. Vodde, Lean Primer, Version 1.6, 2009. [PDF](https://www.leanprimer.com/downloads/lean_primer.pdf).                                                                                                                                                                                |
| [10]   | Tuckman, Bruce (Spring 2001). [Developmental Sequence in Small Groups](https://web.archive.org/web/20151129012409/http://openvce.net/sites/default/files/Tuckman1965DevelopmentalSequence.pdf) (PDF). Group Facilitation: A Research and Applications Journal. 63 (6): 71–72. doi:10.1037/h0022100. |
| [11]   | Adzic, Gojko (2009), "Bridging the Communication Gap" <https://gojko.net/books/bridging-the-communication-gap/>                                                                                                                                                                                     |
| [12]   | J. Richard Hackman, Leading Teams, Harvard Business Review Press, 2002.                                                                                                                                                                                                                             |
| [13]   | Jeffrey Pfeffer, Six Dangerous Myths About Pay, 1998, <https://hbr.org/1998/05/six-dangerous-myths-about-pay>                                                                                                                                                                                       |
| [14]   | Jay R. Galbraith, The Star ModelTM, 2016, <https://www.jaygalbraith.com/services/star-model>                                                                                                                                                                                                        |
| [15]   | Jo Freeman, The Tyranny of Structurelessness, 1970-1973, <https://www.jofreeman.com/joreen/tyranny.htm>                                                                                                                                                                                             |
| [16]   | Frederick Herzberg, One More Time: How Do You Motivate Employees?, Harvard Business Review, 2003, <https://hbr.org/2003/01/one-more-time-how-do-you-motivate-employees>                                                                                                                             |
| [17]   | Alfie Kohn, Punished by Rewards, Houghton Mifflin Company, Twenty-fifth anniversary edition, 2018.                                                                                                                                                                                                  |
| [18]   | Herbert H. Meyer et al., Split Roles in Performance Appraisal, Harvard Business Review, 1965, <https://hbr.org/1965/01/split-roles-in-performance-appraisal>                                                                                                                                        |
| [19]   | Michele & Jim McCarthy, Richard Kasperowski, The Core Protocols, <https://thecoreprotocols.org/>                                                                                                                                                                                                    |
