# 「2時間半で学ぶ初心者向けMySQLデータベースチュートリアル」 プログラミングアカデミー (youtube)

2023/09/02~09/03

**CRUD**

- Create
- Read
- Update
- Delete

## SQL文でデータ検索

- select カラム名 from テーブル名 
- select カラム名 from テーブル名 where 条件式
- 演算子 ..=,<,>,!=,and,or,between,in(),like ..文字列のあいまい検索
- ワイルドカード
  - * ..すべて
  - % ..0文字以上の文字列
  - _ ..任意の1文字の文字列
- order by カラム名 ..並び替えの指定 desc(降順)
- limit ..検索結果の件数を絞る

## データベースの作成

- create database データベース名;
- create table テーブル名 (カラム名 型,カラム名 型);
- insert into テーブル名 (カラム名1,カラム名2) values (値1,値2);

- strictモードの設定
  - my.iniの設定に追記 sql_mode=STRICT_TRANS_TABLES,

- キー
  - 主キー、外部キー
  - 候補キーの中から最も使いやすいキーを主キーに設定する
  - 複合キー ..複数の属性の組合せでキーとする
  - テーブルの作成時に設定する

## データの更新

- 疑似個人データ生成
- update テーブル名
  set カラム名1 =値',カラム名2=値2,カラム名3=値3
  where カラム名 =値;

## データの削除

- delete from テーブル名 where カラム名=値;

## データの検索2

- 集計関数
  - count
  - sum
    - ex. select sum(population) from country;
    - select format(sum(population),0) from country; ..3桁区切り
    - select format(sum(population),0)as WorldPopulation from country; ..集計結果カラム名に別名をつける
    - group by ..～ごとに集計
    - ex. SELECT format(sum(population),0) as continentpopulation from country group by continent;
    - ex. SELECT continent, format(sum(population),0) as continentpopulation from country group by continent;
    - having句 ..グルーピング集計結果に条件をつけて抽出するとき(whereは使えない。whereはグルーピングする前)
  - avg

- join
  - 2つのテーブルを合体させて新しい1つのテーブルを作る
  - ``` select * from city join country on city.countrycode = country.code; ```
    ``` sql
    select
    id,
    city.name,
    city.population as CityPopulation,
    country.population as CountryPopulation,
    city.population/country.population as ratio
    from city join country on city.countrycode = country.code
    where city.name='Tokyo';
    ```
