# Prerequisites

## Virtual Machine

We are providing you with a Ubuntu 18.04 (64-bit) VM image for this assignment. This image has Switchyard, Mininet and Wireshark installed so you do not need to worry about setting up the environment.

- You can find the VM image [here](https://box.nju.edu.cn/d/123a70ac8ff34595b18f/).
(user name: njucs - password: 123)
- You can learn more about importing a VM image in VirtualBox [here](https://docs.oracle.com/cd/E26217_01/E26796/html/qs-import-vm.html).

You are also free to use your favorite virtualization software for importing the image but you will most probably have to deal with the possible issues on yourself.

If you are a free soul and want to setup Switchyard in a different environment you are welcome to do that as well. You can find some useful information [here](../../appendix/environment-setup.md). This might or might not be useful for you depending on your environment.

## Mininet

Mininet enables you to quickly create, interact with, customize and share a software defined network prototype, and provides a smooth path to running on hardware.

The most useful material is their website. Here is the [Mininet Walkthrough](http://mininet.org/walkthrough/). It is better to go through this manual. Because we have not given you the whole network image to you right now, there must be something you do not understand yet. But don not worry, we will have a small practice of Mininet in our manual.

> [!NOTE]
> Ignore the content about switches like Open vSwitch (OVS) setting up.

We expect that you will cost 2 days on this.

## Wireshark

Wireshark is the world’s foremost and widely-used network protocol analyzer. It lets you see what’s happening on your network at a microscopic level and is the de facto (and often de jure) standard across many commercial and non-profit enterprises, government agencies, and educational institutions.

You will use it to inspect your network setting up by Mininet, and test the function of your device written in Switchyard. We also have a small practice of Wireshark in our manual.

[Wireshark User’s Guide](https://www.wireshark.org/docs/wsug_html/) is a verbose document about Wireshark but We **do not** recommend it. So sometimes the official document is hard for user to get started. You can find many blogs writing about how to use Wireshark. Read them instead or the first search result in Google [here](https://www.howtogeek.com/104278/how-to-use-wireshark-to-capture-filter-and-inspect-packets/).

We expect that you will cost an afternoon on this.

## Switchyard

Switchyard is a framework for creating, testing, and experimenting with software implementations of networked systems such as Ethernet switches, IP routers, firewalls and middleboxes, and end-host protocol stacks. It is the framework targeting on teaching and used in University of Wisconsin.

So we have this framework to do some network testing without multiple devices and a bunch of wires. [Switchyard documentation](https://jsommers.github.io/switchyard/index.html) is available here. And this is the document you read most often. In this lab we will combine Mininet, Wireshark and Switchyard together, as we said before.

We expect that you will cost 4 days on this. It is long but important.

## Git (Optional)

You can use Git to manage your projects with a clear editing history and we recommend using it. It is better to have your local repository synchronized with a remote backup on GitHub or some one else. The tutorial of Git is listed below.

- [廖雪峰的 Git 教程](https://www.liaoxuefeng.com/wiki/896043488029600)

We expect that you will cost 2 days on this.

## Visual Studio Code (Optional)

You can use Visual Studio Code (VSC) to develope your projects. I will show how to install it and some plugins may helps you.

- [Switchyard with VSC](./../../appendix/vscode.md)

We expect that you will cost an afternoon on this.
