# 小红书采集器 (Rednote Scraper)

小红书采集器是一个强大的网络爬虫，可以从[小红书](https://www.xiaohongshu.com/)网站上提取各种数据。它支持多种数据采集目标，包括用户信息、笔记、评论、搜索结果等，并且能够模拟用户进行点赞、收藏、发布笔记等操作。

[Start Now (On Apify)](https://apify.com/doliz/rednote-scraper)

[Start Now (Local deployment)](https://hub.docker.com/r/kinifine/rednote-scraper)

## 最佳实践 & 注意事项 (Best Practices & Precautions)

> **⚠️ 重要警告：** 本工具通过调用小红书接口进行数据收集。任何模拟真实用户操作的行为都存在被目标平台风控系统检测的风险。**您因使用本工具而可能导致的小红书账号限制、功能屏蔽乃至封禁等一切后果，均由您自行承担。** 请务必谨慎使用，并强烈建议仅将本工具用于学习和研究目的。
> **重要提示：您提供的 Cookie 就代表了您的登录账号！**

---

### 1. 模仿人类行为，控制速度
真实用户浏览内容是缓慢且有间隔的。请将最大并发数**设置为 1**，并在可能的情况下增加请求间的延迟。这是模仿人类行为、避免被检测到的最重要步骤。

### 2. 使用备用账号并“养号”
为防止主账号被限制，请务必使用一个备用小号。对于新注册的账号，建议先手动正常使用几天（如点赞、浏览、评论），这就是“养号”。这个过程能提高账号的信任度，显著降低被风控的概率。

### 3. 使用多个帐户（cookie）
通过提供一个帐户cookie池，并通过它们轮换不同的请求。这有效地分配了请求负载，并显著降低了任何单个帐户由于高流量而受到速率限制的风险。

### 4. 模拟真实网络环境
Apify 默认的 IP 是服务器 IP，很容易被识别。您有两个选择来模拟真实用户的网络：

*   **选项 A (云端方案): 使用住宅代理**
    在 Apify 的[代理配置](https://console.apify.com/proxy/usage)中，选择**[住宅代理 (Residential Proxy)](https://docs.apify.com/platform/proxy/residential-proxy)** 并启用**[会话 (Session)](https://docs.apify.com/platform/proxy/usage#sessions)** 功能。这能完美模拟一个真实用户在家里、用同一个 IP 稳定上网的环境。

*   **选项 B (本地方案): 使用 Docker**
    您也可以在本地运行此工具，使用您自己的家庭网络。[Start Now (Local deployment)](https://hub.docker.com/r/kinifine/rednote-scraper)

## ✨ 功能

该采集器支持以下功能：

- **个人数据**: 个人用户信息、猜你想搜、关键词推荐、评论和@、赞和收藏、新增关注。
- **公开数据**: 获取首页推荐、搜索笔记、搜索用户、用户信息、用户发布的笔记、用户赞过的笔记、用户收藏的笔记、笔记信息、获取一级评论、获取二级评论。
- **互动操作**: 点赞/取消点赞笔记、收藏/取消收藏笔记、发布/删除评论、点赞/取消点赞评论。
- **内容发布**: 发布图文笔记、创建话题。

## ⚙️ 输入

### ⚙️ `target`
选择要执行的数据采集或操作任务。根据您的选择，下面相应的设置将被使用(其他设置将被忽略)。

| 值/value             | 名称/name     | 花费/cost        | 描述/description                                                                            |
|---------------------|-------------|----------------|-------------------------------------------------------------------------------------------|
| `me`                | 个人用户信息1     | 0.001$ / 次     | /                                                                                         |
| `self_info`         | 个人用户信息2     | 0.001$ / 次     | /                                                                                         |
| `keyword_trending`  | 关键词趋势(猜你想搜) | 0.001$ / 次     | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/keyword_trending.png)  |
| `keyword_recommend` | 关键词推荐       | 0.001$ / 次     | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/keyword_recommend.png) |
| `mentions`          | 评论和@        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/mentions.png)          |
| `likes`             | 赞和收藏        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/likes.png)             |
| `follows`           | 新增关注        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/follows.png)           |
| `homefeed_category` | 首页推荐-分类     | 0.001$ / 次     | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/homefeed_category.png) |
| `homefeed`          | 首页推荐        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/homefeed.png)          |
| `search_filter`     | 搜索过滤        | 0.001$ / 次     | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/search_filter.png)     |
| `search_note`       | 搜索笔记        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/search_note.png)       |
| `search_user`       | 搜索用户        | 0.001$ / item | ![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/search_user.png)       |
| `user_info`         | 用户信息        | 0.001$ / 次     | 根据用户ID获取某用户信息                                                                             |
| `user_note`         | 用户发布的笔记     | 0.001$ / item | 根据用户ID获取某用户的笔记                                                                            |
| `user_like_note`    | 用户赞过的笔记     | 0.001$ / item | 根据用户ID获取某用户赞过的笔记                                                                          |
| `user_collect_note` | 用户收藏的笔记     | 0.001$ / item | 根据用户ID获取某用户收藏的笔记                                                                          |
| `note_info`         | 笔记信息        | 0.001$ / 次     | 根据笔记ID获取笔记信息                                                                              |
| `get_comment`       | 获取一级评论      | 0.001$ / item | 根据笔记ID获取一级评论                                                                              |
| `get_sub_comment`   | 获取二级评论      | 0.001$ / item | 根据笔记ID和一级评论ID获取二级评论                                                                       |
| `like_note`         | 点赞笔记        | 0.005$ / 次     | 根据笔记ID点赞笔记                                                                                |
| `dislike_note`      | 取消点赞笔记      | 0.005$ / 次     | 根据笔记ID取消点赞笔记                                                                              |
| `collect_note`      | 收藏笔记        | 0.005$ / 次     | 根据笔记ID收藏笔记                                                                                |
| `uncollect_note`    | 取消收藏笔记      | 0.005$ / 次     | 根据笔记ID取消收藏笔记                                                                              |
| `post_comment`      | 发布评论        | 0.005$ / 次     | 在某笔记或某评论下发布评论                                                                             |
| `delete_comment`    | 删除评论        | 0.005$ / 次     | 删除已发布的评论                                                                                  |
| `like_comment`      | 点赞评论        | 0.005$ / 次     | 点赞某评论                                                                                     |
| `dislike_comment`   | 取消点赞评论      | 0.005$ / 次     | 取消点赞某评论                                                                                   |
| `search_topic`      | 搜索话题        | 0.001$ / item | 搜索话题                                                                                      |
| `create_topic`      | 创建话题        | 0.005$ / 次     | 创建话题                                                                                      |
| `search_location`   | 搜索地点        | 0.001$ / item | 搜索地点                                                                                      |
| `publish_note`      | 发布图文笔记      | 0.005$ / 次     | 发布图文笔记                                                                                    |

