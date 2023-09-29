# Qiita の記事を GitHub リポジトリで管理

## 導入

参考：<https://qiita.com/Qiita/items/32c79014509987541130>

## 運用

1. public ディレクトリに md ファイルを作成
2. 他のファイルの形式を真似て、md ファイルに記事を書く
3. `npx qiita preview` でプレビュー：fish で以下のように設定したので `qiita` で実行可能
    ```fish
    function qiita
        cd ~/workspace/qiita-content/ && npx qiita preview
    end
    ```
4. `git push` で GitHub に push
