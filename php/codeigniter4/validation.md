# Validation

## 使いまわすな？

### 事象

```php
class Unchi extends BaseController
{
	public function index()
	{
		if($this->validate(['unchi' => 'required',])){
		.
		.
		.
		}
	}
}

-----別ファイル-----------
class BuriUnchi extends BaseController
{
	public function index()
	{
		if($this->validate(['unchibu' => 'required',])){
		.
		.
		.
		}
	}
}

```

こんな感じでいろいろ書いて行くと挙動がおかしくなる。

具体的に遭遇したケースは

featureテスト時に

別クラスのバリデーションルールが追加された状態

かつ

validationはパラメタガン無視(パラメタは取得できていた)する事象。

### 解決策

```php
public function __construct()
{
    $validation =  \Config\Services::validation();
    $validation->reset();
}
public function index()
{

	if($this->validate(['buri' => 'required',])){
	.
	.
	.
	}
}

```
reset挟んだらうまくいった。

正直codeigniter4のvalidation全く理解してない。

公式以外でもっとわかりやすいドキュメントとかないのだろうか。