### ⚙️ `cookies`
**必需。** 您的 小红书 cookies。获取方式: 
![](https://github.com/lofe-w/rednote-scraper-public/raw/main/imgs/get_cookie.png)

---

### ⚙️ 个人用户信息1 (`me`)

无额外入参

入参示例
```json
{
    "target": "me",
    "cookies": "your cookies"
}
```

---

### ⚙️ 个人用户信息2 (`self_info`)

无额外入参

入参示例
```json
{
    "target": "self_info",
    "cookies": "your cookies"
}
```

---

### ⚙️ 关键词趋势(猜你想搜) (`keyword_trending`)

无额外入参

入参示例
```json
{
    "target": "keyword_trending",
    "cookies": "your cookies"
}
```

---

### ⚙️ 关键词推荐 (`keyword_recommend`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `keyword_recommend_keyword` | 关键词。 | `"榴莲"` |

入参示例
```json
{
    "target": "keyword_recommend",
    "cookies": "your cookies",
    "keyword_recommend_keyword": "榴莲"
}
```

---

### ⚙️ 评论和@ (`mentions`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `mentions_num` | 获取数量。 | `20` |
| `mentions_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "mentions",
    "cookies": "your cookies",
    "mentions_num": 20,
    "mentions_cursor": ""
}
```

---

### ⚙️ 赞和收藏 (`likes`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `likes_num` | 获取数量。 | `20` |
| `likes_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "likes",
    "cookies": "your cookies",
    "likes_num": 20,
    "likes_cursor": ""
}
```

---

### ⚙️ 新增关注 (`follows`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `follows_num` | 获取数量。 | `20` |
| `follows_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "follows",
    "cookies": "your cookies",
    "follows_num": 20,
    "follows_cursor": ""
}
```

---

### ⚙️ 首页推荐-分类 (`homefeed_category`)

无额外入参

入参示例
```json
{
    "target": "homefeed_category",
    "cookies": "your cookies"
}
```

---

### ⚙️ 首页推荐 (`homefeed`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `homefeed_cursor_score` | 分页游标，从前一页的结果中获取，第一页时为空。 | `""` |
| `homefeed_num` | 笔记数量。 | `50` |
| `homefeed_refresh_type` | 刷新类型。`1`: 初始加载/下拉刷新; `3`: 上滑加载更多。 | `"1"` |
| `homefeed_note_index` | 笔记总量(累计)。第一页时等于 `笔记数量`。 | `43` |
| `homefeed_category` | 笔记分类，枚举值通过 `首页推荐-分类` 获取。 | `"homefeed_recommend"` |
| `homefeed_search_key` | 搜索关键词。 | `""` |
| `homefeed_need_num` | 客户端实际需要的内容数量。 | `18` |

入参示例
```json
{
    "target": "homefeed",
    "cookies": "your cookies",
    "homefeed_cursor_score": "",
    "homefeed_num": 50,
    "homefeed_refresh_type": "1",
    "homefeed_note_index": 43,
    "homefeed_category": "homefeed_recommend",
    "homefeed_search_key": "",
    "homefeed_need_num": 18
}
```

---

### ⚙️ 搜索过滤 (`search_filter`)

| 字段         | 描述 | 默认值 |
|------------|---|---|
| `search_filter_keyword` | 关键词。 | `"榴莲"` |

入参示例
```json
{
    "target": "search_filter",
    "cookies": "your cookies",
    "search_filter_keyword": "榴莲"
}
```

---

### ⚙️ 搜索笔记 (`search_note`)

| 字段 | 描述                                                                                                                                  | 默认值 |
|---|-------------------------------------------------------------------------------------------------------------------------------------|---|
| `search_note_keyword` | 关键词。                                                                                                                                | `"榴莲"` |
| `search_note_page` | 页码。                                                                                                                                 | `1` |
| `search_note_page_size` | 每页大小。                                                                                                                               | `20` |
| `search_note_note_type` | 笔记类型 (`0`: 全部, `2`: 图文, `1`: 视频)。                                                                                                   | `"0"` |
| `search_note_sort_type` | 排序依据 (`general`: 综合, `time_descending`: 最新, `popularity_descending`: 最多点赞, `comment_descending`: 最多评论, `collect_descending`: 最多收藏)。 | `"general"` |
| `search_note_filter_note_type` | 筛选-笔记类型 (`不限`, `视频笔记`, `普通笔记`)。                                                                                                     | `"不限"` |
| `search_note_filter_note_time` | 筛选-发布时间 (`不限`, `一天内`, `一周内`, `半年内`)。                                                                                                | `"不限"` |
| `search_note_filter_note_range` | 筛选-搜索范围 (`不限`, `已看过`, `未看过`, `已关注`)。                                                                                                | `"不限"` |
| `search_note_filter_pos_distance` | 筛选-位置距离 (`不限`, `同城`, `附近`)。                                                                                                         | `"不限"` |
| `search_note_filter_geo` | 筛选-位置距离-geo，例如: `{"latitude":1.3450101,"longitude":103.9832089}`。                                                                   | `{}` |
| `search_note_filter_hot` | 热词，枚举值通过 `搜索过滤` 获取。                                                                                                                 | `""` |

入参示例
```json
{
    "target": "search_note",
    "cookies": "your cookies",
    "search_note_keyword": "榴莲",
    "search_note_page": 1,
    "search_note_page_size": 20,
    "search_note_note_type": "0",
    "search_note_sort_type": "general",
    "search_note_filter_note_type": "不限",
    "search_note_filter_note_time": "不限",
    "search_note_filter_note_range": "不限",
    "search_note_filter_pos_distance": "不限",
    "search_note_filter_geo": {},
    "search_note_filter_hot": ""
}
```

---

### ⚙️ 搜索用户 (`search_user`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `search_user_keyword` | 关键词。 | `"榴莲"` |
| `search_user_page` | 页码。 | `1` |
| `search_user_page_size` | 每页大小。 | `20` |

入参示例
```json
{
    "target": "search_user",
    "cookies": "your cookies",
    "search_user_keyword": "榴莲",
    "search_user_page": 1,
    "search_user_page_size": 20
}
```

---

### ⚙️ 用户信息 (`user_info`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `user_info_user_id` | 用户ID。 | `"5b24961811be105dfe1079d4"` |

入参示例
```json
{
    "target": "user_info",
    "cookies": "your cookies",
    "user_info_user_id": "5b24961811be105dfe1079d4"
}
```

---

### ⚙️ 用户发布的笔记 (`user_note`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `user_note_user_id` | 用户ID。 | `"5b24961811be105dfe1079d4"` |
| `user_note_num` | 笔记数量。 | `30` |
| `user_note_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "user_note",
    "cookies": "your cookies",
    "user_note_user_id": "5b24961811be105dfe1079d4",
    "user_note_num": 30,
    "user_note_cursor": ""
}
```

---

### ⚙️ 用户赞过的笔记 (`user_like_note`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `user_like_note_user_id` | 用户ID。 | `"5b24961811be105dfe1079d4"` |
| `user_like_note_num` | 笔记数量。 | `30` |
| `user_like_note_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "user_like_note",
    "cookies": "your cookies",
    "user_like_note_user_id": "5b24961811be105dfe1079d4",
    "user_like_note_num": 30,
    "user_like_note_cursor": ""
}
```

---

### ⚙️ 用户收藏的笔记 (`user_collect_note`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `user_collect_note_user_id` | 用户ID。 | `"5b24961811be105dfe1079d4"` |
| `user_collect_note_num` | 笔记数量。 | `30` |
| `user_collect_note_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "user_collect_note",
    "cookies": "your cookies",
    "user_like_note_user_id": "5b24961811be105dfe1079d4",
    "user_like_note_num": 30,
    "user_like_note_cursor": ""
}
```

---

### ⚙️ 笔记信息 (`note_info`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `note_info_source_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `note_info_source_xsec_token` | 安全验证-令牌。 | `"ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q="` |

入参示例
```json
{
    "target": "note_info",
    "cookies": "your cookies",
    "note_info_source_note_id": "68f06fac000000000402bcb1",
    "note_info_source_xsec_token": "ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q="
}
```

---

### ⚙️ 获取一级评论 (`get_comment`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `get_comment_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `get_comment_xsec_token` | 安全验证-令牌。 | `"ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q="` |
| `get_comment_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "get_comment",
    "cookies": "your cookies",
    "get_comment_note_id": "68f06fac000000000402bcb1",
    "get_comment_xsec_token": "ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q=",
    "get_comment_cursor": ""
}
```

---

### ⚙️ 获取二级评论 (`get_sub_comment`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `get_sub_comment_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `get_sub_comment_xsec_token` | 安全验证-令牌。 | `"ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q="` |
| `get_sub_comment_comment_id` | 一级评论ID。 | `""` |
| `get_sub_comment_num` | 评论数量。 | `10` |
| `get_sub_comment_cursor` | 分页游标，从前一页的结果中获取，第一页为空。 | `""` |

入参示例
```json
{
    "target": "get_sub_comment",
    "cookies": "your cookies",
    "get_sub_comment_note_id": "68f06fac000000000402bcb1",
    "get_sub_comment_xsec_token": "ABDo_iNBehhSMA_yz74CU0s9Z7FVKtrC7edgpxHsY3o1Q=",
    "get_sub_comment_comment_id": "",
    "get_sub_comment_num": 10,
    "get_sub_comment_cursor": ""
}
```

---

### ⚙️ 点赞笔记 (`like_note`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `like_note_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |

入参示例
```json
{
    "target": "like_note",
    "cookies": "your cookies",
    "like_note_note_id": "68f06fac000000000402bcb1"
}
```

---

### ⚙️ 取消点赞笔记 (`dislike_note`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `dislike_note_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |

入参示例
```json
{
    "target": "dislike_note",
    "cookies": "your cookies",
    "dislike_note_note_id": "68f06fac000000000402bcb1"
}
```

---

### ⚙️ 收藏笔记 (`collect_note`)

| 字段                      | 描述 | 默认值 |
|-------------------------|---|---|
| `collect_note_note_id`  | 笔记ID。 | `"68f06fac000000000402bcb1"` |

入参示例
```json
{
    "target": "collect_note",
    "cookies": "your cookies",
    "collect_note_note_id": "68f06fac000000000402bcb1"
}
```

---

### ⚙️ 取消收藏笔记 (`uncollect_note`)

| 字段                                              | 描述 | 默认值 |
|-------------------------------------------------|---|---|
| `uncollect_note_note_id`                        | 笔记ID。 | `"68f06fac000000000402bcb1"` |

入参示例
```json
{
    "target": "uncollect_note",
    "cookies": "your cookies",
    "uncollect_note_note_id": "68f06fac000000000402bcb1"
}
```

---

### ⚙️ 发布评论 (`post_comment`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `post_comment_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `post_comment_content` | 评论内容。 | `"评论内容示例"` |
| `post_comment_comment_id` | 评论ID。为空时给某笔记发布评论, 不为空时给某评论发布评论 | `""` |

入参示例
```json
{
    "target": "post_comment",
    "cookies": "your cookies",
    "post_comment_note_id": "68f06fac000000000402bcb1",
    "post_comment_content": "评论内容示例",
    "post_comment_comment_id": ""
}
```

---

### ⚙️ 删除评论 (`delete_comment`)

| 字段 | 描述                           | 默认值 |
|---|------------------------------|---|
| `delete_comment_note_id` | 笔记ID。                        | `"68f06fac000000000402bcb1"` |
| `delete_comment_comment_id` | 评论ID。为空时删除某笔记的评论, 不为空时删除某评论的评论 | `""` |

入参示例
```json
{
    "target": "delete_comment",
    "cookies": "your cookies",
    "delete_comment_note_id": "68f06fac000000000402bcb1",
    "delete_comment_comment_id": ""
}
```

---

### ⚙️ 点赞评论 (`like_comment`)

| 字段                                               | 描述 | 默认值 |
|--------------------------------------------------|---|---|
| `like_comment_note_id`                           | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `like_comment_comment_id`                        | 评论ID。 | `""` |

入参示例
```json
{
    "target": "like_comment",
    "cookies": "your cookies",
    "like_comment_note_id": "68f06fac000000000402bcb1",
    "like_comment_comment_id": ""
}
```

---

### ⚙️ 取消点赞评论 (`dislike_comment`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `dislike_comment_note_id` | 笔记ID。 | `"68f06fac000000000402bcb1"` |
| `dislike_comment_comment_id` | 评论ID。 | `""` |

入参示例
```json
{
    "target": "dislike_comment",
    "cookies": "your cookies",
    "dislike_comment_note_id": "68f06fac000000000402bcb1",
    "dislike_comment_comment_id": ""
}
```

---

### ⚙️ 搜索话题 (`search_topic`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `search_topic_keyword` | 关键词。 | `"榴莲"` |
| `search_topic_page` | 页码。 | `1` |
| `search_topic_page_size` | 每页大小。 | `20` |

入参示例
```json
{
    "target": "search_topic",
    "cookies": "your cookies",
    "search_topic_keyword": "榴莲",
    "search_topic_page": 1,
    "search_topic_page_size": 20
}
```

---

### ⚙️ 创建话题 (`create_topic`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `create_topic_topic_names` | 话题名称。 | `"榴莲"` |

入参示例
```json
{
    "target": "create_topic",
    "cookies": "your cookies",
    "create_topic_topic_names": "榴莲"
}
```

---

### ⚙️ 搜索地点 (`search_location`)

| 字段 | 描述 | 默认值 |
|---|---|---|
| `search_location_keyword` | 关键词。 | `"北京"` |
| `search_location_page` | 页码。 | `1` |
| `search_location_size` | 每页大小。 | `50` |

入参示例
```json
{
    "target": "search_location",
    "cookies": "your cookies",
    "search_location_keyword": "北京",
    "search_location_page": 1,
    "search_location_size": 50
}
```

---

### ⚙️ 发布图文笔记 (`publish_note`)

| 字段 | 描述                                                                                                                       | 默认值 |
|---|--------------------------------------------------------------------------------------------------------------------------|---|
| `publish_note_images` | 图片URL列表。                                                                                                                 | `["https://raw.githubusercontent.com/github/explore/main/topics/python/python.png"]` |
| `publish_note_title` | 标题。                                                                                                                      | `"标题示例"` |
| `publish_note_desc` | 正文内容。                                                                                                                    | `"正文内容示例... #topic1[话题]# #topic2[话题]#"` |
| `publish_note_topics` | 话题列表。如果已有话题则直接引用, 如果没有话题会创建话题后引用。配置话题列表后(例如: ["topic1","topic2"]), 正文内容仍要引用(例如: 正文内容示例... #topic1[话题]# #topic2[话题]#)才会生效 | `["topic1", "topic2"]` |
| `publish_note_location` | 地点。实际会根据入参选择最近(系统推荐)的地点, 可能与输入不完全一致                                                                                      | `"北京"` |

入参示例
```json
{
    "target": "publish_note",
    "cookies": "your cookies",
    "publish_note_images": ["https://raw.githubusercontent.com/github/explore/main/topics/python/python.png"],
    "publish_note_title": "标题示例",
    "publish_note_desc": "正文内容示例... #topic1[话题]# #topic2[话题]#",
    "publish_note_topics": ["topic1", "topic2"],
    "publish_note_location": "北京"
}
```

---

## 📊 输出

采集器将返回小红书官方API的原始JSON响应。输出的数据结构会根据您选择的 `target` 而有所不同。

### 📊️ 个人用户信息1 (`me`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "images": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/360/format/webp",
      "imageb": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/540/format/webp",
      "guest": false,
      "red_id": "633500655",
      "user_id": "5b24961811be105dfe1079d4",
      "nickname": "红薯蜀",
      "desc": "",
      "gender": 0
    }
  }
]
```

---

### 📊️ 个人用户信息2 (`self_info`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "tab_public": {
        "collection": true,
        "collectionBoard": {
          "display": true,
          "lock": false,
          "count": 0
        },
        "collectionNote": {
          "display": true,
          "lock": false,
          "count": 5
        }
      },
      "result": {
        "success": true,
        "code": 0,
        "message": "success"
      },
      "basic_info": {
        "desc": "",
        "imageb": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/540/format/webp",
        "nickname": "红薯蜀",
        "images": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/360/format/webp",
        "red_id": "633500655",
        "gender": 0,
        "ip_location": "上海"
      },
      "interactions": [
        {
          "type": "follows",
          "name": "关注",
          "count": "2"
        },
        {
          "name": "粉丝",
          "count": "1",
          "type": "fans"
        },
        {
          "type": "interaction",
          "name": "获赞与收藏",
          "count": "2"
        }
      ],
      "tags": [
        {
          "icon": "http://ci.xiaohongshu.com/icons/user/gender-male-v1.png",
          "tagType": "info"
        }
      ]
    }
  }
]
```

