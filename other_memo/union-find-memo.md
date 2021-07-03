# Union-Find

どういうことができるかは理解ができた。

しかし、処理はまだ追えてない気がするので、拙作の(コピペも混じってる)~~汚い~~コードを何行ずつかにわけて

私向けに解説していこうと思う。

## Union-Find木

```

// 引用元
// http://sntea.hatenablog.com/entry/2017/06/07/091246
// 上記を少しだけ修正した。
struct UnionFind {
    par: Vec<usize>,
		rank: Vec<usize>,
}

impl UnionFind {
    fn new(n: usize) -> UnionFind {
        let mut vec = vec![0;n];
        for i in 0..n {
            vec[i] = i;
        }
        UnionFind {
            par : vec,
            rank : vec![0;n],
        }
    }

    fn find(&mut self, x: usize) -> usize {
        if x == self.par[x] {
            x
        }else{
		    // ここらへんを修正
            let res = self.find(self.par[x]);
            self.par[x] = res;
            res
        }
    }

    fn same(&mut self, a: usize, b: usize) -> bool {
        self.find(a) == self.find(b)
    }

    fn unite(&mut self, a: usize, b: usize){
        let apar = self.find(a);
        let bpar = self.find(b);
		// ここも修正
		if apar == bpar{
			return
		}
		// ここらへんも修正
        if self.rank[apar] < self.rank[bpar] {
            self.par[apar] = bpar;
        }else{
            self.par[bpar] = apar;
            if self.rank[apar] == self.rank[bpar] {
                self.rank[apar] += 1;
            }
        }
    }
	// これは追加
	fn debug(&mut self){
		println!("par:{:?}, rank:{:?}", self.par, self.rank);
	}
}

```

### new

```

fn new(n: usize) -> UnionFind {
    let mut vec = vec![0;n];
    for i in 0..n {
        vec[i] = i;
    }
    UnionFind {
        par : vec,
        rank : vec![0;n],
    }
}

```

Union-Findの大本はRustでいうところのVecやら配列をつかうっぽい。

本でも引用元でもそうなってた。

ここ、最初はなんでvec[i] = iしてるのかわからんかった(私の知能はそんなレベル)。

これは私の理解力よりも、変数の説明をみてなかったのが原因だった。

parは親、rankは木の深さなのだ。それ以上でもそれ以下でもない。

つまり、iの親はpar[i]ということだ。~~進次郎かな？~~

この処理では、初期はiの親はiということにしている。

また、深さもへったくれもないので、当然0である。

### find

再帰を賞賛する声(ツイート)はよく目にする。私も自分で書いたものに対してはそうだった。

しかし気がついた。私の場合だけかもしれんが、

アルゴリズムをまったく理解してないものを再帰で実装されると途端にわからんくなる。

それループでも一緒じゃね？

いや、ループの方がまだマシだった。

これは経験不足なるものだろうか。私は他人のコードは仕事以外ではあんまりみないからな。

しかし、一つずつ理解していけば今回のはそこまでつらいものではなかった。

```

fn find(&mut self, x: usize) -> usize {
    if x == self.par[x] {
        x
    }else{
	    // ここらへんを修正
        let res = self.find(self.par[x]);
        self.par[x] = res;
        res
    }
}

```

この処理はなんてことはない、親がルートの場合、自身を返し、

そうでない場合は自分の親をfindでルートでたどっていき

ルートを見つける。

そしてそれを自分の親にし、ルート関数である。

直訳じゃん。

#### あほあほ疑問タイム

1. なんでルートを見つけるだけじゃダメなんだ？

2. なんで自分の親をルートにしてるんだ？

3. なんでランクの変更がないんだ？

##### 1と2について

これはおそらくテクニックの一つで

木構造の場合、いわゆる偏りというものが発生することがある。

1-2-3-4がすべて一列になるみたいなやつです。

それって木構造の意味ないやん。

だから、その調整として、うまく分かれるようにコードの中に仕込むことが多いらしい。

今回の場合、findする際にルートの一個下に持っていくみたいだ。

~~グループAの中のグループBの...みたいなことを書くならもっと複雑な処理をかかないといけないと思うけど、~~

~~今回解く題材が題材だったので、これで問題なさそう。~~

やったことないので、ここら辺は消しとく。

##### 3について

基本的にこのソースコードの中でrankをつかうのはuniteだけ(初期化とdebugは除く)なんだけど、

uniteは大前提としてルート同士で処理を行うので、ルート未満の要素にとってrankは必要ない。

だから変える必要がない。

### same

```

fn same(&mut self, a: usize, b: usize) -> bool {
    self.find(a) == self.find(b)
}

```

aとbのルートが同じかどうかを確認しているだけである。

### unite

```

fn unite(&mut self, a: usize, b: usize){
    let apar = self.find(a);
    let bpar = self.find(b);
	// ここも修正
	if apar == bpar{
		return
	}
	// ここらへんも修正
    if self.rank[apar] < self.rank[bpar] {
        self.par[apar] = bpar;
    }else{
        self.par[bpar] = apar;
        if self.rank[apar] == self.rank[bpar] {
            self.rank[apar] += 1;
        }
    }
}

```

このコードの中で一番難しいところ。

ここまでやっといてあれだけど、このコードを見て、AtCoderの説明みてわからんやつは相当アホだと思ってる。

私以外みたことないけど。

ここも処理自体を文章で起こしていくと、

aとbのルートを取得し、同じなら何もしない。

そうでなければ、それぞれの深さを比較し、

小さい方の親を大きい方にする。

なお、同じ場合はaが大きかった場合と同じ処理を行い、

かつ子のランクをあげる。

---

**アホな私の脳内**

...あれ？

rankってなんだっけ？

深さだよな。

...????????

* uniteでは深さが同じ場合、bの親をaにした上で、aの深さを一つ追加する。

これはわかる。同じ深さだから追加すると深さは

例えば、右に偏ってる1-2-3-4-5と同じく右に偏ってる10-11-12-13-14-15をuniteするとして、

すぐ下に追加するから...よし、高さはプラス1になるだけだな。あってる。

例えば片方が圧倒的に大きな深さを有していたとしても、

大きな方のすぐ下に配置されることになり、かつ深さが少なくとも1以上差がある場合は

依然として深さは変わらない。

頭が普通の人は(ry

自分の頭の悪さにかなしくなる。

---

## 終わりに

今回はUnion-Findを主題にしたメモなので、解いた問題については記載しない。

## リンク

* 今回の解説するコードの元々の在処

[github/wasuken/contest-book/src/act2.rs](https://github.com/wasuken/contest-book/blob/master/src/act2.rs)

* ここから593行までが対象のコードとなる。

[src/act2.rs#L497](https://github.com/wasuken/contest-book/blob/master/src/act2.rs#L497)

* Union-Findを検索するとよくでてくるAtCoderのページ

ここのスライド3周くらいした。

[B - Union Find](https://atcoder.jp/contests/atc001/tasks/unionfind_a)
