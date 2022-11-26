# dingding --- 钉钉机器人

## 一、模块介绍
### 版本号
dingding: V1.0.0

### 功能

当前版本支持群机器人相关API调用，包括发送文本消息、文本链接、markdown、整体跳转 ActionCard、独立跳转 ActionCard、FeedCard。

#### 文本消息类型

![image-20221126120040801](.assert\image-20221126120040801.png)

#### 文本链接类型

![image-20221126120159378](.assert\image-20221126120159378.png)

#### markdown 类型

![image-20221126120328924](.assert\image-20221126120328924.png)

#### 整体跳转 ActionCard类型

![image-20221126120347656](.assert\image-20221126120347656.png)

#### 独立跳转 ActionCard 类型

![image-20221126120440779](.assert\image-20221126120440779.png)

#### FeedCard 类型

![image-20221126120456832](.assert\image-20221126120456832.png)

### 如何使用

- 1.创建钉钉群
- 2.创建机器人，复制 webhook，如：https://oapi.dingtalk.com/robot/send?access_token=xxxxx
- 3.调用机器人API，示例见下文

### 安装

将 dingding 包复制到 site-pakages 下

## 二、示例

### 设置token

方式一：

```python
from dingding import set_token


# 机器人的token是webhook中的 access_token 参数
set_token('xxx')
```

方式二：

```python
from dingding import Robot     # Robot 是一个机器人实例对象


Robot.set_token('xxx')
```

方式三：

```python
from dingding import R        # R 是一个机器人类对象


r = R()
r.set_token('xxx')
```

### 查看token

方式一：

```python
from dingding import Robot


print(Robot.token)
```

方式二：

```python
from dingding import R


r = R()
print(r.token)
```

### 设置关键词

方式一：

```python
from dingding import set_key_word


# 机器人的关键词是创建群聊机器人时自己添加的，不包含其中一个关键词消息无法发出
# set_key_word('xxx')
set_key_word(['xxx1', 'xxx2'])
```

方式二：

```python
from dingding import Robot     # Robot 是一个机器人实例对象


# Robot.set_key_word('xxx')
Robot.set_key_word(['xxx1', 'xxx2'])
```

方式三：

```python
from dingding import R        # R 是一个机器人类对象


r = R()
# r.set_key_word('xxx')
r.set_key_word(['xxx1', 'xxx2'])
```

### 查看关键词

方式一：

```python
from dingding import Robot


print(Robot.key_word)
```

方式二：

```python
from dingding import R


r = R()
print(r.key_word)
```

### 设置开头模板

方式一：

```python
from dingding import set_token


# 设置消息的开头模板，例如：提示时间
set_tpl('xxx')
```

方式二：

```python
from dingding import Robot     # Robot 是一个机器人实例对象


Robot.set_tpl('xxx')
```

方式三：

```python
from dingding import R        # R 是一个机器人类对象


r = R()
r.set_tpl('xxx')
```

### 发送文本消息

```python
from dingding import Robot


Robot.send_text('hello word')
# @张三
Robot.send_text('hello word', at_user_ids=['zhangsan'])
# @所有人
Robot.send_text('hello word', at_all=True)
```

### 发送Markdown消息

```python
from dingding import Robot


Robot.send_markdown(title='this is a markdown message', text='**加粗hello world**')
```

### 发送整体跳转 ActionCard 消息

```python
from dingding import Robot


Robot.send_overall_card(title='this is a markdown message', text='**加粗hello world**', link='https://www.baidu.com')
```

### 发送独立跳转 ActionCard 消息

```python
from dingding import Robot


Robot.send_dependent_card(
   title='this is a markdown message', 
   text='**加粗hello world**',
   buttons=[
      {
         "title": "内容不错",
         "actionURL": "https://www.dingtalk.com/"
      },
      {
         "title": "不感兴趣",
         "actionURL": "https://www.dingtalk.com/"
      }
   ]
)
```

### 发送 FeedCard 消息

```python
from dingding import Robot


Robot.send_feed_card(
    title_list=['时代的火车向前开1', '时代的火车向前开2'],
    message_url_list=[
       'https://www.dingtalk.com/', 
       'https://www.dingtalk.com/'
    ],
    pic_url_list=[
       'https://img.alicdn.com/tfs/TB1NwmBEL9TBuNjy1zbXXXpepXa-2400-1218.png', 
       'https://img.alicdn.com/tfs/TB1NwmBEL9TBuNjy1zbXXXpepXa-2400-1218.png'
    ],
)
```

## 三、API

### dingding 模块 API

