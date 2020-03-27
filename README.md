# auto-arknights-python
[![standard-readme compliant](https://img.shields.io/badge/readme%20style-standard-brightgreen.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)

基于opencv-python的明日方舟多功能自动化脚本

# 目录
* 项目介绍
    * 原理
    * 功能列表
* 安装指南
* 配置文件
    * 配置方法
    * 配置文件示例
* 使用示例
* 目录结构
* 版本更新

# 项目介绍
auto-arknights-python是基于 [opencv-python][https://github.com/opencv/opencv] 以及 [Android Debug Bridge (adb)][https://developer.android.com/studio/command-line/adb] 的明日方舟自动化脚本。
理论上支持任何分辨率，支持adb调试的安卓手机或安卓模拟器。

## 原理

1. 使用 `adb shell` 和 `adb pull` 命令获取游戏截图，暂时保存在screenshots文件夹中

2. 根据不同的状态，使用opencv的模板匹配(Template Matching)功能寻找点击坐标

   > 由于模板匹配需要相同分辨率匹配，所以首先将获取到的截图高度等比例压缩至720px

3. 使用 `adb shell input` 命令模拟用户输入

## 功能列表

* 计划任务

    * 根据用户排班表自动安排基建排班
    
    * 被用户顶掉后定时再次上线
    
    * 自动清理智（可指定副本以及次数）
    
    * 自动购买信用商店物品（可自行设置购买优先级）
    
    * 自动领取每天4AM的线索
    
    * 自动赠送线索（指定/随机目标，全部赠送/重复赠送）
    
    * 自动完成每日任务
    
    * 自动3次公招，识别最优tag组合
    
* 手动任务

    （指手动运行上面的计划任务）
    
   > 此脚本并不能智能识别基建干员工作情况，需要用户自行提供排班表，脚本只能严格按照排班表执行。
   
# 安装指南 

1. 安装 [Python与pip](python.org) 并添加至环境变量

2. 安装项目依赖 `opencv-python` 以及 `numpy`

       pip install cv2 numpy
       
3. 安装 [Android Debug Bridge (adb)](https://developer.android.com/studio/command-line/adb) 并添加至系统环境变量

    > 当你在shell或终端中输入 `adb` 后发现被英文刷屏了就说明你安装成功了
    
# 配置文件

## 配置方法

* `infrastructure_layout.json` : 基建布局

    配置指南 : 打开游戏后进入基建，点击左上角的“进驻总览”，并按照从上到下的顺序将设施的名字依次按照`"设施名" : "序号"`的方式填入json文件中
    
    `序号` : 代表你这个设施是从上到下的第几个
    
    > 如果有多个同样的设施，应在设施名后加上序号区分，如：`制造站1`,`制造站2`
    
* `infrastructure_schedule.json` : 干员排班表

    json文件中的键值对组成如下
    
        "hh:mm" : {
            "设施1" : ["干员1","干员2"],
        }
        
    > 注意：
    > 1. 每天第一个时刻对应的值中应该包含所有的设施以及排班情况的键值对
    > 2. 之后的时刻对应的值中，可以只包含需要人员变动的设施及其对应的完整值班干员名单
    > 3. 由于此脚本是根据一天的时刻进行换班，所以编写排班表的时候请根据24小时循环的原则编写
    > 4. 编写排班表时请避免让干员出现注意力涣散的情况，否则会使立绘变红影响模板识别
    > 5. 编写排班表时请避开3:30~4:05的时间段，否则可能执行到一半弹出“信息已更新”
    > 6.`infrastructure_schedule.json`与`infrastructure_layout.json`中填写的设施名称严格对应
    
## 配置文件示例


# 使用示例

# 目录结构

# 版本更新
