# 框架简介

Facebook发布了开源网络服务器框架Tornado，该平台基于Facebook刚刚收购的社交聚合网站FriendFeed的实时信息服务开发而来.Tornado由Python编写，是一款轻量级的Web服务器，同时又是一个开发框架。采用非阻塞I/O模型(epoll)，主要是为了应对高并发 访问量而被开发出来，尤其适用于comet应用。Tornado 是 FriendFeed 使用的可扩展的非阻塞式 web 服务器及其相关工具的开源版本。这个 Web 框架看起来有些像 web.py 或者 Google 的 webapp，不过为了能有效利用非阻塞式服务器环境，这个 Web 框架还包含了一些相关的有用工具 和优化。

Tornado是一个编写易创建，可拓展和强部署能力的不错选择。特别是Tornado的速度，简单，轻量级，在我们的日常项目中使用更是带来了很多的便利性。我们可以可以从多方面资料中了解到，Tornado在很多大中型项目都有出色的表现，特别是其轻量级和其在项目中为开发者提升的速度和乐趣。

本书的目的是对Tornado Web服务器进行全方位的分析，通过对框架基础，tornado模块，HTTP协议，编程模型，gen异步封装，ioloop核心I/O循环，模板选择，tornado实践以及tornado周边章节讲解分析。我们将会使用很多例子来讲解Tornado是如何工作的，为什么要这么做，你会怎样使用，使用时需要注意哪些，并且希望通过其中一些章节来带领读者走进异步服务框架的内部机理。

本书假定您已经对Python有了基本的了解，对数据库有一些熟悉，并且了解计算机基本工作机制。书中都会提到一些，但限于本书不会过份讲解他们，您可以在互联网上很容易就找到资料。

Tornado是使用Python编写的一个高性能，可拓展的Web服务器。特别能应对对速度有比较高要求的场合，配合其他工具和合理的部署，在非常严峻的网络流量压力时依然表现得足够强健，但其从新建至今一直都保持其轻量级。同时其核心ioloop也是很多工具的底层实现。

我们可以在github上看到Tornado是主要由Ben Darnell和其他众多开发者维护，不同于那些最多只能达到1w个并发连接的传统Web服务器，Tornado是新一代Web服务器，它从一开始就是来解决高并发问题的。

我们知道在互联网上有一个经典的C10K的问题。常见的Web框架（如apache，IIS等）通常都是使用的是操作系统的多线程来处理连接，它们会为每个连接分配一个线程池中的连接，线程会由于连接数过多而被大量使用。我们知道多线程可能会由于比较耗时的操作（如IO请求）阻塞，从而导致线程长时间不能释放。

尽管不同的操作系统会为新创建线程分配不同大写的线程堆栈大小，Linux默认为8192KB，Window默认是1024KB。同时1000个连接就将至少消耗8G(1000*8192KB，Window是1G)内存，可以想象连接继续增多对系统是怎样的负担。同时线程池的维护，线程创建和上下文切换也是一笔很大的开销。

随着社交网络的发展，那些动则几十万，上千万，甚至上亿的社交产品已经是很常见的了，使用老一代的Web服务器几乎很难满足这种爆炸式的增长了。我们都知道社交运用都会实时的显示新消息，状态变化和用户通知，这就需要一个一直打开的长连接来不断推送实时信息，对于Apache一类的Web服务器无疑会很快耗尽连接池。

很多的异步服务器正是设计被用来在以上场景中大显神威。当服务器负载增加时，如Node.js，Tornado这样的服务器使用异步协作的方式来进行拓展。当某个请求要进行耗时的操作时，异步服务器能挂起它们，当它们的长时操作完成时，异步服务器能及时的恢复并调用回调函数。

我们知道编写同步运用程序时相对容易，一旦程序变为异步，那么程序复杂度会上升好几个数量级。而Tornado在保持高性能时依然保持了其优雅。

Tornado从2009年至今，已经到了4.1版本，它已经获得了很多社区的支持，并且在一系列不同场景中得到运用。除FriendFeed和Facebook外，还有很多公司在生产上转向Tornado，包括Quora、Turntable.fm、Bit.ly、Hipmunk以及MyYearbook等。

如果您正在选择新的Web服务器框架，或者想升级现有的Web框架，那么Tornado是个很好的选择。当然它不是最好的选择，它依赖具体的使用环境。记住：Tornado是简单的，高效的，轻量级的。