---

### 📊️ 关键词趋势(猜你想搜) (`keyword_trending`)

输出示例
```json
[
  {
    "success": true,
    "msg": "成功",
    "data": {
      "queries": [
        {
          "search_word": "付航宣布结婚",
          "hint_word_request_id": "6af408f3-0da6-4f54-93b3-002151fccc21#1760930738492",
          "title": "付航宣布结婚",
          "desc": "付航宣布结婚",
          "type": "firstEnterOther#trendingSavHighClick#68f121ae0000000003013304#1#0"
        },
        {
          "title": "易梦玲隆胸",
          "desc": "易梦玲隆胸",
          "type": "firstEnterOther#trendingSavHighClick#68ee11120000000003021b72#2#0",
          "search_word": "易梦玲隆胸"
        },
        ... /* omit */
      ],
      "hint_word": {
        "title": "付航宣布结婚",
        "desc": "付航宣布结婚",
        "type": "firstEnterOther#trendingSavHighClick#68f121ae0000000003013304#1#0",
        "search_word": "付航宣布结婚",
        "hint_word_request_id": "6af408f3-0da6-4f54-93b3-002151fccc21#1760930738492"
      },
      "word_request_id": "6af408f3-0da6-4f54-93b3-002151fccc21#1760930738492",
      "title": "猜你想搜"
    },
    "code": 1000
  }
]
```

