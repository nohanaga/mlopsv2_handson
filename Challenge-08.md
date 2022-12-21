# Challenge 8 – Github Actions/Azure DevOps によるオーケストレーション（ストレッチ課題）

[< Previous Challenge](./Challenge-07.md) - **[Home](./README.md)**

## Introduction
Proseware 社の機械学習エンジニアは、多くの技術関係者と協力しています。糖尿病進行度予測モデルをトレーニングしたデータサイエンスチームと協力することに加えて、モデルを使用する Web アプリケーション（開業医が使用）を担当するソフトウェア開発者とも協力します。

現場からの新しい要件に適応するために、Web アプリは時間の経過とともに更新されます。同様に、モデルも時間の経過とともに変更されることが予想されます。データのドリフトやモデルのパフォーマンスの低下がある場合は常に、データサイエンスチームはモデルを修正し、それに応じてコードを更新するように求められます。

Proseware 社では GitHub を使用してコードをバージョン管理しているため、MLOps 戦略のオーケストレーションおよび自動化ツールとして GitHub Actions を使用することが決定されました。

## Description

GitHub Actions は、GitHub 内からソフトウェア開発ワークフローを自動化するのに役立ちます。 コードを保存する場所と同じ場所にワークフローをデプロイし、プルリクエストや Issues に対して共同作業を行うことができます。GitHub Actions の Workflow とは、お使いの GitHub リポジトリで設定する自動化されたプロセスです。 Workflow を使用すると、任意のプロジェクトを GitHub でトレーニング、テスト、パッケージ化、リリース、またはデプロイできます。

今回は [Challenge 4](./Challenge-04.md) で作成したトレーニングパイプラインをコードコミットによってトリガーするアクションを作成します。すでに [Challenge 6](./Challenge-06.md) でデプロイパイプラインを Github Actions で構築済みのため、これでトレーニングとデプロイの 2 つのパイプラインを自動化できるようになります。

## Hack

**本演習では参加者が利用している CI/CD ツールに合わせて複数の技術の中から選択して実装することができます。**

MLOps オーケストレーションを実現するための[複数のテクノロジーの違い](https://learn.microsoft.com/azure/architecture/example-scenario/mlops/aml-decision-tree)を理解し、チームで取り組むテクノロジーを選択してください。下記のいずれかを満たす必要があります。

1. Github Actions の Workflow を使ってパイプラインを実装しコードコミット駆動を使用します。
1. Azure DevOps の Azure Pipelines を使ってパイプラインを実装しコードコミット駆動を使用します。

### 1. Github Actions

Azure Machine Learning コンピューティング クラスターを使用してモデルトレーニングをトリガーする GitHub  Actions を作成するには、次のことを行います。

1. Azure CLI を使用してサービスプリンシパルを作成します。
1. サービスプリンシパルのクレデンシャルをシークレットとして GitHub に保存します。
1. GitHub Actions を作成して、Azure Machine Learning トレーニングパイプラインを起動します。

**Github Actions の全手順解説は[こちら](./Solutions/Solution-Challenge-08-1.md)を参照してください。**

### 2. Azure DevOps
Azure Pipelines を使えば今回作成した機械学習パイプラインと同等のものを実装できますし、コードコミット駆動やリリース ゲートと承認機能を追加することができます。経験のあるエンジニアは Azure Pipelines でトレーニング・デプロイパイプラインを構築しても構いません

  **注意:** 無料アカウントもしくは Azure Pass で Azure DevOps を使用している場合、パイプライン実行時に Requiest Form があり申請に 2,3 日かかります。**すでにパイプラインが実行可能な方のみ**選択してください。

**Azure DevOps の全手順解説は[こちら](./Solutions/Solution-Challenge-08-2.md)を参照してください。**


## 成功基準
- 選択したテクノロジーを使用して任意のトリガーによってパイプラインを起動できること。

<br>

## ヒント
 - [モデルトレーニングに GitHub Actions を使用する](https://learn.microsoft.com/training/modules/trigger-azure-machine-learn-jobs-github-actions/4-use-for-model-training)

## 学習リソース
 - [GitHub Actions で開発タスクを自動化する方法](https://learn.microsoft.com/training/modules/github-actions-automate-tasks/2-github-actions-automate-development-tasks)
 - [Github Actions: ワークフローについて](https://docs.github.com/actions/using-workflows/about-workflows)
 - [Github Actions: ワークフローをトリガーするイベント](https://docs.github.com/actions/using-workflows/events-that-trigger-workflows)
 - [トランクベースの開発で GitHub Actions をトリガーする](https://learn.microsoft.com/training/modules/trigger-github-actions-trunk-based-development/)