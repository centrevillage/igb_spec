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

### 2-1. システム設定

IGB01全体に関わる設定。

```mermaid
flowchart TB
  SystemConf -- "1" --o HardwareConf["ハードウェア設定"]
  SystemConf["システム設定"] -- "1" --o IGBDeviceConf["IGBデバイス設定"] -- "N" --o IGBDeviceConfItem["IGBデバイス個別設定"]
  SystemConf -- "1" --o SampleMng["サンプル管理"] -- "N" --o SampleItemConf["個別サンプル設定"]
  SystemConf -- "1" --o AutomationMng["オートメーション管理"] -- "N" --o AutometionItemConff["個別オートメーション設定"]
```

<details>

#### 2-1-1. ハードウェア設定
  
#### 2-1-2. IGBデバイス設定

#### 2-1-3. サンプル管理

#### 2-1-4. オートメーション管理

</details>

### 2-2. ライブセット

ライブセットは一回一回のライブごとに用意する設定。\
ライブセットではトラックやパターンの管理などメインとなるデータを扱う。

```mermaid
flowchart TB
  LiveSetMng["ライブセット管理"] -- "N" --o LiveSet["ライブセット"]
  LiveSet -- "8" --o MacroKnob["マクロノブ"]
  LiveSet -- "8" --o RibbonController["リボンコントローラ"]
  LiveSet -- "1" --o KeyboardBtn["キーボードボタン"]
  LiveSet -- "N" --o DefaultParameter["パラメータ初期値"]
  LiveSet -- "8" --o Track["トラック"]
  Track -- "N" --o Device["デバイス"]
  Device -- "N" --o Parameter["デバイスパラメータ"]
  Track -- "N" --o ParameterSet["パラメータセット"]
  Track -- "N" --o Pattern["パターン"]
  Pattern -- "0..16" --o Sequence["シーケンス"]
  LiveSet -- "N" --o Variable["変数パラメータ"]
  Variable -. "update" .-> Parameter
  LiveSet -- "N" --o Phrase["フレーズ"]
  subgraph ParameterChange["パラメータ変更"]
    Sequence
    MacroKnob
    RibbonController
    KeyboardBtn
    ParameterSet
    DefaultParameter
  end
  ParameterChange -. "update" .-> Parameter
  ParameterChange -. "update" .-> Variable
  Phrase -. "references" .-> ParameterSet
  Phrase -. "references" .-> Pattern
  Track -- "1" --o ClockDivMult["クロック設定"] 
  subgraph CommonInfo["共通情報"]
    BpmConf["BPM設定"]
    MixerConf["Mixer設定"]
    ScaleQuantizer["スケールクオンタイズ設定"]
  end
  LiveSet -- "1" --o CommonInfo
  ParameterChange -. "update" .-> CommonInfo
  ParameterChange -. "update" .-> ClockDivMult
```

<details>

#### 2-2-x. ライブセット

#### 2-2-x. BPM設定

#### 2-2-x. Mixer設定

#### 2-2-x. スケールクオンタイズ設定

#### 2-2-x. トラック

#### 2-2-x. デバイス

#### 2-2-x. デバイスパラメータ

#### 2-2-x. パラメータセット 

#### 2-2-x. クロック設定

#### 2-2-x. 変数パラメータ

#### 2-2-x. パターン

#### 2-2-x. シーケンス

#### 2-2-x. フレーズ
  
</details>

### 2-3. デバイス

デバイスはモジュラーシンセにおける1モジュールに相当する単位である。\
IGB-DIプロトコルによって通信する外部IGBデバイスと内部デバイスに大きく分かれる。

```mermaid
flowchart TB
  Device["デバイス"] -. "implement" .-> IGBDevice["IGBデバイス"]
  Device -. "implement" .-> InternalSynthDevice["内部音源デバイス"]
  Device -. "implement" .-> InternalFxDevice["内部エフェクトデバイス"]
  Device -. "implement" .-> InternalSamplerDevice["内部サンプラーデバイス"]
  Device -. "implement" .-> InternalLFODevice["内部LFOデバイス"]
  Device -. "implement" .-> InternalEnvDevice["内部エンベロープデバイス"]
  Device -. "implement" .-> InternalAutomationDevice["内部オートメーションデバイス"]
```

<details>

#### 2-3-x. IGBデバイス

#### 2-3-x. 内部音源デバイス

#### 2-3-x. 内部エフェクトデバイス

#### 2-3-x. 内部サンプラーデバイス

#### 2-3-x. 内部LFOデバイス

#### 2-3-x. 内部エンベロープデバイス

#### 2-3-x. 内部オートメーションデバイス

</details>

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
