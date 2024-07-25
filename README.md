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

これらのコンフリクトは以下のようにすることで、 2 のみの対応が可能なように変換できます。

1. main のファイルを develop ブランチにコピーする
    - git restore --source=main case1.txt
3. develop ブランチのファイルを編集して、 develop のみを採用すれば良いようにする
