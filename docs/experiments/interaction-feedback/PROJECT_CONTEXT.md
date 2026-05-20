# PROJECT_CONTEXT.md

## 概要
この案件は、LaLaPad Gen2 の trackpad に対して force interaction、haptic feedback、caret 操作を追加する改造の記録である。

## 現行の source of truth
- `HARDWARE_AND_PIN_PLAN.md`
- `CURRENT_FORCE_BEHAVIOR_SPEC.md`
- `config/boards/shields/lalapadgen2/*.overlay`
- `config/boards/shields/lalapadgen2/*.conf`
- `drivers/input/iqs9151.c`

## 現在の実装要点
- 各 half に `IQS9151`, `DRV2605L`, `ADS1115` を持つ
- FSR は `ADS1115 channel 0` から読む
- Force は有効
- Caret は有効。ただし IQS9151 driver 内のローカル caret ではなく、中央側の `zmk,input-processor-force-caret` で扱う
- Precision は無効。関連コードは残るが実効していない
- 通常 tap haptic は無効
- startup haptic は有効

## split の前提
- 右 half は central
- 左 half は peripheral
- 左 trackpad は split input として central に送る
- 右 trackpad は central 側で local listener として処理する

## ハードウェアの現行前提
- I2C は D4 / D5
- IQS9151 は `0x56`
- DRV2605L は `0x5a`
- ADS1115 は `0x48`
- FSR は `ADS1115 channel 0`

## 最近の実装修正として重要な点
- IQS9151 driver は FSR と haptic を統合しており、企画初期の単純な digital force button とは別物になっている
- Caret は左右共有状態で扱う中央処理に移っている
- 入力抜け対策として、IQS9151 の重い処理を専用 work queue に逃がしている

## 更新ルール
- 新しい事実を追加するときは、まず現役文書を更新する
- 現行仕様の説明を優先し、古い検討メモに引きずられないようにする
