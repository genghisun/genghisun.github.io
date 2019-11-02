---
category: tech
tags: linux keyboard
---

买了新机械键盘Anne Pro 2，想禁用笔记本键盘，使用xinput这个工具
```
xinput list
```
```
⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ SteelSeries Rival Gaming Mouse          	id=12	[slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad              	id=16	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Power Button                            	id=9	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=10	[slave  keyboard (3)]
    ↳ SteelSeries Rival Gaming Mouse          	id=13	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=15	[slave  keyboard (3)]
    ↳ AnnePro2 P2                             	id=18	[slave  keyboard (3)]
```
可以猜出来id=15这个应该就是我想禁用的键盘（你的可能不是15哈），把它的enable值改成0
```
→xinput set-prop 15 "Device Enabled" 0
```
如果以后想启用的话把最后这个0改成1就好啦～