---

### 📊️ 关键词推荐 (`keyword_recommend`)

输出示例
```json
[
  {
    "code": 1000,
    "success": true,
    "msg": "成功",
    "data": {
      "search_cpl_id": "065961ae73ad6ba17f5fcfb268f5abbb",
      "word_request_id": "d5e47202-ec12-47a6-8aac-aa7594bf45e6#1760930747418",
      "sug_items": [
        {
          "text": "榴莲怎么挑选",
          "highlight_flags": [
            true,
            true,
            false,
            false,
            false,
            false
          ],
          "search_type": "notes",
          "type": "top_note"
        },
        {
          "text": "榴莲的功效与作用",
          "highlight_flags": [
            true,
            true,
            false,
            false,
            false,
            false,
            false,
            false
          ],
          "search_type": "notes",
          "type": "top_note"
        },
        ... /* omit */
      ]
    }
  }
]
```

---

### 📊️ 评论和@ (`mentions`)

输出示例
```json
[
  {
    "data": {
      "message_list": [
        {
          "time_flag": 0,
          "type": "mention/comment",
          "score": 7562924856746573000,
          "user_info": {
            "image": "https://sns-avatar-qc.xhscdn.com/avatar/5afec782d2c8a50ded234f95.jpg?imageView2/2/w/120/format/jpg",
            "red_official_verify_type": 0,
            "indicator": "你的好友",
            "xsec_token": "ABRO2OlrMhlBesEX53f_9SQqojI-ZzcjHj3Owga6zj8bg=",
            "userid": "5afec741e8ac2b32d69e7eb2",
            "nickname": "付"
          },
          "item_info": {
            "type": "note_info",
            "id": "68ec9bc70000000003010f94",
            "content": "求问下网友这是哪座山峰？",
            "image_info": {
              "url": "http://ci.xiaohongshu.com/notes_pre_post/1040g3k831nio892qmgd05nh41sp09cs1ujjil6o?imageView2/2/w/1080/format/jpg",
              "width": 3712,
              "height": 5568
            },
            "user_info": {
              "nickname": "MAX",
              "image": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo31jmiekf3io6g5nh41sp09cs1cubt1vg?imageView2/2/w/120/format/jpg",
              "red_official_verify_type": 0,
              "userid": "5e240f32000000000100b381"
            },
            "status": 0,
            "xsec_token": "LBCIW_WcT_TBFJIjdXE6rAIbIJ7hVKNOSsTbt62dKwJ64=",
            "image": "http://ci.xiaohongshu.com/notes_pre_post/1040g3k831nio892qmgd05nh41sp09cs1ujjil6o?imageView2/2/w/1080/format/jpg",
            "illegal_info": {
              "status": 0,
              "desc": "",
              "illegal_status": "NORMAL"
            },
            "link": "xhsdiscover://item/discovery.68ec9bc70000000003010f94?type=normal&sourceID=notifications&feedType=single&anchorCommentId=68f4e814000000003800c974&authorId=5e240f32000000000100b381"
          },
          "comment_info": {
            "liked": false,
            "like_count": 0,
            "id": "68f4e814000000003800c974",
            "content": "@小红薯DCC4634",
            "illegal_info": {
              "status": 0,
              "desc": "",
              "illegal_status": "NORMAL"
            },
            "status": 0
          },
          "track_type": "8",
          "liked": false,
          "id": "7562924856746572429",
          "title": "在评论中@了你",
          "time": 1760880662
        },
        ... /* omit */
      ],
      "has_more": false,
      "cursor": 7562924856746573000,
      "strCursor": "7562924856746572429"
    },
    "code": 0,
    "success": true,
    "msg": "成功"
  }
]
```

---

### 📊️ 赞和收藏 (`likes`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "result": {
        "success": true,
        "code": 0,
        "message": ""
      },
      "message_list": [
        {
          "title": "收藏了你的笔记",
          "user_info": {
            "nickname": "付",
            "image": "https://sns-avatar-qc.xhscdn.com/avatar/5afec782d2c8a50ded234f95.jpg?imageView2/2/w/120/format/jpg",
            "fstatus": "both",
            "red_official_verify_type": 0,
            "indicator": "你的好友",
            "xsec_token": "ABRO2OlrMhlBesEX53f_9SQqojI-ZzcjHj3Owga6zj8bg=",
            "userid": "5afec741e8ac2b32d69e7eb2"
          },
          "track_type": "4",
          "time_flag": 0,
          "liked": false,
          "id": "7562927416545378060",
          "type": "faved/item",
          "time": 1760881258,
          "score": 7562927416545378000,
          "item_info": {
            "xsec_token": "AB5uIZ7C9aefnL8KKKEdlBzjHwDhuiVEh2tgPdTKrZgh4=",
            "type": "board_info",
            "content": "默认专辑",
            "image": "http://ci.xiaohongshu.com/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg?imageView2/2/w/1080/format/jpg",
            "attach_item_info": {
              "xsec_token": "LBoF8K2NOR0dnSL_Hy5W_-qswePXKbw6YjOBlpb-oUO7E=",
              "type": "note_info",
              "id": "68f4e9bf00000000070327cb",
              "image": "http://ci.xiaohongshu.com/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg?imageView2/2/w/1080/format/jpg",
              "image_info": {
                "url": "http://ci.xiaohongshu.com/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg?imageView2/2/w/1080/format/jpg",
                "width": 1920,
                "height": 1080
              },
              "illegal_info": {
                "status": 0,
                "desc": "",
                "illegal_status": "NORMAL"
              },
              "link": "xhsdiscover://item/discovery.68f4e9bf00000000070327cb?type=video&sourceID=notifications&feedType=single",
              "status": 0
            },
            "extra_info": {
              "status": 1,
              "desc": "隐私专辑"
            },
            "status": 0,
            "id": "6248112f000000000101e907",
            "illegal_info": {
              "desc": "",
              "illegal_status": "NORMAL",
              "status": 0
            },
            "link": "xhsdiscover://item/discovery.68f4e9bf00000000070327cb?type=video&sourceID=notifications&feedType=single"
          }
        },
        ... /* omit */
      ],
      "has_more": false,
      "cursor": 7562927412251748000,
      "strCursor": "7562927412251748670"
    }
  }
]
```

---

### 📊️ 新增关注 (`follows`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "message_list": [
        {
          "type": "follow/you",
          "title": "开始关注你了",
          "user": {
            "userid": "5afec741e8ac2b32d69e7eb2",
            "nickname": "付",
            "images": "https://sns-avatar-qc.xhscdn.com/avatar/5afec782d2c8a50ded234f95.jpg?imageView2/2/w/120/format/jpg",
            "fstatus": "both",
            "red_official_verify_type": 0,
            "xsec_token": "ABRO2OlrMhlBesEX53f_9SQqojI-ZzcjHj3Owga6zj8bg="
          },
          "time": 1760880629,
          "score": 7562924715011712000,
          "track_type": "1",
          "id": "7562924715011712425"
        },
        ... /* omit */
      ],
      "has_more": false,
      "cursor": 7562924715011712000,
      "strCursor": "7562924715011712425"
    }
  }
]
```

