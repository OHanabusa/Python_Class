# Pythonチュートリアル：クラスの基本と応用

## はじめに

このチュートリアルでは、Pythonの"クラス"という概念について学びます。クラスはオブジェクト指向プログラミングの中核をなすもので、プログラムを整理しやすくし、再利用可能にするための強力な機能です。

Pythonの文法の基本（変数、関数、if文、for文など）を理解している人を対象に、次のことを目標に進めていきます：

1. クラスの定義と使い方の理解
2. クラスを使ったプログラムの構築方法
3. 実際のシミュレーション（質点-ばねモデル）への応用

---

## 第1章：クラスとは何か？

### クラスの定義
クラスとは、変数（属性）と関数（メソッド）をまとめた「設計図」のようなものです。具体的なデータを持たせることで、実体（インスタンス）を作ることができます。

```python
class MyClass:
    def __init__(self, name):
        self.name = name

    def greet(self):
        print(f"Hello, my name is {self.name}.")

obj = MyClass("Taro")
obj.greet()  # Hello, my name is Taro.
```

---

## 第2章：クラスを使った簡単なプログラム

ここでは、カウンター（数を数える）クラスを作って、複数のインスタンスを作る例を紹介します。

### カウンタークラス
```python
class Counter:
    def __init__(self):
        self.value = 0

    def increment(self):
        self.value += 1

    def get_value(self):
        return self.value

# 複数のカウンターを使ってみる
c1 = Counter()
c2 = Counter()

for _ in range(5):
    c1.increment()

for _ in range(3):
    c2.increment()

print("c1:", c1.get_value())  # 5
print("c2:", c2.get_value())  # 3
```

クラスを使うことで、`c1`と`c2`という独立した状態を持つカウンターを作ることができます。

---

## 第3章：質点-ばね系のシミュレーション

### モデルの概要

- ばねでつながれた1つの質点の運動を扱います。
- 運動方程式は $m \ddot{x} = -kx$（ばねの復元力）
- 数値解法は中間差分法（中央差分）を用います：

$$
x_{n+1} = 2x_n - x_{n-1} + \frac{\Delta t^2}{m}(-k x_n)
$$

### シミュレーションクラスの実装
```python
import numpy as np
import matplotlib.pyplot as plt

class SpringMassSimulator:
    def __init__(self, mass, k, dt, x0, v0):
        self.m = mass
        self.k = k
        self.dt = dt
        self.x_prev = x0 - v0 * dt  # 初期位置から逆算
        self.x_curr = x0
        self.history = [x0]

    def step(self):
        a = -self.k * self.x_curr / self.m
        x_next = 2 * self.x_curr - self.x_prev + (self.dt ** 2) * a
        self.x_prev, self.x_curr = self.x_curr, x_next
        self.history.append(x_next)

    def run(self, steps):
        for _ in range(steps):
            self.step()
        return self.history
```

### 実行と可視化
```python
sim1 = SpringMassSimulator(mass=1.0, k=10.0, dt=0.01, x0=1.0, v0=0.0)
sim2 = SpringMassSimulator(mass=1.0, k=20.0, dt=0.01, x0=1.0, v0=0.0)

x1 = sim1.run(1000)
x2 = sim2.run(1000)

plt.plot(x1, label='k=10')
plt.plot(x2, label='k=20')
plt.xlabel('Time step')
plt.ylabel('Position')
plt.legend()
plt.title('Spring-Mass System Simulation')
plt.show()
```

---

## まとめ
このチュートリアルでは、クラスの定義から始めて、複数のインスタンスを使った簡単な応用、そして実際の物理シミュレーションに至るまでの流れを体験しました。クラスを使うことで、コードの再利用性や可読性が向上するだけでなく、より現実的な問題にも対応できるようになります。

次のステップとしては：
- 複数の質点の連成系（2質点ばね系など）
- 空気抵抗の追加
- クラス継承を使った拡張
なども挑戦してみましょう！

