## MakePl
MakePl是什么？可以理解成情侣之间的todolist，其实灵感主要来自于生活中的痛点。在设计这个app的系统功能时候，我考虑的是什么呢。

首先应该对系统总的角色做一个细分，觉得分类大概如下，

- 用户
- 项目
- 日程
- 任务
- 子任务
- 收藏
- 备注
- 上附件
	- 图片
	- 文本
- 评论
- 聊天
- 通知

当然一开始规划了这么大的系统，实现起来确实繁杂，在此必须要对这个系统进行精简，在项目的开始阶段，保留主要精力来实现主要功能，所以对上述所列进行删减，保留如下内容，

- 用户
- 项目
- 任务
	- 收藏
	- 附件
	- 备注
	- 重复
- 通知

## 页面设计
经过上面的精简之后，页面设计也会简化很多，初步设想是使用TabBar的形式，下面分为3个TabBar，

- 首页
	- 个人项目列表
		- 收件箱
		- 今天
		- 本周
		- 电影
		- 杂项
		- 履行
		- 读书
		- 纪念日
		- ......
	- 添加新的项目
	- 左侧“搜索”按钮
	- 右侧“扫码”按钮
- 创建
	- 创建新的项目
	- 创建新的任务
	- 创建新的文件
- 我的
	- 个人设置
	- 消息中心
		- 到期任务的提示
	- 近期任务
	- 任务汇总
	- 收藏的任务
	
## 模型设计

### User模型
在MakePl系统中，最重要的角色就是用户角色，所有的项目Project和任务都是围绕着用户来进行的，用户User包括如下属性，

- userId
- username
- password
- nickname
- avatar
- address
- birthday
- gender
- qqOpenId
- wechatOpenId
- weiboOpenId

用户有如下的基本行为，

- 注册
- 登录
- 登出

### Project模型
Project在MakePl中代表项目的意思，项目就像是任务的文件夹，对相关任务进行归纳和整理的作用，它有如下属性，
- projectId
- name
- thumbnail
- color
- expireMissionCount
- totalMissionCount
- superProject
- subProjects
- hasShare
- members
- isEmpty（待定）

这里，有几个属性需要特别注明一下，`color`表示项目的颜色，表示了任务的重要性和级别；hasShare是该任务是否与其他人分享了，在MakePl系统中
