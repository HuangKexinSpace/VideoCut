# VideoCut
A script for semi-automatic cutting of required video clips

# 项目描述

这个项目是一个自动化转录文本并切割需要的视频片段的脚本,大致逻辑如下：

* 首先对视频进行切割和预处理（这里是对45min的视频切割成五段，并把每段的画质进行压缩），为了适应openai-whisper的窗口大小（不超过25mb，时长也不能太长，最好不超过20分钟）
* 然后调用whisper将视频转录成文本，保存在.csv文件中
* 作者可以一边看视频，对.csv文件中的句子进行标注
* 最后，程序将打上标签的部分输出

# 操作指南

* 首先将项目中所有的.mp4文件，.json文件，.csv文件通通删掉
* 将需要处理的视频放入主目录，命名为input.mp4
* 执行AudioHandleScript.ipynb脚本，这时会生成part1-5和prepart1-5这些.mp4文件，其中pre版是未压缩画质的，无pre是压缩过画质的；还会生产五个json文件和一个text.csv文件，.csv文件就是完整视频的文本转录了。
* 打开CutScript脚本，执行第一步，生成textmodify.csv文件，这时！（先不要点第二步），可以打开原视频，一边分析原视频，一边在.csv文件中进行标注。
  * 对于需要输出单句的视频，将check值改为1；
  * 对于需要输出连续多句合并的视频，将check值和ifcombine值都改为1
* 执行第二步，所有标注的文件会以id命名，生成在result文件夹中（这里的id会比csv中的id大1，不知道为啥，也不想改了）

# 备注

* 我的测试视频为约200mb，45min，如果视频太大太长可能会报错（openai的窗口限制）
* 运行时需要在当前环境中设置openai的key：
  setx OPENAI_API_KEY  你的key
  设置好后可以重启电脑看看能行不
