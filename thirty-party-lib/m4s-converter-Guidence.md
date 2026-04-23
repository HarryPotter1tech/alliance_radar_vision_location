# m4s-converter-Guidence
## m4s-converter is a tool that transforms m4s files into mp4 files. 
### Usage
1. if you are in this repository, you can run the command below to convert m4s files to mp4 files:
```bash
cd thirty-party-lib/m4s-converter
./m4s-converter -c /path/to/m4s/files 
```
### then you will find the mp4 files in the file's output directory.

## Example:
```bash
cd thirty-party-lib/m4s-converter
./m4s-converter -c /media/harryh/0CB60F5B0CB60F5B/Algorithm/RADAR-DataSet/30334454884    
```
### Results:
```bash
2026-04-15_19:27:19 [WARN ] 使用MP4Box进行音视频合成
2026-04-15_19:27:19 [INFO ] 选择的 BiliBili 缓存目录为: /media/harryh/0CB60F5B0CB60F5B/Algorithm/RADAR-DataSet/30334454884
=====================================================
           使用本程序需遵守以下使用条款
   仅转换本人通过哔哩哔哩官方客户端合法缓存的视频，
  且转换结果严格用于个人备份，绝不传播、分享或商用。
=====================================================
  按任意键同意并继续使用，关闭窗口则拒绝并退出程序！
=====================================================

2026-04-15_19:27:20 [INFO ] 用户同意使用，程序继续执行
2026-04-15_19:27:20 [INFO ] 查找缓存目录下可转换的文件...
2026-04-15_19:27:20 [INFO ] 已将m4s转换为音视频文件: /30334454884-1-30116-video.mp4
2026-04-15_19:27:20 [INFO ] 已将m4s转换为音视频文件: /30334454884-1-30280-audio.mp3
2026-04-15_19:27:22 [INFO ] 已合成视频文件:/media/harryh/0CB60F5B0CB60F5B/Algorithm/RADAR-DataSet/30334454884/output/[RoboMaster·2025]东部区域赛-南京理工大学-雷达站录像-9-___隔夜薯条___/[RoboMaster·2025]东部区域赛-南京理工大学-雷达站录像-9.mp4
2026-04-15_19:27:22 [INFO ] ===========================================
2026-04-15_19:27:22 [INFO ] # 输出目录:
/media/harryh/0CB60F5B0CB60F5B/Algorithm/RADAR-DataSet/30334454884/output
2026-04-15_19:27:22 [INFO ] # 合成的文件:
[RoboMaster·2025]东部区域赛-南京理工大学-雷达站录像-9-___隔夜薯条___/[RoboMaster·2025]东部区域赛-南京理工大学-雷达站录像-9.mp4
2026-04-15_19:27:22 [INFO ] ===========================================
2026-04-15_19:27:22 [INFO ] 已完成合成任务，耗时: 2秒
按任意键退出程序
```