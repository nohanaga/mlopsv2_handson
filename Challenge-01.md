# Challenge 1 – ローカルでモデルを作成する

[< Previous Challenge](./Challenge-00.md) - **[Home](./README.md)** - [Next Challenge >](./Challenge-02.md)

## Introduction

この課題の目的は、回帰を使って患者の糖尿病進行度を予測することです。この課題の全体の流れとして、[Diabetes](https://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_diabetes.html) データベースからのヘルスケアデータの処理、分析、回帰モデルの作成と登録、そして最後に マネージド オンライン エンドポイントへのモデルのデプロイが含まれます。このライフサイクル全体は、[Azure Machine Learning CLI v2](https://docs.microsoft.com/azure/machine-learning/concept-v2) を使用して行われます。

今回は、事前にデータエンジニアによってデータウェアハウス内に蓄積されたデータを利用する想定とします。

## Description
多くのデータ サイエンスや機械学習の実験は、ノートブックでコードを実行することによって行われます。Azure Machine Learning の**コンピューティング インスタンス**には、大規模な作業に使用できる完全な機能を備えた Python ノートブック環境 (Jupyter と JuypyterLab) が含まれています。基本的なノートブックの編集には、Azure Machine Learning スタジオに組み込まれている ノートブック ページを使用してチャレンジを行います。今回はこのノートブック実行環境を**ローカル環境**と呼びます。

## Hack

1. Notebooks フォルダ内の `exercise01_train_on_local.ipynb` を開き、セルを上から実行して回帰トレーニングの一連の処理を体験します。最後のセルでは、作成したモデルによる予測結果と精度を出力します。

  **注意:** これはデータサイエンスの領域ですので詳細なモデル開発手法については扱いません。このハックの焦点はデータサイエンスではなく、**MLOps** にあり、ML プロジェクトを加速し、ML ワークフローの効率、品質、一貫性を高めるために、DevOps のプラクティスと原則をどのように適用できるかを理解することにあります。

## 成功基準

- ローカル環境で回帰モデルを作成し予測結果と精度を出力する。モデルの精度の良し悪しは問いません。


## 学習リソース
 - [ワークスペースで Jupyter Notebook を実行する](https://docs.microsoft.com/azure/machine-learning/how-to-run-jupyter-notebooks)
 - [便利なキーボード ショートカット](https://docs.microsoft.com/azure/machine-learning/how-to-run-jupyter-notebooks#useful-keyboard-shortcuts)