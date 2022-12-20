# ass-db

csv db repo for lite-web-studio(a-soul instance)

## Brach

- main: 修改变更版本管理，发布之前的测试用分支，外部修改 Pull Request 请提交到这里
- release: prod 环境用分支，不接受外部的 Pull Request

## Clean CDN
请在更新对应分支后点击下方链接更新cdn信息来反应最新状态到录播站。如果没有更新的话，请点击对应的文件对象单独更新。
- [Stag ALL Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@main)
  - [Stag DB Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@main/song_database.csv)
  - [Stag Playlist Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@main/playlist_database.csv)
  - [Stag LRC Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@main/lrc_database.csv)
- [Prod Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@release)
  - [Prod DB Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@release/song_database.csv)
  - [Prod Playlist Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@release/playlist_database.csv)
  - [Prod LRC Sync](https://purge.jsdelivr.net/gh/chobitsnerv/ass-db@release/lrc_database.csv)

## CSV File Reference

**注意**：各属性前后请勿留存空格
| Field Name | Type | Mandatory | Description |
| :--- | :--- | :---: | :--- |
| id | String | Yes | 格式:**A000000**。唯一 ID。A 之后请使用 CSV 自动递增赋值。页面内控件显示状态等有关，和歌曲资源访问无关。 |
| 日期 | Date | Yes | 格式:**YYYY.MM.DD**。请不要省略单数字月日前面的 0，保持 01，02 这样的数值。歌曲采集的录播所在日期。和歌曲名共通决定歌曲资源寻址。 |
| 录播来源 | String | No | 用来提供 B 站相关录播传送门。 |
| 录播片段编号 | Number | No | B 站录播的分 P 号。配合**录播来源**和**起始时间点**以及**结束时间点**可以定位跳转 B 站相关录播节点。 |
| 起始时间点 | Number | Yes | B 站分 P 起始时间点。分 P 未收录是使用 0 代替。分 P 存在时格式**00:00:00.000** |
| 结束时间点 | Number | Yes | B 站分 P 起始时间点。**起始时间点**为 0 时，请使用歌曲 ms 数记录总歌曲时长。分 P 存在时格式**00:00:00.000** |
| 文件名 | String | | 存在时优先被使用来匹配资源，不填写时请使用**歌名**，**版本号**和**版本备注**来匹配资源文件 |
| 文件类型 | String | Yes | 文件的扩展名 |
| 歌名 | String | | 歌曲名称。最终和**版本号**以及**版本备注**会按照：日期 歌名【版本号 版本备注】格式来匹配 |
| 版本号 | String | | 歌曲版本号，跟随演唱者升级版本，共同演唱时取最大版本号同步至每一位演唱者作为后续的起步版本号。 |
| 版本备注 | String | | 歌曲内容的备注描述，如改词，钢琴伴奏等 |
| 中文歌名 | String | No | 歌名之后显示在括号里的内容，可以用作歌曲的备注添加用。 |
| 原曲艺术家 | String | No | 原曲作者信息。 |
| 演唱者 | String | Yes | 收录曲演唱者。多人存在的情况下请使用英文""和,来记载多人合唱信息，如："AA,BB"。 |
| 演唱状态 | String | Yes | 是否整首演唱或者片段。 |
| 语言 | String | Yes | 歌曲演唱语言。 |
| 备注 | String | No | 关于歌曲较长的备注信息，比如剪辑版本的备注等。 |
| 参考路灯 man | String | No | 歌曲切片提供者信息 |
| 有没有音频 | Boolean | Yes | TRUE 或者 FALSE。用来标注是否歌曲切片已被收录入库并处在可以播放的状态。 |
| 切片源 | String | No | 切片来自的源文件传送门。 |
| 有没有第二版本 | Boolean | Yes | TRUE 或者 FALSE。用来标注是否歌曲切片存在优化版本或单曲版本已被收录入库处在可以播放的状态。 |
| 第二版文件类型 | String | Yes | 次版本文件的扩展名设置 |

## Song File Naming Convention

为方便音源入库，本文档简要说明文件名命名规范

请切片 Man 在完成切片后参照 csv 命名，如果 csv 有误，请在切片组内反馈。

- 文件名格式为：**时间+空格+参与者代号+空格+歌曲名称【版本号+空格+版本备注】**

  > 如：2022.01.05 C 芒种【2.0 预录】

- 歌曲名称请注意英文大小写和简体繁体字，如《素敌だね》不等于《素敵だね》
- 参与成员代号有：ABCDEFL
- 版本备注有：预录 合唱 改词 单曲 视频，等等。

```
例1（单人演唱）
2022.03.02 E 牛奶面包.m4a
时间：2022.03.02
参与者：E，Eileen，代表乃琳
歌曲名称：牛奶面包

例2（2-3人合作）
2021.09.21 CD 青城山下白素贞.m4a
参与者：CD，"珈乐,嘉然"，按字母顺序排序
2022.02.04 ADE 吉祥三宝.m4a
参与者：ADE，"向晚,嘉然,乃琳"，按字母顺序排序
注：合作歌曲包括所有参与者，如《花海》由向晚伴奏，乃琳演唱，标为AE
《繁花》由贝拉伴舞，乃琳演唱，标为BE

例3（4-5人合作，F）
2022.02.03 F 一千零一个愿望.m4a
参与成员代号：F，4-5位成员参与

例4（联动，L）
2021.04.17 L Hopeful Dreamer【合唱版】.mp3
参与者："嘉然,中国绊爱"
2022.02.03 L 除夕【团曲】.mp3
参与者："A-SOUL,音阙诗听"

例5（版本号 版本备注）
2021.10.28 DE 私奔到月球【2.0】.m4a
2022.01.14 E Sweet Counter【单曲】.m4a
2022.01.05 C 芒种【2.0 预录】.m4a
```
