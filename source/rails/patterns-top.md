# 単純に使うパターンの紹介


## decoratorパターン
 
before: controller -> view  
after:  controller -> decorator -> view  
 
中間にデコレーターを挟むことで、ロジックに手を下さなくても改変ができる。
アダプターパターンと似ている
 
### gem
- ActiveDecorator
- Draper
 
### directory
app/decorators
 
 
## Deliveryオブジェクト
slackとかlineとか通知に関連する処理を統括する
 
before:
- job -> slack
- job -> line

after:
- job -> delivery -> slack, line, etc

### gem
- active_delivery
 
### directory
app/deliveries
 
 
## Formオブジェクト
シンプルなcreateとかupdateとかで完結しない、ActiveRecord関連の処理を実行する時に実装する。
例えば、同時に関連するデータを更新する時とか
[サンプル](https://github.com/tonton-k/BP-form-obj-ptrn)では、複数の関連するモデルをフォームオブジェクトで検証している。

### directory
app/forms
 
 
## Interactorオブジェクト
外部APIとのやりとりや、複数のARを横断する場合に、コントローラーの肥大化を防ぐために使うパターン。サービスパターンと似てる。

### gem
- interactor
 
### directory
app/interactors

## Policyオブジェクト
アプリケーションのルールを定めたオブジェクト。例えば、ユーザーの種類によって変わる処理とかを、Policyオブジェクトに定義することで、コントローラーの🐖化を避けられる。
 
### gem
- pundit
 
### directory
app/policies


## Queryオブジェクト
モデルのスコープにオブジェクトを渡して使用。モデルに変更を加えてもコントローラーへのダメージが少なくなる。

### directory
app/queries

## Validatorオブジェクト
複数の場所で使うvalidationを１箇所にまとめることで、無駄を無くし、保守性をあげる。
例えば、下記のようにやってることは同じなのに複数の場所に同じバリデーションが定義されてたら冗長なんで、だったら１箇所にまとめて書いちゃおうぜって話。

**models**
- Note.rb -> validates: title, length: { minimum: 10, too_short: "もっと暑い魂のこもったタイトルにしようよ" }
- Comment.rb -> validates: title, length: { minimum: 10, too_short: "もっと暑い魂のこもったタイトルにしようよ"}

### directory
app/validators


## Valueオブジェクト
日付だったり、金額だったり、個々によって限定されない物をValueオブジェクトとして扱う。
アダプターパターンのインスタンスと似てる。

[参考](https://techracho.bpsinc.jp/hachi8833/2018_03_27/53794)

### directory
app/values

## View Component オブジェクト
再利用可能なビューをコンポーネント単位でカプセル化する。

### directory
app/view_components


### gem
- view_component


## 参考リンク

[ここ](https://www.sitepoint.com/7-design-patterns-to-refactor-mvc-components-in-rails/)
