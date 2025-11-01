# 小红书采集器 (Rednote Scraper)

小红书采集器是一个强大的网络爬虫，可以从[小红书](https://www.xiaohongshu.com/)网站上提取各种数据。它支持多种数据采集目标，包括用户信息、笔记、评论、搜索结果等，并且能够模拟用户进行点赞、收藏、发布笔记等操作。

[Start Now (On Apify)](https://apify.com/doliz/rednote-scraper)

[Start Now (Local deployment)](https://hub.docker.com/r/kinifine/rednote-scraper)

## ✨ API DOC

**描述:** 一个用于代理小红书后端API的FastAPI服务。

### 当前登录用户的信息
`GET /api/v1/me`

> 获取当前登录用户的信息。可用来验证cookie是否有效。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

---

### 当前登录用户的信息
`GET /api/v1/self_info`

> 获取当前登录用户的信息。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

---

### 首页推荐-分类
`GET /api/v1/homefeed/category`

> 获取首页推荐的分类。可作为首页推荐的入参。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

---

### 首页推荐
`POST /api/v1/homefeed`

> 获取首页推荐内容。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 首页推荐 Model

| 字段                   | 类型    | 是否必须 | 描述                                                     | 默认值               |
| :--------------------- | :------ | :------- | :------------------------------------------------------- | :------------------- |
| `cursor_score`         | string  | No       | 分页游标。从前一页的结果中获取, 第一页为空               | `""`                 |
| `num`                  | integer | No       | 笔记数量                                                 | `50`                 |
| `refresh_type`         | integer | No       | 刷新类型。1: 初始加载/下拉刷新; 3: 上滑加载更多          | `1`                  |
| `note_index`           | integer | No       | 已加载内容数量(累计)。第一页时等于 num                   | `43`                 |
| `unread_begin_note_id` | string  | No       | omit                                                     | `""`                 |
| `unread_end_note_id`   | string  | No       | omit                                                     | `""`                 |
| `unread_note_count`    | integer | No       | omit                                                     | `0`                  |
| `category`             | string  | No       | 笔记分类。可通过 /api/v1/homefeed/category 获取          | `homefeed_recommend` |
| `search_key`           | string  | No       | 搜索关键词                                               | `""`                 |
| `need_num`             | integer | No       | 客户端实际需要的内容数量。这个参数可能与 num 协同工作... | `18`                 |
| `image_formats`        | array   | No       | omit                                                     | `null`               |
| `need_filter_image`    | boolean | No       | omit                                                     | `false`              |

---

### 用户信息
`GET /api/v1/user_info`

> 根据用户ID获取用户详细信息。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述   |
| :----------------- | :----- | :------- | :----- |
| `user_id`          | query  | Yes      | 用户ID |
| `x-rednote-cookie` | header | No       | -      |

---

### 用户发布的笔记
`GET /api/v1/user_note`

> 根据用户ID获取用户发布的笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `user_id`          | query  | Yes      | 用户ID                                     |        |
| `num`              | query  | No       | 笔记数量                                   | `30`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `xsec_token`       | query  | No       | 安全验证-令牌                              | `""`   |
| `xsec_source`      | query  | No       | 安全验证-来源标识                          | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 用户赞过的笔记
`GET /api/v1/user_like_note`

> 根据用户ID获取用户赞过的笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `user_id`          | query  | Yes      | 用户ID                                     |        |
| `num`              | query  | No       | 笔记数量                                   | `30`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `xsec_token`       | query  | No       | 安全验证-令牌                              | `""`   |
| `xsec_source`      | query  | No       | 安全验证-来源标识                          | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 用户收藏的笔记
`GET /api/v1/user_collect_note`

> 根据用户ID获取用户收藏的笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `user_id`          | query  | Yes      | 用户ID                                     |        |
| `num`              | query  | No       | 笔记数量                                   | `30`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `xsec_token`       | query  | No       | 安全验证-令牌                              | `""`   |
| `xsec_source`      | query  | No       | 安全验证-来源标识                          | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 笔记信息
`POST /api/v1/note_info`

> 根据笔记ID和xsec_token获取笔记信息。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 笔记信息 Model

| 字段             | 类型   | 是否必须 | 描述              | 默认值    |
| :--------------- | :----- | :------- | :---------------- | :-------- |
| `source_note_id` | string | Yes      | 笔记 ID           |           |
| `image_formats`  | array  | No       | omit              | `null`    |
| `extra`          | object | No       | omit              | `null`    |
| `xsec_source`    | string | No       | 安全验证-来源标识 | `pc_user` |
| `xsec_token`     | string | Yes      | 安全验证-令牌     |           |

---

### 关键词趋势(猜你想搜)
`GET /api/v1/keyword_trending`

> 获取关键词趋势(猜你想搜)。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

---

### 关键词推荐
`GET /api/v1/keyword_recommend`

> 根据关键词给出推荐关键词。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述   |
| :----------------- | :----- | :------- | :----- |
| `keyword`          | query  | Yes      | 关键词 |
| `x-rednote-cookie` | header | No       | -      |

---

### 搜索过滤
`GET /api/v1/search_filter`

> 根据关键词给出搜索过滤信息(包含热词)。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述   |
| :----------------- | :----- | :------- | :----- |
| `keyword`          | query  | Yes      | 关键词 |
| `x-rednote-cookie` | header | No       | -      |

---

### 搜索笔记
`POST /api/v1/search_note`

> 搜索笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 搜索笔记 Model

| 字段                  | 类型    | 是否必须 | 描述                                                         | 默认值 |
| :-------------------- | :------ | :------- | :----------------------------------------------------------- | :----- |
| `keyword`             | string  | Yes      | 关键词                                                       |        |
| `page`                | integer | No       | 页码                                                         | `1`    |
| `page_size`           | integer | No       | 每页大小                                                     | `20`   |
| `note_type`           | string  | No       | 笔记类型: `全部`, `图文`, `视频`                             | `全部` |
| `sort_type`           | string  | No       | 排序依据: `综合`, `最新`, `最多点赞`, `最多评论`, `最多收藏` | `综合` |
| `filter_note_type`    | string  | No       | 筛选-笔记类型: `不限`, `视频`, `图文`                        | `不限` |
| `filter_note_time`    | string  | No       | 筛选-发布时间: `不限`, `一天内`, `一周内`, `半年内`          | `不限` |
| `filter_note_range`   | string  | No       | 筛选-搜索范围: `不限`, `已看过`, `未看过`, `已关注`          | `不限` |
| `filter_pos_distance` | string  | No       | 筛选-位置距离: `不限`, `同城`, `附近` (需指定geo)            | `不限` |
| `filter_geo`          | object  | No       | 筛选-位置距离-geo。如: `{"latitude":1.3, "longitude":103.9}` | `null` |
| `filter_hot`          | string  | No       | 热词。可通过 /api/v1/search_filter 获取                      | `""`   |

---

### 搜索用户
`POST /api/v1/search_user`

> 搜索用户。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 搜索用户 Model

| 字段        | 类型    | 是否必须 | 描述     | 默认值 |
| :---------- | :------ | :------- | :------- | :----- |
| `keyword`   | string  | Yes      | 关键词   |        |
| `page`      | integer | No       | 页码     | `1`    |
| `page_size` | integer | No       | 每页大小 | `20`   |

---

### 获取一级评论
`GET /api/v1/get_comment`

> 根据笔记ID获取一级评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `note_id`          | query  | Yes      | 笔记ID                                     |        |
| `xsec_token`       | query  | Yes      | 安全验证-令牌                              |        |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 获取二级评论
`GET /api/v1/get_sub_comment`

> 根据笔记ID和一级评论ID获取二级评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `note_id`          | query  | Yes      | 笔记ID                                     |        |
| `xsec_token`       | query  | Yes      | 安全验证-令牌                              |        |
| `comment_id`       | query  | Yes      | 一级评论ID                                 |        |
| `num`              | query  | No       | 评论数量                                   | `10`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 评论和@
`GET /api/v1/mentions`

> 获取评论和@提醒。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `num`              | query  | No       | 获取数量                                   | `20`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 赞和收藏
`GET /api/v1/likes`

> 获取赞和收藏。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `num`              | query  | No       | 获取数量                                   | `20`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 新增关注
`GET /api/v1/follows`

> 获取新增关注。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述                                       | 默认值 |
| :----------------- | :----- | :------- | :----------------------------------------- | :----- |
| `num`              | query  | No       | 获取数量                                   | `20`   |
| `cursor`           | query  | No       | 分页游标。从前一页的结果中获取, 第一页为空 | `""`   |
| `x-rednote-cookie` | header | No       | -                                          |        |

---

### 搜索话题
`POST /api/v1/search_topic`

> 搜索话题。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 搜索话题 Model

| 字段        | 类型    | 是否必须 | 描述     | 默认值 |
| :---------- | :------ | :------- | :------- | :----- |
| `keyword`   | string  | Yes      | 关键词   |        |
| `page`      | integer | No       | 页码     | `1`    |
| `page_size` | integer | No       | 每页大小 | `20`   |

---

### 创建话题
`POST /api/v1/create_topic`

> 创建话题。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 创建话题 Model

| 字段          | 类型   | 是否必须 | 描述     |
| :------------ | :----- | :------- | :------- |
| `topic_names` | string | Yes      | 话题名称 |

---

### 搜索地点
`POST /api/v1/search_location`

> 搜索地点。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 搜索地点 Model

| 字段        | 类型    | 是否必须 | 描述     | 默认值 |
| :---------- | :------ | :------- | :------- | :----- |
| `latitude`  | integer | No       | 纬度     | `0`    |
| `longitude` | integer | No       | 精度     | `0`    |
| `keyword`   | string  | Yes      | 关键词   |        |
| `page`      | integer | No       | 页码     | `1`    |
| `size`      | integer | No       | 每页大小 | `50`   |
| `source`    | string  | No       | omit     | `WEB`  |
| `type`      | integer | No       | omit     | `3`    |

---

### 发布图文笔记
`POST /api/v1/publish_note`

> 发布图文笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

> 发布图文笔记 Model

| 字段       | 类型   | 是否必须 | 描述                               | 默认值 |
| :--------- | :----- | :------- | :--------------------------------- | :----- |
| `images`   | array  | Yes      | 图片URL列表                        |        |
| `title`    | string | Yes      | 标题                               |        |
| `desc`     | string | Yes      | 正文内容                           |        |
| `topics`   | array  | No       | 话题列表。正文中仍要引用才会生效   | `null` |
| `location` | string | No       | 地点。实际会根据入参选择最近的地点 | `""`   |

---

### 点赞笔记
`POST /api/v1/like_note`

> 点赞笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段       | 类型   | 是否必须 | 描述   |
| :--------- | :----- | :------- | :----- |
| `note_oid` | string | Yes      | 笔记ID |

---

### 取消点赞笔记
`POST /api/v1/dislike_note`

> 取消点赞笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段       | 类型   | 是否必须 | 描述   |
| :--------- | :----- | :------- | :----- |
| `note_oid` | string | Yes      | 笔记ID |

---

### 收藏笔记
`POST /api/v1/collect_note`

> 收藏笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段      | 类型   | 是否必须 | 描述   |
| :-------- | :----- | :------- | :----- |
| `note_id` | string | Yes      | 笔记ID |

---

### 取消收藏笔记
`POST /api/v1/uncollect_note`

> 取消收藏笔记。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段       | 类型   | 是否必须 | 描述   |
| :--------- | :----- | :------- | :----- |
| `note_ids` | string | Yes      | 笔记ID |

---

### 发布评论
`POST /api/v1/post_comment`

> 发布评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段                | 类型   | 是否必须 | 描述                                       | 默认值 |
| :------------------ | :----- | :------- | :----------------------------------------- | :----- |
| `note_id`           | string | Yes      | 笔记ID                                     |        |
| `content`           | string | Yes      | 评论内容                                   |        |
| `target_comment_id` | string | No       | 评论ID。为空时给笔记评论，不为空时回复评论 | `""`   |
| `at_users`          | array  | No       | omit                                       | `null` |

---

### 删除评论
`POST /api/v1/delete_comment`

> 删除评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段         | 类型   | 是否必须 | 描述   |
| :----------- | :----- | :------- | :----- |
| `note_id`    | string | Yes      | 笔记ID |
| `comment_id` | string | Yes      | 评论ID |

---

### 点赞评论
`POST /api/v1/like_comment`

> 点赞评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段         | 类型   | 是否必须 | 描述   |
| :----------- | :----- | :------- | :----- |
| `note_id`    | string | Yes      | 笔记ID |
| `comment_id` | string | Yes      | 评论ID |

---

### 取消点赞评论
`POST /api/v1/dislike_comment`

> 取消点赞评论。

#### Parameters

| 名称               | 位置   | 是否必须 | 描述 |
| :----------------- | :----- | :------- | :--- |
| `x-rednote-cookie` | header | No       | -    |

#### Request Body (`application/json`)

| 字段         | 类型   | 是否必须 | 描述   |
| :----------- | :----- | :------- | :----- |
| `note_id`    | string | Yes      | 笔记ID |
| `comment_id` | string | Yes      | 评论ID |



## 如何获取 Cookies

1.  在您的浏览器中打开 [小红书](https://www.xiaohongshu.com/) 并登录。
2.  打开开发者工具（通常按 F12 或 Ctrl+Shift+I）。
3.  切换到 “网络” (Network) 标签页。
4.  刷新页面或与网站进行一些交互（例如，点击一个笔记）。
5.  在网络请求列表中，找到一个对 `edith.xiaohongshu.com` 的请求。
6.  点击该请求，在右侧的 “标头” (Headers) 标签页中，向下滚动到 “请求标头” (Request Headers)。
7.  找到 `cookie` 字段，并复制其完整的值。
8.  将复制的 cookie 字符串粘贴到采集器的 `cookies` 输入字段中。

![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/get_cookie.png)



## 更新日志

- **1.0.0** - 初始版本。

