# Autoften

> 对局内角色识别、定位，脚本解释和执行器

### &nbsp;\################################
### \# Alpha Version Development In Progress \# 
### &nbsp;\################################

### 当前进程逻辑关系：

```
###############################################################
#                         screenshot_window_win32             #
#                         ↓                       ↘          #
#               detect_yolo                 ui_positioning    #
#               ↓         ↘             ↙                   #
#  show_image_cv2          update_for_situ                    #
###############################################################
```

### Tips:

- 目前程序主入口在`test.py`
- 通过调整`test.py`中的`startSequence`, 可以调整进程启动与否和顺序
- 由于目前各任务分线程不完全，单独运行可能会阻塞在`pipe.send`，调试时需自行注释相关内容
- 一部分常用配置已经暴露在`config.py`, 持续添加中...
- 目前捕获目标窗口支持被遮挡（不在前台），但不能被最小化