---

### 📊️ 首页推荐-分类 (`homefeed_category`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "categories": [
        {
          "id": "homefeed.fashion_v3",
          "name": "穿搭"
        },
        {
          "id": "homefeed.food_v3",
          "name": "美食"
        },
        ... /* omit */
      ]
    }
  }
]
```

---

### 📊️ 首页推荐 (`homefeed`)

输出示例
```json
[{
  "code": 0,
  "success": true,
  "msg": "成功",
  "data": {
    "cursor_score": "1.7609309029500036E9",
    "items": [
      {
        "track_id": "2fhbkwjm4xpfd008ydf38",
        "ignore": false,
        "xsec_token": "ABr1-BU0eQazB1KQeblzUKhXOMmSqGM_EJhiCnvIeYPbs=",
        "id": "68d531500000000011016c5d",
        "model_type": "note",
        "note_card": {
          "interact_info": {
            "liked_count": "4124",
            "liked": false
          },
          "cover": {
            "url": "",
            "info_list": [
              {
                "image_scene": "WB_PRV",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201128/979dbac7b4d2cca442875b4353ed0610/1040g2sg31mrsf0lm5i6g5pqgcd9i1aggf8m9s5o!nc_n_webp_prv_1"
              },
              {
                "image_scene": "WB_DFT",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201128/f217b617ba276816966d9158208c73d5/1040g2sg31mrsf0lm5i6g5pqgcd9i1aggf8m9s5o!nc_n_webp_mw_1"
              }
            ],
            "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201128/979dbac7b4d2cca442875b4353ed0610/1040g2sg31mrsf0lm5i6g5pqgcd9i1aggf8m9s5o!nc_n_webp_prv_1",
            "url_default": "http://sns-webpic-qc.xhscdn.com/202510201128/f217b617ba276816966d9158208c73d5/1040g2sg31mrsf0lm5i6g5pqgcd9i1aggf8m9s5o!nc_n_webp_mw_1",
            "file_id": "",
            "height": 2016,
            "width": 1512
          },
          "video": {
            "capa": {
              "duration": 413
            }
          },
          "type": "video",
          "display_title": "这到底是谁发明的？味道真的绝了！",
          "user": {
            "xsec_token": "ABeoFUyOhlVU9A_7d5Of5qrQnvjx8CzwhT46vuUNXi6ss=",
            "nick_name": "莉莉爱掌勺",
            "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo31e5kbhi4gm4g5pqgcd9i1aggespc5g8",
            "user_id": "67506353000000000800aa10",
            "nickname": "莉莉爱掌勺"
          }
        }
      },
      ... /* omit */
    ]
  }
}]
```

---

### 📊️ 搜索过滤 (`search_filter`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "filters": [
        {
          "filter_tags": [
            {
              "id": "general",
              "name": "综合",
              "show_type": 0,
              "need_location_info": false
            },
            {
              "id": "time_descending",
              "name": "最新",
              "show_type": 0,
              "need_location_info": false
            },
            {
              "id": "popularity_descending",
              "name": "最多点赞",
              "show_type": 0,
              "need_location_info": false
            },
            {
              "name": "最多评论",
              "show_type": 0,
              "need_location_info": false,
              "id": "comment_descending"
            },
            {
              "id": "collect_descending",
              "name": "最多收藏",
              "show_type": 0,
              "need_location_info": false
            }
          ],
          "type": "single",
          "name": "排序依据",
          "id": "sort_type",
          "invisible": true,
          "word_request_id": "3278f2c3-262e-4759-a166-ed3c31932658#1760930925373",
          "group_show_type": 0
        },
        ... /* omit */
      ]
    }
  }
]
```

---

### 📊️ 搜索笔记 (`search_note`)

输出示例
```json
[{
  "code": 0,
  "success": true,
  "msg": "成功",
  "data": {
    "has_more": true,
    "items": [
      {
        "model_type": "note",
        "note_card": {
          "cover": {
            "url_default": "http://sns-webpic-qc.xhscdn.com/202510201129/0852093664bf70571e976f7796a0a895/notes_pre_post/1040g3k031hghdmlqja6g5q00tq62ntma1ovoirg!nc_n_webp_mw_1",
            "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201129/0c8c638a621a4d3c7a43b22b866fd458/notes_pre_post/1040g3k031hghdmlqja6g5q00tq62ntma1ovoirg!nc_n_webp_prv_1",
            "height": 1660,
            "width": 1242
          },
          "image_list": [
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/0852093664bf70571e976f7796a0a895/notes_pre_post/1040g3k031hghdmlqja6g5q00tq62ntma1ovoirg!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/0c8c638a621a4d3c7a43b22b866fd458/notes_pre_post/1040g3k031hghdmlqja6g5q00tq62ntma1ovoirg!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/e9c354350a6a588c7f11c95647cbbb27/notes_pre_post/1040g3k031hghdmmdkq6g5q00tq62ntmar2d014g!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/1a1471654dfd37456898ecea455fd593/notes_pre_post/1040g3k031hghdmmdkq6g5q00tq62ntmar2d014g!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/d595242d55b6a09330a24ca7750e264c/notes_pre_post/1040g3k031hghdmoqja3g5q00tq62ntmaft2ru30!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/5fd4567f85a3177e8bf371e1baec09df/notes_pre_post/1040g3k031hghdmoqja3g5q00tq62ntmaft2ru30!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/5cdbe1d7212be88e45f0fcdaad238cd0/notes_pre_post/1040g3k031hghdmlqja5g5q00tq62ntmal3q23mg!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/63a2bc448399eadc45cbf754852bee3b/notes_pre_post/1040g3k031hghdmlqja5g5q00tq62ntmal3q23mg!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/54b66ae1e8a3e77f60a382c9d959d3cf/notes_pre_post/1040g3k031hghdmoqja5g5q00tq62ntmapo4s3to!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/007d600136d23acd804b5314abf61819/notes_pre_post/1040g3k031hghdmoqja5g5q00tq62ntmapo4s3to!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/cf36c7b6dbdf4fa4590d61cc51ff6cab/notes_pre_post/1040g3k831hghdmnk4qk05q00tq62ntma8hib748!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/593823454a92244cd1ca02a1ac2780a5/notes_pre_post/1040g3k831hghdmnk4qk05q00tq62ntma8hib748!nc_n_webp_prv_1"
                }
              ]
            },
            {
              "height": 1660,
              "width": 1242,
              "info_list": [
                {
                  "image_scene": "WB_DFT",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/842c49183d5a663f9b1aa5b19de329e1/notes_pre_post/1040g3k031hghdmnnj8605q00tq62ntmad1bkqlo!nc_n_webp_mw_1"
                },
                {
                  "image_scene": "WB_PRV",
                  "url": "http://sns-webpic-qc.xhscdn.com/202510201129/d98a22f53bc1ed724c6a346252a4da90/notes_pre_post/1040g3k031hghdmnnj8605q00tq62ntmad1bkqlo!nc_n_webp_prv_1"
                }
              ]
            }
          ],
          "corner_tag_info": [
            {
              "type": "publish_time",
              "text": "05-15"
            }
          ],
          "type": "normal",
          "display_title": "入夏后吃榴莲，把阳气“吃”进肚子里‼️",
          "user": {
            "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo31ghbq53g426g5q00tq62ntmapvupm4g?imageView2/2/w/80/format/jpg",
            "user_id": "6800ee8c000000000a03f6ca",
            "nickname": "雪梨养生日记",
            "xsec_token": "ABcnFwGQbCB8mrm6s71BvgtgTmpE9nk8rjmUHIE29W770=",
            "nick_name": "雪梨养生日记"
          },
          "interact_info": {
            "liked": false,
            "liked_count": "3496",
            "collected": false,
            "collected_count": "2777",
            "comment_count": "180",
            "shared_count": "1694"
          }
        },
        "xsec_token": "ABw5rHg9byZVkqAvQhjIbyEBqriqXG1oXbH98KyRC36FA=",
        "id": "6825bbe1000000002301e347"
      },
      ... /* omit */
    ]
  }
}]
```

