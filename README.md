> OpenMix 出品：http://openmix.org

<br>

<p align="center">
<img src="http://mixphp.cn/static/image/logo_php.png" width="120" alt="MixPHP">
</p>

<p align="center">高性能 • 轻量级 • 命令行</p>

<p align="center">
<img src="https://img.shields.io/badge/php-%3E%3D7.2-brightgreen">
<img src="https://img.shields.io/badge/swoole-%3E%3D4.4.4-brightgreen">
<img src="https://img.shields.io/badge/license-apache%202-blue">
</p>

## Mix PHP 是什么

基于 Swoole 开发的高性能 PHP 框架，从 `2017` 年开始经过多年发展收获了很多中小型团队的支持，框架版本也经历了多个版本的迭代：

- `V1.*`: 基于 Swoole 的常驻内存型 PHP 高性能框架
- `V2.0`: 基于 Swoole 的 FastCGI、常驻内存、协程三模 PHP 高性能框架
- `V2.1`: 基于 Swoole 4.4+ 单线程协程 PHP 框架 
- `V2.2`: 基于 Swoole 4.4+ 单线程协程 PHP 微服务框架 🆕

## 与 Mix Go 的关系

[Mix Go](https://github.com/mix-go/mix) 设计哲学与 Mix PHP 几乎完全一致，PHP 的用户可以非常容易的切换到 Mix Go 进行开发，达到学一会二的效果，[OpenMix](http://openmix.org) 可能是现在唯一一个打造跨语言框架的开源机构。

## 与传统 MVC 框架比较

传统框架大部分都是在 HTTP 领域开发，而 Mix 能开发 HTTP、WebSocket、TCP、UDP、RPC 几乎全部互联网领域。

在命令开发方面 Mix 也有更多的封装，填充代码即可开发一个功能完备的命令行程序。

在性能方面采用常驻内存+协程，拥有传统框架无法比拟的性能。 

## 与其他基于 Swoole 的框架比较

服务器全部基于 Swoole\Coroutine\Server 开发，线程模型与 Node.js 一样为单进程单线程模型 (现有其他 Swoole 框架基本都是多进程模型)，组件封装风格参考 Golang，这样既拥有 Golang 的 CSP 并发模型，又无需像 Golang 一样处理数据的并发安全。[[为何从 Reactor+Manager+Worker 多进程改为单线程协程]](https://zhuanlan.zhihu.com/p/93200932)

框架非常轻量灵活，现有组件全部基于 PSR 标准实现，均可独立使用，严格来讲 Mix 其实只封装了 `mix/console` 命令行开发组件，其他全部为选装。

框架集成了众多开箱即用的组件，方便快速开发，且全部与 Golang 使用风格非常类似。

我们的开发文档可能是所有框架中最详细的，源码自带 Demo，稍微修改一下即可使用。

全面采用 Swoole 原生协程与最新的 PHP Stream Hook 一键协程化技术。

采用和 Golang 类似的高度灵活的开发方式，框架只提供底层库，而与具体功能相关的代码都在项目库中实现，用户能更加细粒度的修改每一处细节。

如果说 Hyperf 是 Swoole 技术圈的 Java 框架，那 Mix 就是 Golang 框架。

## 微服务

微服务方面我们激进的选择了和其他 Swoole 框架截然不同的路径，在现有流行语言中只有 java spring cloud, golang go-micro 两大微服务生态最为成熟，由于 Mix 一直是类 golang 风格框架，加上单进程协程的独特优点，我们实现了 [go-micro](https://github.com/micro/go-micro) 的代码级互通，并可以使用 [micro runtime](https://micro.mu/docs/runtime.html) 工具包的网关、代理、Dashboard 等全部微服务治理基础设施，这意味着 PHP 能与 Go 一同无缝打造高性能 RPC 服务网格，加上 Mix = beego + go-micro 两大框架的功能集合，因此采用 Mix 开发的单体应用能在无需大量修改业务代码的情况下低成本升级到微服务。

- [Mix Micro](https://github.com/mix-php/micro)：与 go-micro 生态深度集成的 php 微服务开发框架

## 框架定位

在其他 Swoole 框架都定位于大中型企业的时候，Mix 决定推动这项技术的普及，我们定位于众多的中小型企业、创业型公司，我们将 Swoole 的复杂度封装起来，用简单的编码方式呈现给用户，让更多的中级程序员也可打造高并发系统，让 Swoole 不再只是高级程序员的专利。

## 框架配套工具

- [SwooleFor](https://github.com/mix-php/swoolefor)：自动重启工具，实现热更新功能

## 性能测试

- [MixPHP 2.2 / Beego 1.12 数据库查询性能对比](https://zhuanlan.zhihu.com/p/163700975)
- [PHP7.3+Swoole4.4 / Go1.13 / MixPHP2.2 / Beego1.12 性能对比](https://zhuanlan.zhihu.com/p/162998384)
- [MixPHP 并发性能全面对比测试](http://www.jianshu.com/p/f769b6be1caf)

## 开发文档

MixPHP开发指南：

- http://doc.mixphp.cn
- https://www.kancloud.cn/onanying/mixphp2-2/content

## 环境要求

* Linux, OS X, WSL
* PHP >= 7.2
* Swoole >= 4.4.4 (websocket >= 4.4.15)

## 快速开始

推荐使用 [composer](https://www.phpcomposer.com/) 安装。

```
composer create-project --prefer-dist mix/mix-skeleton mix ~2.2.0
```

启动服务器：

接下来启动 HTTP 服务器。

```
$> php /data/bin/mix.php web
```

如果一切顺利，运行到最后你将看到如下的输出：

```
                              ____
 ______ ___ _____ ___   _____  / /_ _____
  / __ `__ \/ /\ \/ /__ / __ \/ __ \/ __ \
 / / / / / / / /\ \/ _ / /_/ / / / / /_/ /
/_/ /_/ /_/_/ /_/\_\  / .___/_/ /_/ .___/
                     /_/         /_/

Server         Name:      mix-web
System         Name:      darwin
PHP            Version:   7.3.12
Swoole         Version:   4.5.0
Framework      Version:   2.2.2
Listen         Addr:      0.0.0.0
Listen         Port:      9501
[2020-05-16 18:09:43] WEB.INFO: server start
```

访问测试 (新开一个终端)：

```
$> curl http://127.0.0.1:9501/
Hello, World!
```

## 技术交流

知乎：https://www.zhihu.com/people/onanying   
微博：http://weibo.com/onanying    
官方QQ群：[284806582](https://shang.qq.com/wpa/qunwpa?idkey=b3a8618d3977cda4fed2363a666b081a31d89e3d31ab164497f53b72cf49968a), [825122875](http://shang.qq.com/wpa/qunwpa?idkey=d2908b0c7095fc7ec63a2391fa4b39a8c5cb16952f6cfc3f2ce4c9726edeaf20)，敲门暗号：phper

## License

Apache License Version 2.0, http://www.apache.org/licenses/
