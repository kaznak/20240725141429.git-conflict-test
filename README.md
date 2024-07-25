# git のコンフリクトと解消の仕方のメモ

main ブランチを develop ブランチにマージする場合、つまり git switch develop ; git merge main する場合に、
コンフリクトが発生することがあります。
この時コンフリクト解決の手段としては以下の3つのケースがありえます。

1. base を採用する
    - case1.txt
2. develop を採用する
    - case2.txt
3. 当該ファイルを編集した結果を採用する
    - case3.txt

このレポジトリではそれぞれのブランチが以下のタグの時点を想定しています。

- main: conflict-main
- develop: conflict-develop

これらのコンフリクトは以下のようにすることで、 2 のみの対応が可能なように変換できます。

1. main のファイルを develop ブランチにコピーする
    - `git restore --source=main case1.txt`
        - `git restore --source=conflict-main case1.txt` でも可
    - タグ resolve-conflict-case1 のコミット
3. develop ブランチのファイルを編集して、 develop のみを採用すれば良いようにする
    - タグ resolve-conflict-case3 のコミット

その後は以下の手順でマージが可能です。

```bash
git switch develop
git merge main
git checkout --ours .
git add .
it merge --continue
```

タグ resolve-conflict-and-merge のコミットでこの手順を実行しています。
