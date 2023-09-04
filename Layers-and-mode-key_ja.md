## 有効なバージョン

|機能|バージョン|
|----|----|
|レイヤー機能|0.9.0+|
|[デフォルトレイヤーの変更](#デフォルトレイヤーの変更)|0.9.15+|

## 説明

レイヤーは自作キーボードにおいて最も重要な機能の一つだと思います。
PRK は `Keyboard#define_mode_key` メソッドでレイヤー機能を実装しています。

モードキーのふるまいは少しトリッキーなので、このページを注意深く読んでください。

## 使用方法

```ruby
puts "An example for meishi2"

kbd = Keyboard.new

kbd.init_pins(
  [ 6, 7 ],   # row0, row1
  [ 28, 27 ]  # col0, col1
)

#                          key1       key2  key3  key4
kbd.add_layer :default, %i(SPC_LAYER1 KC_A  KC_B  CTR_ENT_LAYER2) # :default レイヤーは最初に追加する必要がある
kbd.add_layer :layer1,  %i(SPC_LAYER1 KC_1  KC_2  CTR_ENT_LAYER2)
kbd.add_layer :layer2,  %i(SPC_LAYER1 KC_F1 KC_F2 CTR_ENT_LAYER2)

kbd.define_mode_key :SPC_LAYER1,    [ :KC_SPACE,            :layer1, 200, 200 ]
kbd.define_mode_key :CTR_ENT_LAYER2,[ %i(KC_RCTL KC_ENTER), :layer2, 300, 150 ]
#                                     ^^^^^^^^^^^^^^^^^^^^  ^^^^^^^  ^^^  ^^^
#                                     (1)                   (2)      (3)  (4)
# (1): 押したときに呼び出される、以下のいずれか
#      キーコードのシンボル または 複数キーコードの配列 または Proc
# (2): キーコードのシンボル（モディファイアのみ） または 保持されるレイヤーのシンボル
#      または Proc
# (3): リリース時間の閾値（ミリ秒）
#      もしこの時間内にキーを離したら、(1)キーが一度呼び出される
# (4): 再押下時間の閾値（ミリ秒）
#      (3)の状態にあるとき、この時間内にキーをまた押した場合、(1)キーが押されたままになる

kbd.start!
```

- key1 を押す（そして200ミリ秒以内に離す）と、ホストPCに "スペース" が送信される
- key1 を押したまま key2 を押すと、"1" が送信される
- key4 を押したまま key3 を押すと、"F2" が送信される
- key4 を押して300ミリ秒以内に離して150ミリ秒以内にまた押して押したままにすると、"CTRL+ENTER" が送信され続ける

## デフォルトレイヤーの変更

もしあなたがWindowsとmacOSの両方をKVMスイッチで使おうとしているとしたら、OSによってGUIとCTRLが入れ替わるキーが欲しいかもしれません。
`Keyboard#define_mode_key`を上手く使うと、デフォルトレイヤーを切り替えることができます。

```ruby
kbd = Keyboard.new

kbd.init_pins([6, 7, 8], [28, 27]) # Depending on PCB

kbd.add_layer :default_mac, %i[ TO_WIN RAISE KC_LGUI KC_X KC_C KC_V ]
kbd.add_layer :default_win, %i[ TO_MAC RAISE KC_LCTL KC_X KC_C KC_V ]
kbd.add_layer :raise,       %i[ KC_NO  RAISE KC_1    KC_2 KC_3 KC_4 ]

kbd.define_mode_key :RAISE,  [ :KC_SPACE, :raise, 200, 200 ]
kbd.define_mode_key :TO_WIN, [ Proc.new { kbd.default_layer = :default_win }, nil, 200, nil]
kbd.define_mode_key :TO_MAC, [ Proc.new { kbd.default_layer = :default_mac }, nil, 200, nil]

kbd.start!
```

## `Keyboard#define_mode_key` のProc

[未定]

## 制限

- "key4" を押したままのときに "key1" の押下を除外することはできません。逆もまた同様です。
- 他にも制限はあります。自分自身で見つけてください。

## よくある間違い

### デフォルトレイヤー名

```ruby
kbd.add_layer :layer1, %i(SPC_LAYER2 KC_1  KC_2  KC_3)
kbd.add_layer :layer2, %i(SPC_LAYER2 KC_A  KC_B  KC_C)
```

最初に追加されるレイヤーの名称は `:default` でなければいけません。そのため、上記のコードは適切に機能しません。

### `:XXXXXXX` は透過キーコードとして機能しない

```ruby
kbd.add_layer :default, %i(SPC_LAYER1 KC_A  KC_B  KC_C)
kbd.add_layer :layer1,  %i(XXXXXXX    KC_1  KC_2  KC_3)
kbd.define_mode_key :SPC_LAYER1, [ :KC_SPACE, :layer1, 200, 200 ]
```

このキーマップは、 `:SPC_LAYER1` キーを押したままのとき、:default と :layer1 の間を高速に行ったり来たりします。  
`:SPC_LAYER1` キーを押したままにしたときの効果は、レイヤーが `:layer1` に切り替わった後に即座に消えます。いま押したままにしているキーは、副作用が何もない `:XXXXXXX` だからです。そしてレイヤーはすでに `:default` に戻っています。
