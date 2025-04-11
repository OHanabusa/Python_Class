# Pythonチュートリアル：クラスの基本と応用

## はじめに

このチュートリアルでは、Pythonの"クラス"という概念について学びます。クラスはオブジェクト指向プログラミングの中核をなすもので、プログラムを整理しやすくし、再利用可能にするための強力な機能です。

Pythonの文法の基本（変数、関数、if文、for文など）を理解している人を対象に、次のことを目標に進めていきます：

1. クラスの定義と使い方の理解
2. クラスを使ったプログラムの構築方法
3. 実際のシミュレーション（質点-ばねモデル）への応用

このチュートリアルの最後では、物理現象をPythonでどのようにシミュレートできるかを、クラスを使った設計とともに体験してもらいます。

---

## 第1章：クラスとは何か？

### この章の実行方法

この章のコードを試すには、以下のいずれかの方法を選んでください：

#### 1. Pythonファイルとして保存する場合
1. 以下のコードを `example_class.py` などの名前で保存します。
2. vscode（またはコマンドプロンプト）で保存した場所に移動します。
3. 次のコマンドで実行します：

```bash
python example_class.py
```

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


