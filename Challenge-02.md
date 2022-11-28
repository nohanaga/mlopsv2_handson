# Challenge 2 – クラウドでモデルを作成する

[< Previous Challenge](./Challenge-01.md) - **[Home](./README.md)** - [Next Challenge >](./Challenge-03.md)

## Introduction
これまでは、データサイエンティストが実験的に自分のローカル環境でモデルを作成していました。しかし徐々にモデル作成の試行回数、使用しているノートブックの量が増大し複雑性が増したため、トレーニングコードと対応するモデルの管理が必要とされています。さらに学習に用いるデータの量も増えてきたため、計算需要に柔軟に対応できてコストパフォーマンスに優れた計算資源が必要になってきました。

そして幸運なことにチームに新たなデータサイエンティストが加わりました。作成したモデルやノートブックをチームで共有し始めましたが、あるメンバーでは Python 環境の問題でうまく動作しなかったり、メンバーによって推論結果が異なるなどの問題も出始めています。

この課題の目的は、ローカルで開発していたトレーニングをクラウドにスケールする際の方法論を理解することです。

## Description
クラウド上でモデルをトレーニングするための一般的な方法は、[環境](https://learn.microsoft.com/ja-jp/azure/machine-learning/concept-environments)、[コンピューティング ターゲット](https://learn.microsoft.com/ja-jp/azure/machine-learning/concept-compute-target)、[トレーニング Python スクリプト](https://learn.microsoft.com/ja-jp/azure/machine-learning/how-to-train-model?tabs=azurecli#4-submit-the-training-job)をそれぞれ作成し、実行構成 YAML としてパッケージ化します。その後、実行構成をクラウドに送信してトレーニングジョブを起動します。[Challenge 1](./Challenge-01.md) では 1 つの Notebook 上ですべてが完結しましたが、今回はなぜこうする必要があるのでしょうか。得られるメリットについてチームで議論します。

機械学習モデルの作成は、ローカル コンピューター上で開始し、後でクラウドベースのクラスターにスケールアウトするのが一般的です。Azure Machine Learning では、トレーニング スクリプトを変更しなくても、さまざまなコンピューティング先でトレーニング スクリプトを実行できます。

ソフトウェアの依存関係の管理は、開発者にとって一般的なタスクです。手動による煩雑なソフトウェア構成を行わずに、モデル作成を再現できることを保証する必要があります。**環境**には、Python パッケージ、環境変数、およびソフトウェア設定を指定します。

## Hack
1. 新しいノートブックを作成します。
1. Azure Machine Learning クラウドでトレーニングを実行するための**トレーニング スクリプト**を作成します。今回は事前に提供された `./scripts/train.py` の中身を参照し、前のチャレンジで Notebook セルに記載されているコードと見比べながら差異を明らかにします。
1. Azure Machine Learning ワークスペースにコンピューティング クラスターを作成します。
1. 事前に提供された conda 環境仕様 YAML ファイル `environments/02_diabetes-env.yml` をロードしてカスタム **環境**を作成します。
1. **トレーニング スクリプト**と**環境**、**コンピューティング クラスター**を**推論構成** `02_train_on_remote.yml` としてパッケージ化します。
1. **ジョブ**を作成しクラウド上に送信して実行します。状況はスタジオ UI 上からも確認できます。
1. リモート トレーニングの完了後に `models` フォルダー（リモート上）に出力されたモデルとジョブ結果ファイル `metric.json` をローカル環境にダウンロードします。
1. 作成したモデルを Azure Machine Learning モデルレジストリに登録します。

**注意**: Azure Machine Learning によって Docker イメージをビルドし、設定に従って、そのコンテナー内に Python 環境が作成されます。Docker イメージはキャッシュされて再利用されます。通常、新しい環境での最初の実行時だけイメージがビルドされるため時間がかかります。10~15 分ほどお待ちください。


## 成功基準
- トレーニング Python スクリプトのコードを理解すること。
- 実行構成(YAML) に環境、コンピューティング クラスター、トレーニング Python スクリプトをセットし、ジョブを送信すること。
- リモート環境で回帰モデルを作成し、モデルをローカル環境にダウンロードすること。
- 作成したモデルを Azure Machine Learning モデルレジストリに登録すること。

<br>

## ヒント
- トレーニング スクリプトにはコマンドライン引数を渡すことができます。指定方法は[こちら](https://learn.microsoft.com/ja-jp/azure/machine-learning/reference-yaml-core-syntax#parameterizing-the-command-with-the-inputs-and-outputs-contexts-of-a-job)を参照。
 - [CLI (v2) を使用した Azure Machine Learning 環境の管理](https://learn.microsoft.com/azure/machine-learning/how-to-manage-environments-v2?tabs=cli)
 - [CLI (v2) を使用してモデルをトレーニングする](https://learn.microsoft.com/azure/machine-learning/how-to-train-model?tabs=azurecli#train-a-model-with-a-custom-script)
 - [CLI (v2) を使用してコンピューティングクラスターを作成する](https://learn.microsoft.com/azure/machine-learning/how-to-train-model?tabs=azurecli#2-create-a-compute-resource-for-training)

## 学習リソース
 - [Azure Machine Learning 環境とは?](https://learn.microsoft.com/azure/machine-learning/concept-environments)
 - [リファレンス: CLI (v2)](https://learn.microsoft.com/cli/azure/ml?view=azure-cli-latest)
 - [リファレンス: CLI (v2) YAML スキーマ](https://learn.microsoft.com/azure/machine-learning/reference-yaml-overview)