---

### 📊️ 搜索用户 (`search_user`)

输出示例
```json
[{
  "data": {
    "result": {
      "code": 1000,
      "message": "成功",
      "success": true
    },
    "users": [
      {
        "xsec_token": "ABuQY04zcWwhcnW8hhaEYhSeosxUkhxUjHN2417OvdumE=",
        "name": "榴莲",
        "followed": false,
        "red_official_verify_type": 0,
        "vshow": 0,
        "update_time": "42分钟前更新",
        "note_count": 96,
        "id": "671bddde000000001d0203f4",
        "image": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo31ir51lhi0o005porrnf7c0vk95ju15g?imageView2/2/w/360/format/webp",
        "sub_title": "小红书号：26286843918",
        "is_self": false,
        "fans": "3.9万",
        "link": "xhsdiscover://1/user/user.671bddde000000001d0203f4",
        "red_id": "26286843918",
        "show_red_official_verify_icon": false,
        "red_official_verified": false
      },
      ... /* omit */
    ],
    "has_more": true
  },
  "code": 1000,
  "success": true,
  "msg": "成功"
}]
```

---

### 📊️ 用户信息 (`user_info`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "tags": [
        {
          "tagType": "info",
          "icon": "http://ci.xiaohongshu.com/icons/user/gender-male-v1.png"
        }
      ],
      "tab_public": {
        "collection": true,
        "collectionNote": {
          "display": true,
          "lock": false,
          "count": 5
        },
        "collectionBoard": {
          "display": true,
          "lock": false,
          "count": 0
        }
      },
      "extra_info": {
        "blockType": "DEFAULT"
      },
      "result": {
        "success": true,
        "code": 0,
        "message": "success"
      },
      "basic_info": {
        "imageb": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/540/format/webp",
        "nickname": "红薯蜀",
        "images": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/360/format/webp",
        "red_id": "633500655",
        "gender": 0,
        "ip_location": "上海",
        "desc": ""
      },
      "interactions": [
        {
          "name": "关注",
          "count": "2",
          "type": "follows"
        },
        {
          "name": "粉丝",
          "count": "1",
          "type": "fans"
        },
        {
          "name": "获赞与收藏",
          "count": "2",
          "type": "interaction"
        }
      ]
    }
  }
]
```

---

### 📊️ 用户发布的笔记 (`user_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "notes": [
        {
          "xsec_token": "ABCpkc82MComsYdo8F3jH6QOvcWHx3746fvDysZi8wJTQ=",
          "type": "video",
          "display_title": "",
          "user": {
            "nick_name": "红薯蜀",
            "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg",
            "user_id": "5b24961811be105dfe1079d4",
            "nickname": "红薯蜀"
          },
          "interact_info": {
            "liked": false,
            "liked_count": "1",
            "sticky": false
          },
          "cover": {
            "trace_id": "",
            "info_list": [
              {
                "image_scene": "WB_PRV",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201137/917cc7580675d3bbecb584e23ca0e616/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nc_n_webp_prv_1"
              },
              {
                "image_scene": "WB_DFT",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201137/710e2497c5cc4890dd8c264161b99888/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nc_n_webp_mw_1"
              }
            ],
            "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201137/917cc7580675d3bbecb584e23ca0e616/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nc_n_webp_prv_1",
            "url_default": "http://sns-webpic-qc.xhscdn.com/202510201137/710e2497c5cc4890dd8c264161b99888/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nc_n_webp_mw_1",
            "file_id": "",
            "height": 1080,
            "width": 1920,
            "url": ""
          },
          "note_id": "68f4e9bf00000000070327cb"
        },
        ... /* omit */
      ],
      "has_more": false,
      "cursor": ""
    }
  }
]
```

---

### 📊️ 用户赞过的笔记 (`user_like_note`)

输出示例
```json
[
  {
    "success": true,
    "msg": "成功",
    "data": {
      "cursor": "68ed16880000000004002e66",
      "has_more": false,
      "notes": [
        {
          "user": {
            "nickname": "EF成人英语培训",
            "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo311u9anmu1o005nqoasn0bkvttmg5lo0?imageView2/2/w/120/format/jpg",
            "xsec_token": "ABYCXMeDs9NeM6guV13JpLJStSuXHr8pMuiKgWUTzy59M=",
            "user_id": "5f58572e000000000101d3fd"
          },
          "interact_info": {
            "liked": true,
            "liked_count": "8556"
          },
          "xsec_token": "AB6IJ9TU27uASGtBhf8ObfSCo6WuyJ-V9aVnE07G5JfmI=",
          "note_id": "6662b63f0000000006005104",
          "display_title": "每天1小时学好英语 改变命运💗",
          "type": "video",
          "cover": {
            "height": 960,
            "width": 720,
            "info_list": [
              {
                "image_scene": "WB_PRV",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201139/dcc4726c12661ff2fd6ce1d9649cba55/1040g2sg313o5ramb1c705nqoasn0bkvt1kf8958!nc_n_webp_prv_1"
              },
              {
                "image_scene": "WB_DFT",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201139/0b28ed7e957bdbcad3d1ec64d33d31e5/1040g2sg313o5ramb1c705nqoasn0bkvt1kf8958!nc_n_webp_mw_1"
              }
            ],
            "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201139/dcc4726c12661ff2fd6ce1d9649cba55/1040g2sg313o5ramb1c705nqoasn0bkvt1kf8958!nc_n_webp_prv_1",
            "url_default": "http://sns-webpic-qc.xhscdn.com/202510201139/0b28ed7e957bdbcad3d1ec64d33d31e5/1040g2sg313o5ramb1c705nqoasn0bkvt1kf8958!nc_n_webp_mw_1"
          }
        },
        ... /* omit */
      ]
    },
    "code": 0
  }
]
```

---

### 📊️ 用户收藏的笔记 (`user_collect_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "cursor": "68e882170000000004015974",
      "has_more": false,
      "notes": [
        {
          "note_id": "68f4e017000000000301ff41",
          "display_title": "谁懂这一口烤西瓜的含金量啊！！！！！",
          "type": "video",
          "cover": {
            "width": 1440,
            "info_list": [
              {
                "image_scene": "WB_PRV",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201139/bab725040256f30ce3839175d1b9143b/1040g00831nqrubpql800412904ol6ukft0fbuvg!nc_n_webp_prv_1"
              },
              {
                "image_scene": "WB_DFT",
                "url": "http://sns-webpic-qc.xhscdn.com/202510201139/345d37c53caaf2361e8f926ee065361d/1040g00831nqrubpql800412904ol6ukft0fbuvg!nc_n_webp_mw_1"
              }
            ],
            "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201139/bab725040256f30ce3839175d1b9143b/1040g00831nqrubpql800412904ol6ukft0fbuvg!nc_n_webp_prv_1",
            "url_default": "http://sns-webpic-qc.xhscdn.com/202510201139/345d37c53caaf2361e8f926ee065361d/1040g00831nqrubpql800412904ol6ukft0fbuvg!nc_n_webp_mw_1",
            "height": 1920
          },
          "user": {
            "xsec_token": "AB5vgspxlzkNXULj8-NK0eboM-J0kyMh0-j-l35ueGjLg=",
            "user_id": "55c8b15341a2b33872e97a8f",
            "nickname": "一颗菜菜子",
            "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/1040g2jo30v0k6si25c00412904ol6ukf2mvu8mo?imageView2/2/w/120/format/jpg"
          },
          "interact_info": {
            "liked": false,
            "liked_count": "450"
          },
          "xsec_token": "ABsHh2Q8kb7PdjQSr-AoAnataMlewZKcFy4tYcpNj8sXg="
        },
        ... /* omit */
      ]
    }
  }
]
```

---

### 📊️ 笔记信息 (`note_info`)

输出示例
```json
[
  {
    "msg": "成功",
    "data": {
      "items": [
        {
          "id": "68f4e9bf00000000070327cb",
          "model_type": "note",
          "note_card": {
            "note_id": "68f4e9bf00000000070327cb",
            "user": {
              "avatar": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg",
              "xsec_token": "ABDuqUKKa_b99AvNiSrQfLfIDfpSUN625mH_mJI-0Drnc=",
              "user_id": "5b24961811be105dfe1079d4",
              "nickname": "红薯蜀"
            },
            "tag_list": [],
            "at_user_list": [],
            "type": "video",
            "video": {
              "capa": {
                "duration": 24
              },
              "consumer": {
                "origin_video_key": "pre_post/1040g0cg31nqrl9gm52q04a6a5db1guek79ia0so"
              },
              "media": {
                "video_id": 137629073389470700,
                "video": {
                  "biz_name": 110,
                  "biz_id": "281744261481703371",
                  "duration": 25,
                  "md5": "1799b39f4b04a28a61a76351a9c887bb",
                  "hdr_type": 0,
                  "drm_type": 0,
                  "stream_types": [
                    259,
                    114,
                    115
                  ]
                },
                "stream": {
                  "av1": [],
                  "h264": [
                    {
                      "psnr": 0,
                      "weight": 62,
                      "stream_type": 259,
                      "width": 1280,
                      "video_duration": 24383,
                      "default_stream": 0,
                      "fps": 60,
                      "audio_codec": "aac",
                      "quality_type": "HD",
                      "rotate": 0,
                      "stream_desc": "WM_X264_MP4",
                      "height": 720,
                      "audio_duration": 24294,
                      "ssim": 0,
                      "size": 4497904,
                      "volume": 0,
                      "video_codec": "h264",
                      "format": "mp4",
                      "audio_bitrate": 64070,
                      "audio_channels": 2,
                      "master_url": "http://sns-video-ak.xhscdn.com/stream/1/110/259/01e8f4e9be2543f50103700399fcb1a6a8_259.mp4",
                      "backup_urls": [
                        "http://sns-bak-v1.xhscdn.com/stream/1/110/259/01e8f4e9be2543f50103700399fcb1a6a8_259.mp4",
                        "http://sns-bak-v6.xhscdn.com/stream/1/110/259/01e8f4e9be2543f50103700399fcb1a6a8_259.mp4"
                      ],
                      "duration": 24386,
                      "hdr_type": 0,
                      "vmaf": -1,
                      "avg_bitrate": 1475569,
                      "video_bitrate": 1401435
                    }
                  ],
                  "h265": [
                    {
                      "psnr": 46.27899932861328,
                      "size": 3209962,
                      "rotate": 0,
                      "backup_urls": [
                        "http://sns-bak-v1.xhscdn.com/stream/1/110/114/01e8f4e9be2543f50103700199fcb2befa_114.mp4",
                        "http://sns-bak-v6.xhscdn.com/stream/1/110/114/01e8f4e9be2543f50103700199fcb2befa_114.mp4"
                      ],
                      "weight": 62,
                      "stream_type": 114,
                      "format": "mp4",
                      "stream_desc": "X265_MP4_WEB_114",
                      "audio_channels": 2,
                      "master_url": "http://sns-video-ak.xhscdn.com/stream/1/110/114/01e8f4e9be2543f50103700199fcb2befa_114.mp4",
                      "ssim": 0,
                      "width": 1280,
                      "video_bitrate": 915150,
                      "vmaf": -1,
                      "default_stream": 0,
                      "avg_bitrate": 1053050,
                      "audio_bitrate": 127953,
                      "audio_duration": 24294,
                      "height": 720,
                      "duration": 24386,
                      "volume": 0,
                      "fps": 60,
                      "audio_codec": "aac",
                      "hdr_type": 0,
                      "quality_type": "HD",
                      "video_codec": "hevc",
                      "video_duration": 24383
                    },
                    {
                      "ssim": 0,
                      "stream_type": 115,
                      "volume": 0,
                      "fps": 60,
                      "audio_codec": "aac",
                      "audio_channels": 2,
                      "rotate": 0,
                      "backup_urls": [
                        "http://sns-bak-v1.xhscdn.com/stream/1/110/115/01e8f4e9be2543f50103700199fcb37fea_115.mp4",
                        "http://sns-bak-v6.xhscdn.com/stream/1/110/115/01e8f4e9be2543f50103700199fcb37fea_115.mp4"
                      ],
                      "height": 1080,
                      "duration": 24386,
                      "video_bitrate": 1194717,
                      "psnr": 46.65599822998047,
                      "avg_bitrate": 1332586,
                      "weight": 70,
                      "width": 1920,
                      "quality_type": "HD",
                      "format": "mp4",
                      "video_duration": 24383,
                      "audio_bitrate": 127953,
                      "master_url": "http://sns-video-ak.xhscdn.com/stream/1/110/115/01e8f4e9be2543f50103700199fcb37fea_115.mp4",
                      "hdr_type": 0,
                      "size": 4062058,
                      "audio_duration": 24294,
                      "stream_desc": "X265_MP4_WEB_115",
                      "default_stream": 0,
                      "video_codec": "hevc",
                      "vmaf": -1
                    }
                  ],
                  "h266": []
                }
              },
              "image": {
                "thumbnail_fileid": "frame/110/0/01e8f4e9be2543f500100000000199fcb148dd_0.webp"
              }
            },
            "time": 1760881087000,
            "last_update_time": 1760881087000,
            "desc": "",
            "ip_location": "上海",
            "title": "",
            "interact_info": {
              "share_count": "0",
              "followed": false,
              "relation": "none",
              "liked": false,
              "liked_count": "1",
              "collected": false,
              "collected_count": "1",
              "comment_count": "2"
            },
            "image_list": [
              {
                "info_list": [
                  {
                    "image_scene": "WB_PRV",
                    "url": "http://sns-webpic-qc.xhscdn.com/202510201140/5eddf6208cbbb037753d809307fbf1e2/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nd_prv_wgth_webp_3"
                  },
                  {
                    "image_scene": "WB_DFT",
                    "url": "http://sns-webpic-qc.xhscdn.com/202510201140/82a36c28d2e97028eff1011393c2dc76/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nd_dft_wgth_webp_3"
                  }
                ],
                "url_default": "http://sns-webpic-qc.xhscdn.com/202510201140/82a36c28d2e97028eff1011393c2dc76/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nd_dft_wgth_webp_3",
                "stream": {},
                "file_id": "",
                "height": 1080,
                "url": "",
                "trace_id": "",
                "width": 1920,
                "url_pre": "http://sns-webpic-qc.xhscdn.com/202510201140/5eddf6208cbbb037753d809307fbf1e2/110/0/01e8f4e9be2543f500100000000199fcb11d03_0.jpg!nd_prv_wgth_webp_3",
                "live_photo": false
              }
            ],
            "share_info": {
              "un_share": false
            }
          }
        }
      ],
      "current_time": 1760931608022,
      "cursor_score": ""
    },
    "code": 0,
    "success": true
  }
]
```

---

### 📊️ 获取一级评论 (`get_comment`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "comments": [
        {
          "note_id": "68f4e9bf00000000070327cb",
          "at_users": [],
          "user_info": {
            "user_id": "5b24961811be105dfe1079d4",
            "nickname": "红薯蜀",
            "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
            "xsec_token": "ABkDWPormTPcoDBjNZXVXHAtk86Wme_yh0HCUEk5pwmPQ="
          },
          "show_tags": [
            "is_author"
          ],
          "ip_location": "上海",
          "id": "68f599c10000000031002403",
          "content": "和顺打铁花",
          "liked": false,
          "create_time": 1760926146000,
          "status": 0,
          "sub_comments": [
            {
              "user_info": {
                "user_id": "5b24961811be105dfe1079d4",
                "nickname": "红薯蜀",
                "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
                "xsec_token": "ABkDWPormTPcoDBjNZXVXHAtk86Wme_yh0HCUEk5pwmPQ="
              },
              "create_time": 1760926166000,
              "note_id": "68f4e9bf00000000070327cb",
              "status": 0,
              "content": "好看",
              "at_users": [],
              "like_count": "0",
              "id": "68f599d50000000031002503",
              "liked": false,
              "show_tags": [
                "is_author"
              ],
              "ip_location": "上海",
              "target_comment": {
                "id": "68f599c10000000031002403",
                "user_info": {
                  "user_id": "5b24961811be105dfe1079d4",
                  "nickname": "红薯蜀",
                  "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
                  "xsec_token": "ABkDWPormTPcoDBjNZXVXHAtk86Wme_yh0HCUEk5pwmPQ="
                }
              }
            }
          ],
          "sub_comment_cursor": "68f599d50000000031002503",
          "sub_comment_has_more": false,
          "like_count": "0",
          "sub_comment_count": "1"
        },
        ... /* omit */
      ],
      "cursor": "68f599c10000000031002403",
      "has_more": false,
      "time": 1760932874002,
      "xsec_token": "ABkDWPormTPcoDBjNZXVXHAtk86Wme_yh0HCUEk5pwmPQ=",
      "user_id": "5b24961811be105dfe1079d4"
    }
  }
]
```

