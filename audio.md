# 音频相关的

### 1. 外接音响电流声问题
**问题设备:** dell笔记本
> 音响使用的是 哈曼卡顿3, 使用3.5mm有线连接, 在电脑本身无声音输出时, 音响会发出滋滋滋的电流声, 很大声。在打开`PulseAudio`设置面板时, 电流声消失。

解决办法: 
1. 编辑`/etc/pulse/default.pa`文件, 将这一句`load-module module-suspend-on-idle` 注释掉。 
2. 重启`PulseAudio`。终端执行 `systemctl restart --user pulseaudio.service`。

PS.
将`PulseAudio`用`Pipewire`代替之后, 问题依旧。 `Pipewire`的解决问题类似, 
```bash
sudo mkdir -p /etc/wireplumber/main.lua.d
sudo cp /usr/share/wireplumber/main.lua.d/50-alsa-config.lua /etc/wireplumber/main.lua.d/50-alsa-config.lua
```
然后编辑该文件, 将最后一句 `["session.suspend-timeout-seconds"] = 5` 前面的注释去掉, 并将值改为0。

**以上2种方法, 都只能解决系统正常使用时的电流声。但是系统睡眠时的电流声一直存在。**



### 2. 声音设置面板出现 3个HDMI音频输出设备
**问题设备:** dell笔记本
> 电脑本身只有1个 HDMI接口,但是却出现3个HDMI声音设备, 干扰我(强迫症晚期了)。决定把这3个一起干掉得了, 毕竟目前内置音响的显示器, 那音质音效, 基本都是`发能出声音`的级别, 除非家里再没有别的音响设备, 不得已才会用。

解决办法: 
1. 在`/etc/modprobe.d`目录下, 新建一个`blacklist.conf`文件(名字不重要, 有个语义即可, 重要是要`.conf`后缀名)
2. 写上`blacklist snd_hda_codec_hdmi`。
3. 重启系统即可。


###  3. 在键盘有输入的地方, 无效键入, 均会发出刺耳的`哔~~~哔~~~`声, 开机也会出现这个声音。
**问题设备:** dell笔记本
> 这个应该是类似台式机的主板上的`蜂鸣器`的作用,  但是这笔记本主板没有蜂鸣器, 借用的是电脑的内置音响, 然后那个声音真的是很刺耳。参见 [https://wiki.archlinux.org/title/PC_speaker_(简体中文)#禁用PC喇叭](https://wiki.archlinux.org/title/PC_speaker_(简体中文)#禁用PC喇叭)

解决办法: 
1. 在`/etc/modprobe.d`目录下, 新建一个`nobeep.conf`文件(名字不重要, 有个语义即可, 重要是要`.conf`后缀名)
2. 写上`blacklist pcspkr`。
3. 重启系统即可。
