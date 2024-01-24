# What is GPT ?  
## 1. GPTとは
GPTとは，Transformerベースの学習済み大規模言語モデルである．  
教師なし学習による事前学習と教師あり学習によるファインチューニングを組み合わせた，半教師あり学習という手法を使用している．  
![画像1](https://github.com/haradakaito/GPT/assets/75819611/b804b76e-7379-44ec-b843-2f4cc8f0a41d)

### 1.1. 教師なし学習フェーズ
教師なし学習フェーズでは，大量のテキストコーパスから得たトークン列に対して，マルチヘッドセルフアテンション機構を持つTransformerデコーダによって，次に続く単語の出現確率が最大になるように学習を進めていく．  
![画像13](https://github.com/haradakaito/GPT/assets/75819611/5d8f56ff-6350-4679-bfd7-c56958d61487)

#### 1.1.1. 事前学習用データセットについて
教師なしフェーズの事前学習用データとしては，Smashwordsと呼ばれる無料小説本(11038冊)に関する大規模テキストコーパス(約4.5GB)を用いて，キャラクターの心情変化やストーリの状況変化などをモデルに学習させている．  
前処理として，ffty2.0によるUnicord問題の修正，SpaCy3.0を用いたトークナイズを行っている．  

### 1.2. 教師あり学習フェーズ
教師なしフェーズによって事前学習されたモデルに対して，解きたいタスクに応じてファインチューニングを行っていく．  
汎用性の高いモデルを実現するため，ファインチューニングを行う際のアーキテクチャがタスクごとに同質のアーキテクチャで行えるように工夫されている．  
![画像3](https://github.com/haradakaito/GPT/assets/75819611/996e36bd-4265-4ced-9e64-0c049fbe656c)

### 1.3. GPT-1の性能評価
#### 1.3.1. 自然言語推論(NLI)タスク
次に続く単語を予測するタスクに対しては，5つのデータセットで評価され，内4つのデータセットに対して当時の言語モデルを超える精度を達成している．これによって複合文に対する合理的推論や，言語的曖昧性の処理能力が示された．  
![画像4](https://github.com/haradakaito/GPT/assets/75819611/43f3143d-6e08-43ac-99ab-f1d9a43a6616)

#### 1.3.2. 質問応答(QA)タスク
質問文に対して適切な回答を行うタスクに対しては，2つのデータセットで評価され，すべてのデータセットに対して当時の最高精度を達成している．これにより，長文の文脈を効果的に捉えて回答できることが示された．  
![画像5](https://github.com/haradakaito/GPT/assets/75819611/21343caa-633a-4e90-b7c4-2c3b7d593218)

#### 1.3.2. テキスト分類・意味的類似性タスク
テキストの類似性を判別するタスクに対しては，5つのデータセットで評価され，内3つのデータセットに対して従来よりも大幅な改善を実現している．  
![画像6](https://github.com/haradakaito/GPT/assets/75819611/66c7113a-0b9b-49ae-95d9-e3e2a8c26e5a)

## 2. GPT-2への進化
GPTよりも多様なタスクに対応可能な汎用的な言語モデルを実現することを目指した．  
モデルの構造自体はあまり変化しておらず，学習用データが大幅に増加したことに伴って，学習モデルのパラメータが増加している．  

### 2.1. GPT-2のZero-Shot学習用データについて
redditと呼ばれる掲示板型ソーシャルニュースサイトをクローリングすることによって独自の学習データセット(約40GB)を作成している．  
Wikipediaをクローリングすることは，評価データセットに対してリーケージを避けるために使用されなかった．  
また，BPE(Byte Pair Encording)と呼ばれる文字列をByte文字列に変換した後にBPE圧縮することにより，学習コストを低減し，より多くの単語を覚えることができるようになっている．  

### 2.2. GPT-2の性能評価
読解，翻訳，要約，質疑応答タスクに関するGPT-2の性能比較を行うために，各タスク1つのデータセットを用意している．  
すると，単一のZero-Shotモデルの性能としては非常に高いが，特定タスク専門の他モデルに比べればまだまだ精度面で劣る結果となった．  
![画像8](https://github.com/haradakaito/GPT/assets/75819611/e3079d07-7cd8-4c02-b011-023c5e60ed2b)

## 3. GPT-3への進化
GPT-2よりもさらに大量のデータ(約570GB)で，より大規模なモデルを学習させることで精度向上を図った．  
特定タスクに特化したモデルよりも精度の高い汎用モデルの実現を目指した．  

### 3.1. GPT-3の性能評価
#### 3.1.1 単語予測タスク
任意の文の最後の単語を予測するタスクでは，2つのデータセットのすべてで当時のSOTAを達成した．  
これは，学習データ量が大幅に増加したことによる恩恵だと考えられる．  
![画像9](https://github.com/haradakaito/GPT/assets/75819611/e9c6887a-f7d9-4518-a16c-122c3a84e4d9)

#### 3.1.2. 質問応答タスク
TriviaQAデータセットに対して，SOTAを達成している．質問応答に特化したモデルを超えているため，GPT-3の性能の高さが見て分かる．  
![画像10](https://github.com/haradakaito/GPT/assets/75819611/ca7bde07-5cdb-453c-ae24-d07991e11c70)

#### 3.1.3. 翻訳タスク
フランス語/ドイツ語から英語への翻訳でSOTAを達成した．  
あくまで確率的に高い単語を並べるだけで翻訳タスクを解くことができることを示した．  
![画像11](https://github.com/haradakaito/GPT/assets/75819611/882887b6-c8d1-4918-9b07-9dd42ff167a4)

※ここからさらにUIやRLHF強化学習，画像とのマルチモーダル学習によって，GPT-3.5，GPT-4などの進化モデルに繋がっていく  

## 参考
GPT：RADFORD, Alec, et al. Improving language understanding by generative pre-training. 2018.  
GPT-1：RADFORD, Alec, et al. Language models are unsupervised multitask learners. OpenAI blog, 2019, 1.8: 9.  
GPT-2：Brown, Tom, et al. "Language models are few-shot learners." Advances in neural information processing systems 33 (2020): 1877-1901.  
