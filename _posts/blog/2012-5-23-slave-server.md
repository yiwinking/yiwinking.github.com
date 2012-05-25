---
layout: post
category : blog
title : Install server density agents on slaves 
tags : [ Server , DensityServer , Agents ]
---
install serverdensity agents on slaves

1.login in server density webapp

2.devices,add new devices,set "name","device dose","group","cpu core",and "Ram" will be set by itself,why? By server?

3.choose os, here is linux , ubuntu,then will comes instructions

4.use SSH to login in server ,then follow the steps in instructions, work on the servers.

   steps:

	1)Install our public repo key: 'wget -q https://www.serverdensity.com/downloads/SOMEKEY.key -O- | sudo apt-key add -'

	2)Add the Server Density repository to apt: `sudo vim  /etc/apt/sources.list.d/sd-agent.list`,add `deb http://www.serverdensity.com/downloads/linux/deb all main`

	3)`sudo apt-get update`

	4)`sudo apt-get install sd-agent`

	5)`sudo vim /etc/sd-agent/config.cfg`

	6)add :

`[Main]`

`sd_url: http://favmed.serverdensity.com`

`agent_key: (Key Number)`

	7)`sudo /etc/init.d/sd-agent start

.5.turn to webapp,and click alerts, then add what we need.

such as :

disk usage,load average , no data receicved ,or script and so on.


