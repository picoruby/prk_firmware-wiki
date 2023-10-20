まずはじめに、以下のドキュメントの "3.2.1. From the desktop" (10ページ目)を読んで、Raspberry Pi Pico にUF2ファイルをインストールする方法を覚えてください。

[https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf)

Sparkfun Pro Micro RP2040を利用する場合、以下のページも役立ちます。

[https://learn.sparkfun.com/tutorials/pro-micro-rp2040-hookup-guide](https://learn.sparkfun.com/tutorials/pro-micro-rp2040-hookup-guide)

その他、利用可能なマイコンボードやキーボードは [[Microcontroller-boards-and-Keyboards]] を参照してください。

## やってみよう！

- [Releases](https://github.com/picoruby/prk_firmware/releases) から最新のリリースバイナリをダウンロードします。

- ダウンロードしたファイルを展開すると、`prk_firmware-0.9.0-20210910-xxxxxxxx.uf2` のようなファイルができるはずです。

- RP2040をBOOTSELモードでマウントし、uf2ファイルを `RPI-RP2` ドライブにドラッグアンドドロップします。

  ![](images/drag_and_drop_1.png)

- 数秒後に `RPI-RP2` ドライブが消え、かわりに `PRK DRIVE` ドライブが自動的にマウントされます。

- あなたの `keymap.rb` を `PRK DRIVE` ドライブにドラッグアンドドロップします。

  ![](images/drag_and_drop_2.png)

PRK Firmware は自動的に `keymap.rb` をリロードします。楽しんで！

### 知っておきたいポイント

- `keymap.rb` をドラッグアンドドロップしても、`PRK DRIVE` ドライブはアンマウントされません。
- `keymap.rb` のリロードには、`keymap.rb` の内容や回路次第で5～7秒程度かかります。
- 新しい `keymap.rb` が正常にリロードできた場合でも、何も起きていないように見えることがあります（特にRGBLEDを持たないキーボードの場合）。しかし、 `keymap.rb` に問題がなければ新しい設定が適用されているはずです。
- もし`keymap.rb` が機能しない場合、[[Debug print]] ページが役立つかもしれません。

### `keymap.rb` の編集

- 2回目以降は、`PRK DRIVE` ドライブにある既存の `keymap.rb` を上書きします。
- `PRK DRIVE` ドライブの `keymap.rb` を直接編集することもできますが、予期せぬトラブルを防ぐため、PCのディスクに保存した `keymap.rb` を編集し、それを `PRK DRIVE` ドライブにドラッグアンドドロップすることをお勧めします。

### PRK Firmware のアップグレード

PRK Firmware の新しいuf2ファイルをインストールしたいときは、RP2040をBOOTSELモードで再起動する必要があります。

詳しくは [[BOOTSEL mode of RP2040]] を参照してください。
