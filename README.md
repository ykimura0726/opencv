# はじめに

本システムは、スマートフォンで撮影した紙媒体の書類フォームをデジタル化する、というコンセプトのもとで作成している卒業研究のものである。  
具体的には、入力画像を二値化した後に矩形領域を取得するという内容である。

# export_array について

export_array という名前のファイルは、矩形領域取得に関するシステムである。詳細は、export_array ディレクトリの README.md を参照。  
以下では、簡単に実行方法と出力画像の説明を行う。

```
python3 export_array.py
```

Dockerfile によってコンテナ作成後、上のコマンドで export_array.py を実行する。実行後、img.png という.png ファイルが生成されると同時に、ターミナルに番号と 4 つの数字が出力される。  
出力画像にはランダムの色で取得した矩形領域の枠が色付けられ、同じ色で番号が振られる。この番号は、ターミナルに出力された番号と一致する。  
4 つの数字は、左上を原点として、対象の矩形領域について[x座標 y座標]というように、各頂点の座標を示している。
~~左下、左上、右上、右下の順が多いが、一部は左上、右上、右下、左下の順で出力されているときもある。~~  
最新バージョンにて、左上、右上、右下、左下と、左上から時計回りに座標が並ぶよう修正済み。以下はターミナルにおける出力の例である。

```
rect(0):
 [[2231  205]
 [2606  199]
 [2614  705]
 [2239  711]]
rect(1):
 [[ 284  366]
 [2110  351]
 [2111  454]
 [ 285  469]]
 .
 .
 .
```

# OCR について

OCR という名前のファイルは、光学文字認識(Optical Character Recognition)に関するシステムである。詳細は、OCR ディレクトリの README.md を参照。
以下では、簡単に実行方法と出力画像の説明を行う。

```
python3 OCR.py
```

Dockerfile によってコンテナ作成後、上のコマンドで OCR.py を実行する。実行後、img_OCR.png という.png ファイルが生成されると同時に、ターミナルに文字と 4 つの数字が出力される。  
出力画像に認識した文字枠が赤色で色付けられる。4 つの数字は、対象の赤枠の左上の点のx, y座標、右下の点のx, y座標の順にそれぞれの角が何ピクセルにあたるかを示している。わかりやすいよう、最後に抽出した文字のみを再表示している。以下は、ターミナルにおける出力の例である。  
なお、最初の OCR ツールの表示は削除予定である。

```
Tesseract (sh)
Tesseract (C-API)
履 歴
((279, 225), (504, 317))
圭
((557, 222), (646, 279))
過

.
.
.

横24一30mm

2.本人単身胸から上

氏名

3.裏面のりづけ

ふりがな

```

### export_array_ex.py について
export_array_ex.py という名前のファイルは、 export_array と同じく矩形領域を検出する機能に加え、新たにその矩形領域ごとに画像を切り取る機能を追加したものである。  
現段階ではまだ使うことはないが、調査したところ、画像を文字ごとに切り取るとよりOCR の精度が向上するようなので、先に実装を進めた。