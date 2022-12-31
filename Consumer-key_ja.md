## 有効なバージョン

0.9.17+

## 使用方法

`keymap.rb` の最初に

```ruby
require "consumer_key"
```

と書きます。

## Keycodes

| シンボル | エイリアス | 説明 |
|----|----|----|
| :KC_SYSTEM_POWER       | :KC_PWR  | システム電源オフ       |
| :KC_SYSTEM_SLEEP       | :KC_SLEP | システムスリープ       |
| :KC_SYSTEM_WAKE        | :KC_WAKE | システムスリープ解除   |
| :KC_MEDIA_FAST_FORWARD | :KC_MFFD | 次の曲へ               |
| :KC_MEDIA_REWIND       | :KC_MRWD | 前の曲へ               |
| :KC_MEDIA_NEXT_TRACK   | :KC_MNXT | 次の曲へ               |
| :KC_MEDIA_PREV_TRACK   | :KC_MPRV | 前の曲へ               |
| :KC_MEDIA_STOP         | :KC_MSTP | 再生停止               |
| :KC_MEDIA_EJECT        | :KC_EJCT | イジェクト             |
| :KC_MEDIA_PLAY_PAUSE   | :KC_MPLY | 再生/一時停止          |
| :KC_MEDIA_SELECT       | :KC_MSEL | Media Player 起動      |
| :KC_AUDIO_MUTE         | :KC_MUTE | ミュート               |
| :KC_AUDIO_VOL_UP       | :KC_VOLU | 音量アップ             |
| :KC_AUDIO_VOL_DOWN     | :KC_VOLD | 音量ダウン             |
| :KC_BRIGHTNESS_UP      | :KC_BRIU | 画面の明るさアップ     |
| :KC_BRIGHTNESS_DOWN    | :KC_BRID | 画面の明るさダウン     |
| :KC_MAIL               |          | メール起動             |
| :KC_CALCULATOR         | :KC_CALC | 電卓起動               |
| :KC_MY_COMPUTER        | :KC_MYCM | マイコンピュータを開く |
| :KC_WWW_SEARCH         | :KC_WSCH | ブラウザ検索           |
| :KC_WWW_HOME           | :KC_WHOM | ブラウザホーム画面     |
| :KC_WWW_BACK           | :KC_WBAK | ブラウザ戻る           |
| :KC_WWW_FORWARD        | :KC_WFWD | ブラウザ進む           |
| :KC_WWW_STOP           | :KC_WSTP | ブラウザ読み込み中止   |
| :KC_WWW_REFRESH        | :KC_WREF | ブラウザ再読み込み     |
| :KC_WWW_FAVORITES      | :KC_WFAV | ブラウザお気に入り     |

