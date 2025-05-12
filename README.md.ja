![Image](./SampleFigures/pyhrv.png)

![GitHub Version](https://img.shields.io/badge/GitHub-v.0.4.1-orange.svg)
[![PyPi Version](https://img.shields.io/pypi/v/pyhrv.svg)](https://pypi.org/project/pyhrv/)
![Python Versions](https://img.shields.io/badge/python-3.X-blue)
[![Issues](https://img.shields.io/github/issues/PGomes92/pyhrv.svg)](https://github.com/PGomes92/pyhrv/issues)
![Development](https://img.shields.io/badge/development-active-green.svg)
[![Documentation Status](https://readthedocs.org/projects/pyhrv/badge/?version=latest)](https://pyhrv.readthedocs.io/en/latest/)
![Downloads](https://img.shields.io/pypi/dm/pyhrv.svg)
![License](https://img.shields.io/pypi/l/pyhrv.svg)

pyHRVは、心電図（ECG）、SpO2、血液量脈波（BVP）、またはその他の心拍数指標を含む信号から最先端の心拍変動（HRV）パラメータを計算するオープンソースのPythonツールボックスです。

pyHRVでは、HRV専用の教育、研究、およびアプリケーション開発のためのユーザーフレンドリーで多目的なPythonツールボックスを提供することを目指しています。

初心者がHRVパラメータ計算の基礎を理解するのに役立つ理解しやすいソースコードを提供すると同時に、開発者には最も重要なHRV分析機能を提供し、研究者には結果の出版品質のプロットを提供します。
# はじめに

### インストール & Python互換性
このツールボックスは`pip`ツールを使用してインストールできます。

```python
pip install pyhrv
```
依存関係: [biosppy](https://github.com/PIA-Group/BioSPPy) | [numpy](http://www.numpy.org) | [scipy](http://scipy.org) | [matplotlib](https://matplotlib.org) | [nolds](https://github.com/CSchoel/nolds) | [spectrum](https://github.com/cokelaer/spectrum)

pyHRVは主にPython 3.Xで維持されていますが、バージョン0.4.0までPython 2.7でもテストされています。


### ドキュメント & チュートリアル
詳細なpyHRVドキュメントはReadTheDocsで利用可能です：

[pyHRV APIリファレンス](https://pyhrv.readthedocs.io)

追加のチュートリアルはこちらで見つけることができます：

- [pyHRV クイックスタートガイド](./pyhrv/README.md)

- [チュートリアル: ECG取得からpyHRVによるHRV分析まで](https://pyhrv.readthedocs.io/en/latest/_pages/tutorials/bitalino.html)

- [チュートリアル: pyHRVによる一括処理](https://pyhrv.readthedocs.io/en/latest/_pages/tutorials/bulk.html)

### 科学的背景
HRVアルゴリズムは、[心拍変動 - 測定基準、生理学的解釈、および臨床使用ガイドライン](https://www.ahajournals.org/doi/full/10.1161/01.CIR.93.5.1043)に従って開発および実装されています。その他の参考文献はコード内および[pyHRVリファレンス](./pyhrv/files/references.txt)に記載されています。

### pyHRVの引用
あなたの研究でpyHRVを引用する場合は、以下の会議論文を使用してください（[会議論文 [PDF]](https://drive.google.com/open?id=1enItjdVXkTYX_h2DkgDl2v8vXAe09QJv)、[会議プロシーディングス [PDF]](https://etran.rs/2019/Proceedings_IcETRAN_ETRAN_2019.pdf)）：

*P. Gomes, P. Margaritoff, and H. P. da Silva, "pyHRV: Development and evaluation of an open-source python toolbox for
 heart rate variability (HRV)," in Proc. Int'l Conf. on Electrical, Electronic and Computing Engineering (IcETRAN), pp. 822-828, 2019*

```latex
@inproceedings{Gomes2019,
   author = {Gomes, Pedro and Margaritoff, Petra and Silva, Hugo},
   booktitle = {Proc. Int'l Conf. on Electrical, Electronic and Computing Engineering (IcETRAN)},
   pages = {822-828},
   title = {{pyHRV: Development and evaluation of an open-source python toolbox for heart rate variability (HRV)}},
   year = {2019}
}
```

# pyHRVの主な機能 & HRVパラメータリスト

pyHRVを使用すると、最大78のHRVパラメータを計算しながら、HRV研究をサポートするための他の有用なパラメータ固有でないツールを使用できます。

### 時間領域パラメータ

- NNI系列の基本統計パラメータ - ```pyhrv.time_domain.nni_parameters()``` 
- ΔNNI系列の基本統計パラメータ - ```pyhrv.time_domain.nni_differences_parameters()```
- 心拍数（HR）系列の基本統計パラメータ - ```pyhrv.time_domain.hr_parameters()``` 
- NNI系列の標準偏差（SDNN） - ```pyhrv.time_domain.sdnn()``` 
- 長期NNI系列から抽出された連続する5つの5分セグメントのSDNNの平均（SDNN<sub>index</sub>）- ```pyhrv.time_domain.sdnn_index()``` 
- 長期NNI系列から抽出された5分セグメントの平均の標準偏差（SDANN） - ```pyhrv.time_domain.sdann()``` 
- 連続差の二乗平均平方根（RMSSD） - ```pyhrv.time_domain.rmssd()``` 
- 連続差の標準偏差（SDSD） - ```pyhrv.time_domain.sdsd()``` 
- NNx & pNNxパラメータ - ```pyhrv.time_domain.nnXX()``` 
- NN20 & pNN20パラメータ - ```pyhrv.time_domain.nn20()``` 
- NN50 & pNN50パラメータ - ```pyhrv.time_domain.nn50()``` 
- 三角指数（ヒストグラムの最大値 / ヒストグラムの幅） - ```pyhrv.time_domain.triangular_index()``` 
- 三角補間関数（TINN）<sup>1</sup> - ```pyhrv.time_domain.tinn()```

<sup><sup>1</sup> pyHRVの現在のバージョンには、TINN関数に対して誤解を招く誤った結果を引き起こすバグがあります。[この目的のために既に問題が開かれています...](https://github.com/PGomes92/pyhrv/issues/5)

![Image](./SampleFigures/SampleHistogram.png)


### 周波数領域パラメータ
以下のPSD方法を使用して計算されたNNI系列のパワースペクトル密度（PSD）から以下の周波数領域パラメータを計算します：

- ウェルチ法 - ```pyhrv.frequency_domain.welch_psd()```
- 自己回帰 - ```pyhrv.frequency_domain.ar_psd()```
- ロンブ-スカーグル - ```pyhrv.frequency_domain.lomb_psd()```

周波数パラメータ：
- ピーク周波数
- 絶対パワー
- 対数パワー
- 相対パワー
- 正規化パワー（LFとHFのみ）
- LF/HF比

パラメータは超低周波（VLF）、低周波（LF）、および高周波（HF）帯域に対して計算されます。周波数帯域はカスタマイズ可能で、超超低周波（ULF）帯域を含めることもできます。

pyHRVを使用した結果のPSDプロットと周波数領域パラメータのサンプルプロットは以下のとおりです：

![Image](./SampleFigures/SampleWelch.png)
![Image](./SampleFigures/SampleAR.png)
![Image](./SampleFigures/SampleLomb.png)

#### PSD比較機能 - 2D比較プロット
ウェルチ、自己回帰、またはロンブ-スカーグル法を使用して、NNI系列から抽出された複数のNNIセグメント（例：60分の記録の5分セグメント）のPSDを3D滝プロットでプロットし、各セグメントから周波数領域パラメータを計算します - ```pyhrv.frequency_domain.psd_comparison()``` [[ソース](https://github.com/PGomes92/pyhrv/blob/b5c5baaa8bf1ad085dc2dfe46b477171fe153682/pyhrv/frequency_domain.py#L970)]。

![Image](./SampleFigures/SamplePSDComparisonWelch.png)
![Image](./SampleFigures/SamplePSDComparisonAR.png)
![Image](./SampleFigures/SamplePSDComparisonLomb.png)

#### PSD比較機能 - 3D滝プロット
ウェルチ、自己回帰、またはロンブ-スカーグル法を使用して、NNI系列から抽出された複数のNNIセグメント（例：60分の記録の5分セグメント）のPSDを単一のプロットでプロットし、各セグメントから周波数領域パラメータを計算します - ```pyhrv.frequency_domain.psd_waterfall()```

![Image](./SampleFigures/SamplePSDWaterfallWelch.png)
![Image](./SampleFigures/SamplePSDWaterfallAR.png)
![Image](./SampleFigures/SamplePSDWaterfallLomb.png)

## 非線形パラメータ
以下の非線形パラメータとそれぞれのプロットを計算します：

- ポアンカレプロット（SD1、SD2、楕円面積、SD2/SD1比） - ```pyhrv.nonlinear.poincare()```
- サンプルエントロピー - ```pyhrv.nonlinear.sample_entropy()```
- 傾向変動解析（短期および長期）- ```pyhrv.nonlinear.dfa()```

![Image](./SampleFigures/SampleNonlinear.png)


## HRVサポートツール & その他の機能

- NNI系列の計算 - ```pyhrv.tools.nn_intervals()``` 
- ∆NNI系列の計算 - ```pyhrv.tools.nn_diff()```
- HR系列の計算 - ```pyhrv.tools.heart_rate()``` 
- 医療グレードのようなECGペーパーレイアウトでのECGプロット - ```pyhrv.tools.plot_ecg()``` 
- NNIタコグラムプロット - ```pyhrv.tools.tachogram()```
- 心拍数ヒートプロット、年齢と性別による正常な心拍数範囲に基づく心拍数パフォーマンスの視覚化と分類 - ```pyhrv.tools.heart_rate_heatplot()```
- 時間経過に伴うHRVパラメータの時間変化プロット - ```pyhrv.tools.time_varying()```
- HRVパラメータの動的レーダーチャート - ```pyhrv.tools.radar_chart()```
- HRV結果をJSONファイルにエクスポート [サンプルファイル](./pyhrv/files/SampleExport.json) - ```pyhrv.tools.hrv_export()``` 

![Image](./SampleFigures/SampleECG.png)
![Image](./SampleFigures/SampleTachogram.png)
![Image](./SampleFigures/SampleHRHeatplot1.png)
![Image](./SampleFigures/SampleRadarChart5.png)
![Image](./SampleFigures/SampleRadarChart8.png)

## HRVレポート
.TXT、.CSV、および.PDF形式のHRVレポートを生成します（v.0.4で新登場！）。以下のようなpyHRVレポートを生成する方法の詳細については、pyHRVレポートサブモジュールの[README](./pyhrv/report/README.md)ファイルをお読みください：

- [pyHRV .TXTレポート](./pyhrv/files/SampleReport.txt)
- [pyHRV .CSVレポート](./pyhrv/files/SampleReport.csv)
- [pyHRV .PDFレポート](./pyhrv/files/SampleReport.pdf)


## ユーティリティ
このツールボックス全体で使用されるいくつかのHRV固有でないユーティリティと一般的な目的の関数：
- テスト目的のためのNNIサンプルシリーズの読み込み - ```pyhrv.utils.load_sample_nni()```
- pyHRVの[hrv_keys.json](./pyhrv/files/hrv_keys.json)ファイルの読み込み - ```pyhrv.utils.load_hrv_keys_json()```
- NNI系列のフォーマット（numpy配列を確保し、秒単位で提供されたデータをmsに変換） - ```pyhrv.utils.nn_format()```
- 時系列（例：NNI系列）のセグメント化 - ```pyhrv.utils.segmentation()```
- その他...

# 免責事項
このプログラムは、有用であることを願って配布され、「現状のまま」提供されますが、商品性または特定目的への適合性の黙示的保証を含め、いかなる保証もなく提供されます。このプログラムは医学的診断を目的としたものではありません。直接的、間接的、結果的、偶発的、または特別な損害、収益の損失、利益の損失、事業中断または情報の損失による損害について、訴訟の形式または法的理論にかかわらず、そのような損害の可能性について知らされていたとしても、明示的に一切の責任を負いません。

このパッケージは当初（バージョン0.3まで）、[ハンブルク応用科学大学、ドイツ（生命科学部、生物医学工学科）](https://www.haw-hamburg.de/fakultaeten-und-departments/ls/studium-und-lehre/master-studiengaenge/mbme.html)と[PLUX wireless biosignals, S.A.](http://www.plux.info)、リスボン、ポルトガルでの修士論文「心拍変動（HRV）のためのオープンソースPythonツールボックスの開発」の範囲内で開発されました。
