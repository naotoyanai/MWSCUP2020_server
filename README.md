# 概要
ELM Blockerのサーバ側では受け取ったドメインから，学習済みのELMモデルを用いて，悪性ドメインか良性ドメインかを分類しユーザ側にその結果を返す．

# アルゴリズム

入力 : ドメイン(例 : osaka-u.ac.jp)

出力 : 予測結果(0 : 良性, 1: 悪性)
1. ドメインから文献~に準ずる9つの特徴量の取得
2. 取得した特徴量を入力とし，ELMを用いて悪性ドメインまたは良性ドメインを判別
3. 予測結果をユーザ側へ送信

# 特徴量取得

# 実行環境
- Node.js v12.18.3
- npm 6.14.6

# 環境構築

- https://nodejs.org/ja/download/ からNode.jsのインストール(v12.18.3)
- ターミナルを起動，各バージョン確認
    - `npm -v` 出力結果 6.14.6
    - `node -v`  出力結果 v12.18.3
- server環境を構築したいディレクトリに移動
- `mkdir http_server` ディレクトリ作成
- `cd http_server`
- `npm init` Nodejs環境を初期化
- `npm install @tensorflow/tfjs-node` //tensorflow.jsのNode.jsに最適化されたライブラリをinstall

# 実行手順     

# デモ

