If your `keymap.rb` doesn't make your keyboard run, you likely have mistyped in the `keymap.rb`.

Syntax checker of Ruby will help you.

On the command line (Be sure to insert `-c` option):

```shell
ruby -c path/to/keymap.rb
```

If the command above prints `Syntax OK`, your `keymap.rb` basically doesn't have any mistake in terms of Ruby syntax
(Note that it doesn't mean there are no mistakes of any kind).

Otherwise, that command reports a syntax error that you have to fix.

If you don't have a `ruby` command, install one according to [https://www.ruby-lang.org/en/documentation/installation/](https://www.ruby-lang.org/en/documentation/installation/)
