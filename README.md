# EMUZ80-Z8002
電脳伝説さん(@vintagechips)のEMUZ80が出力するZ80 CPU信号をメザニンボードで組み替え、Z8002を動作させることができます。  
LH8002とPIC18F47Q83の組み合わせで動作確認しています。

![MEZ80LED](https://github.com/satoshiokue/EMUZ80-Z8002/blob/main/MEZZ8002.jpeg)
 
ソースコードは電脳伝説さんのEMUZ80用main.cを元に改変してGPLライセンスに基づいて公開するものです。

LH8002PとPIC18F47Q83の組み合わせで動作確認しています。  

動作確認済みCPU  
Zilog Z0800206PSC  
SHARP LH8002P  
AMD Z8002ADC  

このソースコードは電脳伝説さんのmain.cを元に改変してGPLライセンスに基づいて公開するものです。

## メザニンボード
https://github.com/satoshiokue/MEZZ8002  

## ファームウェア
emuz80_z8002.cをEMUZ80で配布されているフォルダemuz80.X下のmain.cと置き換えて使用してください。  
ターゲットのPICを適切に変更してビルドしてください。  

## アドレスマップ
```
Memory
ROM   0x0000 - 0x7FFF 16Kbytes
RAM   0x8000 - 0x9FFF 8Kbytes (0x8FFF 4Kbytes:PIC18F47Q43)
      0xA000 - 0xBFFF GHOST
      0xC000 - 0xDFFF GHOST
      0xE000 - 0xFFFF GHOST

I/O
UART  0x0007   Data REGISTER
      0x0005   Control REGISTER
```

## PICプログラムの書き込み
EMUZ80技術資料8ページにしたがってPICに適合するemuz80_z8002_Qxx.hexファイルを書き込んでください。  

またはArduino UNOを用いてPICを書き込みます。  
https://github.com/satoshiokue/Arduino-PIC-Programmer

PIC18F47Q43用ファームウェア：  
emuz80_z8002_Q43.hex  

パワーオンでUniversal Monitorが起動します。  
mコマンドでMONZ8kモニタがコールドスタートします。  
CALL 0B00でUniversal Monitorがコールドスタートします。

```
MEZ8002 1.000MHz

Universal Monitor Z8000
] m

MONZ8k Ver.1.0 SBCZ8002 Edition
Zilog Z8000 Rush Monitor

[8000]call 0b00

Universal Monitor Z8000
]
```
  
PIC18F47Q83/PIC18F47Q84用ファームウェア：  
emuz80_z8002_Q8x.hex  

パワーオンでUniversal Monitorが起動します。  
mコマンドでMONZ8kモニタがコールドスタートします。  
CALL 4600でUniversal Monitorがコールドスタートします。  
MONZ8kモニタからbasicで豊四季タイニーBASIC(float版)が起動します。
```
MEZ8002 1.000MHz

Universal Monitor Z8000
] m

MONZ8k Ver.1.0 r3 SBCZ8002 Edition
Zilog Z8000 Rush Monitor + TOYOSHIKI Tiny BASIC

[8000]call 4600

Universal Monitor Z8000
] m

MONZ8k Ver.1.0 r3 SBCZ8002 Edition
Zilog Z8000 Rush Monitor + TOYOSHIKI Tiny BASIC

[8000]basic
TOYOSHIKI TINY BASIC
SBCZ8002 ROM r3 float EDITION

OK
```
MITライセンスのUniversal MonitorをEMUZ80-Z8002用に改変してhexファイル化しました。  
Universal Monitor  
https://electrelic.com/electrelic/node/1317

@junk_suga 氏
SBCZ8002改で豊四季タイニーBASICを動かす  
https://web.archive.org/web/20230119153223/https://www.ne.jp/asahi/suga/junkyard/sbc/sbcz8002/
「ROM化その3 変数のfloat化」を

## Z8002プログラムの改編
バイナリデータをテキストデータ化してファームウェアの配列rom[]に格納するとZ8002で実行できます。

テキスト変換例
```
xxd -i -c16 foo.bin > foo.txt
```

## 参考）EMUZ80
EUMZ80はZ80CPUとPIC18F47Q43のDIP40ピンIC2つで構成されるシンプルなコンピュータです。

![EMUZ80](https://github.com/satoshiokue/EMUZ80-6502/blob/main/imgs/IMG_Z80.jpeg)

電脳伝説 - EMUZ80が完成  
https://vintagechips.wordpress.com/2022/03/05/emuz80_reference  

EMUZ80専用プリント基板 - オレンジピコショップ  
https://store.shopping.yahoo.co.jp/orangepicoshop/pico-a-051.html
