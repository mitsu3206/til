# Git
Gitでよく使うコマンドを記載する。

#### ブランチを作成する
```
git branch <branch_name>
```

#### リモートブランチからブランチを作成する
```
git branch <branch_name> origin/<src>
```

#### リモートリポジトリをローカルにクローンする
```
git clone <https or ssh>
```

#### ブランチを一覧表示する
```
git branch -a
```

#### 変更内容をステージにあげる
```
git add -A
```

#### コミットする
```
git commit -m "message"
```

#### コミットログを表示する
```
git log -10
```

#### 削除されたリモートリポジトリをフェッチする
```
git fetch --prune
```

#### ブランチを削除する
```
git branch -D <branch_name>
```

#### stageを取り消す
```
// ファイルごと
git restore --staged ファイル名
// 一括
git restore --staged .
```

#### 変更を取り消す（stageしていない）
```
// ファイルごと
git restore ファイル名
// 一括
git restore .
```

#### 追加ファイル・ディレクトリを取り消す
```
// ファイル
git clean -f
// ディレクトリ
git clean -df
```
