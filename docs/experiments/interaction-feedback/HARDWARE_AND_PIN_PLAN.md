# 配線メモ

この文書は、 LaLaPad Gen2 haptic / force feedback 実験における既製品パーツ / 配線メモです。
## 使用部品

| 部品       |  個数 | 用途           | 製品 / 型番（※）                                   | リンク                                                                                         | メモ                                                        |
| -------- | --: | ------------ | -------------------------------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| DRV2605L |   2 | LRA 駆動       | Adafruit DRV2605L Haptic Controller Breakout | [Digikey](https://www.digikey.jp/en/products/detail/adafruit-industries-llc/2305/5356831)   | -                                                         |
| ADS1115  |   2 | FSR アナログ読み取り | ADS1115 モジュール                                | [Amazon](https://amzn.asia/d/0gqnW5av)                                                      | デジタル入力ではなくアナログで読んだが、結果論としてはデジタルで割り切って抵抗値調整だけで感度を詰める案もあるかも |
| LRA      |   2 | 触覚フィードバック    | Vybronics `VG1040003D`                       | [Digikey](https://www.digikey.jp/en/products/detail/vybronics-inc/VG1040003D/10285886)      | 今回の用途に適した水平方向LRAがほかにあるかも？                                 |
| FSR      |   2 | 押圧検知         | Interlink Electronics `30-81794`             | [Digikey](https://www.digikey.jp/en/products/detail/interlink-electronics/30-81794/2476468) | もう少し脚の短いもののほうが扱いやすいかも                                     |
| 抵抗       |   2 | FSR 分圧       | -                                            | [Amazon](https://amzn.asia/d/0bPztfgd)                                                      | 現行メモでは FSR 分圧の固定抵抗は `47kΩ`                                |
| ポロンスポンジ  |   - | 機構材          | -                                            | [Amazon](https://amzn.asia/d/05BENvsO)                                                      | -                                                         |
| 細い電線     |   - | 配線           | -                                            | [Amazon](https://amzn.asia/d/0eE2hHJf)                                                      | -                                                         |
| 絶縁テープ    |   - | 絶縁           | -                                            | [Amazon](https://amzn.asia/d/09UQO5TF)                                                      | -                                                         |
| 両面テープ    |   - | 固定           | -                                            | [Amazon](https://amzn.asia/d/009edvbI)                                                      | -                                                         |
（※）製品/型番やリンクあくまで例。同等製品で代替可能のはずです。
## 補足
- これは再現性を保証する BOM ではありません！

## 片側キーボード分の実配線

以下は、左キーボード / 右キーボードどちらにも共通の1 台分の結線です。
### 配線メモ
- `DRV2605L VIN -> XIAO 3V3`
- `DRV2605L GND -> XIAO GND`
- `DRV2605L SDA/SCL -> XIAO D4/D5`
- `DRV2605L IN/TRIG -> 未接続（現行では未使用）`
- `DRV2605L OUT+ / OUT- -> LRA + / -`

- `ADS1115 VDD/GND -> XIAO 3V3/GND`
- `ADS1115 SDA/SCL -> XIAO D4/D5`
- `ADS1115 ADDR -> GND`（`0x48` 前提）
- `ADS1115 A0 -> FSR -`
- `ADS1115 A1/A2/A3 -> 未使用`

- `FSR + -> 3V3`
- `FSR - -> ADS1115 A0`
- `ADS1115 A0 -> 47kΩ 固定抵抗(※) -> GND`

- `LRA + -> DRV2605L OUT+`
- `LRA - -> DRV2605L OUT-`

補足:
- `FSR` 自体は極性部品ではないので、`+ / -` は便宜上の呼び方です
- 現行ファームは押し込みで `A0` 電圧が上がる向きの分圧を前提にしています
  (`CONFIG_INPUT_IQS9151_FORCE_INVERT_ANALOG=n`)
- (※)固定抵抗値は、私の手元環境で詰めた結果として`47kΩ`としていますが、調整可能です。

