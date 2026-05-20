# HARDWARE_AND_PIN_PLAN.md

## 位置づけ
この文書は、2026-05 時点の LaLaPad Gen2 現行実装に合わせた hardware / pin 構成メモ。
FSR は各 half の `ADS1115` から読む。

## 共有構成

| 項目 | 接続 | 備考 |
| --- | --- | --- |
| MCU | Seeed XIAO BLE / XIAO BLE Plus 系 | 各 half に 1 個 |
| Trackpad sensor | IQS9151 @ `0x56` | 各 half に 1 個 |
| Haptic driver | DRV2605L @ `0x5a` | 各 half に 1 個 |
| FSR ADC | ADS1115 @ `0x48` | 各 half に 1 個 |
| I2C bus | `xiao_i2c` | IQS9151 / DRV2605L / ADS1115 を同居 |
| Trackpad IRQ | `xiao_d6` | `iqs9151@56` の `irq-gpios` |
| FSR read path | `ADS1115 channel 0` | `fsr-channel = <0>` |

## 1 half 分の実配線

以下は、左 half / 右 half どちらにも共通の「1 台分の結線」。
左右差は matrix 配線と split 上の役割だけで、`IQS9151` / `DRV2605L` / `ADS1115` / `FSR` / `LRA` の結線方針は同じ。

### 配線メモ

- `IQS9151 VDD -> XIAO 3V3`
- `IQS9151 GND -> XIAO GND`
- `IQS9151 SDA/SCL -> XIAO D4/D5`
- `IQS9151 RDY/IRQ -> XIAO D6`

- `DRV2605L VIN -> XIAO 3V3`
- `DRV2605L GND -> XIAO GND`
- `DRV2605L SDA/SCL -> XIAO D4/D5`
- `DRV2605L IN/TRIG -> GND`
- `DRV2605L OUT+ / OUT- -> LRA + / -`

- `ADS1115 VDD/GND -> XIAO 3V3/GND`
- `ADS1115 SDA/SCL -> XIAO D4/D5`
- `ADS1115 ADDR -> GND` (`0x48` 前提)
- `ADS1115 A0 -> FSR sense node`
- `ADS1115 A1/A2/A3 -> 未使用`

- `FSR + -> 3V3`
- `FSR - -> A0`
- `A0 node -> 47kΩ 固定抵抗 -> GND`

- `LRA + -> DRV2605L OUT+`
- `LRA - -> DRV2605L OUT-`

補足:
- `FSR` 自体は極性部品ではないので、`+ / -` は便宜上の呼び方
- 現行ファームは `CONFIG_INPUT_IQS9151_FORCE_INVERT_ANALOG=n` なので、押し込みで `A0` 電圧が上がる向きの分圧を前提にしている
- 固定抵抗値は、最後に詰めた前提として `47kΩ` をここに記す

## I2C 周り

| 信号 | XIAO pin | 用途 |
| --- | --- | --- |
| SDA | D4 | IQS9151 / DRV2605L / ADS1115 共用 |
| SCL | D5 | IQS9151 / DRV2605L / ADS1115 共用 |

## Matrix row

`lalapadgen2.dtsi` の `kscan0` では、row は左右共通で以下を使う。

| Row index | pin |
| --- | --- |
| 0 | `xiao_d10` |
| 1 | `xiao_d9` |
| 2 | `xiao_d8` |
| 3 | `xiao_d7` |
| 4 | `gpio1 1` |

## Matrix col

### Left half

| Col order | pin |
| --- | --- |
| 0 | `gpio0 19` |
| 1 | `gpio0 15` |
| 2 | `xiao_d3` |
| 3 | `xiao_d2` |
| 4 | `xiao_d1` |
| 5 | `xiao_d0` |

### Right half

| Col order | pin |
| --- | --- |
| 0 | `xiao_d0` |
| 1 | `xiao_d1` |
| 2 | `xiao_d2` |
| 3 | `xiao_d3` |
| 4 | `gpio0 15` |
| 5 | `gpio0 19` |

右 half は `default_transform` に `col-offset = <6>` を入れて、物理配置上の右側列として扱う。

## Half ごとの trackpad 構成

### Right half
- `trackpad_listener_R`: `okay`
- `trackpad_listener_L`: `okay`
- central 側で local listener を持つ
- 右側の trackpad 入力を直接 pointer / force / caret 処理に流す

### Left half
- `trackpad_split_L`: `okay`
- `trackpad_split_R`: `disabled`
- peripheral 側で左 trackpad 入力を split 越しに central へ送る

## FSR / Haptic の現行前提
- FSR は各 half で `ADS1115` の `channel 0` を読む
- Force 判定は起動時 idle からの絶対差分ベース
- Haptic は `DRV2605L` を各 half に 1 個ずつ持つ
- 通常 tap 用 haptic は無効、Force / Caret 系を優先

## 注意
- 現行構成は `IQS9151` / `ADS1115` / `DRV2605L` / `FSR` / `LRA` を前提にしている
- ピンや wiring を参照するときは、実装側では `config/boards/shields/lalapadgen2/*.overlay` を優先する
