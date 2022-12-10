# AMD主机风扇

## 1. 风扇一直以一个非常低的速度在转, 无论当前温度如何, cpu占用如何。导致主机整体温度, 日常使用时便高达 68度。 ~~目前暂没找到解决方案~~ (已解决)。
执行pwmconfig, 报错。`pwmconfig: There are no pwm-capable sensor modules installed`, 查遍网络暂无头绪。

最后发发现BIOS中有一个 fancontrol的设置, 配置和效果跟linux中的fancontrol一致。
