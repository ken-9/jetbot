# 各ファイル・ディレクトリ説明
```
notebook_tutorial/ : サンプルプログラム群が入っているディレクトリ
original/ : ライントレース+物体検知のプログラムが入っているディレクトリ
confirm_pytorch : pytorchとcudaのバージョンを確認するためのプログラム
readme.md : 本リポジトリ全体に関わる説明(Jetbotのセットアップ，ディレクトリ構造など)を記述したドキュメント
```
※各ディレクトリ以下のファイル群について説明したテキストも要参照．(`notebook_tutorial/explain.txt`や`original/explain.txt`)

# jetbotセットアップ
基本的には本家であるNVIDIAのwikiを参考．(https://github.com/NVIDIA-AI-IOT/jetbot/wiki/software-setup)
1. microSDにOSイメージを焼く
> https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Software-Setup#step-1---flash-jetbot-image-onto-sd-card

2. Jetson Nano にmicroSDを入れて電源ON
> https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Software-Setup#step-2---boot-jetson-nano

3. Jetson Nano をネットワークに繋ぐ
> https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Software-Setup#step-3---connect-jetbot-to-wifi

4. JetbotのOLEDにIPアドレスが表示されるので，PCのブラウザからアクセスする 
> https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Software-Setup#step-4---connect-to-jetbot-from-web-browser  
※PCは同ネットワークに接続しておく事．

5. Jetbotに必要なソフトウェアをJetbotのリポジトリからインストールし，セットアップする
> https://github.com/NVIDIA-AI-IOT/jetbot/wiki/Software-Setup#step-5---install-latest-software-optional

> **Warning**  
> waveshareのJetbotは電力関係部分がNVIDIAと違うので，waveshareのリポジトリからgit clone する事．(以下参照)
> ```
> $ git clone https://github.com/NVIDIA-AI-IOT/jetbot  # NVIDIAのリポジトリからgit clone
> ↓ 
> $ git clone https://github.com/waveshare/jetbot  # waveshareのリポジトリからgit clone
> ```

waveshare jetbotのwiki
やり方が若干違うがこっちもあり
> https://www.waveshare.com/wiki/JetBot_AI_Kit

# 使用時環境
```PowerShell
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
```

その他
```PowerShell
 - python : 2.7.17 / 3.6.9
 - torch : 1.3.0
 - torchvision : 0.4.0a0+d31eafa
 - tensorflow : '1.14.0'
 - tensorRT : 6.0.1.10
```

# その他ソフトウェアのセットアップ手順
## darknetの導入とyolov4-tinyのインストール
物体検知機能を使う場合はdarknetの導入が必要(特にoriginal/rf_and_od.ipynb など)  
手順は以下．  
1.フレームワークであるdarknetを入れる
```
$ git clone https://github.com/AlexeyAB/darknet
```


2. Makefileの中を修正する
```
$ cd darknet
$ nano Makefile
```
```
# darknet/Makefile
GPU=1  
CUDNN=1  
CUDNN_HALF=0  # jetson nanoの場合は0でok 
OPENCV=1  
libso=1

# 64行目あたり
NVCC=/usr/local/cuda/bin/nvcc
```


3. yolov4-tinyを入れる
```
wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v4_pre/yolov4-tiny.weights
```


4.  コンパイルする(-j5 : 4コアあるため5スレッドで分散ビルド)
```
$ make -j5
```
makeをやり直す場合はmake clean してからmake


5. 正常に動作するか確認
```
$ ./darknet detect cfg/yolov4-tiny.cfg yolov4-tiny.weights data/dog.jpg
```

## torch2rtのインストール
ライントレースの学習済みモデルをTensorRTに変換するプログラム('/notebook_tutorial/nvidia/road_following/live_demo_build_trt.ipynb')を使用する場合はtorch2rtのインストールが必要．
以下に従ってインストールする．
> https://github.com/NVIDIA-AI-IOT/torch2trt#setup  
※不足してるパッケージがあれば適宜インストールする．