---

### 📊️ 获取二级评论 (`get_sub_comment`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "user_id": "5b24961811be105dfe1079d4",
      "comments": [
        {
          "status": 0,
          "content": "好看",
          "at_users": [],
          "liked": false,
          "like_count": "0",
          "user_info": {
            "user_id": "5b24961811be105dfe1079d4",
            "nickname": "红薯蜀",
            "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
            "xsec_token": "ABJVAmkGa8T-WYHiLs3T6uKx-ZiAfzL1y0794mJUseSUg="
          },
          "id": "68f599d50000000031002503",
          "note_id": "68f4e9bf00000000070327cb",
          "ip_location": "上海",
          "target_comment": {
            "id": "68f599c10000000031002403",
            "user_info": {
              "user_id": "5b24961811be105dfe1079d4",
              "nickname": "红薯蜀",
              "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
              "xsec_token": "ABJVAmkGa8T-WYHiLs3T6uKx-ZiAfzL1y0794mJUseSUg="
            }
          },
          "show_tags": [
            "is_author"
          ],
          "create_time": 1760926166000
        },
        ... /* omit */
      ],
      "cursor": "68f599d50000000031002503",
      "has_more": false,
      "time": 1760932914363,
      "xsec_token": "ABJVAmkGa8T-WYHiLs3T6uKx-ZiAfzL1y0794mJUseSUg="
    }
  }
]
```

---

### 📊️ 点赞笔记 (`like_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "new_like": true
    }
  }
]
```

---

### 📊️ 取消点赞笔记 (`dislike_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功",
    "data": {
      "like_count": 1
    }
  }
]
```

---

### 📊️ 收藏笔记 (`collect_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功"
  }
]
```

---

### 📊️ 取消收藏笔记 (`uncollect_note`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功"
  }
]
```

