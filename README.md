# Ikayzo::MojiPlusRomajinizer

A gem for converting between hiragana, katakana, and romaji. The bulk of the logic comes from the [moji](https://github.com/gimite/moji) and [romajinizer](https://github.com/joeellis/romajinizer) gems. This gem combines them and changes the methods name to match the current ruby convention.


## Installation

Add this line to your application's `Gemfile`:

```ruby
gem 'ikayzo-moji_plus_romajinizer'
```

And then execute:

```term
$ bundle
```

Or install it yourself as:

```term
$ gem install ikayzo-moji_plus_romajinizer
```

## Usage

Japanese string conversion and detection methods are added to the `String` class. Call these like you would call any `String` object's method.

### Conversion Methods

* Hiragana/katakana --> romaji conversion (平仮名/片仮名 --> ロ－マ字 変換)

```ruby
"つくえ".romaji #=> "tsukue"
"ツクエ".romaji #=> "tsukue"
```

* Katakana/romaji　--> hiragana conversion (片仮名/ロ－マ字 --> 平仮名 変換)

```ruby
"ツクエ".hiragana #=> "つくえ"
"tsukue".hiragana #=> "つくえ"
```

* Hiragana/romaji --> katakana conversion (平仮名/ロ－マ字 --> 片仮名 変換)

```ruby
"つくえ".katakana #=> "ツクエ"
"tsukue".katakana #=> "ツクエ"
```

* Hiragana --> katakana conversion (平仮名 --> 片仮名 変換)
* Katakana --> hiragana conversion (片仮名 --> 平仮名 変換)

```ruby
"つくえ".hira_to_kata #=> "ツクエ"
"ツクエ".kata_to_hira #=> "つくえ"
```

* Zenkaku --> hankaku conversion (全角 --> 半角 文字種変換)
* Hankaku --> zenkaku conversion (半角 --> 全角 文字種変換)

```ruby
"アロハ".zen_to_han #=> "ｱﾛﾊ"
"Ａｌｏｈａ！".zen_to_han.should == "Aloha!"
"ｱﾛﾊ".han_to_zen #=> "アロハ"
"Aloha!".han_to_zen #=> "Ａｌｏｈａ！" 
```

### Detection Methods

Used to detect Japanese character types (i.e., hiragana, katakana, kanji, full/half-width etc.). There are two groups of detection methods: methods that check the entire string, and methods that checks if the string contains character(s) of a specified character type.

#### Check the entire string

* Is the entire string kana(hiragana/katakana)? (かな/カナ・文字種判定)

```ruby
"アロハ".kana? #=> true
"すし".kana? #=> true
"Aloha".kana? #=> false
"Let's eat すし".kana? #=> false
```

* Is the entire string hiragana? (平仮名・文字種判定)
* Is the entire string katakana? (片仮名・文字種判定)

```ruby
"アロハ".katakana? #=> true
"すし".katakana? #=> false
"アロハ everybody".katakana? #=> false
"アロハ".hiragana? #=> false
"すし".hiragana? #=> true
"Let's eat すし".hiragana? #=> false
```

* Is the entire string kanji? (漢字・文字種判定)

```ruby
"金曜日".kanji? #=> true
"金曜日だよ".kanji? #=> false
"It's Friday, 金曜日".kanji? #=> false
```

* Is the entire string hankaku? (半角・文字種判定)
* Is the entire string zenkaku? (全角・文字種判定)

```ruby
"ｱﾛﾊ".hankaku? #=> true
"アロハ".hankaku? #=> false
"ｱﾛﾊ".zenkaku? #=> false
"アロハ".zenkaku? #=> true
```

* Is the entire string Japanese? (日本語・文字種判定)

```ruby
"アロハ".japanese? #=> true
"Let's eat すし".japanese? #=> false
```

#### Check if the string contains

* Does the string contain kana(hiragana/katakana)? (かな/カナ・文字種判定)

```ruby
"Let's eat すし".contains_kana? #=> true
```

* Does the string contain hiragana? (平仮名・文字種判定)
* Does the string contain katakana? (片仮名・文字種判定)

```ruby
"アロハ everybody".contains_katakana? #=> true
"Let's eat すし".contains_katakana? #=> false
"アロハ everybody".contains_hiragana? #=> false
"Let's eat すし".contains_hiragana? #=> true
```

* Does the string contain kanji? (漢字・文字種判定)

```ruby
"金曜日だよ".contains_kanji? #=> true
"It's Friday, Friday".contains_kanji? #=> false
```

* Does the string contain hankaku? (半角・文字種判定)
* Does the string contain zenkaku? (全角・文字種判定)

```ruby
"ｱﾛﾊ everybody".contains_hankaku? #=> true
"Let's eat すし".contains_hankaku? #=> false
"ｱﾛﾊ everybody".contains_zenkaku? #=> false
"Let's eat すし".contains_zenkaku? #=> true
```

* Does the string contain Japanese? (日本語・文字種判定)

```ruby
"Let's eat すし".contains_japanese? #=> true
"It's Friday, Friday".contains_japanese? #=> false
```



## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request