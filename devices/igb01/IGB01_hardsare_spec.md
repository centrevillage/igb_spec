# IGB01ハードウェア構成

```mermaid
flowchart LR
  MainCore["Main Core: STM32MP157"]
  MainRAM["RAM: DDR3 512MB"]
  MainFlash["SDMMC"]
  FRAM["FRAM(Realtime Backup): 256KB"]
  subgraph CoreBoard["Core Board"]
    MainCore --o MainRAM
    MainCore -- "program load" --o MainFlash
    MainCore -. "option" .-o FRAM
  end
  CoreBoard -- "SAI" --> Codec["CODEC: AK4619"] -- "Audio" --> AudioIO(["Audio IO: SND/RTN/EXT/Main"])
  CoreBoard -- "SPI" --> CtrlMCU1["Ctrl MCU #1 (Touch/Encoder): STM32F303"] -- "read" --> Touchh(["Touch"])
  CtrlMCU1 -- "read" --> ParamEncoder(["PARAM Encoder"])
  CoreBoard -- "SPI" --> CtrlMCU2["Ctrl MCU #2 (Analog/Button): STM32G431"] -- "read" --> AnalogSensors(["Analog Sensors: POT/SLIDER/RIBBON"])
  CtrlMCU2 -- "read" --> Buttons(["Buttons"])
  CoreBoard -- "SPI" --> DAC["DAC(for CV): DAC8165(14bit, 4ch)"] -- "DC Out" --> CVOut(["CV1-4 Out"])
  CoreBoard -- "SPI" --> ADC["ADC(for CV): MCP33151(14bit, 1ch) x 2"] -- "DC Out" --> CVIn(["CV1-2 In"])
  CoreBoard -- "I2C" --> LEDDriver["LED Driver: IS31FL3731"] --> LEDs(["LEDs"])
  CoreBoard -- "SPI" --> LCD(("LCD: Waveshare 1.28inch_LCD_Module(Round)"))
  CoreBoard -- "USB" --> USBDevice(["USB Device"])
  CoreBoard -- "USB" --> USBHost(["USB Host"])
  CoreBoard -- "SDMMC" --> ExtSDMMC(["SDMMC Slot"])
  CoreBoard -- "UART" --> IGBPrev(["IGB Prev"])
  CoreBoard -- "UART" --> IGBNext(["IGB Next"])
  CoreBoard -- "UART" --> MIDI(["MIDI"])
  CoreBoard -- "GPIO" --> ClockOut(["Clock Out"])
  CoreBoard -- "GPIO" --> ResetOut(["Reset Out"])
  subgraph IOCon["IO"]
    AudioIO
    CVOut
    CVIn
    ClockOut
    ResetOut
    USBDevice
    USBHost
    ExtSDMMC
    IGBPrev
    IGBNext
    MIDI
    ClockOut
    ResetOut
  end
```

## Core Board

Core Boardは別基板となっており交換可能。

STM32MP157をメインコアとし、512MBのRAMの外付けDDRメモリを持つ。\
プログラムは外部SDMMCカードよりロードする。

プロトタイプ開発時は `Olimex STMP157-SOM-517-EXT` を利用する。

STM32MP1のベアメタルでの開発については、4msのソースコードが参考にできる。

[stm32mp1-baremetal](https://github.com/4ms/stm32mp1-baremetal)

[metamodule](https://github.com/4ms/metamodule)

2025年1月現在では `STM32MP2` シリーズも利用可能であるが、まずは開発環境の整えやすいMP1で開発を進め、将来的にはMP2や他のCoreで置き換えることを想定。

