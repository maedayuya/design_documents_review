# ER図2
## 全体
- 配送先テーブルがない。
  > エンドユーザが複数配送先を持ちたい場合はどうしますか？
- 入荷テーブルがない。
  > 入荷に関するデータはどこで取り扱いますか？
- 計算で出せる値はデータベースには保存しない。（同時計算によるエラーを防ぐため）
  > 計算で出せる値はデータベースには保存しないようにしてください。
    同時計算によるエラーが生じる可能性があります。
- Railsで自動で作成されるカラム(id, created_at, updated_at)を考慮してない。
  > Railsで自動で作成されるカラム(id, created_at, updated_at)に関しても考慮して記載してください。
    PKはテーブル名IDではなくIDとなります。

## 管理者
- PKがない。
  > PKが示されていません。
- リレーションがあるのにFKがない。
- エンドユーザ、商品に対してリレーションは必要か。
  > リレーションがあるのに対してFKが示されていません。
    また、管理人とエントユーザ、商品に対してリレーションは必要でしょうか？

## エンドユーザ
- PKはユーザーIDではなく、エンドユーザID
  > PKはユーザIDで合っていますか？
- 名カラムがない。
　> 名前を登録するカラムがありません。

## 商品
- ディスク枚数は含まれているディスクの数から計算できるのではないか。
  > ディスク枚数は含まれているディスクの数から算出できるため不要です。
- 在庫数カラムとあるが、この値は（入荷数）ー（売上枚数）で算出できるため不要。
　> 在庫数は（入荷数）-（売上枚数）で算出できるため不要です。
- 発売日カラムがない。
　> 発売日に関するカラムがありません。
- ディスクIDはいらない。
  > 商品が親、ディスクが子になるためこちらにディスクIDは不要です。

## ジャンル、レーベル
- テーブルと同じ名前のカラムは作らない。（ジャンル名、レーベル名などにする）
  > テーブル名と同じ名前のカラムは作らないようにしてください。

## ディスク
- 商品とディスクのカーディナリティが逆。（一つの商品に対して複数のディスクがあるため）
- FKに商品IDが必要。
  > 商品が親、ディスクが子になるためカーディナリティは逆になります。
    そのため、こちらにFKで商品IDを持ってくる必要があります。
- トラックNo.とは何か。（曲順を管理するものなら曲名テーブルの方に入れる）
  > トラックNo.カラムは何のデータを保存するカラムでしょうか？カラムの命名を見直してください。
- 曲名IDは不要
  > ディスクが親、曲が子の関係になるためカーディナリティは逆になります。
    そのため、曲名IDは不要です。
 
## 曲名
- ディスクと曲名のカーディナリティが逆。（一つのディスクに対して複数の曲名があるため）
  > カーディナリティが逆なので、こちらにFKとしてディスクIDを含む必要があります。
- 曲順はどのように管理するのか。
  > 曲順はどのように管理しますか？

## カートアイテム
- PKがない。
  > PKが示されていません。
- 小計金額は計算で出せるため不要。
  > 小計金額は（商品の金額）x（購入枚数）で算出できるため不要です。

## 購入、購入詳細
- テーブル名は管理者視点の命名にする。（受注テーブルなど）
  > テーブル名は管理者視点の命名にしてください。

## 購入
- 購入日は登録日から出せるのではないか。
  > 購入日はRailsで自動作成されるcreated_atと内容が被るため不要です。
- 消費税が変わった場合も考慮して消費税カラムがあっても良い。
  > 消費税が変わった場合も考慮して消費税カラムがあった方が良いです。
- 購入と購入詳細のカーディナリティが逆。（一つの注文に対して複数の注文商品があるため）
  > 購入が親、購入詳細が子になるためカーディナリティは逆になります。
    そのため、購入詳細IDは不要です。

## 購入詳細
- 購入と購入詳細のカーディナリティが逆。（一つの注文に対して複数の注文商品があるため）
  > カーディナリティが逆なので、こちらにFKとして購入IDを含む必要があります。
- 商品情報がない。
  > 購入した商品の情報はどこから持ってきますか？
    また、購入した商品の情報が変わった場合も考慮して設計してください。

# 注意
* マークダウン形式で記入してください。
* 全体を通しての指摘事項の場合、テーブル名の部分を「全体」「共通」などとしてください。
