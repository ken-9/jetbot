[各ディレクトリの説明]
basic_motion        : 基本的な動作
collison_avoidvance : 衝突回避
object_following    : 物体追跡
road_following      : 道に沿って自律走行
teleoperation       : 付属コントローラの設定関係

[環境]
$ jetson_release
 - NVIDIA Jetson NANO/TX1
   * Jetpack 4.3 [L4T 32.3.1]
   * CUDA GPU architecture 5.3
 - Libraries:
   * CUDA 10.0.326
   * cuDNN 7.6.3.28-1+cuda10.0
   * TensorRT 6.0.1.10-1+cuda10.0
   * Visionworks 1.6.0.500n
   * OpenCV 4.1.1 compiled CUDA: YES
 - Jetson Performance: inactive

 /* その他 */
 - python : 3.6.9
 - torch : 1.10.0
 - torchvision : 0.11.1

[セットアップ参考]
 - https://github.com/NVIDIA-AI-IOT/jetbot/wiki/software-setup
 - https://www.waveshare.com/wiki/JetBot_AI_Kit
 
 2022/08/08