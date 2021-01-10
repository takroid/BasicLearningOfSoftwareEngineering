# React 学習


- DOMとは

  DocumentObjectModelの略。HTMLなどを解釈し木構造で表現したもの

- 仮想DOMとは

  JSのオブジェクトで仮想的に作られたDOM。いきなりDOMを操作せず、JS上で

  仮想DOMを操作し差分を出してからDOMに反映

- PackageManager(npm/yarn等。内部ではNodeJsが動いている)

  - NPM -> パッケージのレジストリ

  - Package.json　-> 設計書的な役割

  - Package-lock.json または yarn.lock ->自動で生成される。依存関係、バージョンの解決

  - node_modules -> 各モジュールの実態。JSファイルなど。サイズが膨大でGithu1bにはあげない

    

- ECMAScriptとは

  - JSの標準規格、毎年一回発表される
  - ES2015で機能追加が多くあった(let,const アロー関数、class構文　promise などなど)

- モジュールバンドラーとは

  複数のJS(css/image)ファイルを一つにまとめるためのもの(例：webpackなど)

- トランスパイラなど

  - 新しいJSの記法を古い記法に変換してくれる

    ES6に対応していないブラウザに対応するため。開発は新しい記法で行い実行時に変換させる

- SPA(SinglePageAppligcation)

  ※モダンJSはSPAが基本。HTMLは一つのみでJSで画面を書き換える

  ->index.htmlを書き換えるイメージ

  - ページ遷移ごとのチラつきがなくなる
  - 表示速度のアップによるユーザー体験向上
  - コンポーネント分割が容易になることで開発効率アップ





# JS 基本構文

- 厳密性

  var < const < let

- varは再宣言可能。

  ```javascript
  var val1 = "varです";
  console.log(val1);
  *//varは再宣言可能*
  var val1 = "varだってば";
  console.log(val1); //"varだってば";
  ```

- letは上書き可能

- ```javascript
  let let1 = "let";
  console.log(let1);
  let1 = "let2";
  console.log(let2); //let2
  ```

- constは宣言したら再宣言も再代入も不可.

  ```javascript
  const con1 = "con";
  console.log(con1);
  con1 = "concon";
  console.log(con1);  //コンパイルエラー発生
  ```

  - しかしobjectとはこの限りではない。プロパティの書き換え、追加が可能。

  - オブジェクトの定義は基本的にconstを使用する

  - ```javascript
    //オブジェクトのテスト　constで定義したオブジェクトはプロパティの変更が可能
    const obj1 = {
      name: "海太郎",
      country: "JP"
    };
    //nameのプロパティ書き換え
    obj1.name = "海苔太郎";
    //プロパティ追加
    obj1.sex = "male";
    console.log(obj1);　//{name: "海苔太郎", country: "JP", sex: "male"}
    //配列のテスト　constで定義した配列はプロパティの変更が可能
    const catArray = ["mikeNeko", "kuroNeko"];
    catArray[0] = "siroNeko";
    catArray.push("cyatoraNeko");
    console.log(catArray); //["siroNeko", "kuroNeko", "cyatoraNeko"]
    
    ```

## テンプレート文字列

-  文字列と変数の結合を便利に*文字列の中でJS変数の展開が綺麗に描ける*

  ```javascript
  const myName = "パンクリーム";
  const myAge = "365";
  const message = `私の名前は${myName}です。年齢は${myAge}才です。`;
  console.log(message); //私の名前はパンクリームです。年齢は365才です。 
  ```

## アロー関数

- 関数の定義がより簡潔に

  ```javascript
  //通常の関数
  const normalFunc = (str) => {
    return str;
  };
  console.log(normalFunc("ふつーの関数だよ")); //ふつーの関数だよ
  //アロー関数
  const arrFunc = (str) => {
    //引数が一つの時は()を省略可
    //const arrFunc = str => {
    return str;
  };
  //{}の中の処理が1行の単純な処理は下記の様にも書ける
  const arrFunc2 = (str) => str;
  console.log(arrFunc("アロー関数だよ")); //アロー関数だよ
  
  const arrFunc3 = (num1, num2) => num1 + num2;
  
  console.log(arrFunc3(100, 200));
  ```

  ##　分割代入

  - 冗長さ回避。可読性の向上。

- ```javascript
  //分割代入(冗長さの回避)
  const coffeeShop = {
    name: "ドトール",
    recommend: "アイスココア"
  };
  
  //分割代入しない　->冗長である
  const cafe1 = `店名は${coffeeShop.name},おすすめ商品は${coffeeShop.recommend}です`;
  console.log(cafe1);
  //オブジェクトで分割代入
  const { name, recommend } = coffeeShop;
  const cafe1ObjectBunkatu = `店名は${name}、おすすめ商品は${recommend}です`;
  console.log(cafe1ObjectBunkatu);
  
  //配列で分割代入しない
  const coffeeShop2 = ["スタバ", "ソイラテ"];
  const coffeeShop2Array = `店名は${coffeeShop2[0]}、おすすめ商品は${coffeeShop2[1]}}です`;
  console.log(coffeeShop2Array);
  
  //配列で分割代入(順番で要素を抜き出すため変数名は異なっても構わない点に留意)
  const [shopname, productName] = coffeeShop2;
  const coffeeShop2ArrayBunkatu = `店名は${shopname}、おすすめ商品は${productName}ですね`;
  console.log(coffeeShop2ArrayBunkatu);
  ```

- デフォルト値

  変数に何も入っていない場合、JSの初期値が「undefined」となってしまいバグの温床になる。その対策

- ```javascript
  //デフォルト値を使う
  const saySomething = (name) => console.log(`こんにちは${name}さん`);
  saySomething(); //こんにちはundefinedさん
  saySomething("天ぷら"); //こんにちは天ぷらさん
  //デフォルト値を使わない
  const saySomething2 = (name = "名無し") => console.log(`こんにちは${name}さん`);
  saySomething2(); //こんにちは名無しさん
  saySomething2("天ぷら"); //こんにちは天ぷらさん
  ```

- 

