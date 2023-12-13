---
title: 数字资源
description: 整理一下最近的资源。
date: 2023-11-28
draft: false
tags: ["资源"]
---

### z-library 最新地址
- 据说不用翻墙，速度都很快
- 更新一下内容，尝试了一下，的确速度很快，也不用翻墙，可以留着做为一个备用资源
- https://zh.z-library.se/

### pinokio
-  https://pinokio.computer/ 
- 用「pinokio」来本地部署一些 AI 项目
- 真的很方便，我愿称之为开源项目普及之光👍🏻 比如 ComfyUI、SD-WEBUI、SVD、Whisper、RVC、TokenFlow啊都可以在自己电脑上一键部署起来，很适合不太熟悉部署项目，但是又想体验最新技术的朋友。
- 不过由于是部署在本地的，建议还是有 NVIDIA 显卡或者有 m 系列 mac 的用户使用。
- 以后换了电脑一定要试一下😝

### 名言的摘录
- Write about what you learn. It pushes you to understand topics better. Sometimes the gaps in our knowledge only become clear when explaining things to others.
写下你学到的东西。它能促使你更好地理解主题。有时，只有在向他人解释时，我们的知识缺口才会变得清晰。
- Remember, most of your ideas will be bad; it’s part of the process of getting to the good ones.
请记住，你的大部分想法都会是糟糕的；这是产生好想法的过程的一部分。

### Vue 插槽实用案例
插槽这个扩展用法还是没好好掌握得到，用起来不够得心应手，不过我相信会慢慢掌握多点的。
```
<el-table
:data="tableData"
:height="scrollHeight">
<el-table-column v-for="propItem in propList" :key="propItem.prop" v-bind="propItem">
	<template v-slot="{ row }">
	<slot v-else :name="propItem.slotName" :row="row">{{ row[propItem.prop] }}</slot>
	</template>
</el-table-column>

<el-table-column label="" width="120" fixed="right">
<template #="{ row }">
<div class="view-btn" @click="handleView(row)">View</div>

</template>
</el-table-column>
</el-table>

###实际使用的时候
###需要先设置一个对象
export const tableConfig = {
propList: [
	{ prop: 'date', label: "label", slotName: 'date', width: 180 },
]
}

###Html页面调用的时候
<template #date="{row}">
	<span>{{ row.date }}</span>
</template>
```


### TG代理设置
这是[教程](https://nice456.com/index.php/2021/06/17/telegram-2/)
这里我就只截取了**Telegram macOS 客户端**的设置。
- Telegram macOS 客户端不遵从系统代理, 所以需要设置自定义代理, 也可以用Surge/ClashX Pro 开启”增强模式”-(Surge/ClashX Pro 的“增强模式”就是针对这类不遵从系统代理的软件做的功能)
- **自定义代理设置步骤:**
	- Telegram macOS 客户端→设置→数据→使用代理→添加代理→SOCKS5/HTTP→服务器: **127.0.0.1**, 端口: 端口需查看你的代理软件(Surge/ClashX/ShadowsocksX…), 不需要填写用户名和密码.
- **代理软件查看本地端口的方法:**
	- Surge→点击状态栏Surge图标→显示主界面→SOCKS5(默认是: 6153)
	- Clash for Windows: 主界面→General→Port(默认是: 7890)
	- ClashX→点击状态栏_ClashX图标→帮助→端口_→Socks Port(默认是: 7891)
	- ShadowsocksX: 点击状态栏ShadowsocksX_图标_→高级设置→本地Socks5监听端口(默认是: 1086)
	- V2RayX: 点击状态栏V2RayX图标→Configure→Local Socks5 Port(默认是: 1081)
	- V2rayU: 点击状态栏V2rayU图标→偏好设置→Advance→本机 Sock 监听端口(默认是: 1080)
	- **设置完成保存后, 记得重启 Telegram macOS 客户端! 记得重启! 记得重启!**
	- 有可能你或你用的规则修改了代理软件的本地SOCKS5/HTTP端口, 具体以你的代理客户端为准.**不能乱设置乱猜测, 乱设置可能导致 Telegram macOS 连不上网络.**

按照上述步骤我是成功能使用TG了，再也不用使用 TG Lite版本了😈
