![Image](./files/quickstart/pyhrv.png)
# 概要 & クイックスタート

## 目次
* [0. はじめに](#start)
  * [0.1 pyHRVのインストール](#install)
  * [0.2 サンプルデータ](#samples)
  * [0.3 pyHRV出力形式](#output)
* [1. pyHRV構造](#structure)
* [2. ツールモジュール](#tools)
  * [2.1 概要](#tools_overview)
  * [2.2 クイックスタート](#tools_quick)
    * [2.2.1 ECGの読み込み、NNIと∆NNI系列の計算](#tools_quick_start)
    * [2.2.2 ECG信号のプロット](#tools_plot_ecg)
    * [2.2.3 タコグラムのプロット](#tools_tachogram)
    * [2.2.4 HRVファイル管理とHRVレポート](#tools_filem)
* [3. 時間領域モジュール](#time)
  * [3.1 概要](#time_overview)
  * [3.2 クイックスタート](#time_quick)
    * [3.2.1 個別の時間領域パラメータの計算](#time_quick_parameter)
    * [3.2.2 すべての時間領域パラメータを一度に計算](#time_quick_module)
* [4. 周波数領域モジュール](#freq)
  * [4.1 概要](#freq_overview)
  * [4.2 クイックスタート](#freq_quick)
    * [4.2.1 ウェルチ法](#freq_welch)
    * [4.2.2 ロンブ-スカーグル周期図](#freq_welch)
    * [4.2.3 自己回帰法](#freq_ar)
    * [4.2.4 すべてのPSD手法を一度に計算](#freq_quick_module)
* [5. 非線形モジュール](#nonlinear)
  * [5.1 概要](#nonlinear_overview)
  * [5.2 クイックスタート](#nonlinear_quick)
    * [5.2.1 個別の非線形パラメータの計算](#nonlinear_quick_parameter)
    * [5.2.2 すべての非線形パラメータを一度に計算](#nonlinear_quick_module)


##### 略語リスト
(登場順)

* NNI 	正常-正常間隔（連続するR波ピーク間）
* ∆NNI	連続するNNI間の差
* HR    心拍数
* PSD 	パワースペクトル密度
* FFT 	高速フーリエ変換
* ULF		超低周波
* VLF		超低周波
* LF		低周波
* HF 		高周波
* DFA 傾向変動解析

# 0. はじめに <a name="start"></a>
## 0.1 pyHRVのインストール <a name="install"></a>
ターミナルを開き、以下のコマンドでpipツールを使用して`pyhrv`をインストールします：

```python
pip install pyhrv
```

現在のpyHRVは主にPython 2.7プログラミング言語用に開発されています。Python 3を使用して上記のpipコマンドを実行すると、パッケージのインストール時にエラーが発生する可能性があります。この場合、まずpyHRVの依存関係をインストールしてみてください：

```python
pip install biosppy
pip install matplotlib
pip install numpy
pip install scipy
pip install nolds
pip install spectrum
pip install pyhrv
```

## 0.2 サンプルデータ <a name="samples"></a>
このパッケージにはpyHRV GitHubページの`samples`フォルダにあるECGとNNIのサンプルデータが付属しています。

`SampleECG.txt`ファイルには、[BITalino revolution](http://bitalino.com/en/)デバイスと[OpenSignals revolution](http://bitalino.com/en/software)ソフトウェアで取得した公式[BITalino サンプルECG信号](https://github.com/BITalinoWorld/revolution-sample-data/tree/master/ECG)が含まれています。以下の例では[OpenSignalsReader](https://github.com/PGomes92/opensignalsreader)を使用して`SampleECG.txt`ファイルからECGデータを読み込みますが、他のECGセンサーでも同様に動作します。

`series_X`ファイル（.npyまたは.txt）に保存されているNNI系列は、[MIT-BIH NSRDBデータベース（physionet.org）](https://physionet.org/physiobank/database/nsrdb/)から抽出された5分間のセグメントです。

## 0.3 pyHRV出力形式 <a name="output"></a>
ツールボックスのパラメータ関数は、計算されたすべてのHRVパラメータを単一の`biosppy.utils.ReturnTuple`[(詳細はこちら,](https://biosppy.readthedocs.io/en/stable/biosppy.html#biosppy.utils.ReturnTuple) および [こちら)](https://biosppy.readthedocs.io/en/stable/tutorial.html#a-note-on-return-objects)オブジェクトで返します。これらのオブジェクトは、Pythonの辞書で使用されるように_キー_を使用してインデックス付けされるPythonタプル（不変）の混合です。

利用可能なパラメータキーの完全なリストにアクセスするには、[files](./files/)フォルダにある[hrv_keys.json](./files/hrv_keys.json)ファイルを参照してください。

# 1. pyHRV構造 <a name="structure"></a>
pyHRVツールボックスのHRV特徴抽出機能は、ユーザーのニーズやプログラミングの背景に応じて、ツールボックスの使用を容易にし、使いやすさを向上させることを目的とした3つのレベルに分類されて実装されています。この多層アーキテクチャは以下の図に示されています。

![Image](./files/quickstart/function_levels.png)

**レベル1 - HRVレベル：**

このレベルは、`hrv.py`にある`hrv()`関数を呼び出すことで、1行のコードだけですべてのHRVパラメータを計算できる単一の関数で構成されています。この関数は、すべての基礎となるHRVパラメータ関数を呼び出し、バンドルされた結果を`biosppy.utils.ReturnTuple()`オブジェクトで返します。特定のパラメータの計算のためのカスタム設定やパラメータは、必要に応じて`kwargs`入力辞書を使用してhrv()関数に渡すことができます。それ以外の場合は、デフォルト値が使用されます。

**レベル2 - ドメインレベル：**

このレベルのモジュール/ドメイン関数は、特定のドメインのすべてのパラメータを計算したいユーザー向けです。時間領域の例を使用すると、`time domain()`関数はこのドメインのすべてのパラメータ関数を呼び出し、結果を`biosppy.utils.ReturnTuple()`オブジェクトにバンドルして返します。前のレベルと同様に、ユーザー固有の設定とパラメータは、利用可能な`kwargs`辞書を使用してドメイン関数に渡すことができます。モジュールレベルの関数は、それぞれのドメインモジュールにあります。

**レベル3 - パラメータレベル：**

このレベルは、単一の特定のパラメータ（個別に）を計算したい場合のパラメータ固有の関数です（例：`sdnn()`はSDNNパラメータを返します）。これにより、特定のアプリケーションに必要なパラメータや機能のみを選択できます。ユーザー固有の設定とパラメータは、関数をオーバーロードするときに直接行うことができます。

# 2. ツールモジュール <a name="tools"></a>
## 2.1 概要 <a name="tools_overview"></a>
ツールモジュールには、HRV計算のための基本的なデータ系列を計算するための関数と、その他の有用な機能（例：ECG信号プロット、HRVパラメータのエクスポート）が含まれています。利用可能な関数の完全なリストは以下の表に記載されています。

| 関数   		      | 説明                                               								|
| ---                 | ---                                                       								|
| `nn_intervals()`    | R波ピーク位置のシリーズからNNIを計算                    |
| `nn_diff()`        	| NNIシリーズまたはR波ピーク位置から∆NNIを計算    								|
| `nn_format()`			  | NumPy配列を確認し、秒単位のNNIシリーズをミリ秒に変換 									|
| `heart_rate()`     	| 個々のNNIまたはR波ピーク位置からHRデータを計算  								|
| `tachogram()`      	| NNIとHRのタコグラムをプロット                                								|
| `ecg_plot()`        | 医療グレードのようなECG上でECG信号をプロット 												|
| `segmentation()` 		| NNIシリーズを指定された期間のセグメントに分割									|
| `hrv_export()` 		  | HRV結果を.JSONファイルにエクスポート 														|
| `hrv_import()` 		  | .JSONファイルに保存されたHRV結果をインポート 												|
| `hrv_report()` 	  	| .TXTまたは.CSV形式でHRVレポートを生成 												|
| `join_tuples()` 		| 複数の`biosppy.utils.ReturnTuple`オブジェクトを1つのオブジェクトに結合 							|
| `time_vector()`		  | 特定の信号の時間ベクトルを計算 												|
| `std()`				      | データシリーズの標準偏差を計算 												|
| `check_input()`    | （ほぼ）すべてのパラメータ関数の入力データを検証 									|
| `check_interval()`	| 間隔の制限を検証（例：max(limit) < min(limit)を修正）								|

（弱いモジュール関数はこの表に記載されていません）

## 2.2. クイックスタート <a name="tools_quick"></a>
このモジュールを使用するには、以下のようにインポートすることをお勧めします：
```python
import pyhrv.tools as tools
```

### 2.2.1 ECGの読み込み、R波の抽出、NNIの計算 <a name="tools_quick_stat"></a>
以下の例では、ECG信号（ここでは[BITalino](www.bitalino.com)サンプルECG信号）を読み込み、R波ピーク位置を抽出し、NNIシリーズを計算する方法を示しています。
```python
import biosppy
import numpy as np
import pyhrv.tools as tools
from opensignalsreader import OpenSignalsReader 

# サンプルECG信号を読み込み、BioSppyを使用してR波を抽出
signal = OpenSignalsReader('./samples/SampleECG.txt').signal('ECG')
signal, rpeaks = biosppy.signals.ecg.ecg(signal, show=False)[1:3]

# NNIを計算
nni = tools.nn_intervals(rpeaks)

```

### 2.2.2 ECG信号のプロット <a name="tools_plot_ecg"></a>
`plot_ecg()`関数は、医療グレードのようなECGペーパーレイアウトでECGデータをプロットします。
```python
# ECG信号をプロット（間隔：0秒から15秒）
tools.plot_ecg(signal, interval=[0, 15])
```
結果の出力は次のようになります：
![Image](./files/quickstart/ecg15.png)

### 2.2.3 タコグラムのプロット <a name="tools_tachogram"></a>
`tachogram()`関数は、NNIデータとHRデータが時間的な発生に対してプロットされるタコグラムをプロットします。
```python
# ECG信号のタコグラムをプロット（間隔：0秒から15秒）
tools.tachogram(signal, interval=[0, 15])
``` 
結果の出力は次のようになります：
![Image](./files/quickstart/tachogram15.png)

### 2.2.4 HRVファイル管理とHRVレポート <a name="tools_filem"></a>
`hrv_export()`ファイルは、HRV結果を外部ファイルに保存するプロセスを容易にします。この関数を使用するには、HRV結果（ここでは`hrv_results` ReturnTupleオブジェクトに保存）を提供し、出力ファイルの絶対ファイルパスとファイル名を定義する必要があります。
```python
# HRV結果を'path'に保存された'efile'という名前の.JSONファイルにエクスポート
tools.hrv_export(hrv_results, path='/my/favorite/path/', efile='MyFavoriteHRVResults')
```

`hrv_import()`関数を使用して、`hrv_results()`関数によって生成された.JSONファイルに保存されているすべての結果をPythonプロジェクトにインポートします。ここでは、パスとファイル（'.json'拡張子を含む）を単一の文字列で提供する必要があることに注意してください。
```python
# .JSONファイルに保存されたHRV結果をインポート
hrv_results = tools.hrv_import('/my/favorite/path/MyFavoriteHRVResults.json')
```

`hrv_report()`ファイルは、ReturnTupleオブジェクトに保存されたHRV結果をレポートのような.TXTまたは.CSVファイルにエクスポートします：
```python
# .TXTレポートを生成（デフォルトのファイル形式）
tools.hrv_report(hrv_results, path='/my/favorite/path', rfile='MyFavoriteHRVReport')

# .CSVレポートを生成
tools.hrv_report(hrv_results, path='/my/favorite/path', rfile='MyFavoriteHRVReportInCSV', file_format='csv')
```

> 注意： 
> `hrv_export()`と`hrv_report()`には、ファイルを誤って上書きしないための保護メカニズムが付いています。
> 例えば、`'MyFavoriteHRVResults.json'`というファイル名のファイルが既に存在する場合、既存のファイル名は新しいファイル名`'MyFavoriteHRVResults_1.json'`にインクリメントされます。

# 3. 時間領域モジュール <a name="time"></a>
## 3.1 概要 <a name="time_overview"></a>
`time_domain.py`モジュールには、HRV時間領域パラメータを計算するためのすべての関数が含まれています。個々のパラメータレベルの関数は以下の表に記載されています。

| 関数   		    		| 計算されるパラメータ                                  								|
| ---                   		| ---                                                  								|
| `nn_parameters()`    			| NNIシリーズの基本統計パラメータ（最小、最大、平均）   					|
| `nn_differences_parameter()`	| NNI差分シリーズの基本統計パラメータ（最小、最大、平均）		|
| `hr_parameters()`				| HR系列の基本統計パラメータ（最小、最大、平均、SD）					|
| `sdnn()`						| 連続するNNIの標準偏差（SDNN）										|
| `sdnn_inex()`					| 5分セグメントのSDNNの平均（SDNNインデックス）										|
| `rmssd()`						| 連続差の二乗平均平方根（RMSSD）								|
| `sdsd()` 						| 連続するNNI差分の標準偏差（SDSD）							|
| `nnXX()`						| NNXパラメータ（∆NNI > Xmsの数）とpNNX（∆NNI > Xmsの割合）						|
| `nn50()`						| NN50パラメータ（∆NNI > 50msの数）とpNN50（∆NNI > 50msの割合） 					|
| `nn20()` 						| NN20パラメータ（∆NNI > 20msの数）とpNN20（∆NNI > 20msの割合） 					|
| `triangular_index()`			| NNIヒストグラムの三角指数（Tri-Index）					|
| `tinn()` 						| 三角補間に基づくNNIヒストグラムのベースライン幅（TINN）		|
| `geometrical_parameters()`	| `triangular_index()`と`tinn()`関数を呼び出し、単一のNNIヒストグラムを返す 		|

さらに、このモジュールには、1つの関数だけですべての時間領域パラメータを計算できるモジュールレベルの`time_domain()`関数が含まれています（[3.2.2](time_quick_module)を参照）。

| 関数   		    		| 計算されるパラメータ                                  								|
| ---                   		| ---                                                  								|
| `time_domain()`    			| 上記の表に記載されているすべての時間領域パラメータを計算				   		|

## 3.2 クイックスタート <a name="time_quick"></a>
このモジュールを使用するには、以下のようにインポートすることをお勧めします：
```python
import pyhrv.time_domain as td
```

### 3.2.1 個別の時間領域パラメータの計算 <a name="time_quick_parameter"></a>
`time_domain.py`モジュールの関数は、以下の例のように使用できます：

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.time_domain as td 

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# SDNNを計算
result = td.sdnn(nni)

# キー'sdnn'を使用してSDNN値にアクセス
print(result['sdnn'])
```

### 3.2.2 すべての時間領域パラメータを一度に計算 <a name="time_quick_module"></a>
各パラメータ関数を個別に呼び出す代わりに、モジュールレベルの関数`time_domain()`を使用して、1つの関数だけですべての時間領域パラメータを計算できます。

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.time_domain as td 

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# SDNNを計算
results = td.time_domain(nni)

# パラメータキー'sdnn'、'rmssd'、'nn50'を使用して時間領域の結果値にアクセス
print(results['sdnn'])
print(results['rmssd'])
print(results['nn50'])
# など...
```

# 4. 周波数領域モジュール <a name="freq"></a>
## 4.1 概要 <a name="freq_overview"></a>
`frequency_domain.py`モジュールには、異なるPSD推定方法を使用してHRV周波数領域パラメータを計算するための関数が含まれています：FFTベースの[ウェルチ法](https://en.wikipedia.org/wiki/Welch%27s_method)と[ロンブ-スカーグル周期図](https://en.wikipedia.org/wiki/Least-squares_spectral_analysis)。

| 関数   		| パワースペクトル密度（PSD）推定方法        							|
| ---               | ---                                                  								|
| `welch_psd()`    | ウェルチ法を使用したPSD推定；すべての周波数領域パラメータを計算					|
| `lomb_psd()`		| ロンブ-スカーグル周期図を使用したPSD推定；すべての周波数領域パラメータを計算		|
| `ar_psd()`       | 自己回帰法を使用したPSD推定；すべての周波数領域パラメータを計算 |

PSDから計算される以下のパラメータ：

- ピーク周波数 [Hz]
- 絶対パワー [ms^2]
- 対数パワー [ms^2]
- 相対パワー [%]
- 正規化パワー（LFとHF）[-]
- LF/HF比 [-]

さらに、このモジュールには、1つの関数だけですべての周波数領域PSD方法とパラメータを計算できるモジュールレベルの`frequency_domain()`関数が含まれています（[4.3.2](#freq_quick_module)を参照）。

| 関数     			| 計算されるパラメータ                                  			|
| ---                	| ---                                         					|
| `frequency_domain()`  | すべての周波数方法とパラメータを計算	|


## 4.2 クイックスタート <a name="freq_quick"></a>
このモジュールを使用するには、以下のようにインポートすることをお勧めします：
```python
import pyhrv.frequency_domain as fd
```

### 4.2.1. ウェルチ法 <a name="freq_welch"></a>
`welch_psd()`関数を使用して、ウェルチ法を使用してNNIシリーズからPSDを計算します。この関数はPSDプロットと各周波数帯域から計算された周波数領域パラメータを返します。

デフォルトの周波数帯域は以下のように指定されています：

- VLF:	0.00Hz から 0.04Hz
- LF: 	0.04Hz から 0.15Hz
- HF: 	0.15Hz から 0.40Hz

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.frequency_domain as fd

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# PSDと周波数領域パラメータを計算
result = fd.welch_psd(nni=nni)

# キー'fft_peak'を使用してピーク周波数にアクセス
print(result['fft_peak'])
```

出力は以下のようなプロットになります：
![Image](./files/quickstart/welch_default.png)

この関数では、ULF帯域を追加し、カスタム周波数帯域の制限を設定できます：
```python
# カスタム周波数帯域を定義
fbands = {'ulf': (0.0, 0.1), 'vlf': (0.1, 0.2), 'lf': (0.2, 0.3), 'hf': (0.3, 0.4)}

# カスタム周波数帯域でPSDを計算
result = fd.welch_psd(nni=nni, fbands=fbands)
```
出力は以下のようなプロットになります：
![Image](./files/quickstart/welch_custom.png)

### 4.2.2. ロンブ-スカーグル周期図 <a name="freq_lomb"></a>
`lomb_psd()`関数を使用して、ロンブ-スカーグル周期図を使用してNNIシリーズからPSDを計算します。この関数はPSDプロットと各周波数帯域から計算された周波数領域パラメータを返します。

デフォルトの周波数帯域は以下のように指定されています：

- VLF:	0.00Hz から 0.04Hz
- LF: 	0.04Hz から 0.15Hz
- HF: 	0.15Hz から 0.40Hz

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.frequency_domain as fd

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# PSDと周波数領域パラメータを計算
result = fd.lomb_psd(nni=nni)

# キー'lomb_peak'を使用してピーク周波数にアクセス
print(result['lomb_peak'])
```
出力は以下のようなプロットになります：
![Image](./files/quickstart/lomb_default.png)

この関数では、ULF帯域を追加し、カスタム周波数帯域の制限を設定できます：
```python
# カスタム周波数帯域を定義
fbands = {'ulf': (0.0, 0.1), 'vlf': (0.1, 0.2), 'lf': (0.2, 0.3), 'hf': (0.3, 0.4)}

# カスタム周波数帯域でPSDを計算
result = fd.lomb_psd(nni=nni, fbands=fbands)
```
出力は以下のようなプロットになります：
![Image](./files/quickstart/lomb_custom.png)

### 4.2.3. 自己回帰 <a name="freq_ar"></a>
`ar()`関数を使用して、自己回帰法を使用してNNIシリーズからPSDを計算します。この関数はPSDプロットと各周波数帯域から計算された周波数領域パラメータを返します。

デフォルトの周波数帯域は以下のように指定されています：

- VLF:  0.00Hz から 0.04Hz
- LF:   0.04Hz から 0.15Hz
- HF:   0.15Hz から 0.40Hz

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.frequency_domain as fd

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# PSDと周波数領域パラメータを計算
result = fd.ar_psd(nni=nni)

# キー'ar_peak'を使用してピーク周波数にアクセス
print(result['ar_peak'])
```
出力は以下のようなプロットになります：
![Image](./files/quickstart/ar_default.png)

この関数では、ULF帯域を追加し、カスタム周波数帯域の制限を設定できます：
```python
# カスタム周波数帯域を定義
fbands = {'ulf': (0.0, 0.1), 'vlf': (0.1, 0.2), 'lf': (0.2, 0.3), 'hf': (0.3, 0.4)}

# カスタム周波数帯域でPSDを計算
result = fd.ar_psd(nni=nni, fbands=fbands)
```
出力は以下のようなプロットになります：
![Image](./files/quickstart/ar_custom.png)

### 4.2.4 すべてのPSD手法を一度に計算 <a name="freq_quick_module"></a>
各メソッド関数を個別に呼び出す代わりに、モジュールレベルの関数`frequency_domain()`を使用して、1つの関数だけですべてのメソッドと周波数パラメータを計算できます。

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.frequency_domain as fd 

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# 周波数を計算
results = fd.frequency_domain(nni=nni)

# ウェルチ法、ARおよびロンブ-スカーグル周期図で計算された結果にアクセス
print(results['fft_peak'])
print(results['lomb_peak'])
print(results['ar_peak'])
# など...
```
この関数を使用する際に、以下のように方法固有の辞書でパラメータを渡すことで、個々のメソッドの特定のパラメータを定義することもできます。

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.frequency_domain as fd 

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# ウェルチパラメータ
kwargs_welch = {'nfft': 2**12}

# ARパラメータ
kwargs_ar = {'nfft': 2**10}

# ロンブパラメータ
kwargs_lomb= {'nfft': 2**8}

# 周波数を計算
results = fd.frequency_domain(nni=nni, kwargs_welch=kwargs_lomb, kwargs_ar=kwargs_ar, kwargs_lomb=kwargs_lomb)

``` 

# 5. 非線形モジュール <a name="nonlinear"></a>
## 5.1 概要 <a name="nonlinear_overview"></a>
`nonlinear.py`モジュールには、非線形HRVパラメータを計算するためのすべての関数が含まれています。個々のパラメータレベルの関数は以下の表に記載されています。

| 関数            | 計算されるパラメータ                                               |
| ---                 | ---                                                               |
| `poincare()`        | ポアンカレプロット、SD1、SD2、SD1/SD2比、適合楕円の面積    |
| `sample_entropy()`  | サンプルエントロピー                                                    |
| `dfa()`             | 短期および長期の傾向変動解析           |

さらに、このモジュールには、1つの関数だけですべての非線形パラメータを計算できるモジュールレベルの`nonlinear()`関数が含まれています（[5.2.2](#nonlinear_quick_module)を参照）

| 関数      | 計算されるパラメータ                                 |
| ---           | ---                                                 |
| `nonlinear()` | 上記のすべての非線形パラメータを計算 |

## 5.2 クイックスタート <a name="nonlinear_quick"></a>
このモジュールを使用するには、以下のようにインポートすることをお勧めします：
```python
import pyhrv.nonlinear as nl
```

### 5.2.1 個別の非線形パラメータの計算 <a name="nonlinear_quick_parameter"></a>
`nonlinear.py`モジュールの関数は、以下の例のように使用できます：
```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.nonlinear as nl

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# SDNNを計算
result = nl.poincare(nni)

# キー'sd1'を使用してSD1値にアクセス
print(result['sd1'])
```

`poincare()`関数は[ポアンカレ散布図](https://waset.org/publications/10002615/poincaré-plot-for-heart-rate-variability)を生成することに注意してください。出力は以下のようなプロットになります：

![Image](./files/quickstart/poincare.png)

傾向変動解析（DFA）では、DFAを計算するために定義された短期および長期の間隔を設定します。
```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.nonlinear as nl

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# SDNNを計算
result = nl.dfa(nni, short=[4, 16], long=[17, 64])

# キー'dfa_short'を使用してalpha1（短期変動）値にアクセス
print(result['dfa_short'])
```
出力は以下のようなプロットになります：

![Image](./files/quickstart/dfa.png)

### 5.2.2 すべての非線形パラメータを一度に計算 <a name="nonlinear_quick_module"></a>
各パラメータ関数を個別に呼び出す代わりに、モジュールレベルの関数`nonlinear()`を使用して、1つの関数だけですべての非線形パラメータを計算できます。

```python
# パッケージをインポート
import numpy as np
import pyhrv
import pyhrv.nonlinear as nl 

# NNIサンプルシリーズを読み込み
nni = pyhrv.utils.load_sample_nni()

# すべての非線形パラメータを計算
results = nl.nonlinear(nni)

# 結果にアクセス
print(results['sd1'])
print(results['dfa_short'])
# など...
```
