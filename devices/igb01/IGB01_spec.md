# IGB01 仕様

最初のIGB RootデバイスであるIGB01の基本的な仕様について検討する。

IGB01はIGB-DIプロトコルの参照実装デバイスでもある。
Nodeデバイス開発の際は、IGB01との通信が問題なく行えるかどうかが一つの基準となる。

IGB01はプラグインの仕組みにより、シーケンスや内部音源、エフェクト等をカスタマイズ可能である。

IGB01は、他のグルーブボックスや外部音源、外部コントローラを制御するための母艦デバイスとして設計される。

IGB01はライブパフォーマンスのためのデバイスである。
シーケンスを止めることなくあらゆる設定やパラメータの変更が行え、現在の状態を一目で把握できて迷うことなく操作できなくてはならない。

IGB01はユーロラック規格のモジュールである。
横幅は60HPあり、ユーザーは好みのケースや電源を利用することができる。

## 1. ハードウェアインタフェース

![ハードウェアUI](img/IGB01.png)

## 2. データ構造

## 3. 操作フロー

## 4. 機能詳細

### 4-x. IGB-DIデバイス管理

<img src="img/IGB01_Display_device.png" width="30%">

### 4-x. クロック設定

<img src="img/IGB01_Display_clock.png" width="30%">

### 4-x. デバイス選択

<img src="img/IGB01_Display_device_sel.png" width="30%">

### 4-x. パラメータ変更

<img src="img/IGB01_Display_param.png" width="30%">

### 4-x. フレーズ編集

<img src="img/IGB01_Display_phrase.png" width="30%">

### 4-x. 変数設定

<img src="img/IGB01_Display_val.png" width="30%">

### 4-x. マクロ設定

<img src="img/IGB01_Display_macro.png" width="30%">

### 4-x. システム設定

<img src="img/IGB01_Display_system.png" width="30%">
