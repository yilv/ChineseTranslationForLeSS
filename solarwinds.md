# Incremental LeSS Adoption at SolarWinds 在Solarwinds的增量LeSS导入

**Disclaimer:** This text describes the situation in one of the SolarWinds product groups until 2017, i.e. roughly three years before the event known as the [Sunburst supply chain attack](https://www.cynet.com/attack-techniques-hands-on/sunburst-backdoor-c2-communication-protocol/) that happened in late 2020. Any statements in the text are unrelated to the attack.
**免责证明：**本文描述了其中一个SolarWinds产品组在2017年之前的情况，也就是在2020年末发生的被称为[Sunburst供应链攻击](https://www.cynet.com/attack-techniques-hands-on/sunburst-backdoor-c2-communication-protocol/)事件大约3年之前。文中的任何描述都与攻击无关。

## Background 背景

SolarWinds is a leading provider of IT management software, its products are used by tens of thousands of IT professionals around the world and allow them to have a better overview of their networks, applications, databases and other elements of the company IT infrastructure. One of its first products, Network Performance Monitor has been in development since 2001.
SolarWinds是领先的IT管理软件供应商，其产品被全球数万IT专业人士使用，使他们能够更好地了解他们的网络、应用程序、数据库和公司IT基础设施的其它元素。作为该公司的首批产品之一，网络性能监视器从2001年就在开发了。

Soon after, the second product with a similar focus followed. Both products together created a family of products called the Orion family.  The company realized that both products have many things in common and created a common platform - Core - the subject of this case study. Core has been developed by a group of 5-6 teams.
不久之后，跟进了第二款有着类似焦点的产品。这两款产品共同形成了一个产品系列，被称为“Orion系列”。该公司意识到这两款产品有许多共同点，于是创建了一个公共平台Core - 本案例研究的主题。Core由5-6个团队开发。

The company was successful and over time added the third, fourth, and even tenth product.
公司是成功的，并且随着时间的推移，增加了第三、第四甚至第十款产品。

This caused the platform to expand the number of use cases to cover. In addition to serving more modules from a technical point of view, the Core teams (which are component teams) needed to coordinate work with more and more module groups (consisting of other component teams). As always with component teams, that led to a complicated planning and estimating process that took months, and of course was significantly invalidated after the planning, due to the realities of change and imperfect insight. The company hired many managers and fake “Product Owners” (actually, project managers and business analysts) to deal with the coordination problems, and with each additional manager prioritization was even more fuzzy because each had their own agenda and priority list. These management “quick fixes”  always “fixed” the situation only temporarily because their long-term effect was increasing the organizational complexity.
这导致该平台扩大了需要覆盖的用户用例的数量。除了从技术角度为更多模块提供服务外，Core团队（是组件团队）还需要与越来越多的模块组（由其他组件团队组成）协调工作。与组件团队一直都有的问题一致，这导致了需要耗时数月的复杂的计划和估算过程，当然，由于实际会有变更和理解偏差，在计划之后估算显然会变得无效。该公司雇佣了许多经理和伪“PO：Product Owner - 产品负责人”（实际上是PM/BA：Project Managers/Business Analysts - 项目经理/业务分析师）来处理协调的问题，每增加一个经理，优先级就会更加模糊，因为每个人都有自己的议程和优先级列表。这些管理上的“速效方案”总只是暂时“解决”了问题，因为它们的长期影响反而是增加了组织的复杂度。

The management was frustrated. There were so many capabilities they wanted to add to Core (new UI look and feel, support for high availability, make customer upgrade experience seamless). But the Core group was so occupied by the module requests and maintaining the current features that it had no capacity to add new capabilities to the product. Management came with the following approach: separate greenfield initiatives each focused on developing a new capability for all modules (e.g. a new UI framework, a new installer) - another instance of a quick fix. Predictably, that further increased the integration complexity and time to deliver the whole product build to customers.
管理层感到沮丧。他们曾经希望在Core中增加许多能力（新的UI样式和感觉，支持高可用性，无缝的客户升级体验）。但是Core组被模块的请求和维护当前特性占用了太多时间，从而没有产能向产品中添加新的功能。管理层采用了如下方法：独立的新建方案小组，每个小组专注于为所有模块增加一种新的能力（例如：一个新的UI框架，一个新的安装程序）- 又一个快速方案的示例。可以预测的是，这进一步增加了集成的复杂度，以及向客户交付完整产品构建的时间。

These quick fixes failed because they didn’t address the root cause - the _existence_ of the Core teams (component teams), since the number of component teams increases planning complexity, dependencies, delay of delivering end-to-end customer features, and the need for coordination. The need for coordination is often handled by adding more coordinators (a management _quick fix_) which further decreases the ability of the teams to understand the whole product and creates a pressure for more strict component boundaries which again increases planning complexity. Of course,the whole vicious cycle can be eliminated or avoided if component teams are removed, or not introduced in the first place. [Figure 1](#figure1) illustrates the dynamics in a system model.
这些速效方案的失败，是因为它们没有设法解决根本原因 - Core团队（组件团队）的存在，因为组件团队的数量增加了计划的复杂度、依赖、交付端到端客户特性的延迟，以及协调的需求。协调需求通常会通过增加更多的协调人（一种管理速效方案）来解决，这进一步降低了团队理解整体产品的能力，同时产生压力以有更严格的组件边界，从而进一步增加了计划的复杂度。当然，如果移除所有的组件团队，或者一开始就没有引入，整个恶性循环就可以被消除或者避免。[图1](#figure1)以一个系统模型呈现了该动态。

<a name="figure1"></a>
<figure>
<img src="/img/case-studies/solarwinds/systems-model-coordination-need.png" alt="Systems Model on Coordination Needs">
  <figcaption>Figure 1: System model of the need for coordination</figcaption>
</figure>

However, Core _was_ introduced as a dedicated component group. Then, predictably, the following dynamic started (referring to [11 laws of systems thinking](https://en.wikipedia.org/wiki/The_Fifth_Discipline) here). Adding a new coordinator was a “quick fix” that temporarily reduced coordination complexity. However as a result, organizational complexity grew, so after a while the need for coordination was even higher than before. (Law 3: Behavior grows better before it grows worse.) The delay between these two events made it more difficult to see. (Law 7: Cause and effect are not closely related in time and space.)
然而，Core是作为一个专用的组件组织被引入的，之后可以预测的是，以下的动态就开启了（参考[系统思考的11条法则](https://en.wikipedia.org/wiki/The_Fifth_Discipline)）。增加一个新的协调者，是一个“速效方案”，暂时降低了协调的复杂度。然而结果是，组织的复杂度增长了，因此一段时间之后，协调的需求甚至比以前更高（法则3：在情况变糟之前会先变好）。这两个事件之间的延迟又使它更难被察觉到（法则7：因和果在时空上并不紧密相连）。

Having more coordinators (and thus higher organizational complexity) was a result of a long-term adhoc response to problems. It has its roots in the past, when the first coordinator was added, and then the next and then next and next. (Law 1: Today’s problems come from yesterday’s solutions). Each of these steps was seemingly innocent and harmless and seemed to make sense at the time - add one more coordinator. (Law 4: The easy way out usually leads back in.) With each additional coordinator, teams and senior management became more addicted to the results of the coordinators work (usually some intermediate artifacts such as a project plan, status report, acceptance criteria written down for each “story”). Soon nobody could imagine organizing work without them. (Law 5: The cure can be worse than a disease.)
拥有更多的协调者（因此更高的组织复杂度）是对问题长期临时响应的结果。它的根源在过去，当第一个协调者被添加的时候，然后就有下一个，一个接一个（法则1：今天的问题来自于昨天的解）。这些步骤中的每一步看似都是无恶意和无害的，而且在当时看起来也有道理 - 再增加一个协调者（法则4：选择最容易的办法往往会无功而返）。每增加一名协调者，团队和高层管理都会变得更加依赖于协调者工作的成果（通常是一些中间的工件，例如项目计划、状态报告、为每个“故事”写下的验收标准）。很快地，没有人能够想象不靠他们组织工作（法则5：对策可能比问题更糟糕）。

## Scope of the Adoption 导入范围

The root cause of the coordination problems and more coordinators was the very existence of component teams, and so the solution is their elimination. But it wasn’t possible to make this structural change because of the false (and false dichotomy) management belief that work organized to (large) component teams is the _only_ way of developing large products..
协调问题和更多协调人的根本原因在于组件团队的存在本身，因此解决方案就是要消除它。但是没能改变这一结构的原因是错误的管理信念（以及错误的两分法） - 相信把工作按（大型）组件团队组织是开发大型产品的唯一方式。

Given the constraint that we couldn’t eliminate the Core group, to at least achieve some minor improvement in increasing adaptiveness and more likely working on valuable items, we decided to change the following organizational design elements for some minor incremental improvements
考虑到我们受限于不能消除Core组，为了至少在提高适应性和更可能工作于有价值的条目上实现一些小范围的改进，我们决定改变以下组织设计要素：

* Define the “Product” as broad as possible
* Reduce the number of explicit and implicit backlogs in the organization
* Reduce number of coordinators

* 定义尽可能广泛的“产品”
* 减少组织中无论是显式的还是隐含的待办列表
* 减少协调者数量

This case study shows how we used these elements to make the first incremental step towards the system optimizing goal of _increased adaptiveness_ to more easily learn and pivot to working on newly-discovered more-valuable items.
本案例展示了我们如何使用这些要素向提高适应性 - 以易于学习并转向工作于新发现的更有价值的条目 - 的系统优化目标迈出第一步。

Because we didn’t eliminate the first-order influencing factor - the existence of component teams - it led to a slow and painful partial LeSS adoption and the improvement towards the system optimizing goal was limited.
由于我们并没有消除一阶的影响因素，也就是组件团队的存在，这导致了缓慢的和痛苦的部分LeSS导入，以及对系统优化目标的改进有限。

For example, the decision to use Core as an initial “Product” didn’t allow us to prepare a potentially-shippable Product more often, which delayed feedback from customers.
例如，使用Core作为初始“产品”的决定让我们无法更频繁地准备一个潜在可交付的产品，这延迟了来自客户的反馈。

The perceived progress made in the first step is shown in [Figure 2](#figure2).
被视为从第一步中取得的进展呈现在[图2](#figure2)中：

<a name="figure2"></a>
<figure>
<img src="/img/case-studies/solarwinds/perceived-progress.png" alt="Perceived Progress">
  <figcaption>Figure 2: Perfection goal and its progress to it described in this case study.</figcaption>
</figure>

The partial adoption continued later with further steps that are out of scope of this case study. These steps included further broadening of the product definition and reducing the number of backlogs. See [Figure 3](#figure3).
部分导入又进行了后续步骤，但这超出了本案例的范围。这些步骤包括进一步扩展产品定义和减少待办列表的数量。参见[图3](#figure3)。

<a name="figure3"></a>
<figure>
<img src="/img/case-studies/solarwinds/timeline-of-adoption.png" alt="Timeline of the LeSS Adoption">
  <figcaption>Figure 3: Timeline of the adoption.</figcaption>
</figure>

But first things first. Let’s describe how the product development group had been organized before the adoption.
但是首先第一件事，让我们描述产品开发组在导入之前是如何组织的。

### Initial state 初始状态

Architectural Background: The Orion family consisted of multiple “modules” (i.e. components), e.g. NPM (Network Performance Monitor), SAM (Server & Application Monitor) and VMAN (Virtualization Manager). Each module focuses on monitoring a different aspect of the customer company infrastructure. For example, NPM monitors traffic on key network interfaces, VMAN monitors e.g. virtual machines, disks. A module can be downloaded and installed separately but all modules can also be installed together on the same server (as a product _suite_).
架构背景：Orion系列由多个“模块”（即组件）组成，例如NPM（网络性能监视器Network Performance Monitor）、SAM（服务器和应用程序监视器Server & Application Monitor），还有VMAN（虚拟管理器Server & Application Monitor）。每个模块关注于监控客户公司基础设施的不同方面。例如，NPM监控关键网络接口上的流量，VMAN监控例如虚拟机、磁盘。可以独立下载和安装一个模块，但也可以一起安装所有模块在同一台服务器上（作为一个产品套件）。

Before the LeSS adoption the development organization was structured in the typical local optimization of _component teams_, in the following way (see [Figure 4](#figure4)):
在LeSS导入之前，开发组织由典型的局部优化的组件团队构成，如下所示（见[图4](#figure4)）：

* **Module teams** - each module group (e.g. NPM, SAM, VMAN) typically had its own development group consisting of one to three teams
* **Core group** - responsible for maintaining the majority of the shared components (e.g. user management, DB access layer) and some user-centric features (e.g. node and volume monitoring) consisting of 5 (later 6) teams.
    * _Partial LeSS adoption in this group is the scope of this case study._
* **Initiative teams** - as the need for _shared_ services or components was growing and the Core team was unable to deal with the need to deliver new features, separate greenfield initiatives were set up by management. Like the Core group, each focused on developing a new capability for _all_ modules (e.g. a new UI framework, a new installer)
* **Other groups** - some roles like architects or UI designers were not members of the engineering teams but created separate functional groups.

* **模块团队** - 每个模块组（如NPM、SAM、VMAN）通常有自己的开发组，由1到3个团队组成
* **Core组** - 负责维护大多数的共享组件（如用户管理、数据库访问层）和一些用户导向的特性（如节点和卷监控），由5个（后来是6个）团队组成。
    * 该组的部分LeSS导入就是本案例的范围。
* **新方案团队** - 由于对共享服务或组件的需要不断增长，Core团队无法满足交付新特性的需要，管理层制定了单独的新建方案小组。与Core组一样，每个小组都专注于为所有模块开发新能力（例如，新的UI框架，新的安装程序）
* **其他组** - 有些角色例如架构师或UI设计师不是工程团队的成员，而是创建了独立的职能组。

<a name="figure4"></a>
<figure>
<img src="/img/case-studies/solarwinds/component-team-organization.png" alt="Initial Component Organization">
  <figcaption>Figure 4: Orion product group organizational structure before LeSS adoption. For module groups, the number of teams is indicated by the number of team icons.</figcaption>
</figure>

## Approach to adoption 导入方法

### Initial Product Definition 初始产品定义

To maximize adaptiveness it would be ideal to use a product definition that is as broad and end/user/customer-centric as practical (Book 3). “Define Your Product Guide” from Book 3 recommends defining the Product using expanding and restraining questions. Let’s revisit how they had been applied in our case.
为了最大限度地提高适应性，最理想的是使用尽可能广泛和尽可能终端用户/客户导向但又现实的产品定义（第3本书）。第3本书中的“定义你的产品指南”建议使用扩展和限制的两组问题来定义产品。让我们重新回顾一下它们是如何应用在我们的案例中的。

#### Expanding questions 扩展的问题

**What would the end customers answer if we ask them, “What is our Product?”.**
**如果我们问终端客户 “我们的产品是什么？” ，他们会回答什么。**

The answer to this question would probably be “SolarWinds”. Taking into account that Orion customers probably don’t know the complete SolarWinds portfolio and think SolarWinds=Orion we can safely modify this answer to “SolarWinds Orion Suite”
这个问题的答案可能是“SolarWinds”。考虑到Orion客户可能不知道完整的SolarWinds产品组合，并且认为SolarWinds=Orion，我们可以安全地将此答案修改为“SolarWinds Orion套件”。

**Do we have components that are shared or functionality that is the same across our current Products?**
**我们是否有跨越当前所有产品的共享组件或相同功能？**

Yes, actually the majority of the code for Orion family was shared. It also shared the same UI patterns like dashboards, charts, menus, etc.
是的，实际上Orion系列的大部分代码都是共享的。它还共享相同的UI模式，如仪表盘、图表、菜单等等。

**Our Product is part of? What problem does the Product solve for end-customers?**
**我们的产品是什么的一部分？这个产品为终端客户解决了什么问题？**

The users (who are almost equal to customers according to the SolarWinds business model) need to monitor their company infrastructure and be informed about any important events happening there.
用户（在SolarWinds的业务模型里几乎等同于客户）需要监控他们的公司基础设施，并了解那里发生的任何重要事件。

#### Restraining questions 限制的问题

**What is the Product vision? Who are the customers? What is the Product’s customer domain?**
**产品愿景是什么？客户是谁？产品所在的客户领域是什么？**

Different Orion modules serve different customers - e.g. network engineers vs system engineers. However, there are commonalities between the Products and the company actively tries to cross-sell multiple modules to customers who had already bought one module. So the answer to this question would advise us not to restrain the product definition.
不同的Orion模块服务于不同的客户 - 例如网络工程师和系统工程师。然而，这些产品之间存在共性，公司积极尝试向已经购买了一个模块的客户交叉销售多个模块。因此，这个问题的答案会建议我们不要去限制产品定义。

**What development is within our company? How much structural change is practical?**
**哪些开发是在我们公司内部进行的？有多少结构性的变革是现实的？**

The last question was the most difficult. The guide includes considering department boundaries as a possible way to restrain initial product definition, especially if there are dysfunctional management-political forces that make it difficult to go broader. Further guides then recommend expanding product definition later. That makes the initial change politically easier as the amount of structural change for LeSS adoption is minimized.
最后一个问题是最难的。该指南包含了考虑部门边界作为限制初始产品定义的可能方式，特别是如果存在失调的管理-政治力量使其难以扩展。进一步的指南建议之后再扩展产品定义。这使得最初的变革在政治上更容易，因为LeSS导入所需的结构变化程度被最小化了。

On the other hand, there is a risk that the departments represent component teams and therefore an initially defined “Product” will cover only a set of components and not be a true end-to-end customer-focused Product. Also, without a structural change it is easy to miss how deep (front-to-back) LeSS adoptions are supposed to be, as the other supporting roles or intermediate artifacts will most likely remain intact, because they need to serve the departments not participating in the LeSS adoption and will likely interfere with the adopting group. Therefore, while the initial adoption may be easier, the forces in the rest of the organization may be strong enough to revert the initial change later.
另一方面，这里存在这样一种风险，即部门代表组件团队，因此最初定义的“产品”将仅覆盖一组组件，而不是真正的以客户为中心的端到端产品。同时，没有架构变革的话，很容易忽略LeSS实践的能达到什么预期的深度（前端到后端），作为其他支持角色或者中间的工件将可能保持不变，因为它们需要服务于不参与LeSS实践的部门，并且可能妨碍导入组。因此，虽然最初的实践可能更容易，但是组织剩余部分的力量可能足够强大，可以在之后恢复最初的变革。

Another weakness of starting with a partial product definition that is only a set of components (rather than a true front-to-back definition) relates to manager status quo political games: The managers of the existing component teams will want to keep the existing structures so that their positions are not threatened. By allowing a “Product” definition to start with just a set of components opens the door to distorting the change intention so that components can be incorrectly called a “Product” and then component managers can be (fake) “Product Owners.” This has been observed many times in the myriad fake “scaling agile” adoptions around the world.
从只是一组组件（而不是真正的前端到后端的定义）的部分产品定义开始的另一个缺点与管理者目前的政治博弈有关：现有组件团队的管理者希望保留现有的架构，以使其职位不受威胁。允许“产品”定义仅从一组组件开始打开了扭曲变革意图的大门，从而组件可以被错误地称为“产品”，然后组件管理者可以成为（伪）“PO”。这已经在世界各地许多伪“规模化敏捷”导入中被多次观察到。

An alternative way of thinking would be to ignore this question and keep the initial product definition unrestrained. That would typically mean that we are in a LeSS Huge situation, which makes the adoption more complex - we would need to include multiple groups into the initial discussions, adoption would take more time (with one Requirement Area at a time) and would therefore be more vulnerable by company politics.
另一种可以选择的思考方式是忽略这个问题，保持初始的产品定义不受限制。这通常意味着我们处于一个LeSS巨型的环境，会使导入更加复杂 - 我们需要将多个组纳入到初始的讨论，导入也会花费更多时间（一次一个需求领域），并且因此会更容易受公司政治影响。

#### Choosing the Product 选择产品

As you can see, it is not an easy choice. In our case, if we take the output of the _expanding_ questions (SolarWinds Orion Suite) as input to this step we end up with the Product consisting of hundreds of thousands of lines of code in C#, C++, Javascript, SQL, python, go, VB6. The total number of teams developing the Product is 30-40 even if we do not count additional roles currently not included in the teams (architects, UI designers). Even if we imagine removing all coordination roles and imagine reduction of required developers for a simplified Product, it will still mean that we need more (probably a way more) than recommended 8 teams for a smaller LeSS adoption. This means that we are in a LeSS Huge situation.
正如你们所见，这不是一个容易的选择。在我们的案例中，如果我们将扩展问题的输出（SolarWinds Orion套件）作为这一步骤的输入，我们最终得到的产品由数十万行C#、C++、Javascript、SQL、python、go、VB6代码组成。开发产品的团队总数为30-40个，即便我们不把当前未包含的额外角色（架构师、UI设计师）算在内。即使我们设想移除所有的协调角色，并且设想减少所需开发人员来做一个简化产品，这仍然意味着我们需要比小的LeSS导入所推荐的8个团队更多（可能多很多）的团队。这意味着我们处于一个LeSS巨型的环境中。

Out of the two options described above we had chosen the first one: restrain the initial product definition to one department - “Core” (a multi-component group highlighted in [Figure 4](#figure4)). Why? Doing structural change for multiple departments in multiple locations seemed … scary. We assumed that our initial “Product” will later become a Requirements Area for a larger Product, so we tried to keep other properties compatible with a typical Requirements Area definition, namely:
在上述两个选项中，我们选择了第一个：将初始的产品定义限制为一个部门 - “Core”（[图4](#figure4)中高亮显示的一个多组件组）。为什么？在多个地点为多个部门做组织架构变革看起来…让人害怕。我们假设我们最初的“产品”以后将成为更大的产品中的一个需求区域，因此我们尝试让其它属性与一个典型的需求区域定义保持兼容，即：

* Appropriate size - five teams at the time of adoption, later expanded to six teams
* Partial customer orientation - although “Core” served as a shared collection of components and services for other parts of the Orion suite, the Core teams had been able to deliver some customer-oriented features themselves (for example, monitoring and visualizing CPU utilization of a network element)

* 合适的规模 - 导入的时候为五个团队，之后扩展为六个团队
* 部分的客户导向 - 尽管“Core” 作为提供给Orion套件其它部分的组件和服务的共享集合，Core团队自己也已经能够交付一些面向客户的特性（例如，监控和可视化网元的CPU利用率）

To reduce confusion, we will further use the term “partial Product”, “partial-Product Backlog”, etc. when referring to Core and the term “Product” only when referring to the Product after expanding questions (the Orion suite).
为了减少混淆，我们将进一步在提及Core时使用术语“部分产品”、“部分产品待办列表”等；只在提及扩展了的产品（Orion套件）时使用术语“产品”。

We believed that this partial Product would serve as a role model for the other departments later - delivering customer-oriented features with a decreased need for coordination by managers. However, later we realized that it was not a good first choice. In particular the fact that Core was primarily a multi-component group and served internal stakeholders instead of customers led to typical problems:
我们相信，这个部分产品之后将作为其他部门的榜样 - 交付面向客户的特性时减少了对管理者协调的需求。然而，后来我们意识到这不是一个好的第一选择。特别地，Core主要是一个多组件的组，服务于内部利益相关方而不是客户，这一事实导致了如下典型问题：

* Partial-Product Backlog was full of technically-oriented component tasks instead of end-to-end customer features (see section [Product Backlog](#product-backlog))
* Major coordination effort was still required to integrate Core work with module and initiative work to deliver customer-oriented features. A customer-oriented feature often needed implementation in both module and Core codebase. Due to the fact that both groups had different partial-Product Backlogs, this work had to be planned, tracked and checked at the end.
* One month long test phase before each release was another example of coordination effort required between modules and Core.

* 部分产品待办列表充斥着技术导向的组件任务，而不是端到端的客户特性（参见[产品待办列表](#product-backlog)一节）
* 仍然需要大量的协调努力，将Core的工作与模块和新方案工作整合起来以交付面向客户的特性。一个面向客户的特性通常需要在模块和Core代码库两者中实现。由于两个组有不同的部分产品待办列表，最后这项工作不得不被计划、跟踪和检查。
* 每次发布前一个月的测试阶段是在模块和Core之间需要协调努力的另一个示例。

For completeness, there was one more reason considered but dropped against choosing “Core” as the initial scope of the product definition, which we were aware of from the beginning: the fact that the Core teams had been located in two sites (Brno, Czech Republic and Lviv, Ukraine). We had at least a little concern that including two sites of teams in the first step of the change would be too risky. Moreover, the Lviv teams had been employees of a vendor, not SolarWinds itself. However, this disadvantage was perceived as relatively small. Nevertheless, we were careful to overcome communication boundaries that naturally arose and including the two sites didn’t turn out to be a major obstacle.
为了完整起见，我们还曾考虑但又放弃了一个反对选择“Core”作为产品定义初始范围的原因，我们从一开始就意识到：Core团队位于两地（捷克的布尔诺和乌克兰的利沃夫）的这一事实。我们至少有一点担心，在变革的第一步就包括两地的团队会太冒险。此外，利沃夫团队是供应商的员工，而不是SolarWinds自己的员工。然而，这一不利条件被认为相对较小。尽管如此，我们还是小心地克服了由地域自然产生的沟通边界，结果包括这两地并没有成为一个主要障碍。

<a name="figure5"></a>
<figure>
<img src="/img/case-studies/solarwinds/initial-product-definition.png" alt="Initial Product Definition">
  <figcaption>Figure 5: Initial product definition by expanding and restraining questions
</figcaption>
</figure>

With Core as an initial Product (see [Figure 5](#figure5)) we can show progress of the partial adoption on a feature team adoption map on [Figure 6](#figure6).
将Core作为一个初始的产品（参见[图5](#figure5)），我们可以在[图6](#figure6)的特性团队导入地图上显示部分导入的进展。

<a name="figure6"></a>
<figure>
<img src="/img/case-studies/solarwinds/feature-team-adoption-map.png" alt="Feature Team Adoption Map">
  <figcaption>Figure 6: Feature Team adoption map of the partial adoption</figcaption>
</figure>


## Steering part of the organization towards more adaptiveness 引领部分组织实现更大的适应性

Defining the initial “Product” as Core (essentially, a big component) constrained further changes we could make. This section will describe how we reduced the number of coordinators, reduced the number of backlogs, and it also outlines some effects of a slightly broader product definition on team coordination.
将最初的“产品”定义为Core（本质上是一个大组件）限制了我们接下来可以做的改变。本章节将描述我们如何减少协调者的数量，减少待办列表的数量，并略述了稍微宽泛的产品定义对团队协调的一些影响。

Before we do this, let's recall some aspects that were common to all these activities - my personal role in the engineering group and education of people before adoption.
在我们开始前，让我们回顾一下所有这些活动的一些共同方面 - 我在工程部门中的个人角色以及导入前的人员培训。

### History 历史

In 2015, about a year before this case study, I was a member of a group that introduced “Scrum” to the company, which in retrospect mostly meant introducing _Scrum theater_ in the company, with one notable exception. We established the concept of a Team: 5-9 members, long-term membership, partly cross-functional (programmers and testers), but not cross-component across all the components of Core. In 2016, I accepted a position of one of the many inter-team and inter-group coordinators. My official title was “Product Owner”, but as usual in most “agile” faux adoptions, it was just a synonym for a project manager. My assignment was Core. With five teams working in one group I was looking for better ways of organizing the work, for example prioritizing the backlog based on global priorities or looking for ways to gather feedback from customers more often. Starting with LeSS seemed like a natural choice.
在2015年，大约在本案例发生的前一年，我是一个向公司介绍“Scrum”的小组成员，回想起来，主要是在公司引入“Scrum剧场”，但有一个值得注意的例外。我们建立了团队的概念：5-9名成员，长期的成员，部分跨职能（程序员和测试人员），但没有在整个Core范围内跨组件。在2016年，我接受了众多团队间和组间协调者其中一个职位。我的官方头衔是“PO”，但和往常大多数伪“敏捷”导入中一样，它只是项目经理的代名词。我的任务就是Core。有5个团队在一个组中工作，当时我在寻找组织工作的更好方式，例如，基于全局优先级对待办列表排序，或者寻找更频繁地收集客户反馈的方法。从LeSS开始似乎是一个自然的选择。

### Education 培训

I gave the third LeSS book to two first-level line managers and a potential partial-Product Owner and asked them to read chapter 2 (_Introduction of LeSS_). Scrum Masters had discussed LeSS a couple of times in their community. I had the most LeSS knowledge - reading all three LeSS books and working as a Scrum Master in a large-scale context for 12 years. And that was it.
我把第三本LeSS书交给了两位一线经理和一位潜在的部分产品PO，并让他们读一下第二章（LeSS介绍）。Scrum Masters在他们的社区中讨论过LeSS几次。我有最多的LeSS知识 - 阅读了所有三本LeSS书，并在大规模环境中作为Scrum Master工作了12年。就是这样。

In retrospect, the education was desperately insufficient. LeSS adoptions are complex and need deep understanding of all involved participants - management (both first-level and higher management), engineers, Scrum Masters, business departments. All these people need to thoroughly understand the effects of the organizational structure elements on teams and the whole organization before the adoption starts. It is a warning to all people eager to start LeSS adoptions not to start them too early - not before they understand the organizational design and dynamics of their organization.
回顾过去，培训是极度不充分的。LeSS导入是复杂的，需要所有相关参与者 - 管理层（一线和高级管理层都包含），工程师，Scrum Masters，业务部门 - 的深入理解。在导入开始之前，所有这些人都需要彻底理解组织架构要素对团队和整个组织的影响。这是对所有渴望开始LeSS导入的人的一个警告，不要过早开始 - 不要在他们理解组织设计和组织动态之前（开始）。

### Reducing the number of coordinators 减少协调者的数量

#### Core organizational structure before adoption 导入之前的Core组织架构

Core engineering group was organized into teams (see [Figure 7](#figure7)). Teams were typically long-term, the same people stayed together for months or even years until natural attrition or the need for fresh air into the team. Each team had a name of their own choice, for example, Hubble, Legend, Darwin. The team size was usually 5-9 members with the bias towards the lower end of the scale. The teams consisted of developers (mostly C#, rarely other languages) and testers. The teams were always collocated. (Guide “Team Based Organization”, Book 3) Typically, members of a team reported to the same engineering manager and a single manager managed two teams. Scrum Masters existed as well and they had been part-time team members.
Core工程组被组织成多个团队（见[图7](#figure7)）。团队通常是长期的，相同的人在一起待几个月甚至几年，直到自然流失或者需要新鲜空气进入团队。每个团队都有自己选择的名字，例如，哈勃（Hubble），传奇（Legend），达尔文（Darwin）。团队规模通常为5-9人，倾向于较小的规模。团队由开发人员（主要是C#，很少有其他语言）和测试人员组成。团队总是集中办公（“团队型组织”指南，第3本书）。通常，一个团队的成员向同一个工程经理报告，并且一个经理管理两个团队。Scrum Masters也存在，他们是兼职的团队成员。

Other roles outside of the teams still existed, for example, UI designers, documentation writers and architects. These employees fell under different management structures and they were often located in different countries like the US. Of course, it reduced adaptiveness because teams could only deliver features preprocessed or post-processed by these other specialists and could not easily change course. This aspect is visible on FTAM on [Figure 6](#figure6). Also, the existence of these roles generated some amount of coordination work, which has been mostly handled by dedicated coordinators.
团队之外的其他角色也仍然存在，例如UI设计师，文档编写者和架构师。这些员工归属不同的管理架构，并且他们通常位于美国等不同国家。当然，它（这种组织架构）降低了适应性，因为团队只能交付由这些其他专家预处理或后处理的特性，并且不能容易地变更。这个方面在[图6](#figure6)的FTAM上可以看到。这些角色的存在也产生了一些协调工作，主要由专门的协调者处理。

In contrast, if we use real Scrum teams we include all these roles in the teams and as a consequence coordination work would mostly happen inside self-managing teams without the need for external coordinators.
相反地，如果我们使用真正的Scrum团队，将所有这些角色都包含在团队中，协调工作会因此主要发生在自管理团队的内部，而不需要外部协调者。

<a name="figure7"></a>
<figure>
<img src="/img/case-studies/solarwinds/core-group-organizational-structure-before-less.png" alt="Core Group Organizational Structure before LeSS">
  <figcaption>Figure 7: Core group organizational structure before LeSS adoption</figcaption>
</figure>


Engineering managers and the fake “Product Owners” (in fact project managers and business analysts = PM/BA) reported to one senior manager who bore ultimate responsibility for Core.
工程经理和伪“PO”（事实上是PM/BA）向一位对Core最终负责的高级经理报告。

The teams were placed in two locations: two teams in Brno, Czech Republic, three teams in Lviv, Ukraine. The three Ukrainian teams were not employees of SolarWinds, but hired by a vendor company and working for SolarWinds based on contract. However, all of the above is valid also for vendor employees - they were organized in long-term teams consisting of developers and testers. No other product development roles were present on the vendor side. The most experienced vendor employees worked for SolarWinds for close to 10 years.
团队分别位于两个地点：两个团队在捷克共和国的布尔诺，三个团队在乌克兰利沃夫。这三个乌克兰团队不是SolarWinds的员工，而是由一家供应商公司雇用，并根据合同为SolarWinds工作。然而，所有上述描述也适用于供应商员工 - 他们是由开发人员和测试人员组成的长期团队。供应商方面没有其他产品开发角色。经验最丰富的供应商员工为SolarWinds工作了将近10年。

The vendor teams didn’t formally report to SolarWinds management but to local vendor management. The vendor organization appointed a contact person that served as a counterpart of the senior manager for people-related decisions like hiring or firing developers. Other than that the contact person had no authority over the work of the teams.
供应商团队并不正式向SolarWinds管理层报告，而是向当地的供应商管理层报告。供应商组织指定了一名联系人，作为高级经理的对应方，负责与人员相关的决策，例如雇用或解雇开发人员。除此之外，联系人没有授权管理团队的工作。

#### Fake “Product Owner” (PM/BA) 伪“PO”（PM/BA）

Work items for teams had been prepared by fake “Product Owners” who were not that, but just people doing project management and business analysis activities (PM/BA). They were also responsible for coordinating team work with other teams in different groups (e.g. modules) and with other roles (e.g. UI designers), see [Figure 8](#bookmark=id.knp43jun34lm).
团队的工作条目是由伪“PO”准备的，他们并不是（真正的PO）那样的人，只是做项目管理和业务分析活动（PM/BA）的人。他们还负责与不同组（例如模块）的其他团队还有其他角色（例如UI设计师）协调团队的工作，见[图8](figure8)。

As a consequence, PM/BAs had so much on their plate that they could rarely manage more than two teams. When more than two teams were needed a new organizational unit was created with another PM/BA. Core had five teams with three PM/BAs.
因此，PM/BA有太多事情要做，他们很少能管理两个以上的团队。当需要两个以上的团队时，会创建一个新的组织单元，有另一个PM/BA。Core有五个团队，加上三个PM/BA。

For Core, coarse-grained backlog prioritization was done by one Product Manager who was responsible for communication with customers and other parts of the business like top management, sales or marketing. He should have been the one and only one person playing the role of (partial Product) Product Owner.
对于Core，粗粒度的待办列表优先级由一名产品经理完成，他负责与客户和业务的其它部分（例如高管、销售或市场）进行沟通。他应该担任唯一的（部分产品）PO角色。

<a name="figure8"></a>
<figure>
<img src="/img/case-studies/solarwinds/communication-paths-pm.png" alt="Communication Paths of the PM">
  <figcaption>Figure 8: Key groups and their communication paths to the PM/BA.</figcaption>
</figure>

#### Reducing the Number of Coordinators 减少协调者的数量

[Figure 7](#figure7) shows that there were three PM/BAs assigned to Core. We decided to reduce this number to _one_ to reduce the number of coordinators and to create pressure for teams to start coordinating their own work. So the next step was convincing three individuals skilled at business analysis and project management to find a new role - a usual problem even for partial LeSS adoption which is explored in the Guide “Job Safety, but not Role Safety”.
[图7](#figure7)显示了有三个PM/BA分配给Core。我们决定将这个数字减少到1个，以减少协调者的数量，并创造压力让团队开始协调自己的工作。因此，下一步是说服三名擅长业务分析和项目管理的人员找到一个新的角色 - 即使是部分的LeSS导入，这也是一个常见的问题，“工作安全，而非角色安全”指南对此进行了探讨。

Fortunately for the adoption (though not so much for the company), two of them decided to leave the company before the partial adoption started (for unrelated reasons) and the third one (myself) wanted to be a Scrum Master. So a new person for the role was found. He transitioned from a different part of the company and also changed his role from a test lead. Having a new person in the role emphasized the fact that the adoption of a new approach starts.
对导入来说幸运（虽然对公司来说并不怎么幸运）的是，他们中的两人决定在部分导入开始之前离开公司（因为无关的原因），并且第三个人（我自己）想成为一名Scrum Master。因此找了一个新的人选来担任（部分产品PO）角色。他从公司另一个部门的测试主管角色转过来。让一个新人担任这个角色也强调了一种新方法的导入开始了的事实。

To improve adaptiveness it would have been even better if the role would have been filled by the existing _product manager_, a classic Scrum choice for someone approaching a real Product Owner, but organizational constraints prevented us from doing that. He was simply from a different department and engineering management was convinced that they needed someone from the engineering department to be responsible for coordination with the other groups in the company.
为了提高适应性，如果这个角色由现有的产品经理担任，那将会更好，一个接近真正PO人选的经典Scrum选择，但组织的限制阻碍了我们这样做。他只是来自一个不同的部门，工程管理层确信，他们需要工程部门的人来负责与公司其他团队的协调。

One of the key tasks of the PM/BAs was to maintain a balance between requests from different groups of stakeholders (see [Figure 8](#figure8)), which consumed a significant part of their working time. By having only _one_ PM/BA it became clear that he could not do this work at the previous level of intensity - some had to be done by the teams themselves. The techniques we used for it were Product Backlog Refinement and common Sprint Planning.
PM/BA的关键任务之一是在不同利益相关方的请求之间保持平衡（见[图8](#figure8)），这占用了他们大部分的工作时间。由于只有1个PM/BA，他显然不能再用以前的标准来做这项工作，有些工作必须由团队自己来做。我们使用的技术是产品待办列表梳理和共同的迭代计划。

#### Product Backlog Refinement 产品待办列表梳理

With one PM/BA per one or two teams, teams were used to a much higher level of detail being given to them in the form of product backlog items, usually in a written form using acceptance criteria. This changed with only one PM/BA. Being alone he had no capacity to analyze requirements coming from stakeholders in detail because he had much more on his plate. He had to spend some portion of his time prioritizing or reporting to management. He also had to manage undone work, tasks existing because of the teams’ insufficient Definition of Done. The teams were encouraged to talk to stakeholders to clarify details of their backlog items. Stakeholders were willing to discuss with engineers, but as they were typically located in different offices (even different time zones) and spoke a different language, clarification constituted a challenge especially for some of our introverted developers. The teams often delegated the clarification to the most eloquent team member, which again created an information bottleneck, delay, information scatter and loss, and more misunderstandings and “requirement defects”
每一个或两个团队有一个PM/BA，团队习惯于给到他们的产品待办条目包含更高程度的细节，通常是使用验收标准的书面形式。只有一个PM/BA改变了这种情况。由于是独自一人，他没有时间详细分析来自利益相关方的需求，因为他有更多的事情要做。他不得不花费部分时间来做优先级排序或向管理层汇报。他还必须管理未完成的工作 - 因为团队不充分的“完成的定义”而存在的任务。团队被鼓励与利益相关方交谈，以澄清他们的待办列表条目的细节。利益相关方愿意与工程师讨论，但由于他们通常位于不同的办公室（甚至是不同的时区），并且使用不同的语言，澄清对我们一些内向的开发人员来说尤其是一个挑战。团队通常将澄清委托给最有口才的团队成员，这再次造成了信息瓶颈、延迟、信息分散和丢失，以及更多的误解和“需求缺陷”。

Also teams were not talking directly to users/customers, but just to internal stakeholders within the company. Even some of these internal groups didn’t talk directly to customers! As a result each group of internal stakeholders came with different ideas of how to implement backlog items and which items to implement first. That generated conflict and a lot of discussions - another consequence of choosing Core as an initial Product.
同时，团队没有直接与用户/客户交谈，而只是与公司内部的利益相关方交谈。甚至一些内部组也没有直接与客户交谈！因此，每一组内部利益相关方对于如何实现待办列表条目以及首先实现哪些条目都有不同的想法。这产生了冲突和大量讨论 - 选择Core作为初始产品的另一个后果。

In other words, by introducing one PM/BA we reduced the number of coordinators and passed some coordinating and clarifying work to the teams (which supports team adaptiveness), but we didn’t significantly reduce the total amount of coordination work.
换句话说，通过引入一个PM/BA，我们减少了协调者的数量，并交给团队一些协调和澄清工作（这支持了团队的适应性），但是我们没有显著地减少协调工作的总量。

##### Try … diverge-merge for backlog refinement 尝试…分散-合并来梳理待办列表

It was interesting to experiment with different formats of the Product Backlog Refinement in a multisite scenario (each team collocated, but teams in multiple sites). Since the beginning we struggled with less interactivity and engagement compared to local sessions. The real, deep discussions happened locally just after the official refinement session had finished. It almost looked like people were waiting for an official end of the meeting so that they could start talking! We tried various experiments to make the sessions more interactive, e.g.
在多地场景中尝试不同形式的产品待办列表梳理很有趣（每个团队都在一地，但不同团队在多地）。从一开始我们就很艰难，互动性和参与度与本地会议相比都较低。真正深入的讨论在正式的梳理会议刚结束之后在本地发生。看起来几乎就像大家都在等待会议的正式结束，以便可以开始交谈！我们曾经尝试了各种实验，以使会议更具有互动性。例如：

* invite external experts to bring more insight,
* have an advocate for each backlog item who studied it before the session,
* use a shared document to work with during the session.

* 邀请邀请外部专家提供更多见解
* 为每个待办列表条目安排一名支持者，该支持者在会议开始前对其进行了研究
* 在会议期间使用共享文档工作

None of them really helped the participants to overcome language, physical and psychological barriers caused by the multi-site setup.
他们都没有真正帮助参与者克服由于多地设置所造成的语言、身体和心理隔阂。

Finally, we iterated towards the following model that uses diverge-merge cycles (loosely inspired by Guide “Multi-Team PBR”, Book 3). We started with an Overall PBR using a wiki page where the PM/BA copied a list of items he wanted to be refined. The teams marked each item for local refinement in Brno or Lviv. Then two local Multi-Team PBRs were organized in parallel where teams refined selected items without site or language barrier. These local sessions were usually attended by all team members.
最后，我们对以下使用分开-合并循环的模型进行了迭代（灵感来源于“多团队PBR”指南，第三本书）。我们用一个维基页面来开启整体PBR，PM/BA在页面上复制了他想要梳理的一列条目。团队对每一个条目进行了标记 - 是在布尔诺还是在利沃夫本地梳理。然后，并行组织两个本地的多团队PBR，在没有地域或语言隔阂的情况下团队来梳理所选的条目。这些本地会议通常所有的团队成员都会参加。

A couple of days later an Overall PBR session was organized. Team reps from one location introduced the results of the local refinements to the team reps from the other location.
几天后再组织了一次整体PBR会议。来自一地的团队代表向来自另一地的团队代表介绍本地梳理的结果。

Sometimes we intentionally let both locations refine the same items in parallel to potentially discover two solutions. This way everybody had a chance to participate in the deep local session as well as keep an overview of the complete backlog.
有时候，我们有意地让两地并行梳理相同的条目，以便可能发现两个解决方案。这种方式使每个人都有机会参加深入的本地会议，同时又能有对完整待办列表的概观。

This model is not ideal and the teams continue to experiment, but we deemed it as good enough at that  time.
这种模式不是完美的，团队还在继续尝试，但是我们认为它当时来说够好了。

#### Sprint planning 迭代计划

Before the LeSS adoption teams had team backlogs.The teams were used to preselect some items from their backlogs and move it to their virtual Sprint space _before_ the Sprint Planning. Also the unfinished items from the previous Sprint were almost automatically added to the currently-planned Sprint.
在LeSS导入之前，团队有各自的团队待办列表。团队习惯于在迭代计划前从他们的待办列表中预先选择一些条目，并将它们移到各自的虚拟迭代空间。此外，前一个迭代中未完成的条目几乎自动地添加到当前计划的迭代中。

The first LeSS Sprint Planning One meeting was different. Not only there was only one (partial) backlog, but also no preselection was used and unfinished items were all returned back to the backlog and teams were told that we were starting from scratch (Guide “Sprint Planning One”, Book 3 - a group of teams with a set of items). In short, all decisions were expected to be made directly on the Sprint Planning One meeting. Teams were surprised but accepted the fact and we began the event. It turned out that some previously preselected and leftover items were no longer the most important and different items were selected for the Sprint. This first planning event was long but a new standard was established.
第一个LeSS的迭代计划一会议则有所不同。不仅只有一个（部分）待办列表，而且没有预先选择，未完成的条目全部放回到待办列表中，团队被告知我们将从头开始（指南“迭代计划1”，第3本书 - 一组团队共享一组条目）。简单来说，就是期望所有决策都直接在迭代计划一会议上做出。团队很惊讶，但是都接受了这个事实，然后我们开始了这个活动。结果是，一些之前预选的和剩余的条目不再是最重要的，而不同的条目被选入了迭代。第一次计划活动的时间有些长，但是一个新的标准被建立了。

Still the Sprint Planning One event suffered from two problems:
迭代计划一活动仍然存在两个问题：

* Sprint planning with 5 (later 6) teams was long and most of the time people passively sit on the call and wait for their turn
* The current tooling was not good enough in visualizing the team’s speculated load for the Sprint.

* 5个（后来6个）团队的迭代计划有些长，多数时候大家被动地坐在电话旁边，等待轮到他们（发言）
* 当前的工具在对团队预测的迭代负载可视化上还不够好

The following sections describe an experiment that tries to overcome these difficulties.
以下部分描述了一个试图克服这些困难的实验。

##### Try … multisite Sprint Planning in a shared document 尝试…在一份共享文档中进行多地迭代计划

The PM/BA chose enough items for one Sprint in a private document by copy-pasting them from the tracking system. The facilitator of the Sprint Planning event prepared the following document with all team reps and the PM/BA having edit access to the document.
PM/BA为一个迭代选择了足够的条目，把它们从跟踪系统复制-粘贴到个人文档中。迭代计划活动的引导者准备了以下文件，所有团队代表和PM/BA都有该文件的编辑权限。

<figure>
<img src="/img/case-studies/solarwinds/sprint-planning-document.png" alt="Sprint Planning shared document">
</figure>

The first five cells constitute space for team Sprint plans. Each cell was identified by a team name (e.g. Columbus, Hubble, Darwin) The sixth cell can contain a general Sprint info (e.g. Sprint goals, public holidays)
前五个单元格构成团队迭代计划的空间。每个单元格都由一个团队名称标识（例如哥伦布、哈勃、达尔文）。第六个单元格可以包含一般的迭代信息（例如迭代目标、公共假日）

The PM/BA started Sprint Planning One by communicating the goals of the Sprint and providing general info. After answering all questions he started copying backlog items to the “Product Backlog” area below the team cells.
PM/BA通过传达迭代目标并提供大体的信息启动了迭代计划一。回答完所有问题后，他开始将待办条目复制到团队单元格下方的“产品待办列表”区域。

Whenever he copied a batch of items to the document, team reps started moving the items to their cells _all at the same time in parallel_. This limits waiting and increases engagement of the team reps in Sprint Planning. When all items from the first batch were distributed, the PM/BA copied the next batch and so on until all teams were full.
每当他将一批条目复制到文档中，团队代表就开始同时并行地将这些条目移动到他们的单元格中。这减少了等待时间，同时增加了团队代表在迭代计划中的参与度。当第一批中的所有条目都被分发后，PM/BA复制下一批，以此类推，直到所有团队都满了为止。

At each moment it was highly visible how many items each team forecasted for the Sprint and their decisions can be challenged by other teams, if any conflict arose it was solved on the spot. For example, when two teams wanted to work on the same item, their reps immediately agreed which team is more suitable for the item, for example if they wanted to learn more.
每时每刻每个团队预测这个迭代做多少条目都高度可视化，其他团队可以挑战他们的决策，如果出现任何冲突则当场解决。例如，当两个团队想要工作同一个条目时，他们的代表会立即约定哪个团队更适合该条目，例如，如果他们想学更多。

Usually the team with the best knowledge took the item, but sometimes a team asked for an item from a new area and if they really wanted it the team with a better knowledge “allowed” them to take it. When no agreement could be reached (a very rare case) we had to roll a (virtual) dice to distribute an item which nobody wanted.
通常知识最丰富的团队会认领条目，但是有时候一个团队也会想要从一个新领域拿一个条目，如果他们真得想要，知识更丰富的团队会“允许”他们拿。当无法达成约定时（这种情况非常罕见），我们不得不掷（虚拟）骰子来分配没有人想要的条目。

After Sprint Planning One was finished the agreed plan was reflected in the tracking system. The PM/BA then informed the rest of the world about the results of the Sprint Planning One. The whole meeting usually didn’t take more than 30 minutes with five teams. It reduced waiting and greatly improved transparency and coordination
迭代计划一完成后，约定的计划会反映到跟踪系统中。然后，PM/BA将迭代计划一的结果通知其他人。整个会议，5个团队参加，通常不会花费超过30分钟。它减少了等待，并大大提高了透明度和协作。

### Number of backlogs reduction 减少待办列表的数量

#### Product Backlog 产品待办列表

Our starting point was having multiple _explicit_ and multiple _implicit_ lists.
我们的起点是有多个显式的和多个隐含的列表。

Each of the PM/BAs had their own _explicit_ list for a few teams.
每个PM/BA都有各自为几个团队（创建）的显式的列表。

And there were many more _implicit_ lists too. That is, if Team X was the specialist for task Y, then Team X did Y, a local optimization which degraded the adaptiveness (agility) of the teams to do new and different work, due to their narrow limited knowledge. In this way, even though there was only **one** _explicit_ list for multiple teams maintained by each PM/BA, in reality there were N _implicit_ lists for the N teams, each for their single specialization.
同时也有更多的隐含的列表。也就是说，如果团队X是任务Y的专家，那么团队X就会做Y。这是一种局部优化，它会降低团队做新的和不同的工作的适应性（敏捷性），因为他们狭窄局限的知识。这样的话，即使每个PM/BA只为多个团队维护一份显式的列表，但实际上，N个有各自单一专业的团队，就会有N份隐含的列表。

With the elimination of the multiple PM/BAs (and their multiple explicit lists) and moving to only one PM/BA for all the teams (the “partial-Product Owner”) these multiple explicit lists disappeared and only one explicit prioritized list was maintained.
随着多个PM/BA（以及他们的多个显式的列表）的消除，并转向所有团队只有一个PM/BA（“部分产品的PO”），多份显式的列表消失了，并只维护一份显式的优先级列表。

Though having one explicit list enables more adaptiveness than multiple lists it still suffered from deficiencies preventing improving adaptiveness significantly:
虽然有一份显式的列表比多份列表更具适应性，但是仍然存在一些不足，阻碍着我们显著提高适应性：

* Most items were not end-2-end customer-oriented _features_, but just component _tasks_
* Only coarse-grained items might possibly benefit stakeholders and prioritization typically happened on this coarse-grained level

* 大多数条目都不是端到端面向客户的的特性，而只是组件任务
* 只有粗粒度的条目才可能使利益相关方受益，优先级排序通常在粗粒度级别上进行

Let’s look at these two issues in detail.
让我们详细看看这两个问题。

#### Lack of customer orientation in product backlog items 产品待办条目缺乏客户导向

The content of the backlog was constrained by two important factors:
待办列表的内容受到两个重要因素的制约：

* initial product definition
* teams setup

* 初始的产品定义
* 团队设置

Both of these factors left some groups outside Core teams intact. Having Core as an initial partial Product meant that _module_ teams existed outside of the initial Product group. Having only developers and testers in the teams meant that architects, UI designers and support reps existed outside of the initial Product teams. All these groups had their own interests and some of these manifested as items in the Core backlog. Some examples:
这两个因素都让Core团队之外的一些组保持了原样。将Core作为初始的部分产品，意味着模块团队存在于初始产品组之外。团队中只有开发人员和测试人员，意味着架构师、UI设计师和支持代表存在于初始的产品团队之外。所有这些组都有自己的利益，并且其中一些表现为Core待办列表中的条目。一些示例：

**Architectural improvements** - Architects (a separate group, see [Figure 4](#figure4)) came up with ideas for new architectural elements that were hypothesized to bring benefit later.
**架构改进** - 架构师（一个单独的小组，见[图4](#figure4)）提出了新架构要素的想法，假设这些要素在以后会带来好处。

**Module requests** - Some requests started as a customer request to a module team. The module team then did a preliminary analysis and realized that the request has a “module part” and a “Core part”. The Core part was put to the Core list often without the original business context.
**模块请求** - 一些请求开始是对模块团队的一个客户请求。模块团队随后进行了初步分析，并意识到该请求有一个“模块部分”和一个“Core部分”。Core部分被放入了Core列表，但经常没有带原始的业务上下文。

**Engineering improvements** - these were brought by engineers themselves and reflected the inability of programmers to improve the Product incrementally.
**工程改进** - 这些改进是由工程师自己提出的，反映了程序员缺乏增量地改进产品的能力。

**Customer features** - a Product manager did the job of market research and brought a couple of coarse grained items to the Core list.
**客户特性** - 一位产品经理做了市场调查的工作，并将几个粗粒度的条目添加到Core列表中。

**Supportability improvements** - Usually brought by support representatives and engineers who worked with real existing customers. They were supposed to address the pain experienced by the current customers.
**可支持性改进** - 通常由支持代表和与真实存在的客户一起工作的工程师带来。这些改进应该可以解决当前客户所经历的痛苦。


#### Coarse-grained prioritization 粗粒度的优先级排序

Two factors influenced the fact that coarse-grained items were the perceived unit of prioritization:
有两个因素影响了粗粒度条目被视作优先级排序单元的事实：

* six-month release cycle driven by The Contract Game
* backlog items were defined by _internal_ stakeholders

* 合同游戏驱动的六个月发布周期
* 待办列表条目由内部的利益相关方定义

We discuss the long release cycle in [later sections](#release-frequency), now we would like to focus on its effect on backlog items. When stakeholders have a one-in-six-month chance to get something into the Product they want it to matter. They see this vast six-month space in front of them and imagine all the big things that can be delivered in this time period. As a result, the items they initially propose are typically bigger than necessary with all the bells and whistles they imagined.
我们将在[后面的章节](#release-frequency)中讨论长发布周期，现在我们会重点关注它对待办列表条目的影响。当利益相关方每六个月才有一次机会将某些东西加入产品时，他们希望这些东西能产生影响。他们看到眼前广阔的六个月空间，想象着在这段时间内能够交付的所有大的东西。因此，他们最初提出的条目通常比必要的要大，带着他们想象的所有浮华虚饰。

The second effect that plays a role here is the fact that the backlog items are not defined by customers themselves but by internal stakeholders - typically company middle managers. The stakeholders spend different amounts of time with real paying customers - some of them close to zero. When they lack direct contact they speculate. When speculating they want to cover all bases (because what if they are wrong) and therefore their proposed backlog items tend to be more complex and bigger than necessary. This effect is stronger with the distance of a stakeholder from the real paying customer/user.
在这里起作用的第二个影响是，待办列表条目不是由客户自己而是由内部利益相关方定义的 - 通常是公司的中层管理人员。利益相关方花费了不同的时间与真正的付费客户在一起 - 其中一些接近于零。当他们缺乏直接联系时，他们会猜测。在猜测时，他们想要面面俱到（因为如果他们错了怎么办），因此他们提议的待办列表条目往往比必要的更大更复杂。随着利益利益相关方与真正的付费客户/用户之间的距离越来越远，这种影响也越来越大。

This thinking is based on the assumption that company top/middle managers know in advance what is best for the customers. This is rarely true. Even if all managers are domain experts (unlikely in a big corporation), they need validation from real paying customers to make sure their prior ideas are beneficial for the customers.
这种想法是基于公司高层/中层管理人员预先知道对客户最有利的是什么的假设。这很少是真的。即使所有的管理者都是领域专家（在大型公司中不太可能），他们也需要得到真正的付费客户的验证，以确保他们先前的想法对客户有益。

Both these effects caused Core partial-Product development to be organized as a series of projects (called releases). Each project had its defined deliverables (coarse-grained items). To finish a deliverable a series of tasks has been defined. These tasks formed a list that teams used for their Sprint Planning - fake partial-Product Backlog (see [Figure 9](#figure9)). Stakeholders were only interested in progress towards finishing these big coarse-grained deliverables.
这两种影响导致Core部分产品开发被组织为一系列的项目（被称为版本）。每个项目都有它定义的交付物（粗粒度条目）。为了完成交付物，一系列任务被定义。这些任务形成了团队用于迭代计划的列表 - 伪的部分产品待办列表（见[图9](#figure9)）。利益相关方只对完成这些粗粒度交付物的进展感兴趣。

<a name="figure9"></a>
<figure>
<img src="/img/case-studies/solarwinds/work-breakdown-project.jpg" alt="Work Breakdown of Project">
  <figcaption>Figure 9: Example of work breakdown structure of one project.</figcaption>
</figure>

This stands in stark contrast with a true Product Backlog idea according to Scrum: an ordered list of independent potentially-valuable items that can be finished in one Sprint, which is adapted (items added, removed, changed priority) every Sprint based on learning, and  prioritized by a true Product Owner. Why did such deviation happen?
这与Scrum所说的真正的产品待办列表理念形成了鲜明对比：一个有序列表，包含了可以在一个迭代中完成、且有独立潜在价值的条目，该列表在每个迭代都会基于学习来进行调整（添加或删除条目、更改优先级），并由真正的PO进行优先级排序。为什么会发生这种偏差？

Items in our lists were not independent because each of them belonged to one deliverable - each item was interesting only to the point, to which it contributed to finishing the deliverable. Item independence was not appreciated by anyone in the company. Not by stakeholders (they wanted deliverables), not by PM/BAs (they wanted to finish deliverables to stakeholder’s satisfaction).
我们列表中的条目不是独立的，因为每一个都属于同一个交付物 - 每个条目的意义在于它对完成交付物的贡献。条目的独立性并不被公司里的所有人重视。不被利益相关方重视（他们需要交付物），也不被PM/BA重视（他们想要完成交付物以满足利益相关方）。

For the same reasons the items were typically not small and were often not finished in one Sprint. It didn’t matter whether one item was finished, it mattered how it contributed to finishing the respective deliverable.
出于同样的原因，这些条目通常并不小，而且往往不会在一个迭代中完成。一个条目是否完成并不重要，重要的是它如何帮助完成各自的交付物。

Item ordering was not absolute but rather followed a two-dimensional scheme shown in [Figure 9](#figure9). PM/BA had the right to prioritize items in one column, while deliverables were prioritized by the product manager - another indicator that the product manager should become a true Product Owner.
条目排序不是绝对的，而是遵循[图9](#figure9)所示的二维方案。PM/BA有权在一列中对条目进行优先级排序，而交付物则由产品经理进行优先级排序 - 这是产品经理应成为真正的PO的另一个指示。

Why did stakeholders want big deliverables? We’ve already mentioned two reasons: big expectations and covering what-if scenarios caused by the six-month long release cycle. Let’s add another important one. In a company with multiple management layers lower and mid-level managers will _not_ have business success of the developed Product as their primary objective (implicit or explicit). In fact, they _can’t_ have business success as their objective, since their scope of influence is just a narrow set of components or a predefined set of items to deliver in “the project” (all part of the Contract Game). So they will focus on “delivering features”, especially if the added feature is clearly visible or its idea can be sold internally in the company. In other words, they prefer predefined big-bang deliverables to small incremental improvements that are adaptively based on learning and feedback.
为什么利益相关方想要大的交付物？我们已经提到了两个原因：巨大的期望，以及六个月长的发布周期导致想要覆盖各种假设场景。让我们再加一个重要的原因。在一个有多层管理的公司中，中低层管理人员不会将开发产品的业务成功作为他们的主要目标（隐含的或显式的）。事实上，他们不可能以业务成功为目标，因为他们的影响范围只是“项目”（合同游戏的所有部分）中要交付的一小组组件或一组预定义的条目。因此，他们将专注于“交付特性”，尤其如果添加的特性清晰可见，或者它的创意可以在公司内部推销时。换句话说，他们更喜欢预定义的大爆炸式交付物，而不是基于学习和反馈自适应的小的增量改进。

Focus on big deliverables obviously reduces adaptiveness at a global level. If the delivered items are big, they take longer time to deliver, which delays customer feedback and delays validation of our hypotheses/speculation about customer behavior. Also, implementing bigger items tends to bring more complexity to the Product and codebase which makes further development more costly and further reduces adaptiveness.
专注于大的交付物显然会降低全局的适应性。如果交付的条目较大，它们的交付时间也会较长，这会延迟客户反馈，并延迟我们对客户行为的假设/猜测的验证。同时，实现更大的条目往往会给产品和代码库带来更大的复杂性，使得后续开发成本更高，并进一步降低适应性。


#### Impact of big deliverables on opportunity cost 大的交付物对机会成本的影响

Big deliverables are also more likely to contain a mixture of probable higher-impact items and probable lower-impact items. Holding shipping of probable higher-impact items until all probable lower-impact items are ready to ship brings opportunity cost to the company. Let’s demonstrate it in an example.
大的交付物也更有可能混合了潜在高影响条目和潜在低影响条目。暂缓发布潜在高影响条目，直到所有潜在低影响条目都准备好（发布），会给公司带来机会成本。让我们用一个示例来演示它。

We have a deliverable consisting of two items - I1 and I2. I1 is hypothesized to have impact 100 (imagine e.g. increased sales by $100,000), I2 is hypothesized to have impact 50. Now imagine that there is an item I3 with the hypothesized impact 75 in the backlog and waiting for a team to pick up. If we decide to deliver items I1 and I2 (because they are part of the same deliverable) then our opportunity cost is 75-50 = 25. The bigger the deliverable is, the more likely it is that at least some items in the backlog have higher probable impact than the unfinished parts of the deliverable currently being worked on.
我们的交付物包括两个条目 - I1和I2。假设I1有100个影响值（想象成销售额增加10万美元），假设I2有50个影响值。现在想象一下，在待办列表中有一个假设影响值为75的条目I3，正在等待团队来取。如果我们决定交付条目I1和I2（因为它们是同一交付物的部分），那么我们的机会成本是75-50=25。交付物越大，更有可能至少待办列表中的一些条目比当前正在开发交付物中的未完成部分有较高的潜在影响。

#### Reducing planning duration and complexity 降低计划持续时间和复杂性

Six-month release cycle combined with wishlists from multiple groups of stakeholders led to another common problem - to estimate and plan a large number of backlog items in the beginning of the six-month cycle. This was now exacerbated by the fact that there was only one backlog instead of five - the list was much longer and we wanted all teams to participate in estimates and the planning process.
六个月的发布周期再加上来自多组利益相关方的愿望清单，导致了另一个常见的问题 - 在六个月周期开始时去估算和计划大量的待办列表条目。现在由于只有一份而不是五份待办列表，这一情况更加严重了 - 列表更长，并且我们希望所有的团队都能参与估算和计划过程。

Before the adoption, the estimation and planning process took a significant amount of time and effort. In the further text, we describe two concrete experiments that allowed us to reduce planning overhead (waste from the lean point of view) - using affinity grouping estimates for the backlog and using the “Buy a feature” game for planning with many stakeholders.
在导入之前，估算和计划过程花费了大量的时间和精力。在接下来的文字中，我们描述了两个能使我们降低计划开销（从精益的角度来看是浪费）的具体实验 - 对待办列表使用相似性分组估算，和使用“购买特性”游戏来与许多利益相关方一起计划。

Once again though, let us emphasize that this improvement in adaptiveness was relatively minor (an order of magnitude smaller) compared to the situation, when a broadly-defined Product is delivered by feature teams frequently to customers and feedback is gathered directly from customers. Nevertheless, we thought these experiments might be worth sharing because all were triggered and made possible by the fact that we merged three lists into one.
让我们再次强调，与特性团队频繁交付给客户一个广泛定义的产品，并直接从客户那里收集反馈的情况相比，这一改进对适应性的影响相对较小（小一个数量级）。然而，我们认为这些实验可能值得分享，因为这一切都是通过将三份列表合并为一份列表这一事实所触发并成为可能的。

##### Try … Reduce planning duration by using affinity grouping estimates 尝试…通过使用相似性分组估算来缩短计划的持续时间

Asking for estimates for deliverables took a significant amount of time. How did it work? Deliverable definitions were typically very fuzzy, sometimes as much as “support monitoring of device X”. Engineers did not feel comfortable to provide an estimate for such a fuzzy requirement and asked for research time. “Research” (in fact a synonym for upfront requirement analysis) was planned as a product backlog item for the next Sprint. When the Sprint was over, the outcome of the research was consulted with the stakeholder who requested the feature. This often led to another research item in the next Sprint and so on.
要求对交付物进行估算花费了大量时间。它是如何工作的？交付物的定义通常非常模糊，有时甚至与“支持设备X的监控”一样模糊。工程师们对给这样一个模糊需求提供估算感到不自在，因而要求研究的时间。“研究”（实际上是前期需求分析的同义词）被计划作为下一个迭代的产品待办条目。当迭代结束时，研究的结果会给请求该特性的利益相关方咨询。这常常导致在下一个迭代又一个研究条目，以此类推。

To reduce this ping-pong we asked teams to do a time-boxed one week research on all deliverables given by the business. After this period we organized a one-hour estimation session with representatives from all teams. As a preparation for this session we prepared a Trello board with 5 empty columns (XS - XL) prefilled with examples of features finished in the last six-month cycle. As these items were finished, their size was known so they can be assigned to the appropriate columns (see [Figure 10](#figure10)).
为了减少这种来回，我们要求团队对业务提供的所有交付物进行定期一周的研究。在这段时间之后，我们与所有团队的代表组织了一个小时的估算会议。作为本次会议的准备，我们准备了一个Trello板，其中有5个空列（XS-XL），预先填充了在过去六个月周期内完成的特性示例。因为这些条目已经完成了，所以它们的大小是已知的，可以将它们分配到合适的列（参见[图10](#figure10)）。

<a name="figure10"></a>
<figure>
<img src="/img/case-studies/solarwinds/trello-before-estimation.png" alt="Trello before estimation">
  <figcaption>Figure 10: Trello board before the estimation session.</figcaption>
</figure>

The first column of the board was pre-filled with titles of all the coarse-grained items. At the session the team representatives took the trello cards one by one in a round-robin fashion and moved them to the appropriate columns. Always one item was moved by one person. If the next person disagreed he/she can move the already assigned item to a different column instead of assigning a new feature. Finished item served as reference for better comparison especially at the beginning of the session when only a few new items had been assigned.
板的第一列预先填写了所有粗粒度条目的标题。在会议上，团队代表以轮流的方式将Trello卡片一张一张地移动到合适的列中。总是一个条目被一个人所移动。如果下一个人不同意，他/她可以将已分配的条目移动到其它列，而不是分配一个新的特性。完成的条目用作参考，以帮助更好的比较，特别是在会议开始时，只有几个新的条目已经被分配。

The session typically took about an hour and resulted in an item distribution shown in [Figure 11](#figure11). The columns were then assigned numbers corresponding to the number of fine-grained backlog items corresponding to each deliverable. The number was estimated using the finished-items examples.
这个会议通常需要花费大约一个小时，结果是如[图11](#figure11)所示的条目分布。然后，根据每个交付物对应的细粒度待办列表条目的数量，来为这些列分配相应的数字。这个数字是使用已完成条目的示例来估算的。

We didn’t use story points for individual backlog items, but rather followed the #NoEstimates assumption that all backlog items are of the same size _on average_, the assumption backed by historical data in our case.
我们没有对单个待办列表条目使用故事点，而是遵循#不估算（#NoEstimates）假设，即所有待办列表条目平均来说大小相同，这一假设在我们的案例中有历史数据的支持。

Another observed effect was playing it safe for vague items. For example, the “AddNode API restructuring” item in the picture below ended up in the last column (XL) just because the teams knew nearly nothing about it at the time of estimation. This clearly indicated to the item donors (architects in this case) to communicate more with the teams regarding the item content.
另一个观察到的效果是对模糊的条目谨慎行事。例如，下图中的“AddNode API重构”条目最终出现在最后一列（XL），因为团队在估算时对它几乎一无所知。这清楚地表明条目的提出人（本例中为架构师）需要就条目的内容与团队进行更多的沟通。

<a name="figure11"></a>
<figure>
<img src="/img/case-studies/solarwinds/trello-after-estimation.png" alt="Trello after estimation">
  <figcaption>Figure 11: Trello board after estimation session.</figcaption>
</figure>

Time-boxing the research and doing all estimations in one hour helped us reduce time needed for the planning phase and the teams could spend more time working on the Product, learning by doing.
对研究限定时间以及在一个小时内完成所有估算，帮我们减少了计划阶段所需要的时间，团队因此可以花费更多时间工作在产品上，通过做来学习。

##### Try … Buy a feature game when you have many stakeholders 尝试…“购买特性”游戏，当你有许多利益相关方时

Even after all items were added to one backlog, stakeholders still looked at some items as “theirs” and pushed hard to have them prioritized over the others. This attitude led to the backlog consisting of items satisfying one particular stakeholder instead of a prioritized list that all stakeholders would agree on.
即使在将所有条目添加到一份待办列表中之后，利益相关方仍然将某些条目看作是“他们的”，并努力将其优先于其它条目。这种态度导致（待办列表是）一份是由满足一个特定利益相关方的条目组成的待办列表，而不是由所有利益相关方都同意的经过优先级排序的列表。

To break this dynamic we used the Buy a feature game. First, we prepared the list of all features with estimated costs given by the engineering groups, see section [Try … Reduce planning duration by using affinity grouping estimates](https://docs.google.com/document/d/1T2x4WRlC5IAUPLyHWrtU4ovDfpZTRfBdB9dQ2f-8xZY/edit#heading=h.pw84nzjp8aih). Second, we gave each stakeholder a certain amount of _virtual money_. The table could look like this:
为了打破这种动态，我们使用了“购买特性”游戏。首先，我们准备了所有特性的列表，带有工程组给出的估算成本，请参阅[通过使用相似性分组估算，缩短计划的持续时间](...)一节。其次，我们给每个利益相关方一定数量的虚拟资金。表格可以如下所示：

<style>
    .beforeEstimationTable tr:nth-child(1) { background: lightgray; }
</style>

|                          | Stakeholder | Jeff | Tom | Kate |
|--------------------------|-------------|:----:|:---:|:----:|
|                          | Budget      | 60   | 20  | 20   |
| Feature A                | 40          |      |     |      |
| Feature B                | 25          |      |     |      |
| Feature C                | 15          |      |     |      |
| Feature D                | 20          |      |     |      |
| Feature E                | 50          |      |     |      |
| Feature F                | 20          |      |     |      |
{: .grid_table_with_header .beforeEstimationTable}

Then, we organized the session with all stakeholders where they can invest their money into features. At the end of the session the table could look like this.
然后，我们组织了与所有利益相关方的会议，他们可以将资金投资到特性上。在会议结束时，表格可能如下所示。

<style>
    .afterEstimationTable tr:nth-child(1) { background: lightgray; }
    .afterEstimationTable tr:nth-child(2) td:nth-child(1) { background: lightgreen; }
    .afterEstimationTable tr:nth-child(3) td:nth-child(1) { background: lightgreen; }
    .afterEstimationTable tr:nth-child(4) td:nth-child(1) { background: tomato; }
    .afterEstimationTable tr:nth-child(5) td:nth-child(1) { background: tomato; }
    .afterEstimationTable tr:nth-child(6) td:nth-child(1) { background: tomato; }
    .afterEstimationTable tr:nth-child(7) td:nth-child(1) { background: lightgreen; }
</style>

|                          | Stakeholder | Jeff | Tom | Kate |
|--------------------------|-------------|:----:|:---:|:----:|
|                          | Budget      | 60   | 20  | 20   |
| Feature A                | 40          | 25   | 15  |      |
| Feature B                | 25          | 25   |     |      |
| Feature C                | 15          | 10   | 5   |      |
| Feature D                | 20          |      | 5   |      |
| Feature E                | 50          |      |     |      |
| Feature F                | 20          |      |     | 20   |
{: .grid_table_with_header .afterEstimationTable}

In this artificial example, features A, B and F would be planned into the major release, while features C, D and E would be rejected. Sometimes we organized multiple rounds of buying features so that stakeholders could reallocate their money and spend money from rejected features.
在这个编造的示例中，特性A、B和F将被计划进主要发布，而特性C、D和E则被拒绝。有时候，我们会组织多轮“购买特性”，以便利益相关方重新分配资金，花费来自被拒特性上的资金。

Overall this approach brought better transparency to the planning process and less fights between stakeholders (like Jeff and Tom buying feature A together in the example above). However, it also came with some drawbacks. The Contract Game was still here, although in a more collaborative way - stakeholders assumed that what had been bought will be delivered in a six month release. Also it was difficult to set priorities between the accepted (green) features - again, stakeholders assumed that _all_ features would be delivered.
总的来说，这种方法提高了计划过程的透明度，减少了利益相关方之间的争吵（如上面示例中Jeff和Tom一起购买特性A）。然而，它也有一些缺点。合同游戏仍然存在，尽管以一种更具协作性的方式 - 利益相关方仍然假设购买的内容将在六个月的发布中交付。此外，很难在已接受的（绿色）特性之间设置优先级 - 利益相关方还是认为所有特性都将交付。

### Product broadness effects on team specialization 产品广度对团队专业化的影响

Before the partial LeSS adoption, teams were used to having the work prepared by multiple PM/BAs. Let’s remember that there were three PM/BAs for five Core teams so one PM/BA typically served 1-2 teams.
在部分LeSS导入之前，团队习惯于让多个PM/BA准备工作。记得那时有3个PM/BA对应5个Core团队，因此一个PM/BA通常为1-2个团队服务。

The previous paragraph reveals two interesting facts. First, the work items were prepared to be suitable for _teams_, not individuals - which is consistent with adaptiveness as the highest goal. Second, there were multiple PM/BAs, which led to implicit team specialization. The team specialization did not necessarily respect the component boundaries in the code, but rather boundaries given by the specialization of “their” PM/BA. This kind of single-specialization (even if it is not defined by code boundaries) is _not_ consistent with adaptiveness as the highest goal.
前一段揭示了两个有趣的事实。首先，工作条目是为适合团队而不是个人而准备的，这与适应性作为最高目标是一致的。其次，存在多个PM/BA，这导致了隐性的团队专业化。团队专业化并不必需遵从代码中的组件边界，而是“他们的”PM/BA的专业化所带来的边界。这类单一专业化（即使它不是由代码边界定义的）与作为适应性作为最高目标并不一致。

By replacing three PM/BAs with one we removed the boundaries that nudged the teams to single-specialize and opened the path for broader knowledge and flexibility. No strict code ownership policies were in place so we didn’t have to _unlearn_ anything. We also had an advantage of relying on historical knowledge - some team members developed the partial Product for years and remembered times when they were _not_ single-specialized.
通过将3个PM/BA替换为1个，我们消除了把团队往单一专业化方向推动的边界，为更广泛的知识和灵活性开辟了道路。我们没有严格的代码所有权政策，不需要抛弃已有的进展。我们还有一个优势，可以依靠历史经验 - 一些团队成员多年前就在开发部分产品了，他们记得那时并没有单一专业化。

Of course, primary tools to nudge teams towards broader knowledge are Sprint Planning with a single backlog and Multi-Team Product Backlog Refinement. We mentioned them in the section [Reducing the number of coordinators](#reducing-the-number-of-coordinators). Here, we would like to mention two additional elements that supported this process - communities and maintenance.
当然，推动团队获得更广泛知识的主要工具是1）以单份待办列表进行的迭代计划，2）多团队产品待办列表梳理。我们在“减少协调者的数量”一节中提到了它们。在这里，我们想提及支持这一过程的另外两个因素 - 社区和维护。

#### Communities 社区

The concept of communities was introduced in the company in 2015, about one year before the partial LeSS adoption. Since then several communities have been established (see [Figure 12](#figure12)). Examples include: security community, continuous integration community, hiring community, automated testing community, agile club. The communities were typically not limited to Core but spread across the whole company (although they tended to stay in one location). Engineers were actively encouraged by managers to participate in community life. In general, communities helped their members to get inspired from the other teams or groups and often helped them overcome the local mindset and see the whole. Specifically for the members of the Core teams, participating in the community helped them see Core as a part of a bigger system (Orion product development) and reduced their pushback to learn multiple components of Core during their work.
2015年，大约在部分LeSS导入的一年前，公司引入了社区的概念。从那个时候开始，已经建立了几个社区（见[图12](#figure12)）。示例包括：安全社区，持续集成社区，招聘社区，自动化测试社区，敏捷俱乐部。这些社区通常不限于Core，而是遍布整个公司（尽管他们倾向于在一地）。管理人员积极鼓励工程师参与社区生活。一般来说，社区可以帮助其成员从其他组或团队中获得灵感，而且经常能帮助他们克服局部思维以看到整体。特别是对于Core团队的成员来说，参与社区有助于他们将Core视为更大系统（Orion产品开发）的一部分，从而减少了他们对在工作中学习Core的多个组件的抵制。

<a name="figure12"></a>
<figure>
<img src="/img/case-studies/solarwinds/example-of-communities.png" alt="Example of Communities">
  <figcaption>Figure 12: Examples of communities.</figcaption>
</figure>

#### Handling Maintenance Load 处理维护工作量

The Product we developed historically had a high maintenance load. Why? There are multiple reasons.
我们过去开发的产品的维护工作量很大。为什么？这里有很多原因。

First, it has been caused by the nature of the Product. Orion is an on premise software installed at tens of thousands of customer sites in very diverse environments. Although the perceived product quality is high (judging from the very high percentage of customers renewing their paid maintenance support every year) the diversity of environments still brings unexpected situations that cause customers to report problems.
首先，它是由产品的本质引起的。Orion是一种预置软件，安装在成千上万个客户站点非常多样化的环境中。虽然感观的产品质量很高（从每年续费维护支持的客户比例很高得到的判断），但环境的差异仍然会带来意外的情况，从而导致客户报告问题。

The second reason for high maintenance load  is systemic and company-internal. Each customer problem is primarily handled by a representative of a support department, a group separate from engineering. Support reps handle the vast majority of the issues taken,  but a minority of the most difficult ones had to be handled by the engineering group.
高维护工作量的第二个原因是系统性的和公司内部的。每个客户问题主要由支持部门 - 一个独立于工程部门的组 - 的代表处理，。支持代表处理绝大多数问题，但少数最困难的问题不得不由工程组处理。

In the short term this setup looks like a good idea (see [Figure 13](#figure13)). The more customer problems are handled by a support group, the less open problems we have, the less support reps we need, which creates a balancing cycle B. There is, however, a strong long-term effect. When customer problems are handled by a group separate from product developers, these developers are unaware of customer problems and it is highly likely that they will develop the Product in a way that customers will not like (at least _existing_ customers). If this dynamic is not understood, it creates a reinforcing cycle R of a growing number of customer problems followed by a growing size of the support group.
在短期内，这种设置看起来像是一个好主意（见[图13](#figure13)）。支持组处理的客户问题越多，待解决的问题就越少，需要的支持代表就越少，这就形成了一个平衡（B）回路。然而，这有很强的长期影响。当客户问题由一个独立于产品开发人员的组处理时，这些开发人员不知道客户的问题，他们很可能会开发出客户（至少是现有客户）不喜欢的产品。如果不了解这一动态，它会形成一个增强（R）回路，导致越来越多的客户问题，接着支持组的规模也会不断扩大。

<a name="figure13"></a>
<figure>
<img src="/img/case-studies/solarwinds/dynamics-of-separate-support-group.png" alt="Dynamics of separate support group">
  <figcaption>Figure 13: System dynamics of having a separate support group inside the company.</figcaption>
</figure>

As our adoption was only a partial adoption we didn’t address the fundamental problem described above. Our ambition was only to use the engineering effort spent by maintenance as a learning opportunity that will lead to a better understanding of the whole partial Product and therefore more adaptiveness. As a side effect we expected a slight decrease of customer problems reported.
由于我们的导入只是部分导入，我们并没有解决上述根本问题。我们的目标只是把花在维护上的工程活动用作学习机会，从而更好地理解整个部分产品，从而提高适应性。作为连带影响，我们预计报告的客户问题会略有减少。

Our starting point was 20% of engineering time spent by working on customer problems. A rotating maintenance duty had been established (based on the [Batman idea](https://www.jamesshore.com/Agile-Book/iteration_planning.html) from _The Art of Agile Development_ book, first edition). Every Sprint one of the five teams had been “sacrificed” and dealt only with so-called customer issues. Two advantages were expected. First, the remaining teams will be shielded from unexpected interruptions and switching context in the Sprint. Second, as customer issues come from all areas of the partial Product, teams will learn the whole partial Product over time which will lead to more informed design and implementation decisions when developing new features.
我们的出发点是20%的工程时间用于解决客户问题。一种轮流的维护职责被建立了（基于《敏捷开发的艺术》第一版书中的[蝙蝠侠理念](https://www.jamesshore.com/Agile-Book/iteration_planning.html)）。每一个迭代，5个团队中都有1个被“牺牲”只处理所谓的客户问题。期望有两个好处。首先，剩余的团队可以在迭代中避免意外中断和切换上下文。其次，由于客户问题来自部分产品的所有领域，团队将会随着时间的推移了解整个部分产品，这将导致在开发新功能时有更明智的设计和实现决策。

The number of interruptions slightly decreased, however, the overall situation didn’t improve as the expected learning didn’t happen. Teams hated maintenance duty. In addition to that team members knew they needed to deal with customer issues only once in five Sprints. So the path of least resistance was to delay the customer issue resolution until someone else took over. Several attempts had been made to improve the situation. For example, a group of the most experienced engineers from all teams met every day and discussed the most difficult long-term customer issues. Or we tried to share success stories of fixed customer problems. However, none of these experiments were able to overcome the lack of learning within the teams.
中断次数稍有减少，但总体情况没有改善，因为预期的学习并没有发生。团队讨厌维护职责。除此之外，团队成员知道他们只需要每五次迭代轮到一个迭代处理客户问题。因此，阻力最小的方法是推迟客户问题的解决，直到其他人接手。已经作了几种尝试来改善这一情况。例如，来自所有团队的一组最有经验的工程师每天会面来讨论最困难的长期客户问题。或者我们尝试分享解决客户问题的成功故事。然而，这些实验都无法克服团队里缺乏学习。

After almost two years of experimenting with rotating maintenance duty teams themselves came up with the idea of splitting the partial Product into parts - each team would specialize in certain partial-Product functions and deal with all customer issues related to these functions. (Let us emphasize here that the split didn’t apply to the partial-Product Backlog - teams were still supposed to implement items according to their priority.) This proposal had been implemented and it led to more learning than before although the learning happens in a limited scope only. Moreover, teams were able to identify problems in their parts of the partial Product faster and propose improvements there.
经过近两年的轮流维护责任实验，团队自己提出了将部分产品分拆的想法 - 每个团队都将在某些部分产品功能上专业化，并处理与这些功能相关的所有客户问题（让我们在此强调，这种划分并没有应用于部分产品待办列表的工作 - 团队仍然应该根据优先级来实现条目）。这项建议已经被实现，虽然学习只发生在有限的范围内，但比以前还是有了更多。此外，团队能够更快地识别部分产品中他们负责部分的问题，并提出改进建议。

Interestingly and showing the situational – perhaps even individual – nature of this dynamic, in contrast to the Core group that didn’t (or couldn’t) take advantage from rotating, rotating maintenance duty _was successful_ in other parts of the company. Some smaller groups (up to 4 teams) were able to apply it long-term and it improved their teams’ knowledge of the partial Product. A key difference between these groups and Core is the codebase size and partial-product complexity. Both were an order of magnitude higher for Core so some specialization was probably inevitable, because the cognitive load of understanding the whole partial Product and codebase is too high for the teams.
有趣的是，也显示了这种动态视情景（也许甚至是个人）而定的特征，与Core团队没有（或没能）从轮流中获得益处相比，轮流维护职责在公司的其它部门却是成功的。一些较小的组（最多4个团队）能够长期应用它，并提高了他们团队对部分产品的认识。这些组和Core之间的一个关键区别是代码库大小和部分产品的复杂性。对于Core来说，两者都高出了一个数量级；因此，一些专业化可能是不可避免的，因为理解整个部分产品和代码库的认知负荷对团队来说确实太大了。

In future, when introducing specialization we shall avoid the false dichotomy between “every team knows the whole Product” and “every team must be specialized on a few fixed components”. We shall rather consider the cognitive load of developers to be a system constraint and try to support the highest adaptiveness possible while maximizing the constraint. This is the same dynamic that leads to introducing LeSS Huge, where cognitive limits of the Product Owner are usually the limiting factor.
未来，在引入专业化时，我们应该避免“每个团队都知道整个产品”和“每个团队必须专门处理几个固定组件”之间的错误二分法。我们更应该将开发人员的认知负荷视为一个系统约束，尝试在最大化约束的同时支持尽可能最高的适应性。这也是导致不得不引出LeSS巨型的同一个动态，其中PO的认知限制通常是限制因素。

Multiple approaches can be taken that lead to higher adaptiveness than fixed component assignment. For example, if LeSS Huge is used, teams can be responsible for all customer issues in their customer-oriented areas regardless of the components that they need to know to solve them. Or they could use accidental specialization for distributing customer issues as it is used for backlog items.
可以采取多种方法，带来比固定的组件分配更高的适应性。例如，如果使用LeSS巨型，团队可以负责其面向客户的领域中的所有客户问题，而不用管他们需要了解哪些组件来解决这些问题。或者，他们可以使用偶然的专业化来分发客户问题，就像对待办列表条目采用的方式。


### Release frequency 发布频率

Learning to be _potentially_ able to release software to customers _every Sprint_ is often a major challenge in agile adoptions. When a sequential lifecycle is used, releasing is a big event that requires heroic effort of many individuals and takes weeks if not months (as you can see from the figure below this was also our case). Changing this to frequent releases and following the Guide “Ship at Least Every Sprint” (Book 3) is … difficult. We were not successful in this aspect, mainly because our product definition was too narrow and we had to coordinate releases with other groups in the company.
理解在每次迭代都可能向客户发布软件，这通常是敏捷导入中的一个主要挑战。当使用连续的生命周期时，发布是一个需要许多人英勇努力的成就，需要数周甚至数月的时间（从下图中可以看出，这也是我们的情况）。变更它为频繁发布，并遵循指南“至少在每次冲刺时发布”（第3册）是……困难的。我们在这方面没有成功，主要是因为我们的产品定义太窄，我们必须与公司的其他团队协调发布。

Still, it might be interesting to share some of the analysis that shows how a long release cycle affected adaptiveness of product development.
尽管如此，分享一些分析可能会很有意思，这些分析显示了较长的发布周期是如何影响产品开发的适应性的。

#### Release cycle 发布周期

Core was released to the public every six months. It had always been released together with NPM - a flagship module. The release cycle consisted of four phases shown in [Figure 14](#figure14). As you can see it is a sequential (waterfall) lifecycle with a typical fake Scrum adoption pattern - using fake “sprints” only for the development (which doesn’t improve adaptiveness), and which violates the very meaning of real Sprint: that each ends in a completely Done Product Increment (including all forms of testing)
Core每六个月对外发布一次。它总是与旗舰模块NPM（网络性能监视器Network Performance Monitor）一起发布。发布周期由[图14](#figure14)所示的四个阶段组成。正如你所看到的，这是一个具有典型伪Scrum导入模式的顺序（瀑布）生命周期 - 仅在开发（阶段）使用伪“迭代”（这并不能提高适应性），违背了真正迭代的根本含义：每个迭代都以完全完成（包括所有形式的测试）的产品增量结束。

<a name="figure14"></a>
<figure>
<img src="/img/case-studies/solarwinds/major-release-cycle.png" alt="Major Release Cycle">
  <figcaption>Figure 14: Major release cycle.</figcaption>
</figure>


* **Planning.** The goal of the planning was to fix the content of the whole release (See also [The Contract Game](#the-contract-game) section).
* **Development.** Development was organized in two-week fake Sprints that were really just development increments. Software was typically integrated multiple times a day and each Sprint resulted in a build that could be consumed by modules, but it was _not_ potentially shippable (and lots of _undone_ work, such as regression testing, was growing).
* **Regression testing.** About one month long regression-testing phase where all the previously undone work was planned in order to get the software into a shippable state.
* **Customer Acceptance (CA)**. This one-month phase was used to collect feedback from customers on the new features and overall quality of the Product. It started with a release candidate build given to the customers and ended with the General Availability (GA) milestone.

* **计划。**计划的目标是确定整个版本的内容（也请参阅[合同游戏](#the-contract-game)部分）。
* **开发。**开发被组织成两周的伪迭代，实际上只产出开发增量。软件通常一天集成多次，每次迭代都会生成一个可供模块使用的构建，但它不是潜在可发布的（有许多未完成的工作，如回归测试，一直在增加）
* **回归测试。**大约一个月的回归测试阶段，计划来做所有之前未完成的工作，以让软件达到可交付状态。
* **客户验收（CA - Customer Accepantance）。**这个为期一个月的阶段用于收集客户对产品新功能和整体质量的反馈。它开始于向客户提供一个发布备选构建，结束于达成一般可用（GA - General Availability）里程碑。

#### Historical reasons that prevented more frequent releases 阻碍更频繁发布的历史原因

Delivering once in six months is not ideal when optimizing for rapid feedback from customers that tries to invalidate hypothesized customer value. The thinking behind long releases was of course rooted in management conviction that we know what to do and do not need to try to invalidate our hypotheses.
当我们优化从客户那里获取快速反馈，以试图证伪假设的客户价值时，每六个月交付一次是不理想的。当然，长期发布背后的想法根植于管理层的信念，即我们知道该做什么，不需要试图证伪我们的假设。

There are two important historical reasons why SolarWinds was able to develop successful products for years despite long sequential release cycles. Let’s summarize them here before we move on.
尽管采用很长的顺序发布周期，SolarWinds多年来仍能开发出成功的产品，这里有两个重要的历史原因。

First, over time the company developed multiple surrogate mechanisms to collect feedback. Product Managers spent hours every week on calls with customers, the company employed UX researchers who gathered feedback on the product usability, customers had an opportunity to upvote features on a community portal and the whole CA phase was focused on collecting feedback from the customers.
首先，公司逐渐形成了多种代理机制来收集反馈。产品经理们每周花费数小时与客户通电话，公司雇佣用户体验研究员收集产品可用性的反馈，客户有机会在社区门户网站上投票，整个CA阶段都专注于收集客户的反馈。

Second, the company was implicitly optimized for a six-month release cycle for every product with an online marketing campaign following each public release being the main event. Each campaign drove new sales, maintenance renewals and brand awareness. Six months was determined as an optimal time interval between two subsequent marketing campaigns. With a little exaggeration it can be said that a new product version has always been only a deliverable to the marketing campaign.
其次，公司对每个产品的六个月发布周期进行了隐式优化，每次公开发布后都会进行在线营销活动。每个活动都推动了新的销售、维护更新和品牌认识。六个月被确定为两次连续营销活动之间的最佳时间间隔。稍微夸张点，可以说一个新产品版本一直都只是市场营销活动的一个交付物。

#### Consequences of six-month releases 六个月发布的后果

Long releases of course come with costs. We have already discussed one in the section [Coarse-grained prioritization](#coarse-grained-prioritization) - big deliverables. Big deliverables are a consequence of the need to prepare regular marketing campaigns - it is easier to build marketing around big features rather than around small ones.
当然，长周期发布会带来成本。我们已经在[粗粒度的优先级排序](#coarse-grained-prioritization)一节中讨论了一项 - 大的交付物。大的交付物是需要准备定期营销活动的一个后果 - 围绕大特性而不是围绕小特性更容易进行营销。

As long release is one big (in fact, huge) deliverable itself, it brings all problems described for big deliverables, especially [Opportunity cost](#impact-of-big-deliverables-on-opportunity-cost). We will not repeat the analysis here as it is identical.
由于长周期发布本身就是一个大的（事实上是巨大的）交付物，它带来了描述大的交付物的那些所有问题，特别是[机会成本](#impact-of-big-deliverables-on-opportunity-cost)。我们在此不再重复分析，因为它是相同的。

Other costs are interesting as well, though, especially the ones that create reinforcing loops. For example, if you ship your Product to customers rarely, you typically don’t care too much about the upgrade experience (because upgrade is a rare event). As a consequence, upgrading a Product is usually a pain. People in the company who have to deal with the customers’ upgrades (for example, in the support group) feel the pain and push for less frequent releases so that they do not need to go through the pain often.
不过其它成本也很有趣，尤其是那些形成增强回路的成本。例如，如果你很少将产品交付给客户，那么你通常不会太在意升级体验（因为升级是一种罕见的事件）。因此，升级产品通常是一种痛苦。公司中必须处理客户升级的人员（例如，支持组里的人员）会感受到痛苦，并推动降低发布频率，以便他们不需要经常地经历这种痛苦。

It was the case in our situation. Especially bigger customers had to spend hours, sometimes days upgrading the Product per each new major version released. To revert this trend the company had decided to explicitly invest in improving upgrade experience (one of the so-called “initiatives” in [Figure 4](#figure4)), but at the time of this case study this initiative was at its beginning and no improvement in upgrade experience was observed yet.
在我们的情况中就是如此。特别是较大的客户，每发布一个新的主要版本，就必须花费数小时，有时甚至数天来升级产品。为了扭转这一趋势，公司决定明确投资去改善升级体验（[图4](#figure4)中所谓的“举措”之一），但在撰写本案例时，该举措尚处于起步阶段，还未观察到升级体验的改善。

A lean answer to painful upgrades would be: if it hurts, do it more often. Each public release is an opportunity to identify what exactly makes the customer upgrade experience painful and slow and to address it so that next time they need less time and effort to upgrade. By applying this repeatedly, we would gradually decrease transaction costs of upgrade to (almost) zero that would allow us to upgrade at a whim and (supposedly) earn higher customer satisfaction as a side effect.
对于痛苦升级，一个精益的答案是：如果感到痛，就多做它。每次公开发布都是一个机会，可以识别是什么让客户的升级体验痛苦而缓慢，并解决它，以便下次升级时他们需要更少的时间和精力。通过反复这样做，我们将逐步把升级的交易成本降低到（几乎）为零，这将允许我们随心所欲地升级，并作为连带结果（据推测）会赢得更高的客户满意度。

Long releasing cycles also led to lack of proper test automation - when you release once in a while it is acceptable to do manual testing. And when you need to use manual testing in order to ship the Product, you don’t want to repeat this effort too often - another reinforcing cycle. In our case, manual testing occupied a major part of the regression-testing phase.
长的发布周期还导致缺乏适当的自动化测试 - 当你偶尔发布一次时，可以接受手动测试。当你需要使用手动测试来交付产品时，你就不想经常重复这一工作 - 又一个增强回路。在我们的案例中，手动测试占据了回归测试阶段的主要部分。

Lack of test automation coverage was exacerbated by the fact that Core was only a partial Product - in order to produce a shippable Product Core group had to coordinate the regression testing with module teams. The coordination and testing of all integration points was a manual activity that required a couple of weeks to finish.
缺乏自动化测试覆盖这一问题由于Core只是一个部分产品而加剧了 - 为了产出一个可发布产品，Core组必须与模块团队协调回归测试。所有集成点的协调和测试是一项人工活动，需要两个星期才能完成。

#### The Contract Game 合同游戏

Long release cycle also led to what is known as The Contract Game (Book 2, Section _Thinking About Product Management_). The business side of the organization starts with a long list of requirements. The engineering side provides estimates that make it clear that only one third of the requirements can be delivered in the release. The business side is unhappy and asks engineering leaders to deliver more.
长的发布周期也导致了所谓的合同游戏（第二本书，思考产品管理一节）。组织的业务方开始有一份长长的需求列表。工程方提供了估算，清楚地表明只有三分之一的需求可以在发布中交付。业务方不满意，要求工程领导交付更多。

Both parties meet several times to discuss various options for increasing the group capacity or changing the scope of individual deliverables (the process called “horse trading” in SolarWinds). The horse trading takes up to two months and consumes a significant amount of the engineering group capacity. After two months nobody is happy but only three months are remaining for development within a six-month-long release cycle so all parties quickly agree on something and the development starts. Of course, no one wants to later revisit the question, “Are we still today doing the most skillful things?” And as a result, resources are spent on outputs for which we usually have only weak speculation, which itself may have become invalidated over time.
双方多次会面，讨论增加团队产能或改变单个交付物范围的各种选择（SolarWinds中称为“马匹交易”的过程）。马匹交易需要长达两个月的时间，并消耗了工程组的大量产能。两个月后，没有人感到满意，但是在六个月的发布周期内，只剩下三个月的开发时间了，所以各方很快就一些事情达成一致，然后开始开发。当然，没有人之后想再问这个问题，“我们今天还在做着最高明的事吗？”结果是，资源被花费在那些我们通常只有薄弱推断的产出上，而推断本身随着时间的推移可能已经失效。

Near the end of the cycle engineering realizes that the initial estimates were wrong and another round of negotiation starts. Programmers come with ideas to cut tasks that keep the gist of the big deliverable intact. If they are lucky they will find some. But as the deadline is approaching this is less and less of an option. So programmers look into their _secret toolbox_ and find some magic tools that make the deadline happen with “original scope”. This is the time when they stop refactoring or writing automated tests, do quick fixes of bugs instead of finding root causes and so on.
在周期接近尾声时，工程人员意识到最初的估算是错误的，于是又开始了另一轮谈判。程序员来寻找削减任务但保留大交付物要点的想法。如果幸运的话，他们会找到一些。但随着最后期限的临近，这一选项越来越不可能。因此，程序员查看他们的秘密工具箱，找到一些神奇的工具可以在截止日期前交付“原始范围”。在这个时候，他们会停止重构或编写自动化测试，会没找到根因就快速修复缺陷，等等。

#### Try ... Regular cumulative service packs to gather customer feedback more frequently 尝试…定期的累积服务包，以更频繁地收集客户反馈

Of course the world doesn’t stop when you spend time planning and “executing” on the long major release. Customers that use your Product discover many ways to improve them. Some of these tasks are very difficult to postpone for 6 months or more. Examples include:
然，当你在花时间计划和“执行”长周期的主要发布的时候，世界不会停止。使用你们产品的客户会发现许多改进方式。其中一些任务很难推迟6个月或更长时间。示例包括：

* An important security fix
* A very small improvement that immediately helps close a very large deal
* A bug that affects many customers
* An incompatibility with a new version of another software your Product integrates with

* 一个重要的安全修复
* 一个非常小的改进，但可以立即帮助完成一笔非常大的交易
* 一个影响许多客户的缺陷
* 一个与你们产品集成的其它软件新版本的不兼容

Of course, when shipping to customers every Sprint one can just include all of the above as backlog items and properly prioritize them. With a six-month major release cycle the company used so-called hotfixes to deliver these critical fixes. As we didn’t succeed in shortening the major release cycle (which would be a major improvement towards adaptiveness) we experimented with using hotfixes as a way of collecting feedback and trying to invalidate our hypotheses.
当然，当我们每一个迭代都交付给客户时，可以将上述所有内容作为待办列表条目，并对其进行适当的优先级排序。在六个月的主要发布周期中，公司使用所谓的热补丁来交付这些关键的修复。由于我们没有成功缩短主要发布的周期（这将是对适应性的一个重大改进），我们尝试使用热补丁作为一种收集反馈的方式，并试图证伪我们的假设。

During the partial LeSS adoption we changed the way of releasing hotfixes significantly, in fact turning them into small and regular minor releases.
在部分LeSS导入的过程中，我们显著地改变了发布热补丁的方式，事实上，将它们转变为小型和常规的次要发布。

**First**, we completely automated hotfix installation (no more copying binaries).
**首先**，我们完全自动化了热补丁安装过程（不再复制二进制文件）。

**Second**, we had made hotfixes cumulative, i.e. every new hotfix had to include everything included in the previous hotfixes. By doing this we increased the chance that problems with combination of fixes will be discovered internally before the hotfix will be released to customers.
**其次**，我们让热补丁是累积的，即每个新的热补丁都必须包括以前补丁中的所有内容。通过这样做，我们增加了在发布补丁给客户之前内部发现补丁组合问题的概率。

**Third**, we had changed the installer so that it automatically installs the latest cumulative hotfix whenever a customer installs the latest major release. That increased the number of customers with the latest hotfix installed and thus the amount of feedback on changes released in this hotfix.
**第三**，我们已经改变了安装程序，以便每当客户安装最新的主要发布时，它都会自动安装最新累积的热补丁。这增加了安装了最新热补丁的客户数量，从而增加了对此热补丁中发布的更改的反馈量。

**Fourth,** we defined a regular cadence of cumulative hotfixes  - one every month.
**第四**，我们定义了一个发布累积热补丁的固定节奏 - 每月一次。

**Fifth,** we were able to ship some fixes hidden under feature toggles and enable them for selected customers.
**第五**，我们能够发布一些补丁，通过特性开关将其隐藏，为选定的客户开启它们。

All these changes helped reduce [The Contract Game](#the-contract-game) at least for small items. Stakeholders were much more relaxed at the major release planning because they knew they could ship some of the small critical items in regular hotfixes.
所有这些变化都有助于减少[合同游戏](#the-contract-game)，至少对小的条目而言是如此。利益相关方在主要发布的计划时更加放松了，因为他们知道可以在定期的热补丁中发布一些小的关键条目。


## Conclusion 结论

This case study describes a partial and incremental LeSS adoption in a multi-component product group that was a part of a larger product suite. We decided to use Core (a large set of low-level components) as an initial Product and proceed with adoption in the corresponding multi-component product group consisting of 5 Teams.
本案例描述了，在一个属于大型产品套件一部分的多组件产品部门中，一次部分和增量的LeSS导入。我们决定使用Core（一大批底层组件）作为初始的产品，并在由5个团队组成的对应多组件产品部门中进行了导入。

It was a mistake. It constrained our thinking and organizational changes to one big component and kept many mechanisms that prevented adaptiveness in place - component teams, big batch releases, big deliverables and so on. It would have been better to start with all of Orion as an initial Product, take a LeSS Huge approach and incrementally start the adoption in one true customer-oriented Requirement Area.
这是一个错误。它将我们的思维和组织变革限制在一个大组件上，并保留了许多妨碍适应性的机制 - 组件团队、大批量发布、大的交付物，等等。可能更好的做法是，开始以整个Orion作为初始的产品，采用LeSS巨型的方式，并逐步在一个真正面向客户的需求领域开始导入。

All that said, “the art of the possible” is an important mindset and behavior in organizational change. We didn’t have the senior management support needed to start in the recommended “top-down and bottom-up” LeSS adoption approach, and so we did what we thought we could, learned a lot from that, and did nudge the organization towards some improvements.
尽管这么说，“可能的艺术”是组织变革中的一种重要心态和行为。我们并没有所需的高级管理层支持，来以“自上而下和自下而上”的LeSS导入推荐方式开始，所以我们做了我们认为能做的事情，从中学到了很多东西，并推动组织通向一些改进。

Of course, this key decision allowed us to do only relatively minor improvements towards adaptiveness - reducing the number of fake POs improved Teams’ ability to coordinate, reducing number of backlogs let us reduce the overhead of planning and using a bit broader Product than before helped us reduce Teams single-specialization.
当然，这个关键的决策只允许我们在适应性方面做相对较小的改进 - 减少伪PO的数量；提高了团队的协调能力；减少待办列表的数量，让我们减少了计划的开销；使用比以前更广泛的产品定义帮助我们减轻了团队的单一专业化。

Many aspects affecting adaptiveness remained unchanged though. Component teams (existing due to both lack-of cross-functionality and too narrow product definition) still required a lot of handovers and coordination by managers and other intermediaries. The Product could only be released to customers every six months and each release required a major manual coordination effort. This, too, was a consequence of the initial decision of taking a set of components and calling it a “Product” and we were not able to overcome it even in the years following this case study.
可是，影响适应性的许多方面仍保持不变。组件团队（由于缺乏跨职能和产品定义过于狭窄而存在）仍然需要管理者和其他中间人进行大量的交接和协调。产品只能每六个月发布给客户一次，每次发布都需要大量人工协调精力。这也是拿一批组件放一起称为“产品”的最初决定的后果，我们即使在本案例之后的几年里也无法克服它。

## References 参考文献

I frequently refer to the 3 LeSS books in the text.
我经常在文章中提及三本LeSS书。

**Book 1.** Craig Larman, Bas Vodde: Scaling Lean & Agile Development: Thinking and Organizational Tools for Large-Scale Scrum, 2008

**Book 2.** Craig Larman, Bas Vodde: Practices for Scaling Lean & Agile Development: Large, Multisite, and Offshore Product Development with Large-Scale Scrum, 2010

**Book 3.** Craig Larman, Bas Vodde: Large-Scale Scrum: More with Less, 2016

* **第一本**，精益和敏捷开发大型应用指南
* **第二本**，精益和敏捷开发大型应用实战
* **第三本**，大规模Scrum - 大规模敏捷组织的设计

The other books and resources are directly linked from the text.
其它书籍和资源直接在文章中放入了链接。
