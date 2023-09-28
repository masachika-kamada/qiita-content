---
title: 【Azure】kaggleコンペで使うAzure AutoMLについて
tags:
  - Python
  - Azure
  - Kaggle
  - AutoML
private: false
updated_at: '2022-12-04T07:03:13+09:00'
id: ff71611b7c6bfcd12bbf
organization_url_name: cdleyouth
slide: false
ignorePublish: false
---
# はじめに

この記事は [CDLE youth Advent Calendar 2022](https://qiita.com/advent-calendar/2022/cdleyouth) 4日目の記事です。
先日 [CDLE youth](https://sites.google.com/view/cdleyouthhp) で Kaggle の[Home Credit Default Risk](https://www.kaggle.com/competitions/home-credit-default-risk) に AutoML で参戦したのでそのときの記録を。
あまり整理されていませんが GitHub リポジトリは [こちら](https://github.com/masachika-kamada/kaggle_home-credit-default-risk)

# モチベーション

今回参加した Home Credit Default Risk のコンペでは、債務不履行の予測を行います。Discussions や Code を眺めて感じたのは、コンペで上位に食い込むには新しい特徴量を作成する必要があり、それを求めるには専門知識が必要であるということです。そんな世界は間違っている！！！ということで **専門知識がなくても高いスコアを出したい！** というのが今回のモチベーションです。

# Microsoft Azure

Azure とは Microsoft のクラウドコンピューティングサービスです。その機能の一つに自動 ML があります。これは、データセットと予測したいカラムなどを指定することで、自動で予測に適したモデルを作成してくれるというものです。ちょうど私が Azure の資格を取得したばかりだったので、Azure の自動 ML を使用して専門知識なしでよいスコアが得られないか、実験を行いました。目標は、「Azure が勝手にメダル圏内のモデル作ってくれる」です。
下は正攻法（普通にプログラムを書いて分析）と自動 ML の作業量を比較した図です。自動 ML が圧倒的にラクそうに見えます。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/873482/5c6834f4-9bea-3120-92c9-bbe3e63262cf.png)

# 実験

正攻法（Kaggleの上位解法）と自動 ML でそれぞれ学習～推論～サブミットを行い、精度を比較しました。プログラムの詳細は GitHub リポジトリをご覧ください。

Azure の自動 ML を行うための作業画面はこんな感じです（詳細は割愛）。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/873482/e1c7b6b8-a698-1259-30da-e0e55340b765.png)
自動 ML の結果画面はこんな感じです。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/873482/6ca245a9-cac0-3ba9-f8a5-b1688d0aa1f8.png)

# 実験結果

結局、自動 ML で正攻法のスコアを超えることはできませんでした。学習時間、学習アルゴリズムなどを変更すればもっとスコアを伸ばすことができるかもしれません。修業が足りないのかも…。（夢破れorz）

|  | private score | public score |
|:---:|:---:|:---:|
| 正攻法 | 0.79023 | 0.79136 |
| 自動 ML | 0.72756 | 0.73050 |

特徴量の重要度も全然違いました。
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/873482/9d2f67e0-d0fd-2c98-f4ba-ecf24a059c88.png)

# まとめ

- 現実はそう甘くない
- 勝手にメダル圏内のモデルは手に入らない
- Azure についてもうちょっと勉強してみれば、もっと上が見えるのかも

# 悲報

リソース放置してたら学生が無料でもらえる100ドル分のクレジットが吹き飛んだので使えなくなりました。もう自力でやるしかありません(笑)

