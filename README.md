# ForwardWidgets

### 一、豆瓣我看&豆瓣个性化推荐

<img src="https://i.miji.bid/2025/05/05/ee9c89a97e226fa0cebaae2990b13836.jpeg" style="width:200px" /><img src="https://i.miji.bid/2025/05/05/d1b4ddc054156a87ccd1a4bff8197b53.jpeg" style="width:200px" /><img src="https://i.miji.bid/2025/05/05/ffee8bded4b121831d1b8da95c047bb9.jpeg" style="width:200px" /><img src="https://i.miji.bid/2025/05/05/ad56685688d7cd354b6cfcbed97b3e09.jpeg" style="width:200px" />

其中用户ID和Cookie必填

#### 用户ID获取
<img src="https://i.miji.bid/2025/05/05/de6358e6a8cca3e890f51e5f385e5aaa.png" alt="de6358e6a8cca3e890f51e5f385e5aaa.png" border="0" />
我的豆瓣标签页中有显示用户ID

#### Cookie获取
最好用iPhone网页登陆豆瓣，然后用Loon或者Qx等工具抓包获取Cookie（不清楚Cookie多久失效，所以可能过一段时间需要重新获取填一次）

### 二、Trakt我看&Trakt个性化推荐

```shell
几点说明：
1. trakt.js之所以不用官方trakt api，是因为尝试后发现目前生成的token 24小时之后会过期，如果要继续使用，需用上一次返回的refresh_token重新生成，当前插件也没有好的保存方式
2. trakt看过里是包含看了一半的电视的，也就是说正在看的电视也会出现在 看过-电视 里
3. 尝试后发现当前ForwardWidget插件的数据模型里如果type是tmdb，貌似有数据会被缓存覆盖的问题，douban和imdb类型不存在该问题
```

<img src="https://i.miji.bid/2025/05/08/e7bae366ee0d96b8e4cd0fa809ef8d52.md.png" style="width:200px" /><img src="https://i.miji.bid/2025/05/08/63d7160f9ced06ff18de3be8723b884e.md.png" style="width:200px" />

其中用户名和Cookie必填

#### 用户名获取
在网页上登录你的Trakt，查看url如下 https://trakt.tv/users/xxxx/watchlist ，其中users后面跟的就是你的用户名，填了用户名后还是获取不到数据的请在Trakt设置里打开隐私开关

#### Cookie获取
最好用iPhone网页登陆Trakt，然后用Loon或者Qx等工具抓包获取Cookie（不清楚Cookie多久失效，所以可能过一段时间需要重新获取填一次），一般找_traktsession=xxxx长这样的Cookie

### 三、Trakt片单&Trakt追剧日历
`说明：追剧日历只是尝鲜版，j佬到时候应该会在APP内嵌追剧功能 :)`

<img src="https://i.miji.bid/2025/05/12/d88147b5a3764acc1037a16ac736835b.png" style="width:200px" /><img src="https://i.miji.bid/2025/05/12/a918ef099ae6b3c0babb6ce2b6eb071d.png" style="width:200px" />

其中用户名/片单列表名/Cookie同上，另外追剧日历中新增参数开始日期/天数/排序方式

> 片单示例 
https://trakt.tv/users/giladg/lists/latest-4k-releases?sort=added,asc

```shell
用户名：giladg
片单列表名：latest-4k-releases
```

#### 排序依据
```shell
rank：排名算法
added：添加时间
title：标题
released：发布日期
runtime：内容时长
popularity：流行度
random：随机
```

#### 排序方向
asc：正序 or desc：反序

> Trakt追剧日历会将个人watched, collected, or watchlisted中的节目在日历中呈现，具体可查看 https://trakt.tv/calendars/my/shows-movies

#### 开始日期
填数字，0表示今天，-1表示昨天，1表示明天，插件内会自动转换成相应日期

#### 天数
填数字，表示从开始日期的n天内的时间区间，最大值33天

#### 排序方式
如有时间区间[2025-05-01, 2025-05-07]

日期升序：返回 从 2025-05-01 -> 2025-05-07 的节目信息

日期降序：返回 从 2025-05-07 -> 2025-05-01 的节目信息

### 四、豆瓣想看/已看数据迁移Trakt脚本

#### 使用教程
`说明：可能有部分会迁移失败`
1. 先将`douban2trakt.py`脚本中的几个必填参数填上
```shell
# 豆瓣用户ID
DOUBAN_USER_ID = ""
# TRAKT API APPS的Client ID，请前往 https://trakt.tv/oauth/applications/new 创建
TRAKT_CLIENT_ID = ""
# TRAKT抓包获取的x-csrf-token，需有增删改操作的接口才有
TRAKT_X_CSRF_TOKEN = ""
# TRAKT抓包获取的cookie
TRAKT_COOKIE = ""
```
2. 执行脚本
```shell
# 迁移想看列表
python douban2trakt.py --type watchlist
# 迁移已看列表和打分，因为豆瓣是5分制，Trakt是10分制，所以会做乘以2操作后打分
python douban2trakt.py --type watched
```

### 五、直播（电视+网络）
`只能说是尝鲜版，有挺多问题的，看j佬有没有时间优化下 :)`
```shell
没有统一ping，不知道哪些会超时，也没预览
没有分类显示的地方
小组件已经添加的情况下，没有搜索入口
有些源播放会闪退，不知道是什么原因，可能是缓冲太大？
插件有缓存，如果不清缓存，会老是打开同一个时间点
```
<img src="https://i.miji.bid/2025/05/17/31b417b1edf82192b1edaa752aa18504.jpeg" style="width:200px" /><img src="https://i.miji.bid/2025/05/17/9685eb351a2c5892b647dbd9c33532f5.jpeg" style="width:200px" /><img src="https://i.miji.bid/2025/05/17/fe4ed1f17a9fb5e2b3808b4f6a0c7ae2.jpeg" style="width:600px" /><img src="https://i.miji.bid/2025/05/17/bc5bbe2a8efa99eba6ca0c72e4681a79.jpeg" style="width:600px" />

#### 订阅链接
内嵌了几个公开源，也可以自定义

#### 按组关键字过滤
一个订阅链接可能有上百上千个频道，可以按组名关键字筛选，至于有哪些组，需要自己打开订阅链接看下

#### 按频道名关键字过滤
一个订阅链接可能有上百上千个频道，可以按频道名称关键字筛选，至于有哪些频道，需要自己打开订阅链接看下

### 六、雅图(每日放送+点播排行榜+评分排行榜)
`接口+tmdb查询挺慢的，不过等等还是会出现的 :)`

<img src="https://i.miji.bid/2025/05/18/6c97648fe9aed6398c76c56b28bdd3e5.jpeg" style="width:200px" />

#### 每日放送
```shell
类型：动漫/电影/电视剧
开始日期：n天前，0表示今天，-1表示昨天，以此类推
天数：从开始日期开始的后面m天的数据
```

#### 点播排行榜
```shell
类型：连载动漫/剧场动漫/电影/香港电影/欧美电影/电视剧/美剧/综艺
时间：今日/本月/历史
```

#### 评分排行榜
```shell
类型：动漫/电影/电视剧
等级：非常好看/好看/一般/烂片
```
