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

这里，有几个属性需要特别注明一下，`color`表示项目的颜色，表示了任务的重要性和级别；hasShare是该任务是否与其他人分享了，在MakePl系统中尽量表示用户是否与另一方分享；members表示参与该项目的人，在MakePl系统中，最多只会有两个参与的人，因为它是恋人todo list应用程序嘛。默认情况，project的members只包含用户自己，如果包含了对方，则hasShare属性则被设置为YES值。

### Mission模型

Mission是Project项目文件夹中的具体的一个任务，它包含如下属性，

- title
- dateline
- remindDate
- superProject
- subMissions
- isCollect
- priority 优先级
- remark 备注
- comments
- files
- tags 标签


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
- 消息中心
	- 消息盒子
	- 聊天页面
	
### 用户登录/注册逻辑
系统中，用户的角色是第一位的，所有的业务和逻辑都是基于用户来维持的。登录和注册作为吸收用户的一个入口，这一块的逻辑应该好好整理。


用户注册，什么样的信息最重要呢？笔者认为，在当前，手机号和微信是一等的选择，因为每个人都有手机，每个人都有微信，这无疑为用户登录和注册提供了方便。
So，在设计用户注册和登录页面时，应该以手机号和微信为核心。

在MakePl系统中，一方面用户可以无需注册、直接使用微信登录；另一方面，用户可通过手机号码注册账户，使用手机号直接登录系统。如果通过手机号注册的用户忘记了密码，可在忘记密码的页面，通过发送短信到手机重置密码。

另外，在设计初期，笔者想使用邮箱号来作为用户注册的首选，但是考虑到邮箱并没有手机号普及程度大，所以暂时放弃了使用邮箱号注册、登陆的选择。后面随着系统完善，考虑为用户开放邮箱注册、登录以及绑定账户的功能。
