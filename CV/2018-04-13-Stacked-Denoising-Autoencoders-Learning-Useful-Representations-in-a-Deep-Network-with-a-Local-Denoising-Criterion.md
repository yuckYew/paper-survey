## 1. どんなもの？
ノイズ付きの入力から原画像を復元するように学習を行うdenoising autoencoderを提案.

## 2. 先行研究と比べてどこがすごいの？
通常のオートエンコーダと比較して,本手法によってdenoising autoencoderは画像からGabor-likeエッジ特徴,数字画像からは筆跡のストローク特徴を学習することができる.
また,本手法である教師なし学習によって得られた高次な特徴表現はSVM識別器などの精度向上にも貢献している.

## 3. 技術や手法の"キモ"はどこにある？
従来のbottleneckやsparse表現などの様に中間表現そのものに制約を加えるのではなく,Autoencoderの復元基準に変更を加えた.
単純な入力の最構成を行い恒等関数を学習する代わりにdenoising,つまりノイズ付与入力画像から雑音を取り除くように学習を行った.
本アプローチでは以下の2つの考えを暗に示している.
1. 高次な特徴表現は比較的安定し,ノイズにも頑健であることが期待できる
2. denoisingタスクを上手に行う上でモデルは入力分布をよく表す特徴を抽出する必要があることが期待できる

本研究の目的は入力画像のノイズ除去ではなく,その過程で得られる入力をより良く表す高次特徴表現の獲得である.

## 4. どうやって有効だと検証した？
学習済みの特徴表現の重みをNN等の識別器の初期値に採用することで,識別器の精度から表現の有効性を定量的に評価することができる
また同様に各隠れ層を直接Linear SVMの入力として与えて性能評価を行った.
ベンチマークより,従来手法であるDBNの識別性能と互角,もしくはそれ以上の結果が得られた.

## 5. 議論はあるか？
deep denoising autoencodersの検討など
ノイズの加え方に対するさらなる検証の必要性

## 6. 次に読むべき論文はあるか？
[Stacked Convolutional Denoising Auto-Encoders for Feature Representation](https://pdfs.semanticscholar.org/7da5/bb40e171c7cc9cffe82e66eea4faff936fc7.pdf)

### 論文情報・参考サイト
http://www.jmlr.org/papers/volume11/vincent10a/vincent10a.pdf
