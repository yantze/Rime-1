# Rime Config

----

## Install
macOS Rime 配置地址: ~/Library/Rime

1. 使用 https://github.com/rime/plum 安装词库和新配置

2. Init self config
```
./init_mac.sh
```

## 简要说明
- essay 是八股文词典，应该是直接内部调用的
- opencc 文件夹也是类似，不过需要有些需要指定文件名, `opencc -i A.txt -o B.txt -c t2s.json`
- custom_phrase.txt 可以添加快捷名称，或者强制提升单词排序
- 如果出现很多方块问号，可以安装 HanaMinA 和 HanaMinB

去掉 ipa，因爲直接誒輸入 /a /b 這種就可以直接輸入音標了

### 官方教程
https://github.com/rime/home/wiki/CustomizationGuide


## 同步配置和用户数据
编辑 `installation.yaml` 主要是 installation_id 是 同步的目录名称
点击 Sync user data，可以让配置自动同步到这个目录

目前使用的是，RimeSync/mac 软链到 系统的配置，通过 init_mac.sh 自动实现了
然后同步用户数据，rime 会自动把软链替换为实体文件，所以不能让 rime 同步到 RimeSync/mac ,而应该用另外一个文件夹
然后同步后，自行把内容替换到 RimeSync/mac 中,然后查看 git 的变化内容

所以上面的方法太麻烦，直接在 installation_id 设置好目录，自动同步到本目录，然后同步后，用 git 查看有什么相同的地方
其实这样想就比较清楚了，如果在 /Users/yantze/Library/Rime/installation.yaml 添加了同步路径参数，应该在 installation_id 一致的时候，自动同步 sync_dir 的内容

## 黑魔法
https://placeless.net/blog/my-rime-squirrel-config

在 macOS 10.9 以前，是可以去掉系统默认输入法，只保留一个常用的，比如「鼠须管」，中英文一个键切换。方法就是额外勾选一个比如「越南输入法」，这时候，美式英语的可删除状态就不再是不可点击的灰色，而是可以直接删除的黑色。

但是这个方法在之后的 macOS 不再可用了，后来在一个远古国外 BBS 上发现一个古老的方法，一直适用到现在，就是稍微有一点麻烦，需要需改系统文件，弄得不好，可能会有些小 bug。

一共五个步骤：

- 备份 ~/Library/Preferences/com.apple.HIToolbox.plist
- 将当前活跃输入法选为「英文」输入法
- 终端运行plutil -convert xml1 ~/Library/Preferences/com.apple.HIToolbox.plist
- 用 vim、sublime text 或者其他编辑器，打开com.apple.HIToolbox.plist，删除掉AppleEnabledInputSources键下不需要的输入法dict
- 主要是删掉：com.apple.inputmethod.SCIM.ITABC
- 还有下面这个:
```
<dict>
    <key>InputSourceKind</key>
    <string>Keyboard Layout</string>
    <key>KeyboardLayout ID</key>
    <integer>-2</integer>
    <key>KeyboardLayout Name</key>
    <string>US Extended</string>
</dict>
```

## 事项

## Shortcut
<kbd>Control+Option+`</kbd> 同步配置到当前软件
<kbd>Control+`</kbd>
<kbd>`shift+fn+delete`</kbd> 词频调整:可以删除记忆错误的

### 默认英文
- 关于 ESC 自动切换为英文的方法 https://github.com/rime/squirrel/issues/124

### 每次启动输入法
注意：在squirrel.custom.yaml内搭配好需要开启ascii_mode的应用程序，避免在密码输入框等场景下，中文状态不好上屏，西文状态又是大写的尴尬，尤其是对于跟我一样喜欢改 Shift 而用 CapsLock 键切状态的用户。

### 开启英文联想
- http://tieba.baidu.com/p/5127922981?traceid=

