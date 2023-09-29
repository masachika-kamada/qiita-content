---
title: PythonパッケージをPyPIに公開するはじめの一歩
tags:
  - Python
  - PyPI
  - ライブラリ
  - パッケージ
  - モジュール
private: false
updated_at: '2023-09-30T00:47:10+09:00'
id: fb28ba414e1d9dc56a60
organization_url_name: null
slide: false
ignorePublish: false
---
この記事では、簡単な Python パッケージを PyPI に公開する方法を解説します。

## PyPI とは

[PyPI](https://pypi.org/) とは、Python Package Index の略で、Python のパッケージを公開するためのリポジトリです。
Python で書かれたソフトウェアとライブラリを公開、共有するための中央リポジトリとしての役割を果たしています。

### 仕組み

* パッケージの公開: 開発者は自分が作成した Python パッケージを PyPI にアップロードします。
* パッケージの検索とダウンロード: `pip`` はこの PyPI からパッケージを検索し、ダウンロードしてインストールします。

## 1. PyPI のアカウントを作成する

1. [PyPI のアカウント作成ページ](https://pypi.org/account/register/) にアクセスし、アカウントを作成します。
2. 二要素認証（2FA）を有効にします。[PyPI のアカウント設定ページ](https://pypi.org/manage/account/) にアクセスし、`Add 2FA with authentication application` から 2FA を有効にします。
3. 同じページで API トークンを作成します。API トークンの項目で `API トークンの追加` をクリックし、トークンを作成します。
4. `.pypirc` というファイルをホームディレクトリに作成します。以下のように記述します。
    ```ini:.pypirc
    [pypi]
    username = __token__
    password = <3 で作成した API トークン>
    ```

## 2. パッケージを作成する

ここではランダムな「コンプリメント」（褒め言葉）を生成するパッケージを作成してみます。
まずディレクトリを作成します。

```console
mkdir compliment_generator
cd compliment_generator
```

次に、プロジェクトディレクトリ内に `compliment_generator.py` という Python ファイルを作成します。

```python:compliment_generator.py
import random

def generate_compliment():
    compliments = [
        "You look great today!",
        "You're a smart cookie!",
        "I like your style!",
        "You're the bee's knees!"
    ]
    return random.choice(compliments)

```

次に `setup.py` というファイルを作成します。

```python:setup.py
from setuptools import setup

setup(
    name='compliment_generator',
    version='0.1',
    py_modules=['compliment_generator'],
    install_requires=[],
)
```

## 3. パッケージのビルド

`setup.py` が存在するディレクトリで以下のコマンドを実行します。

```console
python setup.py sdist bdist_wheel
```

## 4. パッケージを PyPI にアップロードする

`twine` というパッケージをインストールします。

```console
pip install twine
```

`twine` を使って PyPI にアップロードします。

```console
twine upload dist/*
```

## 最後に使ってみる

### インストール

```console
$ pip install compliment-generator
  Downloading compliment_generator-0.1-py3-none-any.whl (1.4 kB)
Successfully installed compliment-generator-0.1
```

### 実行

```console
$ python
Python 3.7.3 (default, Apr 24 2019, 15:29:51) [MSC v.1915 64 bit (AMD64)] :: Anaconda, Inc. on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import compliment_generator
>>> compliment_generator.generate_compliment()
'I like your style!'
>>> compliment_generator.generate_compliment()
"You're the bee's knees!"
```

以下のページから今回作成したプロジェクトを確認できます。
<https://pypi.org/project/compliment-generator/>
