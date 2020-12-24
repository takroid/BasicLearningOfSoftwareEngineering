# SQL学習


- MAX関数
                                                                                                                                		
  指定したカラムのデータの中から最大のデータを取得できる

  ```sql
  SELECT MAX(price) FROM purchases;
  ```

  ​																																		

- MIN関数

  指定したカラムのデータの中から最小のデータを取得できる

  ```sql
        SELECT MIN(price) FROM purchases;
  ```

  

- グループ化

データをグループ化することができる

```sql
SELECT SUM(price),purchased_at

FROM purchases 

GROUP BY purchased_at;
```



- グループ化したデータの絞り込み

HAVING句を使用する

これはGROUP BY によってグループ化されたデータを検索対象とする

```sql
SELECT SUM(price),purchased_at

FROM purchases

GROUP BY purchased_at

HAVING SUM(price) > 1000;
```



- サブクエリ

  2つ以上のクエリを１つにまとめる事が可能で、より複雑なデータを取得できる

  ```sql
  SELECT name
  FROM players
  WHERE goals > (
    SELECT goals
    FROM players
    WHERE name = "ウィル"
  );
  ```

  

- データの可読性を上げる

  AS を使用

  ```sql
  SELECT name AS "身長180cm以上の選手"
  FROM players
  WHERE height >= 180;
  ```




- テーブルを紐づける

  外部キーと主キーを使用する

  ※外部キーと主キーで紐付け可能



- 複数のテーブルを一つに結合したいとき

  JOINを使用する

  ```SQL
  SELECT * FROM players JOIN countries ON players.country_id = countries.id;
  ```

  

- LEFT JOINdd

  ```sql
  SELECT * FROM players LEFT JOIN teams on players.previous_team_id = teams.id;
  ```

  









