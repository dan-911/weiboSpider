[![Build Status](https://github.com/dataabc/weiboSpider/workflows/Python%20application/badge.svg)](https://badge.fury.io/py/weibo-spider)
[![Python](https://img.shields.io/pypi/pyversions/weibo-spider)](https://badge.fury.io/py/weibo-spider)
[![PyPI](https://badge.fury.io/py/weibo-spider.svg)](https://badge.fury.io/py/weibo-spider)

# Weibo Spider

本程序可以连续爬取**一个**或**多个**新浪微博用户（如[胡歌](https://weibo.cn/u/1223178222)、[迪丽热巴](https://weibo.cn/u/1669879400)、[郭碧婷](https://weibo.cn/u/1729370543)）的数据，并将结果信息写入**文件**或**数据库**。
爬取结果可写入文件和数据库，具体的写入文件类型如下：

- **txt文件**（默认）
- **csv文件**（默认）
- **json文件**（可选）
- **MySQL数据库**（可选）
- **MongoDB数据库**（可选）
- **SQLite数据库**（可选）

同时支持下载微博中的图片和视频，具体的可下载文件如下：
- **原创**微博中的原始**图片**（可选）
- **原创**微博中的**视频**（可选）

## 获取到的字段

**用户信息**

- 用户id：微博用户id，如"1669879400"，其实这个字段本来就是已知字段
- 昵称：用户昵称，如"Dear-迪丽热巴"
- 性别：微博用户性别
- 生日：用户出生日期
- 所在地：用户所在地
- 学习经历：用户上学时学校的名字和时间
- 工作经历：用户所属公司名字和时间
- 微博数：用户的全部微博数（转发微博+原创微博）
- 关注数：用户关注的微博数量
- 粉丝数：用户的粉丝数
- 简介：用户简介
- 认证信息：为认证用户特有，用户信息栏显示的认证信息

***

**微博信息**

- 微博id：微博唯一标志
- 微博内容：微博正文
- 头条文章url：微博中头条文章的url，若微博中不存在头条文章，则值为''
- 原始图片url：原创微博图片和转发微博转发理由中图片的url，若某条微博存在多张图片，每个url以英文逗号分隔，若没有图片则值为"无"
- 视频url: 微博中的视频url，若微博中没有视频，则值为"无"
- 微博发布位置：位置微博中的发布位置
- 微博发布时间：微博发布时的时间，精确到分
- 点赞数：微博被赞的数量
- 转发数：微博被转发的数量
- 评论数：微博被评论的数量
- 微博发布工具：微博的发布工具，如iPhone客户端、HUAWEI Mate 20 Pro等
- 结果文件：保存在当前目录weibo文件夹下以用户昵称为名的文件夹里，名字为"user_id.csv"和"user_id.txt"的形式
- 微博图片：原创微博中的图片和转发微博转发理由中的图片，保存在以用户昵称为名的文件夹下的img文件夹里
- 微博视频：原创微博中的视频，保存在以用户昵称为名的文件夹下的video文件夹里

## 运行环境

- 开发语言：python3
- 系统： Windows/Linux/macOS

## 使用说明

### 1.源码安装

 $ git clone https://github.com/CUMT-YuqingTeam/weibo.git

$ cd weiboSpider

$ pip install -r requirements.txt



### 2.程序设置

源码下载安装的用户在weiboSpider目录下运行如下命令，pip安装的用户在任意有写权限的目录运行如下命令：
```bash
$ python3 -m weibo_spider
```

设置user_id_list：

user_id_list是我们要爬取的微博的id，可以是一个，也可以是多个，例如：

"user_id_list": ["1223178222", "1669879400", "1729370543"],

user_id_list的值也可以是文件路径，我们可以把要爬的所有微博用户的user_id都写到txt文件里，然后把文件的位置路径赋值给user_id_list：
文件内容示例如下：

1223178222 胡歌

1669879400 迪丽热巴

1729370543 郭碧婷

假如文件叫user_id_list.txt，则user_id_list设置代码为：

```bash
"user_id_list": "user_id_list.txt",
```
### 3.运行程序

在weiboSpider目录运行如下命令
```bash
$ python3 -m weibo_spider
```

第一次执行，会自动在当前目录创建config.json配置文件，配置好后执行同样的命令就可以获取微博了。

如果你已经有config.json文件了，也可以通过config_path参数配置config.json路径，运行程序，命令行如下：

```bash
$ python3 -m weibo_spider --config_path="config.json"
```

如果你想指定文件（csv、txt、json、图片、视频）保存路径，可以通过output_dir参数设定。假如你想把文件保存到/home/weibo/目录，可以运行如下命令：
```
$ python3 -m weibo_spider --output_dir="/home/weibo/"
```
如果你想通过命令行输入user_id，可以使用参数u，可以输入一个或多个user_id，每个user_id以英文逗号分开，如果这些user_id中有重复的user_id，程序会自动去重。命令行如下：
```
$ python3 -m weibo_spider --u="1669879400,1223178222"
```
程序会获取user_id分别为1669879400和1223178222的微博用户的微博

## 注意事项

1.user_id不能为爬虫微博的user_id。因为要爬微博信息，必须先登录到某个微博账号，此账号我们姑且称为爬虫微博。爬虫微博访问自己的页面和访问其他用户的页面，得到的网页格式不同，所以无法爬取自己的微博信息；

2.cookie有期限限制，大约三个月。若提示cookie错误或已过期，需要重新更新cookie。
