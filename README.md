#Radtel RT-890自定义固件


该项目致力于在功能和无线电性能方面改进Radtel RT-890的固件。


它是基于【DualTachyon的OEFW】(https://github.com/dualtachyon/radtel-rt-890-oefw)这与最初的Radtel 1.34固件相反。

感谢他让这一切成为可能！


##免责声明

此固件正在进行中，可能不稳定；它可能会改变你的收音机及其数据。

自担风险使用，并记得在安装任何自定义固件之前备份SPI内存。


##特点

-所有库存功能：[查看用户手册](https://cdn.shopifycdn.net/s/files/1/0564/8855/8800/files/rt-890_user_manual.pdf?v=1670288968)

-RX频率可以设置在10到1300 MHz之间（结果可能会有所不同）

-SSB接收

-灯光主题

-AM Fix（通过强信号改善AM接收，是@OneOfEleven在全盛UV-K5上出色工作的端口）

-完全控制侧键和主键快捷键

-新的可配置操作（调频收音机、扫描仪、荧光灯）

-0.01K步长

-在单VFO模式下显示寄存器

-接收时显示dBM

-返工扫描仪

-8扫描列表

-更快的扫描

-恢复模式：时间、载波、否

-扫描时更改扫描方向（向上/向下键）

-强制恢复扫描（向上/向下键）

-返工的主菜单

-扫描时禁用LED切换的能力

-还有更多！


###默认快捷键（长按）-可在主菜单中配置

```

1=>开始/停止扫描内存通道

2=>切换AM修复

3=>切换VOX

4=>更改当前信道上的TX电源

5=>更改静噪级别

6=>切换双表

7=>切换背光

8=>更改频率步长

9=>转到预设频道

0=>启动广播调频模式

*=>编辑当前频道的发送频率

#=>切换钥匙锁

菜单=>DTMF解码器

退出=>单/双VFO显示

```


###扫描向导

扫描列表管理：

-此固件有8个扫描列表。

-可以使用“Ch In List X”菜单将当前频道添加到任何扫描列表中。

-可以在“要扫描的列表”菜单中选择要使用的扫描列表。

-要忽略扫描列表并扫描所有频道，请在“要扫描的列表”菜单中选择“*”。

-要将当前频道添加/删除到当前扫描列表，请使用“切换SList”快捷方式。


正在扫描：

-要开始扫描，请按映射到“Freq scanner”快捷方式的键（默认设置：长按“1”键）。

-当扫描正在进行时，使用“Freq scanner”键更改扫描列表，此操作将移动到下一个非空扫描列表，或者如果所有后续列表都为空，则切换到扫描所有模式。

-要更改当前扫描的方向，请使用“向上”/“向下”键。

-要在扫描仪收到信号停止时强制恢复扫描，请使用“向上”/“向下”键。

-按除“Freq scanner”以外的任意键停止扫描。


###频谱使用

通过使用主菜单将一个键（侧键或小键盘）映射到spectrum（频谱）操作来启动频谱。频谱将启动，以活动VFO/内存通道的频率为中心。


频谱密钥：

```

向上=>正常：将频率范围增加+/-（底部行中间的数字）

保持一个频率：向上移动到下一个频率

向下=>正常：将频率范围减小+/-（底部行中间的数字）

保持一个频率：向下移动到上一个频率

1=>更改扫描步数（16、32、64或128）

2=>

3=>更改调制（AM、FM或SSB）

4=>更改步长（0.25k-50k）

5=>

6=>润滑油静噪级别

7=>保持当前频率

8=>

9=>降低静噪级别

0=>切换过滤器（U=未过滤，F=已过滤）

*=>更改扫描延迟（0-40ms）

#=>切换带宽（W=宽，N=窄）

菜单=>使用当前频率和设置跳转到VFO模式（允许TX）

退出=>退出频谱

```


频谱显示：

<p float=“left”>

<img src=“/Images/SpectrumDisplay.png”height=300/>

</p>


##更新说明

###SPI内存备份

使用[RT-890-闪光灯](https://github.com/dualtachyon/radtel-rt-890-flasher)


###SPI内存恢复

使用[RT-890-SPI-restore-CLI](https://github.com/dualtachyon/radtel-rt-890-spi-restore-cli)


###自定义

```

UART_DEBUG=>UART调试输出

MOTO_STARTUP_TONE=>MOTO XPS启动蜂鸣声

ENABLE_AM_FIX=>OneOfEleven的大UV-K5 AM修复的实验端口

ENABLE_LTO=>链路时间优化

ENABLE_NOAA=>NOAA天气频道（修改可用操作后，始终从菜单重新设置侧键操作）

```


###构建和闪存

请参阅下面的__Compiler__、__Building__和__Flashing__部分。


##预构建固件

您可以在[Actions]中找到预构建的固件(https://github.com/oefw-community/rt-890-custom-firmware/actions)


##从浏览器构建


要在不安装任何软件的情况下构建固件，您可以使用GitHub代码空间在浏览器中运行功能齐全的IDE和编译器。

预配置的环境运行Linux Ubuntu 22.04，带有gcc arm none eabi 15:10.3-2021.07-4。


###启动新的代码空间


您只需要点击绿色按钮`<>Code`->`Codespace`->`Create Codespace on…`

代码空间初始化后，您可以打开和编辑任何文件，例如，修改makefile中的选项，并在终端面板中键入“make”来构建固件。


###启动现有代码空间


如果您在不到7天前启动了一个代码空间，并且没有手动删除它，那么您将可以重新启动它，而不是创建一个新的代码空间。

启动速度会快得多，但在编译之前需要更新代码，因为它将包含创建时的代码版本。

要做到这一点，只需在控制台中键入以下命令：“make clean”，然后是“git pull”，最后是“make”。


###关于免费报价的一句话

最善于观察的用户会注意到这条消息：“此存储库的代码空间使用由…支付。”

未经同意，Github永远不会向您收费。如果你达到了免费提供的限制（这是非常不可能的），你将无法启动你的代码空间，直到每月的限制重置，仅此而已。

[更多信息](https://docs.github.com/en/billing/managing-billing-for-github-codespaces/about-billing-for-github-codespaces)


##Telegram组

如果你想讨论这个项目，你可以加入[电报小组](https://t.me/rt890_oefw)。




---

_原始OEFW自述_


#支持


*如果你喜欢我的工作，你可以支持我度过难关https://ko-fi.com/dualtachyon


#打开Radtel RT-890 v1。34固件


该存储库是Radtel RT-890 v1的一个保护项目。34固件。

它致力于了解收音机的工作原理，并帮助开发人员进行自己的定制/修复等。

它并没有被完全理解，也没有正确命名所有变量/函数，因为这只是尽最大努力。

因此，此存储库将不包括对原始固件的任何定制或改进。


#编译器


建议使用arm-none eabi GCC 10.3.1版本，这是Ubuntu 22.04.03 LTS上的当前版本。

其他版本可能会生成过大的闪存文件。

您可以从以下位置获取适当的版本：https://developer.arm.com/downloads/-/gnu-rm


#建筑物


要构建固件，您需要获取子模块，然后运行make：

```

git子模块更新--init--recursive--depth=1

制作

```


#闪烁


*使用固件。带有[RT-890-Flasher]的bin文件(https://github.com/dualtachyon/radtel-rt-890-flasher)或[RT-890 Flasher-CLI](https://github.com/dualtachyon/radtel-rt-890-flasher-cli)


#许可证


版权所有2023双速子

https://github.com/dualtachyon


根据Apache许可证2.0版许可（“许可证”）；

除非符合许可证的规定，否则您不得使用此文件。

您可以在获取许可证副本


http://www.apache.org/licenses/license-2.0


除非适用法律要求或书面同意，软件

根据许可证进行的分发是在“按原样”的基础上进行的，

无任何明示或暗示的保证或条件。

有关管理权限的特定语言，请参阅许可证和

许可证下的限制。
