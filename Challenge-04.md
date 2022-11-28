# Challenge 4 – トレーニングパイプラインの作成

[< Previous Challenge](./Challenge-03.md) - **[Home](./README.md)** - [Next Challenge >](./Challenge-05.md)

## Introduction
目標の精度を達成した予測モデルと魅力的なビジュアライズの効果もありプロジェクトは上層部の支持を得ることができ、定常的な社内プロジェクトとして昇格しました。今後は技術の横展開や他のシステムのデータに対して同様の予測を行うことが求められています。それに伴いデータサイエンティストの作業量は増大しており、より高度な並列化・自動化が必要です。現状は各々のデータサイエンティストがノートブック上でモデル作成のためのコードを記述しており、中には車輪の再発明的な無駄な作業が生じたり、モデル作成に必要な前処理の一つが抜けてしまったり、うまく共同作業ができなかったりしています。さらに情報システム担当役員からモデルの品質管理の強化に関する通達が出され、品質管理部門の監査に対してレポートする際の実験証跡も管理する必要があります。

この課題の目的は、**機械学習パイプライン**を使用して、機械学習ワークフローの構築、最適化、管理を行う方法について理解することです。

## Description
**機械学習パイプライン**を使用し、機械学習フェーズをつなげるワークフローを作成して管理します。たとえば、パイプラインには、データ準備、モデル トレーニング、モデル デプロイ、推論/スコアリングの各フェーズが含まれることが考えられます。それぞれのフェーズには、複数のステップを含めることができ、各ステップは、さまざまなコンピューティング先において無人実行することができます。

![aml-pipelines-concept](./images/004.png)

機械学習の各フェーズをパイプライン化することのメリットを[解説](https://learn.microsoft.com/azure/machine-learning/concept-ml-pipelines)を参照しながらチームで議論します。

Azure Machine Learning のパイプラインの複数のステップを組み合わせて構成して、共有可能で再利用可能な Azure Machine Learning ワークフローであるパイプラインを構築できます。 パイプラインの各ステップは、ステップの内容 (スクリプトと依存関係) に加えて入力とパラメーターが変更されていない場合に、以前の実行結果を再利用できるように構成することができます。

## Hack
1. 新しいノートブックを作成します。
1. パイプライン定義 YAML `04_training_pipeline_job.yml` を作成します。
    1. `train.py` を使用してトレーニングを実行する 1 つ目のパイプライン ステップを定義します。
    1. `register.py` を作成してモデルを登録する 2 つ目のパイプライン ステップを定義します。
1. パイプライン ジョブを送信します。
1. AML スタジオ上から、パイプラインを発行します。
1. AML スタジオ上から、発行されたパイプラインを実行します。

## 成功基準
- 機械学習プロセスをパイプライン化することのメリットをコーチに説明します。
- 作成したパイプラインのステップが `[train, register]` の 2 ステップで構成されていること。
- パイプライン ジョブが正常に実行されること。
- パイプラインエンドポイントにパイプラインがアクティブ状態で登録されていること。
- 発行されたパイプラインが正常に実行されること。

<br>

## ヒント
 - [CLI (v2) パイプライン ジョブ サンプル集](https://learn.microsoft.com/azure/machine-learning/reference-yaml-job-pipeline#examples)

## 学習リソース
 - [Azure Machine Learning パイプラインとは](https://learn.microsoft.com/azure/machine-learning/concept-ml-pipelines)
 - [Azure Machine Learning CLI でコンポーネントを使用して機械学習パイプラインを作成して実行する](https://learn.microsoft.com/azure/machine-learning/how-to-create-component-pipelines-cli)
 - [リファレンス: CLI (v2) パイプライン ジョブの YAML スキーマ](https://learn.microsoft.com/azure/machine-learning/reference-yaml-job-pipeline)
 


## さらなる学習
 - トレーニングパイプラインは、Azure DevOps や Github Actions を使っても構築することができます。Azure DevOps/Github Actions を使って本チャレンジのパイプラインを構築してください。
 - データ加工フェーズをパイプライン化することも重要です。データ変換ステップを追加してパイプラインを構築してください。