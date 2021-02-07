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
 外部APIとの
 ## Interactorオブジェクトやr
 ## Interactorオブジェクト
 
 
 
 
 
 
 
 
 
