# iterator pattern

イテレーターパータンは配列を全て、順番にスキャンしていく方法。

# iterator

```python
import random
a_list: list = [random.randrange(1, 100) for x in range(10)]

for i in a_list:
  if i % 2 == 0: print(f'{i} is even')

  if i % 2 == 1: print(f'{i} is odd')
```

# 実装してみる

```python

# インターフェースを実装
## インターフェースとは欲しい機能だけを取り出して、使えるAPIチックなもの
from abc import ABCMeta, abstractmethod

class IteratorInterface(metaclass=ABCMeta):
  # @abstractmethodでメソッドを抽象化
  @abstractmethod
  def has_next():
    pass

  def next():
    pass

## 本棚クラスはイテレーターインターフェースを継承
class BookShelfIterator(IteratorInterface):
  def __init__(self, books):
    self.books: list = books
    self.index: int = 0

  def has_next(self):
    return False if self.index >= len(self.books) else True

  def next(self):
    book = self.books[self.index]
    self.index += 1
    return book

  def remove(self):
    return self.books.pop()


# bookクラス
## 本の名前を取得するだけ
class Book:
  def __init__(self, name):
    self.__name: str = name

  def get_name(self):
    return self.__name

# book shelfクラス
## 集合体として使うためにaggregateインターフェースを実装
class BookShelf():
  def __init__(self):
    self.books: list = []

  def add_book(self, book):
    if book.__class__.__name__ != 'Book': raise TypeError("it is not a instance of Book") 
    self.books.append(book)

  def get_book_at(self, index: int):
    return self.books[2]

  def length(self):
    return len(self.books)

  def iterator(self):
    return BookShelfIterator(self.books)

# 本を生成
lorems = [ Book(s) for s in 'lorem ipsum dollor sit de hoge fuga'.split()]

# 本棚を生成
book_shelf = BookShelf()

# 本棚に本を追加
[book_shelf.add_book(book) for book in lorems]

print(f'book_shelf has {book_shelf.length()}books' if book_shelf.length() == len(lorems) else False)

print('second book in the book shelf is' + book_shelf.get_book_at(2).get_name())

iterator: object = book_shelf.iterator()

while iterator.has_next():
  book = iterator.next()
  print(f'title of the book is {book.get_name()}')

```
    
 
