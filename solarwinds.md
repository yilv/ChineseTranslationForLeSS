# Incremental LeSS Adoption at SolarWinds 在Solarwinds的增量LeSS导入

**Disclaimer:** This text describes the situation in one of the SolarWinds product groups until 2017, i.e. roughly three years before the event known as the [Sunburst supply chain attack](https://www.cynet.com/attack-techniques-hands-on/sunburst-backdoor-c2-communication-protocol/) that happened in late 2020. Any statements in the text are unrelated to the attack.
免责证明：本文描述了其中一个SolarWinds产品组在2017年之前的情况，也就是在2020年末发生的被称为“Sunburst供应链攻击”事件大约3年之前。文中的任何描述都与攻击无关。

## Background 背景

SolarWinds is a leading provider of IT management software, its products are used by tens of thousands of IT professionals around the world and allow them to have a better overview of their networks, applications, databases and other elements of the company IT infrastructure. One of its first products, Network Performance Monitor has been in development since 2001.
SolarWinds是领先的IT管理软件供应商，其产品被全球数万IT专业人士使用，使他们能够更好地了解他们的网络、应用程序、数据库和公司IT基础设施的其它元素。作为该公司的首批产品之一，网络性能监视器从2001年就在开发了。

Soon after, the second product with a similar focus followed. Both products together created a family of products called the Orion family.  The company realized that both products have many things in common and created a common platform - Core - the subject of this case study. Core has been developed by a group of 5-6 teams.
不久之后，跟进了第二款有着类似焦点的产品。这两款产品共同形成了一个产品系列，被称为“Orion系列”。该公司意识到这两款产品有许多共同点，于是创建了一个公共平台Core - 本案例研究的主题。Core由5-6个团队开发。

The company was successful and over time added the third, fourth, and even tenth product.
公司是成功的，并且随着时间的推移，增加了第三、第四甚至第十款产品。

This caused the platform to expand the number of use cases to cover. In addition to serving more modules from a technical point of view, the Core teams (which are component teams) needed to coordinate work with more and more module groups (consisting of other component teams). As always with component teams, that led to a complicated planning and estimating process that took months, and of course was significantly invalidated after the planning, due to the realities of change and imperfect insight. The company hired many managers and fake “Product Owners” (actually, project managers and business analysts) to deal with the coordination problems, and with each additional manager prioritization was even more fuzzy because each had their own agenda and priority list. These management “quick fixes”  always “fixed” the situation only temporarily because their long-term effect was increasing the organizational complexity.
这导致该平台扩大了需要覆盖的用户用例的数量。除了从技术角度为更多模块提供服务外，Core团队（是组件团队）还需要与越来越多的模块组（由其他组件团队组成）协调工作。与组件团队一直都有的问题一致，这导致了需要耗时数月的复杂的计划和评估过程，当然，由于实际会有变更和理解偏差，在计划之后评估显然会变得无效。该公司雇佣了许多经理和假的“产品负责人”（实际上是项目经理和业务分析师）来处理协调的问题，每增加一个经理，优先级就会更加模糊，因为每个人都有自己的议程和优先级列表。这些管理上的“速效方案”总只是暂时“解决”了问题，因为它们的长期影响反而是增加了组织的复杂度。

The management was frustrated. There were so many capabilities they wanted to add to Core (new UI look and feel, support for high availability, make customer upgrade experience seamless). But the Core group was so occupied by the module requests and maintaining the current features that it had no capacity to add new capabilities to the product. Management came with the following approach: separate greenfield initiatives each focused on developing a new capability for all modules (e.g. a new UI framework, a new installer) - another instance of a quick fix. Predictably, that further increased the integration complexity and time to deliver the whole product build to customers.
管理层感到沮丧。他们曾经希望在Core中增加许多能力（新的UI样式和感觉，支持高可用性，无缝的客户升级体验）。但是Core组被模块的请求和维护当前特性占用了太多时间，从而没有产能向产品中添加新的功能。管理层采用了如下方法：独立的新建方案小组，每个小组专注于为所有模块增加一种新的能力（例如：一个新的UI框架，一个新的安装程序）- 又一个快速方案的例子。可以预测的是，这进一步增加了集成的复杂度，以及向客户交付完整产品构建的时间。

These quick fixes failed because they didn’t address the root cause - the _existence_ of the Core teams (component teams), since the number of component teams increases planning complexity, dependencies, delay of delivering end-to-end customer features, and the need for coordination. The need for coordination is often handled by adding more coordinators (a management _quick fix_) which further decreases the ability of the teams to understand the whole product and creates a pressure for more strict component boundaries which again increases planning complexity. Of course,the whole vicious cycle can be eliminated or avoided if component teams are removed, or not introduced in the first place. [Figure 1](#figure1) illustrates the dynamics in a system model.
这些速效方案的失败，是因为它们没有设法解决根本原因 - Core团队（组件团队）的存在，因为组件团队的数量增加了计划的复杂度、依赖、交付端到端客户特性的延迟，以及协调的需求。协调需求通常会通过增加更多的协调人（一种管理速效方案）来解决，这进一步降低了团队理解整体产品的能力，同时产生压力以有更严格的组件边界，从而进一步增加了计划的复杂度。当然，如果移除所有的组件团队，或者一开始就没有引入，整个恶性循环就可以被消除或者避免。[图1](#figure1)以一个系统模型呈现了该动态。

<a name="figure1"></a>
<figure>
<img src="/img/case-studies/solarwinds/systems-model-coordination-need.png" alt="Systems Model on Coordination Needs">
  <figcaption>Figure 1: System model of the need for coordination</figcaption>
</figure>

However, Core _was_ introduced as a dedicated component group. Then, predictably, the following dynamic started (referring to [11 laws of systems thinking](https://en.wikipedia.org/wiki/The_Fifth_Discipline) here). Adding a new coordinator was a “quick fix” that temporarily reduced coordination complexity. However as a result, organizational complexity grew, so after a while the need for coordination was even higher than before. (Law 3: Behavior grows better before it grows worse.) The delay between these two events made it more difficult to see. (Law 7: Cause and effect are not closely related in time and space.)
然而，Core是作为一个专用的组件组织被引入的，之后可以预测的是，以下的动态就开启了（参考[系统思考的11条法则](https://en.wikipedia.org/wiki/The_Fifth_Discipline)）。增加一个新的协调员，是一个“速效方案”，暂时降低了协调的复杂度。然而结果是，组织的复杂度增长了，因此一段时间之后，协调的需求甚至比以前更高（法则3：在情况变糟之前会先变好）。这两个事件之间的延迟又使它更难被察觉到（法则7：因和果在时空上并不紧密相连）。

Having more coordinators (and thus higher organizational complexity) was a result of a long-term adhoc response to problems. It has its roots in the past, when the first coordinator was added, and then the next and then next and next. (Law 1: Today’s problems come from yesterday’s solutions). Each of these steps was seemingly innocent and harmless and seemed to make sense at the time - add one more coordinator. (Law 4: The easy way out usually leads back in.) With each additional coordinator, teams and senior management became more addicted to the results of the coordinators work (usually some intermediate artifacts such as a project plan, status report, acceptance criteria written down for each “story”). Soon nobody could imagine organizing work without them. (Law 5: The cure can be worse than a disease.)
拥有更多的协调员（因此更高的组织复杂度）是对问题长期临时响应的结果。它的根源在过去，当第一个协调员被添加的时候，然后就有下一个，一个接一个（法则1：今天的问题来自于昨天的解）。这些步骤中的每一步看似都是无恶意和无害的，而且在当时看起来也有道理 - 再增加一个协调员（法则4：选择最容易的办法往往会无功而返）。每增加一名协调员，团队和高层管理都会变得更加依赖于协调员工作的成果（通常是一些中间的工件，例如项目计划、状态报告、为每个“故事”写下的验收标准）。很快地，没有人能够想象不靠他们组织工作（法则5：对策可能比问题更糟糕）。

## Scope of the Adoption 导入范围

The root cause of the coordination problems and more coordinators was the very existence of component teams, and so the solution is their elimination. But it wasn’t possible to make this structural change because of the false (and false dichotomy) management belief that work organized to (large) component teams is the _only_ way of developing large products..
协调问题和更多协调人的根本原因在于组件团队的存在本身，因此解决方案就是要消除它。但是没能改变这一结构的原因是错误的管理信念（以及错误的两分法） - 相信把工作按（大型）组件团队组织是开发大型产品的唯一方式。

Given the constraint that we couldn’t eliminate the Core group, to at least achieve some minor improvement in increasing adaptiveness and more likely working on valuable items, we decided to change the following organizational design elements for some minor incremental improvements
考虑到我们受限于不能消除Core组，为了至少在提高适应性和更可能工作于有价值的事项上实现一些小范围的改进，我们决定改变以下组织设计要素：

* Define the “Product” as broad as possible
* Reduce the number of explicit and implicit backlogs in the organization
* Reduce number of coordinators

* 定义尽可能广泛的“产品”
* 减少组织中无论是显式的还是隐含的待办列表
* 减少协调员数量

This case study shows how we used these elements to make the first incremental step towards the system optimizing goal of _increased adaptiveness_ to more easily learn and pivot to working on newly-discovered more-valuable items.
本案例展示了我们如何使用这些要素向提高适应性 - 以易于学习并转向工作于新发现的更有价值的事项 - 的系统优化目标迈出第一步。

Because we didn’t eliminate the first-order influencing factor - the existence of component teams - it led to a slow and painful partial LeSS adoption and the improvement towards the system optimizing goal was limited.
由于我们并没有消除一阶的影响因素，也就是组件团队的存在，这导致了缓慢的和痛苦的部分LeSS导入，以及对系统优化目标的改进有限。

For example, the decision to use Core as an initial “Product” didn’t allow us to prepare a potentially-shippable Product more often, which delayed feedback from customers.
例如，使用Core作为初始“产品”的决定让我们没法更频繁地准备一个潜在可交付的产品，这延迟了来自客户的反馈。

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
另一方面，这里存在这样一种风险，即部门代表组件团队，因此最初定义的“产品”将仅覆盖一组组件，而不是真正的以客户为中心的端到端产品。同时，没有架构变革的话，很容易忽略LeSS实践的能达到什么预期的深度（前端到后端），作为其他支持角色或者中间的工件将可能保持不变，因为它们需要服务于不参与LeSS实践的部门，并且可能妨碍实践组。因此，虽然最初的实践可能更容易，但是组织剩余部分的力量可能足够强大，可以在之后恢复最初的变革。

Another weakness of starting with a partial product definition that is only a set of components (rather than a true front-to-back definition) relates to manager status quo political games: The managers of the existing component teams will want to keep the existing structures so that their positions are not threatened. By allowing a “Product” definition to start with just a set of components opens the door to distorting the change intention so that components can be incorrectly called a “Product” and then component managers can be (fake) “Product Owners.” This has been observed many times in the myriad fake “scaling agile” adoptions around the world.
从只是一组组件（而不是真正的前端到后端的定义）的部分产品定义开始的另一个缺点与管理者目前的政治博弈有关：现有组件团队的管理者希望保留现有的架构，以使其职位不受威胁。允许“产品”定义仅从一组组件开始打开了扭曲变革意图的大门，从而组件可以被错误地称为“产品”，然后组件管理者可以成为（假的）“产品负责人”。这已经在世界各地许多虚假的“规模化敏捷”导入中被多次观察到。

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
我们相信，这个部分产品之后将作为其他部门的榜样 - 交付面向客户的特性时减少了对管理者协调的需求。然而，后来我们意识到这不是一个好的第一选择。特别地，Core主要是一个多组件的组，服务于内部相关方而不是客户，这一事实导致了如下典型问题：

* Partial-Product Backlog was full of technically-oriented component tasks instead of end-to-end customer features (see section [Product Backlog](#product-backlog))
* Major coordination effort was still required to integrate Core work with module and initiative work to deliver customer-oriented features. A customer-oriented feature often needed implementation in both module and Core codebase. Due to the fact that both groups had different partial-Product Backlogs, this work had to be planned, tracked and checked at the end.
* One month long test phase before each release was another example of coordination effort required between modules and Core.

* 部分产品待办列表充斥着技术导向的组件任务，而不是端到端的客户特性（参见[产品待办列表](#product-backlog)一节）
* 仍然需要大量的协调努力，将Core的工作与模块和新方案工作整合起来以交付面向客户的特性。一个面向客户的特性通常需要在模块和Core代码库两者中实现。由于两个组有不同的部分产品待办列表，最后这项工作不得不被计划、跟踪和检查。
* 每次发布前一个月的测试阶段是在模块和Core之间需要协调努力的另一个例子。

For completeness, there was one more reason considered but dropped against choosing “Core” as the initial scope of the product definition, which we were aware of from the beginning: the fact that the Core teams had been located in two sites (Brno, Czech Republic and Lviv, Ukraine). We had at least a little concern that including two sites of teams in the first step of the change would be too risky. Moreover, the Lviv teams had been employees of a vendor, not SolarWinds itself. However, this disadvantage was perceived as relatively small. Nevertheless, we were careful to overcome communication boundaries that naturally arose and including the two sites didn’t turn out to be a major obstacle.
为了完整起见，我们还曾考虑但又放弃了一个反对选择“Core”作为产品定义初始范围的原因，我们从一开始就意识到：Core团队位于两地（捷克的布尔诺和乌克兰的利沃夫）的事实。我们至少有一点担心，在变革的第一步就包括两地的团队会太冒险。此外，利沃夫团队是供应商的员工，而不是SolarWinds自己的员工。然而，这一不利条件被认为相对较小。尽管如此，我们还是小心地克服了由地域自然产生的沟通边界，结果包括这两地并没有成为一个主要障碍。

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


## Steering part of the organization towards more adaptiveness

Defining the initial “Product” as Core (essentially, a big component) constrained further changes we could make. This section will describe how we reduced the number of coordinators, reduced the number of backlogs, and it also outlines some effects of a slightly broader product definition on team coordination.

Before we do this, let's recall some aspects that were common to all these activities - my personal role in the engineering group and education of people before adoption.

### History

In 2015, about a year before this case study, I was a member of a group that introduced “Scrum” to the company, which in retrospect mostly meant introducing _Scrum theater_ in the company, with one notable exception. We established the concept of a Team: 5-9 members, long-term membership, partly cross-functional (programmers and testers), but not cross-component across all the components of Core. In 2016, I accepted a position of one of the many inter-team and inter-group coordinators. My official title was “Product Owner”, but as usual in most “agile” faux adoptions, it was just a synonym for a project manager. My assignment was Core. With five teams working in one group I was looking for better ways of organizing the work, for example prioritizing the backlog based on global priorities or looking for ways to gather feedback from customers more often. Starting with LeSS seemed like a natural choice.

### Education

I gave the third LeSS book to two first-level line managers and a potential partial-Product Owner and asked them to read chapter 2 (_Introduction of LeSS_). Scrum Masters had discussed LeSS a couple of times in their community. I had the most LeSS knowledge - reading all three LeSS books and working as a Scrum Master in a large-scale context for 12 years. And that was it.

In retrospect, the education was desperately insufficient. LeSS adoptions are complex and need deep understanding of all involved participants - management (both first-level and higher management), engineers, Scrum Masters, business departments. All these people need to thoroughly understand the effects of the organizational structure elements on teams and the whole organization before the adoption starts. It is a warning to all people eager to start LeSS adoptions not to start them too early - not before they understand the organizational design and dynamics of their organization.

### Reducing the number of coordinators

#### Core organizational structure before adoption

Core engineering group was organized into teams (see [Figure 7](#figure7)). Teams were typically long-term, the same people stayed together for months or even years until natural attrition or the need for fresh air into the team. Each team had a name of their own choice, for example, Hubble, Legend, Darwin. The team size was usually 5-9 members with the bias towards the lower end of the scale. The teams consisted of developers (mostly C#, rarely other languages) and testers. The teams were always collocated. (Guide “Team Based Organization”, Book 3) Typically, members of a team reported to the same engineering manager and a single manager managed two teams. Scrum Masters existed as well and they had been part-time team members.

Other roles outside of the teams still existed, for example, UI designers, documentation writers and architects. These employees fell under different management structures and they were often located in different countries like the US. Of course, it reduced adaptiveness because teams could only deliver features preprocessed or post-processed by these other specialists and could not easily change course. This aspect is visible on FTAM on [Figure 6](#figure6). Also, the existence of these roles generated some amount of coordination work, which has been mostly handled by dedicated coordinators.

In contrast, if we use real Scrum teams we include all these roles in the teams and as a consequence coordination work would mostly happen inside self-managing teams without the need for external coordinators.

<a name="figure7"></a>
<figure>
<img src="/img/case-studies/solarwinds/core-group-organizational-structure-before-less.png" alt="Core Group Organizational Structure before LeSS">
  <figcaption>Figure 7: Core group organizational structure before LeSS adoption</figcaption>
</figure>


Engineering managers and the fake “Product Owners” (in fact project managers and business analysts = PM/BA) reported to one senior manager who bore ultimate responsibility for Core.

The teams were placed in two locations: two teams in Brno, Czech Republic, three teams in Lviv, Ukraine. The three Ukrainian teams were not employees of SolarWinds, but hired by a vendor company and working for SolarWinds based on contract. However, all of the above is valid also for vendor employees - they were organized in long-term teams consisting of developers and testers. No other product development roles were present on the vendor side. The most experienced vendor employees worked for SolarWinds for close to 10 years.

The vendor teams didn’t formally report to SolarWinds management but to local vendor management. The vendor organization appointed a contact person that served as a counterpart of the senior manager for people-related decisions like hiring or firing developers. Other than that the contact person had no authority over the work of the teams.


#### Fake “Product Owner” (PM/BA)

Work items for teams had been prepared by fake “Product Owners” who were not that, but just people doing project management and business analysis activities (PM/BA). They were also responsible for coordinating team work with other teams in different groups (e.g. modules) and with other roles (e.g. UI designers), see [Figure 8](#bookmark=id.knp43jun34lm).

As a consequence, PM/BAs had so much on their plate that they could rarely manage more than two teams. When more than two teams were needed a new organizational unit was created with another PM/BA. Core had five teams with three PM/BAs.

For Core, coarse-grained backlog prioritization was done by one Product Manager who was responsible for communication with customers and other parts of the business like top management, sales or marketing. He should have been the one and only one person playing the role of (partial Product) Product Owner.

<a name="figure8"></a>
<figure>
<img src="/img/case-studies/solarwinds/communication-paths-pm.png" alt="Communication Paths of the PM">
  <figcaption>Figure 8: Key groups and their communication paths to the PM/BA.</figcaption>
</figure>

#### Reducing the Number of Coordinators

[Figure 7](#figure7) shows that there were three PM/BAs assigned to Core. We decided to reduce this number to _one_ to reduce the number of coordinators and to create pressure for teams to start coordinating their own work. So the next step was convincing three individuals skilled at business analysis and project management to find a new role - a usual problem even for partial LeSS adoption which is explored in the Guide “Job Safety, but not Role Safety”.

Fortunately for the adoption (though not so much for the company), two of them decided to leave the company before the partial adoption started (for unrelated reasons) and the third one (myself) wanted to be a Scrum Master. So a new person for the role was found. He transitioned from a different part of the company and also changed his role from a test lead. Having a new person in the role emphasized the fact that the adoption of a new approach starts.

To improve adaptiveness it would have been even better if the role would have been filled by the existing _product manager_, a classic Scrum choice for someone approaching a real Product Owner, but organizational constraints prevented us from doing that. He was simply from a different department and engineering management was convinced that they needed someone from the engineering department to be responsible for coordination with the other groups in the company.

One of the key tasks of the PM/BAs was to maintain a balance between requests from different groups of stakeholders (see [Figure 8](#figure8)), which consumed a significant part of their working time. By having only _one_ PM/BA it became clear that he could not do this work at the previous level of intensity - some had to be done by the teams themselves. The techniques we used for it were Product Backlog Refinement and common Sprint Planning.


#### Product Backlog Refinement

With one PM/BA per one or two teams, teams were used to a much higher level of detail being given to them in the form of product backlog items, usually in a written form using acceptance criteria. This changed with only one PM/BA. Being alone he had no capacity to analyze requirements coming from stakeholders in detail because he had much more on his plate. He had to spend some portion of his time prioritizing or reporting to management. He also had to manage undone work, tasks existing because of the teams’ insufficient Definition of Done. The teams were encouraged to talk to stakeholders to clarify details of their backlog items. Stakeholders were willing to discuss with engineers, but as they were typically located in different offices (even different time zones) and spoke a different language, clarification constituted a challenge especially for some of our introverted developers. The teams often delegated the clarification to the most eloquent team member, which again created an information bottleneck, delay, information scatter and loss, and more misunderstandings and “requirement defects”

Also teams were not talking directly to users/customers, but just to internal stakeholders within the company. Even some of these internal groups didn’t talk directly to customers! As a result each group of internal stakeholders came with different ideas of how to implement backlog items and which items to implement first. That generated conflict and a lot of discussions - another consequence of choosing Core as an initial Product.

In other words, by introducing one PM/BA we reduced the number of coordinators and passed some coordinating and clarifying work to the teams (which supports team adaptiveness), but we didn’t significantly reduce the total amount of coordination work.


##### Try … diverge-merge for backlog refinement

It was interesting to experiment with different formats of the Product Backlog Refinement in a multisite scenario (each team collocated, but teams in multiple sites). Since the beginning we struggled with less interactivity and engagement compared to local sessions. The real, deep discussions happened locally just after the official refinement session had finished. It almost looked like people were waiting for an official end of the meeting so that they could start talking! We tried various experiments to make the sessions more interactive, e.g.

* invite external experts to bring more insight,
* have an advocate for each backlog item who studied it before the session,
* use a shared document to work with during the session.

None of them really helped the participants to overcome language, physical and psychological barriers caused by the multi-site setup.

Finally, we iterated towards the following model that uses diverge-merge cycles (loosely inspired by Guide “Multi-Team PBR”, Book 3). We started with an Overall PBR using a wiki page where the PM/BA copied a list of items he wanted to be refined. The teams marked each item for local refinement in Brno or Lviv. Then two local Multi-Team PBRs were organized in parallel where teams refined selected items without site or language barrier. These local sessions were usually attended by all team members.

A couple of days later an Overall PBR session was organized. Team reps from one location introduced the results of the local refinements to the team reps from the other location.

Sometimes we intentionally let both locations refine the same items in parallel to potentially discover two solutions. This way everybody had a chance to participate in the deep local session as well as keep an overview of the complete backlog.

This model is not ideal and the teams continue to experiment, but we deemed it as good enough at that  time.

#### Sprint planning

Before the LeSS adoption teams had team backlogs.The teams were used to preselect some items from their backlogs and move it to their virtual Sprint space _before_ the Sprint Planning. Also the unfinished items from the previous Sprint were almost automatically added to the currently-planned Sprint.

The first LeSS Sprint Planning One meeting was different. Not only there was only one (partial) backlog, but also no preselection was used and unfinished items were all returned back to the backlog and teams were told that we were starting from scratch (Guide “Sprint Planning One”, Book 3 - a group of teams with a set of items). In short, all decisions were expected to be made directly on the Sprint Planning One meeting. Teams were surprised but accepted the fact and we began the event. It turned out that some previously preselected and leftover items were no longer the most important and different items were selected for the Sprint. This first planning event was long but a new standard was established.

Still the Sprint Planning One event suffered from two problems:

* Sprint planning with 5 (later 6) teams was long and most of the time people passively sit on the call and wait for their turn
* The current tooling was not good enough in visualizing the team’s speculated load for the Sprint.

The following sections describe an experiment that tries to overcome these difficulties.

##### Try … multisite Sprint Planning in a shared document

The PM/BA chose enough items for one Sprint in a private document by copy-pasting them from the tracking system. The facilitator of the Sprint Planning event prepared the following document with all team reps and the PM/BA having edit access to the document.

<figure>
<img src="/img/case-studies/solarwinds/sprint-planning-document.png" alt="Sprint Planning shared document">
</figure>

The first five cells constitute space for team Sprint plans. Each cell was identified by a team name (e.g. Columbus, Hubble, Darwin) The sixth cell can contain a general Sprint info (e.g. Sprint goals, public holidays)

The PM/BA started Sprint Planning One by communicating the goals of the Sprint and providing general info. After answering all questions he started copying backlog items to the “Product Backlog” area below the team cells.

Whenever he copied a batch of items to the document, team reps started moving the items to their cells _all at the same time in parallel_. This limits waiting and increases engagement of the team reps in Sprint Planning. When all items from the first batch were distributed, the PM/BA copied the next batch and so on until all teams were full.

At each moment it was highly visible how many items each team forecasted for the Sprint and their decisions can be challenged by other teams, if any conflict arose it was solved on the spot. For example, when two teams wanted to work on the same item, their reps immediately agreed which team is more suitable for the item, for example if they wanted to learn more.

Usually the team with the best knowledge took the item, but sometimes a team asked for an item from a new area and if they really wanted it the team with a better knowledge “allowed” them to take it. When no agreement could be reached (a very rare case) we had to roll a (virtual) dice to distribute an item which nobody wanted.

After Sprint Planning One was finished the agreed plan was reflected in the tracking system. The PM/BA then informed the rest of the world about the results of the Sprint Planning One. The whole meeting usually didn’t take more than 30 minutes with five teams. It reduced waiting and greatly improved transparency and coordination

### Number of backlogs reduction

#### Product Backlog

Our starting point was having multiple _explicit_ and multiple _implicit_ lists.

Each of the PM/BAs had their own _explicit_ list for a few teams.

And there were many more _implicit_ lists too. That is, if Team X was the specialist for task Y, then Team X did Y, a local optimization which degraded the adaptiveness (agility) of the teams to do new and different work, due to their narrow limited knowledge. In this way, even though there was only **one** _explicit_ list for multiple teams maintained by each PM/BA, in reality there were N _implicit_ lists for the N teams, each for their single specialization.

With the elimination of the multiple PM/BAs (and their multiple explicit lists) and moving to only one PM/BA for all the teams (the “partial-Product Owner”) these multiple explicit lists disappeared and only one explicit prioritized list was maintained.

Though having one explicit list enables more adaptiveness than multiple lists it still suffered from deficiencies preventing improving adaptiveness significantly:

* Most items were not end-2-end customer-oriented _features_, but just component _tasks_
* Only coarse-grained items might possibly benefit stakeholders and prioritization typically happened on this coarse-grained level

Let’s look at these two issues in detail.

#### Lack of customer orientation in product backlog items

The content of the backlog was constrained by two important factors:

* initial product definition
* teams setup

Both of these factors left some groups outside Core teams intact. Having Core as an initial partial Product meant that _module_ teams existed outside of the initial Product group. Having only developers and testers in the teams meant that architects, UI designers and support reps existed outside of the initial Product teams. All these groups had their own interests and some of these manifested as items in the Core backlog. Some examples:

**Architectural improvements** - Architects (a separate group, see [Figure 4](#figure4)) came up with ideas for new architectural elements that were hypothesized to bring benefit later.

**Module requests** - Some requests started as a customer request to a module team. The module team then did a preliminary analysis and realized that the request has a “module part” and a “Core part”. The Core part was put to the Core list often without the original business context.

**Engineering improvements** - these were brought by engineers themselves and reflected the inability of programmers to improve the Product incrementally.

**Customer features** - a Product manager did the job of market research and brought a couple of coarse grained items to the Core list.

**Supportability improvements** - Usually brought by support representatives and engineers who worked with real existing customers. They were supposed to address the pain experienced by the current customers.


#### Coarse-grained prioritization

Two factors influenced the fact that coarse-grained items were the perceived unit of prioritization:


* six-month release cycle driven by The Contract Game
* backlog items were defined by _internal_ stakeholders

We discuss the long release cycle in [later sections](#release-frequency), now we would like to focus on its effect on backlog items. When stakeholders have a one-in-six-month chance to get something into the Product they want it to matter. They see this vast six-month space in front of them and imagine all the big things that can be delivered in this time period. As a result, the items they initially propose are typically bigger than necessary with all the bells and whistles they imagined.

The second effect that plays a role here is the fact that the backlog items are not defined by customers themselves but by internal stakeholders - typically company middle managers. The stakeholders spend different amounts of time with real paying customers - some of them close to zero. When they lack direct contact they speculate. When speculating they want to cover all bases (because what if they are wrong) and therefore their proposed backlog items tend to be more complex and bigger than necessary. This effect is stronger with the distance of a stakeholder from the real paying customer/user.

This thinking is based on the assumption that company top/middle managers know in advance what is best for the customers. This is rarely true. Even if all managers are domain experts (unlikely in a big corporation), they need validation from real paying customers to make sure their prior ideas are beneficial for the customers.

Both these effects caused Core partial-Product development to be organized as a series of projects (called releases). Each project had its defined deliverables (coarse-grained items). To finish a deliverable a series of tasks has been defined. These tasks formed a list that teams used for their Sprint Planning - fake partial-Product Backlog (see [Figure 9](#figure9)). Stakeholders were only interested in progress towards finishing these big coarse-grained deliverables.

<a name="figure9"></a>
<figure>
<img src="/img/case-studies/solarwinds/work-breakdown-project.jpg" alt="Work Breakdown of Project">
  <figcaption>Figure 9: Example of work breakdown structure of one project.</figcaption>
</figure>

This stands in stark contrast with a true Product Backlog idea according to Scrum: an ordered list of independent potentially-valuable items that can be finished in one Sprint, which is adapted (items added, removed, changed priority) every Sprint based on learning, and  prioritized by a true Product Owner. Why did such deviation happen?

Items in our lists were not independent because each of them belonged to one deliverable - each item was interesting only to the point, to which it contributed to finishing the deliverable. Item independence was not appreciated by anyone in the company. Not by stakeholders (they wanted deliverables), not by PM/BAs (they wanted to finish deliverables to stakeholder’s satisfaction).

For the same reasons the items were typically not small and were often not finished in one Sprint. It didn’t matter whether one item was finished, it mattered how it contributed to finishing the respective deliverable.

Item ordering was not absolute but rather followed a two-dimensional scheme shown in [Figure 9](#figure9). PM/BA had the right to prioritize items in one column, while deliverables were prioritized by the product manager - another indicator that the product manager should become a true Product Owner.

Why did stakeholders want big deliverables? We’ve already mentioned two reasons: big expectations and covering what-if scenarios caused by the six-month long release cycle. Let’s add another important one. In a company with multiple management layers lower and mid-level managers will _not_ have business success of the developed Product as their primary objective (implicit or explicit). In fact, they _can’t_ have business success as their objective, since their scope of influence is just a narrow set of components or a predefined set of items to deliver in “the project” (all part of the Contract Game). So they will focus on “delivering features”, especially if the added feature is clearly visible or its idea can be sold internally in the company. In other words, they prefer predefined big-bang deliverables to small incremental improvements that are adaptively based on learning and feedback.

Focus on big deliverables obviously reduces adaptiveness at a global level. If the delivered items are big, they take longer time to deliver, which delays customer feedback and delays validation of our hypotheses/speculation about customer behavior. Also, implementing bigger items tends to bring more complexity to the Product and codebase which makes further development more costly and further reduces adaptiveness.


#### Impact of big deliverables on opportunity cost

Big deliverables are also more likely to contain a mixture of probable higher-impact items and probable lower-impact items. Holding shipping of probable higher-impact items until all probable lower-impact items are ready to ship brings opportunity cost to the company. Let’s demonstrate it in an example.

We have a deliverable consisting of two items - I1 and I2. I1 is hypothesized to have impact 100 (imagine e.g. increased sales by $100,000), I2 is hypothesized to have impact 50. Now imagine that there is an item I3 with the hypothesized impact 75 in the backlog and waiting for a team to pick up. If we decide to deliver items I1 and I2 (because they are part of the same deliverable) then our opportunity cost is 75-50 = 25. The bigger the deliverable is, the more likely it is that at least some items in the backlog have higher probable impact than the unfinished parts of the deliverable currently being worked on.


#### Reducing planning duration and complexity

Six-month release cycle combined with wishlists from multiple groups of stakeholders led to another common problem - to estimate and plan a large number of backlog items in the beginning of the six-month cycle. This was now exacerbated by the fact that there was only one backlog instead of five - the list was much longer and we wanted all teams to participate in estimates and the planning process.

Before the adoption, the estimation and planning process took a significant amount of time and effort. In the further text, we describe two concrete experiments that allowed us to reduce planning overhead (waste from the lean point of view) - using affinity grouping estimates for the backlog and using the “Buy a feature” game for planning with many stakeholders.

Once again though, let us emphasize that this improvement in adaptiveness was relatively minor (an order of magnitude smaller) compared to the situation, when a broadly-defined Product is delivered by feature teams frequently to customers and feedback is gathered directly from customers. Nevertheless, we thought these experiments might be worth sharing because all were triggered and made possible by the fact that we merged three lists into one.


##### Try … Reduce planning duration by using affinity grouping estimates

Asking for estimates for deliverables took a significant amount of time. How did it work? Deliverable definitions were typically very fuzzy, sometimes as much as “support monitoring of device X”. Engineers did not feel comfortable to provide an estimate for such a fuzzy requirement and asked for research time. “Research” (in fact a synonym for upfront requirement analysis) was planned as a product backlog item for the next Sprint. When the Sprint was over, the outcome of the research was consulted with the stakeholder who requested the feature. This often led to another research item in the next Sprint and so on.

To reduce this ping-pong we asked teams to do a time-boxed one week research on all deliverables given by the business. After this period we organized a one-hour estimation session with representatives from all teams. As a preparation for this session we prepared a Trello board with 5 empty columns (XS - XL) prefilled with examples of features finished in the last six-month cycle. As these items were finished, their size was known so they can be assigned to the appropriate columns (see [Figure 10](#figure10)).

<a name="figure10"></a>
<figure>
<img src="/img/case-studies/solarwinds/trello-before-estimation.png" alt="Trello before estimation">
  <figcaption>Figure 10: Trello board before the estimation session.</figcaption>
</figure>

The first column of the board was pre-filled with titles of all the coarse-grained items. At the session the team representatives took the trello cards one by one in a round-robin fashion and moved them to the appropriate columns. Always one item was moved by one person. If the next person disagreed he/she can move the already assigned item to a different column instead of assigning a new feature. Finished item served as reference for better comparison especially at the beginning of the session when only a few new items had been assigned.

The session typically took about an hour and resulted in an item distribution shown in [Figure 11](#figure11). The columns were then assigned numbers corresponding to the number of fine-grained backlog items corresponding to each deliverable. The number was estimated using the finished-items examples.

We didn’t use story points for individual backlog items, but rather followed the #NoEstimates assumption that all backlog items are of the same size _on average_, the assumption backed by historical data in our case.

Another observed effect was playing it safe for vague items. For example, the “AddNode API restructuring” item in the picture below ended up in the last column (XL) just because the teams knew nearly nothing about it at the time of estimation. This clearly indicated to the item donors (architects in this case) to communicate more with the teams regarding the item content.

<a name="figure11"></a>
<figure>
<img src="/img/case-studies/solarwinds/trello-after-estimation.png" alt="Trello after estimation">
  <figcaption>Figure 11: Trello board after estimation session.</figcaption>
</figure>

Time-boxing the research and doing all estimations in one hour helped us reduce time needed for the planning phase and the teams could spend more time working on the Product, learning by doing.

##### Try … Buy a feature game when you have many stakeholders

Even after all items were added to one backlog, stakeholders still looked at some items as “theirs” and pushed hard to have them prioritized over the others. This attitude led to the backlog consisting of items satisfying one particular stakeholder instead of a prioritized list that all stakeholders would agree on.

To break this dynamic we used the Buy a feature game. First, we prepared the list of all features with estimated costs given by the engineering groups, see section [Try … Reduce planning duration by using affinity grouping estimates](https://docs.google.com/document/d/1T2x4WRlC5IAUPLyHWrtU4ovDfpZTRfBdB9dQ2f-8xZY/edit#heading=h.pw84nzjp8aih). Second, we gave each stakeholder a certain amount of _virtual money_. The table could look like this:

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

Overall this approach brought better transparency to the planning process and less fights between stakeholders (like Jeff and Tom buying feature A together in the example above). However, it also came with some drawbacks. The Contract Game was still here, although in a more collaborative way - stakeholders assumed that what had been bought will be delivered in a six month release. Also it was difficult to set priorities between the accepted (green) features - again, stakeholders assumed that _all_ features would be delivered.


### Product broadness effects on team specialization

Before the partial LeSS adoption, teams were used to having the work prepared by multiple PM/BAs. Let’s remember that there were three PM/BAs for five Core teams so one PM/BA typically served 1-2 teams.

The previous paragraph reveals two interesting facts. First, the work items were prepared to be suitable for _teams_, not individuals - which is consistent with adaptiveness as the highest goal. Second, there were multiple PM/BAs, which led to implicit team specialization. The team specialization did not necessarily respect the component boundaries in the code, but rather boundaries given by the specialization of “their” PM/BA. This kind of single-specialization (even if it is not defined by code boundaries) is _not_ consistent with adaptiveness as the highest goal.

By replacing three PM/BAs with one we removed the boundaries that nudged the teams to single-specialize and opened the path for broader knowledge and flexibility. No strict code ownership policies were in place so we didn’t have to _unlearn_ anything. We also had an advantage of relying on historical knowledge - some team members developed the partial Product for years and remembered times when they were _not_ single-specialized.

Of course, primary tools to nudge teams towards broader knowledge are Sprint Planning with a single backlog and Multi-Team Product Backlog Refinement. We mentioned them in the section [Reducing the number of coordinators](#reducing-the-number-of-coordinators). Here, we would like to mention two additional elements that supported this process - communities and maintenance.


#### Communities

The concept of communities was introduced in the company in 2015, about one year before the partial LeSS adoption. Since then several communities have been established (see [Figure 12](#figure12)). Examples include: security community, continuous integration community, hiring community, automated testing community, agile club. The communities were typically not limited to Core but spread across the whole company (although they tended to stay in one location). Engineers were actively encouraged by managers to participate in community life. In general, communities helped their members to get inspired from the other teams or groups and often helped them overcome the local mindset and see the whole. Specifically for the members of the Core teams, participating in the community helped them see Core as a part of a bigger system (Orion product development) and reduced their pushback to learn multiple components of Core during their work.

<a name="figure12"></a>
<figure>
<img src="/img/case-studies/solarwinds/example-of-communities.png" alt="Example of Communities">
  <figcaption>Figure 12: Examples of communities.</figcaption>
</figure>

#### Handling Maintenance Load

The Product we developed historically had a high maintenance load. Why? There are multiple reasons.

First, it has been caused by the nature of the Product. Orion is an on premise software installed at tens of thousands of customer sites in very diverse environments. Although the perceived product quality is high (judging from the very high percentage of customers renewing their paid maintenance support every year) the diversity of environments still brings unexpected situations that cause customers to report problems.

The second reason for high maintenance load  is systemic and company-internal. Each customer problem is primarily handled by a representative of a support department, a group separate from engineering. Support reps handle the vast majority of the issues taken,  but a minority of the most difficult ones had to be handled by the engineering group.

In the short term this setup looks like a good idea (see [Figure 13](#figure13)). The more customer problems are handled by a support group, the less open problems we have, the less support reps we need, which creates a balancing cycle B. There is, however, a strong long-term effect. When customer problems are handled by a group separate from product developers, these developers are unaware of customer problems and it is highly likely that they will develop the Product in a way that customers will not like (at least _existing_ customers). If this dynamic is not understood, it creates a reinforcing cycle R of a growing number of customer problems followed by a growing size of the support group.

<a name="figure13"></a>
<figure>
<img src="/img/case-studies/solarwinds/dynamics-of-separate-support-group.png" alt="Dynamics of separate support group">
  <figcaption>Figure 13: System dynamics of having a separate support group inside the company.</figcaption>
</figure>

As our adoption was only a partial adoption we didn’t address the fundamental problem described above. Our ambition was only to use the engineering effort spent by maintenance as a learning opportunity that will lead to a better understanding of the whole partial Product and therefore more adaptiveness. As a side effect we expected a slight decrease of customer problems reported.

Our starting point was 20% of engineering time spent by working on customer problems. A rotating maintenance duty had been established (based on the [Batman idea](https://www.jamesshore.com/Agile-Book/iteration_planning.html) from _The Art of Agile Development_ book, first edition). Every Sprint one of the five teams had been “sacrificed” and dealt only with so-called customer issues. Two advantages were expected. First, the remaining teams will be shielded from unexpected interruptions and switching context in the Sprint. Second, as customer issues come from all areas of the partial Product, teams will learn the whole partial Product over time which will lead to more informed design and implementation decisions when developing new features.

The number of interruptions slightly decreased, however, the overall situation didn’t improve as the expected learning didn’t happen. Teams hated maintenance duty. In addition to that team members knew they needed to deal with customer issues only once in five Sprints. So the path of least resistance was to delay the customer issue resolution until someone else took over. Several attempts had been made to improve the situation. For example, a group of the most experienced engineers from all teams met every day and discussed the most difficult long-term customer issues. Or we tried to share success stories of fixed customer problems. However, none of these experiments were able to overcome the lack of learning within the teams.

After almost two years of experimenting with rotating maintenance duty teams themselves came up with the idea of splitting the partial Product into parts - each team would specialize in certain partial-Product functions and deal with all customer issues related to these functions. (Let us emphasize here that the split didn’t apply to the partial-Product Backlog - teams were still supposed to implement items according to their priority.) This proposal had been implemented and it led to more learning than before although the learning happens in a limited scope only. Moreover, teams were able to identify problems in their parts of the partial Product faster and propose improvements there.

Interestingly and showing the situational – perhaps even individual – nature of this dynamic, in contrast to the Core group that didn’t (or couldn’t) take advantage from rotating, rotating maintenance duty _was successful_ in other parts of the company. Some smaller groups (up to 4 teams) were able to apply it long-term and it improved their teams’ knowledge of the partial Product. A key difference between these groups and Core is the codebase size and partial-product complexity. Both were an order of magnitude higher for Core so some specialization was probably inevitable, because the cognitive load of understanding the whole partial Product and codebase is too high for the teams.

In future, when introducing specialization we shall avoid the false dichotomy between “every team knows the whole Product” and “every team must be specialized on a few fixed components”. We shall rather consider the cognitive load of developers to be a system constraint and try to support the highest adaptiveness possible while maximizing the constraint. This is the same dynamic that leads to introducing LeSS Huge, where cognitive limits of the Product Owner are usually the limiting factor.

Multiple approaches can be taken that lead to higher adaptiveness than fixed component assignment. For example, if LeSS Huge is used, teams can be responsible for all customer issues in their customer-oriented areas regardless of the components that they need to know to solve them. Or they could use accidental specialization for distributing customer issues as it is used for backlog items.


### Release frequency

Learning to be _potentially_ able to release software to customers _every Sprint_ is often a major challenge in agile adoptions. When a sequential lifecycle is used, releasing is a big event that requires heroic effort of many individuals and takes weeks if not months (as you can see from the figure below this was also our case). Changing this to frequent releases and following the Guide “Ship at Least Every Sprint” (Book 3) is … difficult. We were not successful in this aspect, mainly because our product definition was too narrow and we had to coordinate releases with other groups in the company.

Still, it might be interesting to share some of the analysis that shows how a long release cycle affected adaptiveness of product development.


#### Release cycle

Core was released to the public every six months. It had always been released together with NPM - a flagship module. The release cycle consisted of four phases shown in [Figure 14](#figure14). As you can see it is a sequential (waterfall) lifecycle with a typical fake Scrum adoption pattern - using fake “sprints” only for the development (which doesn’t improve adaptiveness), and which violates the very meaning of real Sprint: that each ends in a completely Done Product Increment (including all forms of testing)

<a name="figure14"></a>
<figure>
<img src="/img/case-studies/solarwinds/major-release-cycle.png" alt="Major Release Cycle">
  <figcaption>Figure 14: Major release cycle.</figcaption>
</figure>


* **Planning.** The goal of the planning was to fix the content of the whole release (See also [The Contract Game](#the-contract-game) section).
* **Development.** Development was organized in two-week fake Sprints that were really just development increments. Software was typically integrated multiple times a day and each Sprint resulted in a build that could be consumed by modules, but it was _not_ potentially shippable (and lots of _undone_ work, such as regression testing, was growing).
* **Regression testing.** About one month long regression-testing phase where all the previously undone work was planned in order to get the software into a shippable state.
* **Customer Acceptance (CA)**. This one-month phase was used to collect feedback from customers on the new features and overall quality of the Product. It started with a release candidate build given to the customers and ended with the General Availability (GA) milestone.


#### Historical reasons that prevented more frequent releases

Delivering once in six months is not ideal when optimizing for rapid feedback from customers that tries to invalidate hypothesized customer value. The thinking behind long releases was of course rooted in management conviction that we know what to do and do not need to try to invalidate our hypotheses.

There are two important historical reasons why SolarWinds was able to develop successful products for years despite long sequential release cycles. Let’s summarize them here before we move on.

First, over time the company developed multiple surrogate mechanisms to collect feedback. Product Managers spent hours every week on calls with customers, the company employed UX researchers who gathered feedback on the product usability, customers had an opportunity to upvote features on a community portal and the whole CA phase was focused on collecting feedback from the customers.

Second, the company was implicitly optimized for a six-month release cycle for every product with an online marketing campaign following each public release being the main event. Each campaign drove new sales, maintenance renewals and brand awareness. Six months was determined as an optimal time interval between two subsequent marketing campaigns. With a little exaggeration it can be said that a new product version has always been only a deliverable to the marketing campaign.


#### Consequences of six-month releases

Long releases of course come with costs. We have already discussed one in the section [Coarse-grained prioritization](#coarse-grained-prioritization) - big deliverables. Big deliverables are a consequence of the need to prepare regular marketing campaigns - it is easier to build marketing around big features rather than around small ones.

As long release is one big (in fact, huge) deliverable itself, it brings all problems described for big deliverables, especially [Opportunity cost](#impact-of-big-deliverables-on-opportunity-cost). We will not repeat the analysis here as it is identical.

Other costs are interesting as well, though, especially the ones that create reinforcing loops. For example, if you ship your Product to customers rarely, you typically don’t care too much about the upgrade experience (because upgrade is a rare event). As a consequence, upgrading a Product is usually a pain. People in the company who have to deal with the customers’ upgrades (for example, in the support group) feel the pain and push for less frequent releases so that they do not need to go through the pain often.

It was the case in our situation. Especially bigger customers had to spend hours, sometimes days upgrading the Product per each new major version released. To revert this trend the company had decided to explicitly invest in improving upgrade experience (one of the so-called “initiatives” in [Figure 4](#figure4)), but at the time of this case study this initiative was at its beginning and no improvement in upgrade experience was observed yet.

A lean answer to painful upgrades would be: if it hurts, do it more often. Each public release is an opportunity to identify what exactly makes the customer upgrade experience painful and slow and to address it so that next time they need less time and effort to upgrade. By applying this repeatedly, we would gradually decrease transaction costs of upgrade to (almost) zero that would allow us to upgrade at a whim and (supposedly) earn higher customer satisfaction as a side effect.

Long releasing cycles also led to lack of proper test automation - when you release once in a while it is acceptable to do manual testing. And when you need to use manual testing in order to ship the Product, you don’t want to repeat this effort too often - another reinforcing cycle. In our case, manual testing occupied a major part of the regression-testing phase.

Lack of test automation coverage was exacerbated by the fact that Core was only a partial Product - in order to produce a shippable Product Core group had to coordinate the regression testing with module teams. The coordination and testing of all integration points was a manual activity that required a couple of weeks to finish.


#### The Contract Game

Long release cycle also led to what is known as The Contract Game (Book 2, Section _Thinking About Product Management_). The business side of the organization starts with a long list of requirements. The engineering side provides estimates that make it clear that only one third of the requirements can be delivered in the release. The business side is unhappy and asks engineering leaders to deliver more.

Both parties meet several times to discuss various options for increasing the group capacity or changing the scope of individual deliverables (the process called “horse trading” in SolarWinds). The horse trading takes up to two months and consumes a significant amount of the engineering group capacity. After two months nobody is happy but only three months are remaining for development within a six-month-long release cycle so all parties quickly agree on something and the development starts. Of course, no one wants to later revisit the question, “Are we still today doing the most skillful things?” And as a result, resources are spent on outputs for which we usually have only weak speculation, which itself may have become invalidated over time.

Near the end of the cycle engineering realizes that the initial estimates were wrong and another round of negotiation starts. Programmers come with ideas to cut tasks that keep the gist of the big deliverable intact. If they are lucky they will find some. But as the deadline is approaching this is less and less of an option. So programmers look into their _secret toolbox_ and find some magic tools that make the deadline happen with “original scope”. This is the time when they stop refactoring or writing automated tests, do quick fixes of bugs instead of finding root causes and so on.


#### Try ... Regular cumulative service packs to gather customer feedback more frequently

Of course the world doesn’t stop when you spend time planning and “executing” on the long major release. Customers that use your Product discover many ways to improve them. Some of these tasks are very difficult to postpone for 6 months or more. Examples include:

* An important security fix
* A very small improvement that immediately helps close a very large deal
* A bug that affects many customers
* An incompatibility with a new version of another software your Product integrates with

Of course, when shipping to customers every Sprint one can just include all of the above as backlog items and properly prioritize them. With a six-month major release cycle the company used so-called hotfixes to deliver these critical fixes. As we didn’t succeed in shortening the major release cycle (which would be a major improvement towards adaptiveness) we experimented with using hotfixes as a way of collecting feedback and trying to invalidate our hypotheses.

During the partial LeSS adoption we changed the way of releasing hotfixes significantly, in fact turning them into small and regular minor releases.

**First**, we completely automated hotfix installation (no more copying binaries).

**Second**, we had made hotfixes cumulative, i.e. every new hotfix had to include everything included in the previous hotfixes. By doing this we increased the chance that problems with combination of fixes will be discovered internally before the hotfix will be released to customers.

**Third**, we had changed the installer so that it automatically installs the latest cumulative hotfix whenever a customer installs the latest major release. That increased the number of customers with the latest hotfix installed and thus the amount of feedback on changes released in this hotfix.

**Fourth,** we defined a regular cadence of cumulative hotfixes  - one every month.

**Fifth,** we were able to ship some fixes hidden under feature toggles and enable them for selected customers.

All these changes helped reduce [The Contract Game](#the-contract-game) at least for small items. Stakeholders were much more relaxed at the major release planning because they knew they could ship some of the small critical items in regular hotfixes.


## Conclusion

This case study describes a partial and incremental LeSS adoption in a multi-component product group that was a part of a larger product suite. We decided to use Core (a large set of low-level components) as an initial Product and proceed with adoption in the corresponding multi-component product group consisting of 5 Teams.

It was a mistake. It constrained our thinking and organizational changes to one big component and kept many mechanisms that prevented adaptiveness in place - component teams, big batch releases, big deliverables and so on. It would have been better to start with all of Orion as an initial Product, take a LeSS Huge approach and incrementally start the adoption in one true customer-oriented Requirement Area.

All that said, “the art of the possible” is an important mindset and behavior in organizational change. We didn’t have the senior management support needed to start in the recommended “top-down and bottom-up” LeSS adoption approach, and so we did what we thought we could, learned a lot from that, and did nudge the organization towards some improvements.

Of course, this key decision allowed us to do only relatively minor improvements towards adaptiveness - reducing the number of fake POs improved Teams’ ability to coordinate, reducing number of backlogs let us reduce the overhead of planning and using a bit broader Product than before helped us reduce Teams single-specialization.

Many aspects affecting adaptiveness remained unchanged though. Component teams (existing due to both lack-of cross-functionality and too narrow product definition) still required a lot of handovers and coordination by managers and other intermediaries. The Product could only be released to customers every six months and each release required a major manual coordination effort. This, too, was a consequence of the initial decision of taking a set of components and calling it a “Product” and we were not able to overcome it even in the years following this case study.


## References

I frequently refer to the 3 LeSS books in the text.

**Book 1.** Craig Larman, Bas Vodde: Scaling Lean & Agile Development: Thinking and Organizational Tools for Large-Scale Scrum, 2008

**Book 2.** Craig Larman, Bas Vodde: Practices for Scaling Lean & Agile Development: Large, Multisite, and Offshore Product Development with Large-Scale Scrum, 2010

**Book 3.** Craig Larman, Bas Vodde: Large-Scale Scrum: More with Less, 2016

The other books and resources are directly linked from the text.

