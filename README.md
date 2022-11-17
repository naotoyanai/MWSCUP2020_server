# Summary
The server-side in MADMAX classifies the received domain as malicious or benign by using the trained ELM model, and returns the result to the user side.
Specifically, the server obtains nine features from the received domain, as shown in the following literature, and uses them as input to the ELM.

Shi et al., “Malicious Domain Name Detection Based on Extreme Machine Learning”, Neural Process Lett 48, 1347–1357, 2018

A user can use MADMAX by installing Firefox addons in the following repository: 

https://github.com/kzk-IS/MWSCUP2020_addon

# Algorithm

Input : domain

Output : result (0 : benign, 1: malicious)
1. obtain 9 features from the domain according to the literature. 

2. take the features obtained as input and determine whether the domain is malicious or benign. 

3. send the prediction result (0 or 1) to the user side

# Feature Extraction
The following 9 features are used: 

1. ドメイン名の文字数  
ドメイン名に含まれる全文字数  
例: 13 (osaka-u.ac.jp)
2. 連続文字の最大連続数  
ドメイン名において、連続する文字の最大長  
例: 3 (aaabcbbb.jp)
3. ドメイン名のエントロピー  
各文字の出現回数を{*c<sub>1</sub>, c<sub>2</sub>, ... c<sub>n</sub>*}、
ドメイン名の全文字数を*d*としたとき、
その頻度*p<sub>i</sub>=c<sub>i</sub> / d*を用いて、エントロピー*E*は
以下のように表すことができる  
    <img src="https://latex.codecogs.com/gif.latex?\begin{align*}&space;E&space;=&space;-&space;\sum_{i=1}^{n}&space;p_{i}&space;\times&space;\log_{2}p_{i}&space;\end{align*}" />  
例: 3.180832987205441 (osaka-u.ac.jp)
4. ドメインに紐づけられたIPアドレス数  
5種類のDNSサーバ `1.1.1.1`, `8.8.8.8`, `208.67.222.123`, `176.103.130.130`, `64.6.64.6`
に介してドメインに紐づけられたIPアドレスを探し、その種類を数える  
例: 3 (github.com)
5. IPアドレスの所属する国数  
上記IPアドレスが割り振られた国を検索し、その種類を数える  
例: 1 (github.com)
6. Time To Live (TTL) の平均値  
上記DNSサーバへの問い合わせ時に取得したTTL値の平均  
例: 53667 (osaka-u.ac.jp)
7. TTLの標準偏差  
上記DNSサーバへの問い合わせ時に取得したTTL値の標準偏差  
例: 102768.95645475826 (osaka-u.ac.jp)
8. ドメインの有効日数  
whoisサーバに登録されたドメインの情報から、ドメインの作成日から有効期限までの日数を計算する  
例: 2268 (osaka-u.ac.jp)
9. ドメインのアクティブ日数  
whoisサーバに登録されたドメインの情報から、ドメインの作成日から直近の更新日までの日数を計算する  
例: 1904 (osaka-u.ac.jp)

# Training

The ELM model in the server was trained using a real dataset newly created by extracting the features described earlier. The size of the dataset is 4000 cases (malignant domain: 2000 cases, benign domain: 2000 cases).

Roughly speaking, we trained the structure of domains as generated by the Domain Generation Algorithm and the features of domains that are valid only for a short period of time to be used for attacks.

Cross-validation was conducted to measure the performance of the learned ELM models, and the results showed an accuracy rate of 90.1%.


# Environment
- Amazon Linux AMI release 2018.03
- Node.js v12.18.3
- npm 6.14.6

# How to use

- Install Node.js (v12.18.3) from https://nodejs.org/ja/download/
- Run the terminal and check each version
    - `npm -v` --> output 6.14.6
    - `node -v` --> output v12.18.3
- Move to a directory to construct the server environment
- `mkdir http_server` 
- `cd http_server`
- `npm install @tensorflow/tfjs-node` 

# Contributors
- [kzk-IS](https://github.com/kzk-IS)
- [akazs](https://github.com/akazs)
- [nanana710](https://github.com/nanana710)
- [han9umeda](https://github.com/han9umeda)
- [takemr](https://github.com/takemr)
- [flabrei926](https://github.com/flabrei926)

