# アダプターパターン
例えば１００V の電流を今必要な１２Vに変換してくれるACアダプターのような変換機能を持ったパターンである。

プログラムでは「すでにある物」と「必要な物」の間にあるズレを変換する。これをデザインパターンと呼ぶ。
また、wrapperと呼ばれることもある。

アダプターパターンには２種類ある

1. クラス（継承）による、アダプターパターン
2. インスタンス（委譲）による、アダプターパターン

## 継承パターン

```python
from abc import ABCMeta, abstractmethod


# 継承元となるクラス（標準ライブラリーだったり、その他だったり）

class Banner:
  def __init__(self, text):
    self.__text: str = text

  def show_text(self):
    return self.__text

  def show_with_asterisk(self):
    return '*' + self.__text + '*'


# interface
class PrintInterface(metaclass=ABCMeta):
  @abstractmethod
  def print_string(self):
    pass

  def print_weak(self):
    pass


# 元々あるクラスを継承して拡張する
# また、インターフェースを実装する
class PrintBanner(Banner, PrintInterface):
  def __init__(self, text):
    super(PrintBanner, self).__init__(text)
    self.__text = text

  def print_string(self):
    return self.__text.upper()

  def print_weak(self):
    return '(' + self.__text + ')'


banner = Banner('hoge')
print(banner.show_text())

banner = PrintBanner('heyhey')
print(banner.print_weak())

print(banner.print_string())
```

## 委譲パターン
インスタンスを生成して行う  
(これ合ってるのか？🤔）

```python
from abc import ABCMeta, abstractmethod


# インスタンスの元となるクラス（標準ライブラリーだったり、その他だったり）

class Banner:
  def __init__(self, text):
    self.__text: str = text

  def show_text(self):
    return self.__text

  def show_with_asterisk(self):
    return '*' + self.__text + '*'


# interface
class PrintInterface(metaclass=ABCMeta):
  @abstractmethod
  def print_string(self):
    pass

  def print_weak(self):
    pass


# 元々あるクラスのインスタンスをゴニョるクラス
# また、インターフェースを実装する
class PrintBanner(PrintInterface):
  def __init__(self, text):
    self.banner = Banner(text)

  def print_string(self):
    return self.banner.show_text().upper()

  def print_weak(self):
    return '(' + self.banner.show_text() + ')'


banner = Banner('hoge')
print(banner.show_text())

banner = PrintBanner('heyhey')
print(banner.print_weak())

print(banner.print_string())
```