| API          | 说明                     |
| ------------ | ------------------------ |
| R            | 机器人类对象             |
| Robot        | 机器人实例对象           |
| set_token    | 给机器人实例设置token    |
| set_key_word | 给机器人实例设置关键词   |
| set_tpl      | 给机器人实例设置开头模板 |

### Robot API

| API                   | 说明                     |
| --------------------- | ----------------------- |
| set_token             | 给机器人实例设置token      |
| set_key_word          | 给机器人实例设置关键词      |
| set_tpl               | 给机器人实例设置开头模板    |
| send_text             | 发送文本消息              |
| send_markdown         | 发送markdown文本消息      |
| send_overall_card     | 发送图片消息              |
| send_dependent_card   | 发送图片文本              |
| send_feed_card        | 发送文件                 |

### Robot API 参数

#### set_token 参数：

| 参数  | 类型   | 说明                      |
| ----- | ------ | ------------------------- |
| token | 列表 | token，webhook中的key参数 |

#### set_key_word 参数：

| 参数  | 类型   | 说明                      |
| ----- | ------ | ------------------------- |
| key_word | 列表 | 关键词，机器人的关键词是创建群聊机器人时自己添加的，不包含其中一个关键词消息无法发出 |

#### set_tpl 参数：

| 参数  | 类型   | 说明   |
| ----- | ------ | ------ |
| tpl | 列表 | 开头模板 |

#### send_text 参数：

| 参数                  | 类型   | 说明                                                         |
| --------------------- | ------ | ------------------------------------------------------------ |
| text                  | 字符串 | 消息内容                                                     |
| at_all                | bool  | @all                                                        |
| at_user_ids           | 列表   | userid的列表，提醒群中的指定成员(@某个成员)。如：['zhangsan', 'lisi'] |
| at_mobiles            | 列表   | 手机号列表，提醒手机号对应的群成员(@某个成员) 如：['19912345678']|
| index                 | int   | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息 |

#### send_markdown 参数：

| 参数         | 类型   | 说明                                                         |
| ----------- | ------ | ----------------------------------------------------------- |
| title       | 字符串 | 消息标题                                                       |
| text        | 字符串 | 消息内容                                                       |
| at_all      | bool  | @all                                                          |
| at_user_ids | 列表   | userid的列表，提醒群中的指定成员(@某个成员)。如：['zhangsan', 'lisi'] |
| at_mobiles  | 列表   | 手机号列表，提醒手机号对应的群成员(@某个成员) 如：['19912345678']     |
| index       | int   | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息          |

#### send_link 参数：

| 参数          | 类型               | 说明                                                     |
| ------------ | ------------------ | ------------------------------------------------------- |
| title        | 字符串              | 图片路径                                                  |
| at_all       | bool               | 图片路径                                                  |
| at_user_ids  | 列表                | 图片路径                                                 |
| at_mobiles   | 列表                | 图片路径                                                 |
| index        | int                 | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息  |

####  send_overall_card 参数：

| 参数          | 类型         | 说明                                                   |
| ------------ | ------------ | ----------------------------------------------------- |
| title        | 字符串        | 消息标题                                                |
| text         | 字符串        | 消息内容                                                |
| link         | 字符串        | 消息链接                                                |
| single_title | 字符串        | 消息结尾提示标题，如：全文阅读                              |
| index        | int          | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息 |

#### send_dependent_card 参数：

| 参数     | 类型  | 说明                                                   |
| ------- | ----- | ----------------------------------------------------- |
| title   | 字符串 | 消息标题                                                |
| text    | 字符串 | 消息内容                                                |
| buttons | 列表   | 消息跳转按钮列表                                         |
| index   | int   | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息 |

buttons 参数字段说明：
| 参数        | 类型  | 说明                                                   |
| ---------- | ----- | ----------------------------------------------------- |
| title      | 字符串 | 消息标题                                                |
| actionURL  | 字符串 | 跳转url                                                |

- botton 构造参数示例：
```json
[
   {
      "title": "内容不错",
      "actionURL": "https://www.dingtalk.com/"
   },
   {
      "title": "不感兴趣",
      "actionURL": "https://www.dingtalk.com/"
   }
]
```

#### send_feed_card 参数：

| 参数                | 类型  | 说明                                                   |
| ------------------ | ----- | ---------------------------------------------- ------ |
| title_list         | 列表   | 消息标题列表                                            |
| message_url_list   | 列表   | 消息跳转url列表                                         |
| pic_url_list       | 列表   | 消息封面url列表                                         |
| index              | int   | 关键词索引，如果设置了多个关键词，index 表示用第几个官籍此发消息 |                      |
