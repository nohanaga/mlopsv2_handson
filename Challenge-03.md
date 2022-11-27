# Challenge 3 – クラウドにモデルをデプロイする

[< Previous Challenge](./Challenge-02.md) - **[Home](./README.md)** - [Next Challenge >](./Challenge-04.md)

## Introduction
データサイエンティストチームと現場部門のコラボレーションによりモデルの精度が上層部に見せられるレベルまで高まりました。それを知った事業企画担当メンバーから、すぐにチームに対してモデルの予測値を Web アプリ Mock にデモとして表示して上層部にプレゼンしたいとの要求が寄せられており、メンバーは作成した最も精度の良いモデルをホスティングして HTTP リクエストに応じて推論を行うエンドポイントを構築しなければなりません。ただデータサイエンティストにとって独自に Web アプリケーションサーバーを立ち上げてモデルをホスティングし、REST エンドポイントを運用することは技術的に困難であったり、担当領域外であることが多く、できれば構築・運用・管理はやりたくありません。

この課題の目的は、作成した機械学習モデルを Azure Machine Learning に登録し、Web サービスとして Azure クラウドにデプロイする方法を理解することです。

## Description

Web サービスとしてモデルをデプロイする場合、マネージド オンライン エンドポイント、Kubernetes オンライン エンドポイント にデプロイできます。また、オンプレミスの IoT Edge デバイスおよび Azure Stack Edge デバイスに、モデルを同様にデプロイすることもできます。モデル、スコアリング スクリプト、および関連ファイルからサービスを作成します。これらは、モデルの実行環境を含むベース コンテナー イメージに配置されます。イメージには、Web サービスに送信されるスコアリング要求を受け取る、負荷分散された[エンドポイント](https://docs.microsoft.com/azure/machine-learning/concept-endpoints)があります。

次の図は、リアルタイムの推論に使用される**オンライン エンドポイント**を示しています。オンライン エンドポイントには、クライアントからデータを受信する準備が整い、リアルタイムで応答を返信できる**デプロイ**が含まれています。

![モデルの推論ワークフロー](./images/003.png)

図と[解説](https://docs.microsoft.com/azure/machine-learning/concept-endpoints#online-deployments-requirements)を見ながらオンライン デプロイの要件ついて理解してから、以下のタスクを完了させます。

## Hack
1. 新しいノートブックを作成します。
1. Azure クラウドで推論を実行するための**スコアリング スクリプト**を作成します。今回は事前に提供された `./scripts/score.py` の中身を参照し、[Challenge 1](./Challenge-01.md) で Notebook セルに記載されているコードと見比べながら差異を明らかにします。
1. オンライン エンドポイントの名前と認証方法を指定して `03_managed_endpoint.yml`　を作成し、**マネージド オンライン エンドポイント**を作成します。
1. サービング用の conda 環境仕様 YAML ファイル `03_conda_env.yml` を作成します。
1. **エンドポイント名**、**モデル名**、**スコアリング スクリプト**と**環境**、マネージド オンライン エンドポイントを実行するために必要とするメモリとコアの量を指定した `03_managed_deployment.yml` を定義して マネージド オンライン エンドポイント に**デプロイ**します。状況はスタジオ UI 上からも確認できます。
1. マネージド オンライン エンドポイントをテストします。


## 成功基準
- スコアリング Python スクリプトのコードを理解すること。
- マネージド オンライン エンドポイントが正常に作成されること。
- スクリプトの実行構成に環境、コンピューティング ターゲット、スコアリング Python スクリプトをセットし、リアルタイムエンドポイントのデプロイに成功(プロビジョニングの状態が**成功**)すること。
- マネージド オンライン エンドポイントにリクエスト送信し推論結果が返却されること。

<br>

## ヒント
 - [オンライン エンドポイントを使用して機械学習モデルをデプロイおよびスコア付けする](https://docs.microsoft.com/azure/machine-learning/how-to-deploy-managed-online-endpoints)

## 学習リソース
 - [Azure Machine Learning エンドポイントとは](https://docs.microsoft.com/azure/machine-learning/concept-endpoints)
 - [リファレンス: CLI (v2) az ml environment](https://docs.microsoft.com/cli/azure/ml/environment?view=azure-cli-latest)
 - [リファレンス: CLI (v2) az ml online-endpoint](https://docs.microsoft.com/cli/azure/ml/online-endpoint?view=azure-cli-latest)
 - [リファレンス: CLI (v2) az ml online-deployment](https://docs.microsoft.com/cli/azure/ml/online-deployment?view=azure-cli-latest)
 