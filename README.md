# Xbox One Kinect センサー       #訂正版　2026/11/10

## 1. 概要
Xbox One Kinect センサーは、Microsoftが開発したセンサーである。
カラー画像や赤外線画像に加え、物体の奥行きを表す深度データを取得できる。
また、Kinect for Windows SDK 2.0を利用することで、人の身体や関節の位置を追跡できる。
SDKとは、センサーの機能を利用するプログラムを開発するための道具や機能をまとめたものである。

今回は、使用例として、Kinectセンサーを床に向けて配置し、深度画像の中央に置いた物体の高さを測定する。
物体を置いていない状態の床の深度を記録し、物体を置いた後の深度との差から高さを求める。

### 1.1 主な機能
#### カラー画像の取得

物体の色や形をカラー画像として取得できる。
撮影した範囲に何があるかを画像で確認できる。

#### 深度データの取得

各画素に対応する物体までの距離を、ミリメートル単位のデータとして取得できる。
この情報を利用して、物体の奥行きや位置を調べることができる。

#### 赤外線画像の取得

赤外線を利用した画像を取得できる。
赤外線画像と深度画像では、同じ位置の画素が対応している。

#### 人体の追跡

SDKを利用して、最大6人の身体を同時に追跡できる。
追跡情報には、関節の位置や向き、手の状態などが含まれる。

## 2. 使用する機材
PC、Kinect本体、PC接続アダプター、ケーブル、電源。

## 3. センサーの外観・ケーブル類について

### 3.1 センサーの外観

Xbox One Kinect センサー本体の箱の写真を以下に示す。

![Kinectセンサー本体](<images/XBOX One Kinect センサー 箱.jpg>)

箱の中身を以下に示す。kinect本体と接続されているケーブルが収納されている。

![Kinectセンサー本体](<images/XBOX One Kinect 中身.jpg>)

### 3.2 ケーブル類

PCと接続するために必要なケーブル類の箱を以下に示す。

![Kinectセンサー本体](<images/XBOX One Kinect PC アダプター 箱.jpg>)

箱の中身を以下に示す。中身としては、ACアダプター、PC接続用アダプター（接続ハブ）、USB 3.0ケーブル、電源コードが収納されている。

![Kinectセンサー本体](<images/XBOX One Kinect PC アダプター 中身.jpg>)

## 4. 接続・設定方法

### 4.1 SDKのインストール

KinectをPCで使用するために、Kinect for Windows SDK 2.0をインストールする。

1. 以下のMicrosoft公式サイトを開き、「Download」をクリックする。

   [Kinect for Windows SDK 2.0](https://www.microsoft.com/en-us/download/details.aspx?id=44561)

2. KinectのUSBケーブルをPCから外し、
   ダウンロードした「KinectSDK-v2.0_1409-Setup.exe」を実行する。

3. ライセンス条項を確認して同意のチェックを入れ、
   「Install」をクリックする。

![SDKのインストール画面](<images/ソフトウェア.png>)

4. 「Setup Complete」と表示されたら、「Close」をクリックする。

![SDKのインストール完了画面](<images/Setup_Complete.png>)

### 4.2 配線・PCへの接続

SDKのインストール後、次の順番で接続する。

1. Kinect本体のケーブルをPC接続用アダプター（接続ハブ）につなぐ。
2. ACアダプターを接続ハブにつなぎ、電源コードでコンセントに接続する。
3. USB 3.0ケーブルで、接続ハブとPCのUSB 3.0ポートをつなぐ。
4. ドライバーの設定が完了するまで待つ。

実際の配線を以下に示す。

![KinectとPCの配線](<images/実際の配線.jpg>)

### 4.3 開発環境の準備

サンプルプログラムを改造するため、今回はVisual Studio Community 2026を使用した。

1. 以下の公式サイトからVisual Studio Communityをダウンロードする。

   [Visual Studio ダウンロードページ](https://visualstudio.microsoft.com/ja/downloads/)

2. インストール時に「.NET デスクトップ開発」を選択する。
3. インストール完了後、Visual Studioを起動する。

### 4.4 サンプルコードの準備

1. Windowsのスタートメニューから「SDK Browser v2.0」を起動する。
2. 「Depth Basics-WPF」の「Install」を選び、サンプルコードを保存する。
3. Visual Studioで、保存先の「DepthBasics-WPF.sln」を開く。
4. 対象フレームワークの警告が表示された場合は、
   「対象を.NET Framework 4.8に更新する」を選択する。
5. Ctrl＋Shift＋Bでビルドし、正常に終了したことを確認する。

今回はWindows 11で動作を確認した。
サンプルの実行方法と結果は、次の「5. 動作確認」に記載する。


## 5. 動作確認

### 5.1 サンプルの実行

SDK Browser v2.0で「Depth Basics-WPF」の「Run」を選択し、
深度画像が表示されることを確認した。

### 5.2 高さ測定の方法

サンプルを改造し、画面中央の物体の高さを自動表示した。

高さ（推定）＝ 床の深度 − 物体上面の深度

1. Kinectを床に向けて固定し、Visual StudioからF5キーで実行する。
2. 箱がない状態でアプリを選択し、Bキーで床を記録する。
3. 箱の上面を中央の白い十字に合わせ、高さを確認する。

### 5.3 測定結果

箱1個の高さは75mmである。各状態の配置と測定画面を以下に示す。

#### 箱なし

![箱なしの配置](<images/箱なし.jpg>)

![箱なしの測定画面](<images/box_0.png>)

#### 箱1個

![箱1個の配置](<images/箱1個.jpg>)

![箱1個の測定画面](<images/box_1.png>)

#### 箱2個

![箱2個の配置](<images/箱2個.jpg>)

![箱2個の測定画面](<images/box_2.png>)

| 状態 | 実際の高さ | 表示値 | 差（表示値 − 実際の高さ） |
|---|---:|---:|---:|
| 箱なし | 0mm | 2mm | ＋2mm |
| 箱1個 | 75mm | 70mm | −5mm |
| 箱2個 | 150mm | 161mm | ＋11mm |

実際の高さとの差はあるが、箱を重ねることによる高さの変化を確認できた。
上記は各スクリーンショット撮影時の値であり、測定値には変動があった。

## 6. 注意点・困ったこと
- 深度の差を高さとして扱うため、Kinectは平らな床に対して真下に向ける。
- 測定するのは中央の1点なので、箱の上面を白い十字に合わせる。
- 深度画像が暗く見えても、測定できている場合があるため、数値も確認する。


## 7. 参考資料
参考にした資料のタイトル、URL、閲覧日を記載する。

https://github.com/Kinect/Docs/blob/master/Kinect4Windows2.0/k4w2/Programming_Guide/Kinect_API_Overview.md?utm_source=chatgpt.com

(https://visualstudio.microsoft.com/ja/downloads/)

(https://www.microsoft.com/en-us/download/details.aspx?id=44561)
