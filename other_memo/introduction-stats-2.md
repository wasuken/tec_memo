# 挫折しない統計学入門

## 2章

### 例題

> ある試験の点数の分布は正規分布であるとします。この試験の受験者数から、
> 10人からなる標本を無造作抽出して、この人たちの点数を平均したところ50点でした。
> この試験の受験者全体の点数の分散が25であるとわかっているとき、受験者全体の
> 平均点の95%信頼区間を求めてください。

```
import math
# 受験者全体の点数の分散
dist = 25 
# 取り出したデータの平均
trim_avg = 50
# 取り出した総数
trim_n = 10 

# x-u / sqrt(dist / trim_n) = 1.96
def answer(ans, is_minus=False):
    if is_minus:
        return trim_avg - (ans * math.sqrt(dist / trim_n))
    else:
        return trim_avg + (ans * math.sqrt(dist / trim_n))

print(answer(1.96, True))
print(answer(1.96))
```

コードはpython。
