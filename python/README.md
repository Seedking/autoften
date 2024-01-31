<div align="center">
<img src="assets/docs/logo.png" alt="logo" width="256" height="auto" />

# Autoften

> 对局内角色识别、定位，脚本解释和执行器

谐音“自动凹分”，最终可以使用的脚本执行器客户端。

其通过YOLO作为关卡内识别角色和敌人的主要手段，辅以传统OpenCV和位置记忆、惯性算法等措施，实现在局内大部分时间、甚至是角色被特效遮挡时，可以做到识别和定位各个角色和需要攻击的敌人的位置，可以在任何需要的时间点逐帧级精确释放技能和进行其他操作。

此外，定义了一套BA局内条件判断和操作的脚本语法，以及与此语法对应的脚本解释器。用户可以将自己摸出的轴编写至此脚本语法上，或使用其他Sensei分享的脚本，即可全自动执行。脚本会按脚本规则反复执行，直到暴击/安定等达到期望状态。享受从凹分大牢中解脱的快感吧！

注：此部分作为整个项目的最终产物，如果用户希望，可以是完全离线运行的。

---

### &nbsp;\################################
### \# Alpha Version Development In Progress \# 
### &nbsp;\################################

---

</div>

### 当前进程逻辑关系：

```
###############################################################
#                         screenshot_window_win32             #
#                         ↓                       ↘          #
#               detect_yolo                 ui_positioning    #
#               ↓         ↘             ↙                   #
#  show_image_cv2            script_exec                      #
###############################################################
```

### Q&A

1. 这是什么？

> Autoften是一款总力战自动脚本，设计为只要有给定操作轴的文字描述和对应角色即可自动反复尝试，直到对局表现符合预期为止。
作为BAAS Project（Blue Archive Auto Sensei）的一部分，Autoften被设计为可以处理任意自动处理不了、手动又过于麻烦的局内操作。
与Project的其他部分一起，目标是最终会构成7x24小时接管BA所有日常活动的全自动自律脚本。

2. 局内自动操作是如何实现的？

> YOLO是关卡内识别角色和敌人的主要手段，此外会通过传统OpenCV和位置记忆、惯性算法等措施覆盖一些极端情况。

3. 目前支持在什么环境和配置下运行？

> - 由于仍处于早期开发阶段，因此只对指定的开发环境做保障。未来我们会逐步添加对各种平台和环境的支持。对带来的不便十分抱歉！
> - 某些不受支持的配置有可能可以正常运行，但不做保证。此外，也欢迎各位加入开发，扩充和优化支持配置的范围。
> - 实体机需求：
>
>   1. NVIDIA显卡（安装CUDA）
>   2. Windows系统（目前只在win11经过测试）
>   3. 大于1080p屏幕且开启1.5倍系统缩放(可通过调整配置适配)
>
> - 虚拟机需求：
>       
>   1. 目前限定MuMu12
>   2. 分辨率设置为2560*1440（640DPI）
>   3. 最高帧率限定为60
>   4. 保持MuMu默认窗口大小，不要缩放或全屏（可通过调整配置适配）
>   5. 可以用其他窗口遮挡住MuMu，但不要移到屏幕以外，不要最小化
>   6. (建议)开启后台保活

4. 为什么性能占用这么大？/为什么窗口不能被最小化？

> - Autoften仍处于早期开发阶段，优化持续进行中...
> - 相比其他游戏的脚本/BAAS Project的其他部分，Autoften由于需要局内进行精细操作，对时间间隙的要求较大。
然而ADB目前没有比较成熟的低延迟高速连续截图方案，也没有持续稳定的录屏逐帧转录方案，因此目前的屏幕捕获方案依赖win32完成。
尽管win32API可以做到窗口被遮挡时正常截图，但win32 GUI实现并不渲染屏幕范围外的窗口和最小化的窗口，因此仍需避免最小化窗口，可以将其放在其他窗口后面，除部分性能占用外基本不影响前台正常使用。

5. 我可以参与并帮助BAAS开发吗？

> 当前BAAS Project处于开发早期，仍十分缺乏人手，非常需要你的帮助！只要你符合以下任意一点，欢迎积极联系BAAS的任意一位成员加入开发：
> - 热心开源和Blue Archive，愿意为帮助各位老师更轻松地享受Blue Archive的方方面面；
> - 总 &nbsp;&nbsp; 力 &nbsp;&nbsp; 战 &nbsp;&nbsp; 高 &nbsp;&nbsp; 手
> - 有YOLO训练、预测、部署、性能调优的经验
> - 熟悉编译原理，有简单编译器/解释器的设计思路或经验
> - 有逆向工程经验/熟悉游戏拆包提取模型
> - 有模型渲染、修改、相关3D软件使用经验等
> - 希望向BAAS提供新的想法、创意或需求
> - (更多待补充...)
> 
> 此外，我们欢迎且积极寻求其他相关项目/DB/Wiki/社区的合作，如果你有兴趣，欢迎联系我们！

6. 为什么选择了先开发这个，而不是其他内容，比如日常脚本？

> - 目前有不少替代方案，或单纯使用操作录制、按键精灵等，一定程度上可以满足需求。
> - 另外，BA的日常每天也就五分钟，此外考虑到总力战才是最大的负担和导致玩家退坑的主因，日常脚本的优先级不是最高的。
> - 后续开发至时机成熟时，我们可能会逐步添加日常脚本，以及其他更多有趣的功能。 


### Tips:

- 目前程序主入口在`test.py`
- 通过调整`test.py`中的`startSequence`, 可以调整进程启动与否和顺序
- 由于目前各任务分线程不完全，单独运行可能会阻塞在`pipe.send`，调试时需自行注释相关内容
- 一部分常用配置已经暴露在`config.py`/`config.yaml`, 持续添加中...
- 目前捕获目标窗口支持被遮挡（不在前台），但不能被最小化