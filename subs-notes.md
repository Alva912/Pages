## 打轴的一些基础

### 工具

推荐[Aegisub](https://www.bilibili.com/video/BV1oK411T7kL)或[Premiere](https://www.bilibili.com/video/BV1dy4y1j714)（因为 PR2021 新版加入 CC 字幕功能已经比较方便了，而且可以同时编辑视频例如加片头片尾、打码之类

主要过程就是

    - 新建字幕
    - 用aegisub打开字幕文件/将字幕拖入PR时间轴
    - 添加字幕块
    - 输入文字

具体使用基础比如快捷键之类请参考上面链接的基础教学视频

### 主要原则

- 说话时间：**跟随说话者的气口**，即吸气时开始字幕，停顿/呼气时结束字幕。停顿过多时，在不影响语义的情况下合并为完整的一句话作为一条字幕

  ```
  我觉得（停顿）就是（停顿）它是一首很好听的歌
  I think it is a great song
  ```

- 阅读时间：在不影响下一条字幕的前提下，一条字幕结尾处应**拖长 300ms 左右**，给肉眼多一些阅读字幕的时间

- 标点符号：尽量**不使用**全角（汉字）标点符号，中文大部分情况是逗号和句号 这些都要去掉，英文一句话分两条字幕时中间也不会用逗号，更详细的标点符号使用规则请参考[Netflix 官方的字幕规范文档](https://partnerhelp.netflixstudios.com/hc/ja/articles/215767517-Japanese-Timed-Text-Style-Guide)，[英文字幕](https://partnerhelp.netflixstudios.com/hc/en-us/articles/217350977-English-Timed-Text-Style-Guide)以及[日文字幕](https://partnerhelp.netflixstudios.com/hc/ja/articles/215767517-Japanese-Timed-Text-Style-Guide)的规范也有

- 双人字幕：用单横杠`-`作为各自开头，如

  - 多语字幕同时出现所以两人的话要放在同一行

  ```
  -你好我是XXX -你好
  - Hello I'm XXX  - Hello
  ```

  - 只出现一种语言的字幕所以可以换行

  ```
  - Hello I'm XXX (换行符\N)
  - Hello
  ```

- 多人字幕：首选是做成内嵌字幕，字幕位置**跟随对应说话者**的位置。如做成外挂 CC 字幕/Lower-Third 下部三分之一字幕，则保留主说话者的字幕，其余人合并/忽略

## 以下为一些进阶要求

### [对帧轴](https://www.bilibili.com/video/BV1oK411T7kL?p=6)

- 适用于原视频物料自带中文字幕、并且我们并不会把原中文字幕去掉的时候
- 顾名思义，即字幕开始和结束的时间点跟原视频上的字幕完全一致，帧对帧级别的

### [防闪轴](https://www.bilibili.com/video/BV1oK411T7kL?p=7)

- 视频画面元素出现过短，肉眼看上去的感觉就是画面上什么东西闪了一下
- 一般字幕前后间隔时间最短**300~500ms**
- 镜头画面切换时结束上一句字幕
- 对帧轴也是为了防止出现画面闪烁，比如中文字幕还有 1~2 帧的时候日英字幕已经结束这样的情况
  ```
  中日英（几秒）👉中（2帧）👉中日英
  ```
- 如出现原物料制作者本身的失误，比如一句话已经到结尾并且镜头切换到下一个画面，然而字幕还是在新镜头画面停留 1~2 帧，此时应考虑字幕长短及后面有无字幕而做取舍

## 关于机器打轴

### 准备工具

- 剪映 Pro
- json 转 srt 格式转换器
  - [在线转换器](https://pansong291.gitee.io/web/html/tool/JianyingPro.html)
  - [剪映字幕导入 PR 的插件](https://www.bilibili.com/video/BV1qX4y1c7kB)
  - [转换脚本（粗糙）](https://github.com/fofen/jianying-json2srt)
    - 需要安装 node 👉 用来运行 JavaScript 文件
    - 脚本作者很久未更新，下载后需要手动编辑 js 文件来更新剪映项目文件路径

### 步骤

1. 打开剪映 pro，点击【开始创作】

   - 这个步骤会生成剪映项目，默认名字为当前日期时间，比如 `202112210930` 意思是 `2021年12月21日9点30分`

2. 导入视频，点击【文本】👉【智能字幕】👉【识别字幕-开始识别】👉 等待剪映 pro 运行完成

   - 这个步骤会生成机听字幕文件`draft_content.json`，储存于`C:\\Users\\AppData\\Local\\JianyingPro\\User Data\\Projects\\com.lvediteor.draft\\`
   - 此时可以关闭剪映，但是不可以删除剪映项目，否则会丢失上面的字幕文件

3. 选择【在线转换器】或者【PR 插件】则跳过以下步骤

4. 运行`cmd`打开电脑命令行窗口

   - 右键【开始】👉【运行】👉【cmd】👉【开始】
   - Mac 电脑系统稍有不同，直接搜 cmd 或者 shell

5. 输入命令`node --version`确定已安装好 node

6. 输入命令`node json2srt.js 202112210930`
   - `202112210930`👉 记得改成自己的目标剪映项目名称
   - 这个步骤会在相同目录生成`draft_content.srt`字幕文件，有可能不能直接作为字幕文件打开，需要原地传送一下
     - 用文本编辑器打开后复制整个文本
     - 粘贴进一个新建的文本文件里`.txt`
     - 更改新文本文件的扩展名为`.srt`
7. 最后这个`.srt`文件就是我们想要的东西了 👉 机器打轴生成的字幕文件

   - 最后记得删除剪映项目，保持电脑整洁干净

8. 打开你常用的打轴工具检查笨笨机器听错的地方

### 小结

- 可以注意到这个方法的步骤比较繁琐，如果只是短视频，还是建议手动打轴，反而比较快
- 机器打轴也比较粗糙，是剪映根据音频中的人声来提取计算生成的，所以遇到人声不清晰的视频也建议不要用这个方法
- 那么这个方法到底适合什么样的视频呢？
  - 时间冗长
  - 人声较清晰
  - 也就是单人/少人直播和采访
