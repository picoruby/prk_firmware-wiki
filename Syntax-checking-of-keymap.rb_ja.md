もしあなたの `keymap.rb` でキーボードが動かないなら、`keymap.rb` にミスタイプがあるかもしれません。

Rubyの文法チェッカーが役立つでしょう。

コマンドラインで以下のように実行します（`-c` オプションを付けるのを忘れずに）

```shell
ruby -c path/to/keymap.rb
```

もし上記のコマンドで `Syntax OK` が表示されたなら、あなたの `keymap.rb` には基本的にRuby文法上の間違いはありません。
（あらゆる間違いがないことを意味するものではありません）

あるいは、上記のコマンドは修正すべき文法エラーを報告するかもしれません。

もし `ruby` コマンドがないなら、[https://www.ruby-lang.org/ja/documentation/installation/](https://www.ruby-lang.org/ja/documentation/installation/) に従ってインストールしてください。