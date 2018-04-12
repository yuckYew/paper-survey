## 1. どんなもの？
Stacked RBMによって初期化されたAutoencoderをBackpropagationによってfine-tuningしたモデルを用いて32x32の入力画像から28-bitおよび256-bitのバイナリ列(ハッシュ)を取得.
取得したハッシュから文書検索に有効な手法であるSemantic Hashingを画像に転用し画像のContent-based Image Retrieval System(類似症例検索システム)の構築を提案した.

## 2. 先行研究と比べてどこがすごいの？
上述したモデルにカラー画像から得られた384次元のGIST記述子を入力に用いた先行研究[8]と比較して,本研究では原画像を入力に用いている.
[9]では高次元データに対して,"spectral"な手法を採用してバイナリ列を生成し, [8]より限定的な状況でより有効であることを示した.

## 3. 技術や手法の"キモ"はどこにある？
得られるハッシュをバイナリ列に変換するため,中心のコードを出力する層を1か0に四捨五入している.この操作による2値化は[6]で採用された手法と同程度に有効でシンプルにコード層にノイズを付加することができる.
Autoencoderにて行ったfine-tuningによって,RBMの重みは多少しか変化しなかったものの,復元画像の精度は著しく改善された.

## 4. どうやって有効だと検証した？
8000万枚から構成されるで画像データセットのサブセットを2つ用いてモデルのテストを行った.
ノイズの多いデータラベルは学習には使用しなかった.
160万個の256-bitバイナリ列の線形検索は,pixel空間でユークリッド距離を指標とした検索より高い精度を示し,計算時間も1000倍高速であった.

### メモ
ユークリッド距離を指標にした検索では,平滑な画像が類似画像としてヒットすることが多い. 画像の高周波成分をマッチングできない場合,pixelの平均値を合わせることで距離を最小化するiことができる. 画像認識において低次なpixelより画像に含まれる物体といった高次な情報のほうが重要.

## 5. 議論はあるか？
本研究は,先行研究と比較して入力画像からより良いsemantic(意味的な)情報を抽出することができ,なおかつ検索においてデータベースの規模によりよくスケールすることができる.

## 6. 次に読むべき論文はあるか？
[6] Semantic hashing. In Proceedings of the SIGIR Workshop on Information Retrieval and Applications of Graphical Models, Amsterdam, 2007.

### 論文情報・参考サイト
http://www.cs.toronto.edu/~fritz/absps/esann-deep-final.pdf
https://www.youtube.com/watch?v=MSYmyJgYOnU

## メモ
Binary Discriptor(画像は屋外か屋内か？, RGBかGreyScaleか?等)

Euclidean Distance will retreive smooth images 
If you cant match high frequency variation of the images, its better to match its average. pixel space. more sensitive to objects than pixel intensities
