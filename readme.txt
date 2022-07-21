[各ディレクトリの説明]
basic_motion        : 基本的な動作
collison_avoidvance : 衝突回避
object_following    : 物体追跡
road_following      : 道に沿って自律走行
teleoperation       : 付属コントローラの設定関係

[環境]
$ jetson_release
 - NVIDIA Jetson NANO/TX1
   * Jetpack UNKNOWN [L4T 32.7.2]  // unknownとなっているが4.6.2相当
   * CUDA GPU architecture 5.3
 - Libraries:
   * CUDA 10.2.300
   * cuDNN 8.2.1.32-1+cuda10.2
   * TensorRT 8.2.1.8-1+cuda10.2
   * Visionworks 1.6.0.501
   * OpenCV 4.1.1 compiled CUDA: YES
 - Jetson Performance: inactive

 /* その他 */
 - python : 3.6.9
 - torch : 1.10.0
 - torchvision : 0.11.1

[セットアップ参考]
 - https://github.com/NVIDIA-AI-IOT/jetbot/wiki/software-setup
 - https://www.waveshare.com/wiki/JetBot_AI_Kit