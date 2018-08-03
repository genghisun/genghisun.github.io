---
category: tech
tags: port
---

## Windows
1. in powershell or cmd,`netstat -ano |findstr PORT_NUMBER`
2. the last number is pid
3. kill that process
    * `taskkill /pid PID_NUMBER /f`f means forcefully
    * goto TaskManager?

ss被系统空闲进程占用，应该是ss的问题，退出ss再开就行了

## Linux