---

### 📊️ 发布评论 (`post_comment`)

输出示例
```json
[
  {
    "msg": "成功",
    "data": {
      "comment": {
        "id": "68f5b4b90000000030026de4",
        "note_id": "68f4e9bf00000000070327cb",
        "at_users": [],
        "liked": false,
        "like_count": "0",
        "user_info": {
          "nickname": "红薯蜀",
          "image": "https://sns-avatar-qc.xhscdn.com/avatar/5b249653b46c5d69bc4de7d6.jpg?imageView2/2/w/120/format/jpg",
          "user_id": "5b24961811be105dfe1079d4"
        },
        "status": 2,
        "content": "评论内容示例",
        "show_tags": [
          "is_author"
        ],
        "create_time": 1760933049174,
        "ip_location": "美国"
      },
      "time": 1760933049191,
      "toast": "评论已发布"
    },
    "code": 0,
    "success": true
  }
]
```

---

### 📊️ 删除评论 (`delete_comment`)

输出示例
```json
[
  {
    "code": 0,
    "success": true,
    "msg": "成功"
  }
]
```

---

### 📊️ 点赞评论 (`like_comment`)

输出示例
```json
[
  {
    "success": true,
    "msg": "成功",
    "code": 0
  }
]
```

---

### 📊️ 取消点赞评论 (`dislike_comment`)

输出示例
```json
[
  {
    "msg": "成功",
    "code": 0,
    "success": true
  }
]
```

---

### 📊️ 搜索话题 (`search_topic`)

输出示例
```json
[
  {
    "data": {
      "result": {
        "success": true
      },
      "topic_info_dtos": [
        {
          "name": "榴莲",
          "link": "https://www.xiaohongshu.com/page/topics/5be97dda9ef973000186f749?naviHidden=yes",
          "view_num": 5433525569,
          "type": "official",
          "smart": false,
          "id": "53d32942b4c4d63f967a8d86"
        },
        {
          "smart": false,
          "id": "66457785000000001b03cd29",
          "name": "榴莲爱好者大家可以看下一篇",
          "link": "https://www.xiaohongshu.com/page/topics/66457786bf5a76000171394a?naviHidden=yes",
          "view_num": 0,
          "type": "official"
        },
        ... /* omit */
      ]
    },
    "code": 0,
    "success": true,
    "msg": "成功"
  }
]
```

---

### 📊️ 创建话题 (`create_topic`)

输出示例
```json
[
  {
    "result": 0,
    "success": true,
    "msg": "",
    "data": {
      "topic_infos": [
        {
          "id": "53d32942b4c4d63f967a8d86",
          "name": "榴莲"
        }
      ]
    }
  }
]
```

---

### 📊️ 搜索地点 (`search_location`)

输出示例
```json
[{
  "data": {
    "poi_list": [
      {
        "name": "北京市",
        "poi_id": "B000ABCR66",
        "poi_type": 12,
        "longitude": 116.407387,
        "type": "location",
        "full_address": "北京市东城区东城区",
        "city_name": "北京市",
        "latitude": 39.904179,
        "address": "东城区"
      },
      {
        "latitude": 39.944699,
        "type": "location",
        "name": "北京北站",
        "full_address": "北京市西城区西直门北大街北滨河路1号",
        "poi_id": "B000A833V8",
        "city_name": "北京市",
        "poi_type": 12,
        "longitude": 116.353464,
        "address": "西直门北大街北滨河路1号"
      },
      ... /* omit */
    ]
  },
  "code": 0,
  "success": true,
  "msg": "成功"
}]
```

---

### 📊️ 发布图文笔记 (`publish_note`)

输出示例
```json
[
  {
    "business_bind_results": [],
    "result": 0,
    "success": true,
    "msg": "",
    "data": {
      "score": 10,
      "id": "68f5b6310000000004021340"
    },
    "share_link": "https://www.xiaohongshu.com/discovery/item/68f5b6310000000004021340"
  }
]
```

---

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
