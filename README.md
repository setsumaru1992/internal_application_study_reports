# internal_application_study_reports
普段使っているWebアプリケーションの裏側で何をやっているか勉強する記録を残すリポジトリ

以下がアプリケーションのビジネス面をやっているように、裏側についても学びたい。  
ただし優先度は上記リポジトリの方がこのリポジトリよりも上
https://github.com/setsumaru1992/todo_list_with_modern_environment

上記リポジトリと違ってコードに残すの面倒な可能性もあるから、何を元に調査したかなど、考えのログを残すことがメイン。

# 20200418構想
## やりたいこと
形式
- [ ] やりたいこと
  - できるようになることで実現できること
    - 抱えている問題
      - ~
    - 実現できること
      - ~
  - 具体的に何をしたいのか
    - [ ] 

### DB
- [ ] データベースの裏側で何をやっているか知りたい
  - できるようになることで実現できること
    - 抱えている問題
      - DBにしろ検索エンジンにしろ、表層の提供しているところだけ使っているのみ
      - 大抵それで困らない
      - しかし以下の場合に自分に知識がないことを呪う
        - アプリケーション内でちょっと大きなデータ(10万レコード)とか柔軟に処理したい場合にベストプラクティスを知らずに悪手を取ってしまう
        - 完全な私事だが、Elasticsearchを知らないけど会社でElasticsearchを使っていてキャッチアップしたい。だけど歴史が巨大すぎて、上澄みしか掬えない。
    - 実現できること
      - アプリケーションでDBチックなことをするときに、暗中模索ではなくレールに載った感じでコードが書けるようになる
      - DBの根幹を知りDB・検索エンジンのコミッターと同じ問題意識を持つことでコードがスラスラ読めること、次のリリースの予期ができることを期待
  - 具体的に何をしたいのか（以下は順番にやっていくというより、レベルに合わせて全部少しずつ進める）
    - 参考資料があれば読む
      - 直接的なデータベースの話
        - [ ] 『Database Internal』
      - 間接的に一助となるもの
        - [ ] 『Go言語でつくるインタプリタ』
          - SQLを解析するときとか構文木解析とかできた方が捗るから
    - DBや検索エンジンの内部実装を読む
      - [ ] MySQL
      - [ ] Elasticsearch
    - [ ] DBを作ってみる

### Javascript
- [x] ReactとReduxの裏側で何やってるか見たい 
  - できるようになることで実現できること
    - 抱えている問題
      - React,Redux関連のライブラリを使うことがあり、細かなことでも独立したライブラリを使うことが多く、とにかく使うライブラリの数が多い。
      - 問題領域が独立した細かいライブラリを使うことに対して異論はないが、その管理を開発者に委ねられるため、リテラシーが求められる
      - RailsのようにバカみたいにReact入れとけばやりたいことが事足りる、つまり独立した個々のライブラリの管理をフレームワークに委ねられるのが理想だが現実そうなっていない。
      - 個々のライブラリ、ひいてはReact,Reduxも含め思想ともに理解することで、適切にこれらをハンドリングできるようになりたい
    - 実現できること
      - React,Redux関連のライブラリの思想を知ることで、それらのライブラリに振り回されなくなること
  - 具体的に何をしたいのか
    - 大元のReact,Reduxのコードを読む
      - 知りたいこと
        - 元々はバニラJSのくせしてなんであんなに強力なツールになりうるのか。その構造やそれを支える裏実装。
      - 進め方
        - いつも触れていて実装もラッパーにすぎなさそうなReduxの方から読んで小さな達成感を得て、Reactのコードをみる問題意識を深めてからReactのコードを読む
      - TODO
        - [x] Redux
        - [x] React
- [x] Javascriptの知識をアップデートしたい
  - できるようになることで実現できること
    - 抱えている問題
      - 学びなおしたいとかじゃなく、普段曖昧にとらえている個別具体のjs記法を流儀・作法ともに知りたい
    - 実現できること
      - jsを読むときに曖昧に捉えなくなる
  - 具体的に何をしたいのか
    - [x] 条件式について知りたい
      - `if(obj)`が何を判断していて何が返り、ifは何をもってtrueと判断するか
      - `num && list[num]`とかよく見るけど、それぞれのパターンで何が返るのかnumがnullだったら何が返るのか
    - [x] `{obj}`(obj = {hoge: 1})の記法
      - 予想だと変数名をキーにその値を入れているって感じだろうけどそれが正しいのかどうか
      - コーディング規約を読むことで知ろう（またはES2015資料）

### Rails
- [ ] spring
  - できるようになることで実現できること
    - 抱えている問題
      - springが変になってエラーになるとか、springがキャッシュ持って更新されないとか色々ある
    - 実現できること
      - spring関連のエラーがわかっても思想や最低限の知識があるから、その知識をもとにハンドリングしたり、知ってる知識をアップデートできる
  - 具体的に何をしたいのか
    - [ ] springのドキュメント読むとか？
- [ ] rakeタスク
  - できるようになることで実現できること
    - 抱えている問題
      - `rake db:migrate`とかおまじないとしてしか使えていない。基本思想やベストプラクティスがわかっていない
      - 本来rakeを使うべき場所やrake使われているときのエントリーポイントとかがわからない
    - 実現できること
      - rakeが使われているときに「はいはい、あれね」とレールを知っている状態で接せられる
  - 具体的に何をしたいのか
    - [ ] rakeタスクを作ってみる？