# Pythonチュートリアル：クラスの基本と応用

## はじめに

Python のクラスは、現代的なソフトウェア開発において非常に重要な概念です。このチュートリアルでは、クラスの基本から応用までを体系的に学びます。特に、「コードの再利用性」「構造化された設計」「柔軟な拡張性」といったクラスの本質的な利点に触れながら、実践的なコード例を通じて理解を深めていきます。

対象読者は、Python の文法（変数、関数、if文、for文など）の基礎を身につけている初学者を想定しています。

このチュートリアルでは、以下のステップで学習を進めます：

1. クラスの定義と使い方の理解
2. クラスを使ったプログラムの構築方法
3. クラス継承とポリモーフィズムの応用
4. クラスをモジュールとして整理・拡張する方法

シンプルなカウンターから始まり、継承やモジュール化といった設計技法に至るまで、段階的にスキルアップできる内容です。

---

## 第1章：クラスとは何か？

### この章の実行方法

この章のコードを試すには、以下のいずれかの方法を選んでください：

#### Pythonファイルとして保存する場合
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

## 第3章：クラス継承とポリモーフィズム

継承とは、共通の処理を親クラスにまとめて、子クラスで個別の動作だけを上書きすることで、コードの重複を減らし、柔軟な設計を可能にする仕組みです。

ここでは「家電（Appliance）」という親クラスを作り、それを継承して `WashingMachine`（洗濯機）や `Microwave`（電子レンジ）を実装してみます。共通の「電源ON」処理は親クラスに持たせ、それぞれの機器固有の機能は子クラスで定義します。

### 例：家電クラスの継承
```python
class Appliance:
    def __init__(self, name):
        self.name = name

    def power_on(self):
        print(f"{self.name} の電源を入れました。")

    def run(self):
        print(f"{self.name} を動かします。")

class WashingMachine(Appliance):
    def run(self):
        print(f"{self.name} は洗濯を開始します。")

class Microwave(Appliance):
    def run(self):
        print(f"{self.name} は食べ物を温めます。")

appliances = [WashingMachine("日立 洗濯機"), Microwave("パナソニック 電子レンジ")]

for app in appliances:
    app.power_on()
    app.run()
```

この例では、すべての家電に共通する `power_on()` は親クラスに定義されており、`run()` メソッドだけを子クラスで異なる処理にしています。これが継承とポリモーフィズムの基本的な考え方です。


---

## 第4章：クラスとモジュール設計

第3章で作成した家電（Appliance）クラスを、実際にモジュールとして複数ファイルに分けて管理する方法を学びます。

これにより、個別の機器（洗濯機や電子レンジ）の定義を独立させることができ、保守や拡張が容易になります。

### ディレクトリ構成例とファイルの作り方（手動作成の場合）
以下の手順でファイルとフォルダを手動で作成してください：

1. 任意の場所に `my_appliances` という名前のフォルダを作成します。
2. その中に `appliances` という名前のサブフォルダを作成します。
3. `my_appliances` フォルダ内に `main.py` という名前のファイルを作成します。
4. `appliances` フォルダ内に以下の 4 つのファイルを作成します：
   - `__init__.py`（空でOK）
   - `appliance.py`
   - `washing_machine.py`
   - `microwave.py`

以下のような構成になります：

```
my_appliances/
├── main.py
└── appliances/
    ├── __init__.py
    ├── appliance.py
    ├── washing_machine.py
    └── microwave.py
```

### appliance.py
```python
class Appliance:
    def __init__(self, name):
        self.name = name

    def power_on(self):
        print(f"{self.name} の電源を入れました。")
```

### washing_machine.py
```python
from appliances.appliance import Appliance

class WashingMachine(Appliance):
    def run(self):
        print(f"{self.name} は洗濯を開始します。")
```

### microwave.py
```python
from appliances.appliance import Appliance

class Microwave(Appliance):
    def run(self):
        print(f"{self.name} は食べ物を温めます。")
```

### main.py
```python
from appliances.washing_machine import WashingMachine
from appliances.microwave import Microwave

appliances = [WashingMachine("日立 洗濯機"), Microwave("パナソニック 電子レンジ")]

for app in appliances:
    app.power_on()
    app.run()
```

このようにファイルを分割することで、それぞれのクラスの役割が明確になり、大規模なプロジェクトでも柔軟に管理できるようになります。

---

## まとめ

このチュートリアルでは、Pythonにおけるクラスの基本概念から始まり、クラスを使った簡単なプログラム、継承やモジュール分割といった発展的なトピックまでを扱いました。

学んだことを振り返ってみましょう：
- クラスとは、データ（属性）と振る舞い（メソッド）をまとめた設計図である
- 複数のインスタンスを作ることで、同じクラスから異なる状態のオブジェクトを管理できる
- 継承を使うことで、既存のクラスを拡張し、より汎用的で再利用可能な設計ができる
- モジュール構成を用いることで、実用的で保守性の高いプロジェクト構造が実現できる


