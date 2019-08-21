
## 概要

rails4.2.11 では、`simple_format` を利用するとデフォルトではほとんどのタグとアトリビュートが削除される。
最初から `rails4.2.11` を利用していれば最初から表示されないことがわかっているので、以下の対応できる。

https://api.rubyonrails.org/v4.2.11/classes/ActionView/Helpers/SanitizeHelper.html

```
# In config/application.rb
config.action_view.sanitized_allowed_tags = ['strong', 'em', 'a']
config.action_view.sanitized_allowed_attributes = ['href', 'title']
```

本来は上記の設定をRails4.2.1 でも行うべきであったが、`rails-html-sanitizer`（※ rails4.2.1 に依存するバージョン）がデフォルトで用意されていた許可タグ・アトリビュートで事なきを得ていた。
rails のバージョンアップに伴い、`config`の修正を行っていなかったため、タグ・アトリビュートがサニタイズされてしまった。



```slim
# syntax with slim
- content = "<a href="https://example.com" target="_blank" style="text-align:center;text-docration:none;"><span style="color: red">https://example.com</span></a>
= simple_format content
```

#### 出力結果

```
<p><a href="https://example.com"><span>https://example.com</span></a></p>
```

