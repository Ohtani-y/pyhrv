アップデート バージョン 0.4.1
--------------------
**追加**
- Issue #22 & Issue #15からのリクエスト: 非線形領域関数 ``poincare()`` と ``dfa()`` に ``mode`` を追加:
   - ``normal``: 計算された出力データとプロット図を返します
   - ``dev``: 計算された出力データのみを返します

**修正**
  - Issue #28を修正: pyhrv.utils._check_limits()関数がエラーと警告メッセージの文字列を正しくフォーマットしていなかった問題（皮肉にもこれによりエラーが発生していた）
  - Python 3.8+でレポートが正しく生成されない問題を修正
  - Python 3.8+で心拍数ヒートプロットが「StopIteration」エラーをスローする問題を修正
  - Issue #13を修正（``nonlinear.py``での不足しているインポート）
  - 生のECG信号が提供された場合に、一部の高レベル関数が時間的なrpeaksの位置の代わりにrpeakインデックスを使用していた問題を修正

**ドキュメント更新**
  - Issue #29を修正: biosppy使用の複数のサンプルコードがNNI計算に間違ったr-peaksシリーズを使用していた問題
  - Issue #26を修正: ドキュメントが古いサンプルデータにリンクしていた問題

アップデート バージョン 0.4.0
--------------------
#### 主な変更点
- hrv_keys.jsonを更新し、いくつかのタイプミスを修正
- 周波数領域関数 ``welch_psd()``、``ar_psd()``、および ``lomb_psd()`` に ``modes`` を追加:
   -	``normal``: ReturnTupleオブジェクトで周波数領域パラメータとPSDプロット図を返します
	-	``dev``: 周波数領域パラメータ、周波数と電力の配列を返し、プロット図はありません
	-	``devplot``: 周波数領域パラメータ、周波数配列、電力配列、およびプロット図を返します
- 周波数領域比較機能:
   - ``pyhrv.frequency_domain.psd_comparison()`` 関数を追加して、複数のNNIセグメントから複数のPSD（welch、ar、またはlomb）を単一のプロット図にプロット
    
        **サンプルプロット:**
        [Welch](./SampleFigures/SamplePSDComparisonWelch.png),
        [Autoregressive](./SampleFigures/SamplePSDComparisonAR.png), and
        [Lomb-Scargle](./SampleFigures/SamplePSDComparisonLomb.png)     
        **ドキュメント:**
        https://pyhrv.readthedocs.io/en/latest/_pages/api/frequency.html#d-psd-comparison-plot-psd-comparison
   - ``pyhrv.frequency_domain.psd_waterfall()`` 関数を追加して、複数のNNiセグメントから複数のPSD（welch、ar、またはlomb）を3Dプロットにプロット（サンプルプロット: [Welch](./SampleFigures/SamplePSDWaterfallWelch.png), [Autoregressive](
   ./SampleFigures/SamplePSDWaterfallAR.png), [Lomb](./SampleFigures/SamplePSDWaterfallLomb.png)）
- ``pyhrv.tools.heart_rate_heatplot()`` 関数を追加して、年齢と性別による正常な心拍数範囲に基づいた心拍数パフォーマンスのグラフィカルな視覚化と分類を行う（サンプルプロット: [plot 1](./SampleFigures/SampleHRHeatplot1.png), [plot 2](
./SampleFigures/SampleHRheatplot2), and [plot 3](./SampleFigures/SampleHRHeatplot3.png)）
- ``pyhrv.tools.radar_chart()`` 関数を追加して、ユーザーが選択したHRVパラメータのシリーズからレーダーチャートをプロット
- この関数の以前の更新により効果がなくなったため、``pyhrv.utils.segmentation()`` 関数から ``overlap`` 入力引数を削除
- 同じ理由で ``pyhrv.utils.sdnn_index()`` と ``pyhrv.utils.sdann()`` 関数からも ``overlap`` 入力引数が削除されました（両方とも ``pyhrv.utils.segmentation()`` を使用）
- ``hrv_report()`` を移動、修正、改善
- pyHRVパッケージの全体的な安定性を向上
- pyHRVパッケージを再構成（特に ``tools.py`` と ``utils.py`` モジュールを参照）:

```
    pyhrv                           # ツールボックス
    ├── files                       # pyHRVサポートファイル
    |   ├── quickstart              # クイックスタートガイドの図（pyHRVモジュールのREADME.mdを参照）
    |   ├── hr_heatplot.json        # hr_heatplot()関数用のHR参照正常値
    |   ├── hrv_keys.json           # パラメータ結果にアクセスするためのHRVキー
    |   ├── references.txt          # pyHRV関数が基づいている出版物の参考文献
    |   ├── SampleECG.txt           # サンプルECG信号（テスト目的）
    |   ├── SampleExport.json       # サンプルHRV結果エクスポート（デモンストレーション目的）
    |   ├── SampleNNISeriesLong.npy # 60分のサンプルNNIシリーズ（テスト目的）
    |   ├── SampleNNISeriesShort.npy# 5分のサンプルNNIシリーズ（テスト目的）
    |   ├── SampleReport.csv        # .csv形式のサンプルレポート
    |   ├── SampleReport.pdf        # .pdf形式のサンプルレポート
    |   └── SampleReport.txt        # .txt形式のサンプルレポート
    |      
    ├── report                      # PDF、TXT、およびCSVレポート生成のためのサブパッケージ
    |   ├── build                   # 生成されたPDF、TXT、およびCSVレポートのデフォルトパス 
    |   ├── figure                  # PDFレポート用の図が一時的に保存される作業ディレクトリ
    |   ├── templates               # PDFレポート用のLaTeXテンプレート（自由にカスタマイズ可能）
    |   ├── __init__.py             # レポート初期化ファイル
    |   ├── main.tex                # メインLaTeXファイル
    |   ├── parameters.tex          # HRVパラメータが保存される変数を含むファイル
    |   ├── pyhrv.png               # PDFヘッダー用のpyHRVロゴ
    |   ├── README.md               # レポートREADME
    |   └── settings.tex            # LaTeXベースのプロジェクト用の設定ファイル
    |   
    ├── __init__.py                 # pyHRV初期化ファイル
    ├── __version__.py              # pyHRVバージョン
    ├── hrv.py                      # HRV関数
    ├── frequency_domain_.py        # 周波数領域関数
    ├── nonlinear.py                # 非線形パラメータ関数
    ├── time_domain.py              # 時間領域関数
    ├── tools.py                    # HRVツール関数（タコグラム、ECG、レーダーチャート、HRヒートプロット、その他 
    |                               # 比較関数
    └── utils.py                    # 一般的なデータ検証、変換、ファイル処理など

```

- ``tools.py`` にはHRV分析（サポート）専用に設計されたツールのみが含まれるようになりました
- ``utils.py`` にはツールの計算とHRVパラメータの計算に必要なサポート関数のみが含まれるようになりました

#### 小さな変更点
- pyhrv.nonlinear.dfa(): 短期変動の ``dfa_alpha1_beats`` 戻りキーと長期変動値の ``dfa_alpha2_beats`` 戻りキーを追加
- hrv_keys.jsonファイルを更新
- ``tools.plot_ecg`` と ``tools.tachogram`` 関数の ``interval`` 入力パラメータの有効な値として ``complete`` を追加
- pyhrv.time_domain.tinn() & pyhrv.time_domain.geometrical_parameters() 関数は、TINN関数の現在の問題（間違った結果を提供する）のために警告を発行するようになりました（issue #5を参照）
- ``sdnn`` と ``sdnn_index`` 関数から 'overlap' 入力パラメータを削除 
- メインREADMEを更新
- #6、#7、#9を修正

アップデート バージョン 0.3.2
--------------------
- 重要: pip installを使用したPython3でのインストールの問題を修正（完全なサポートはまだテストする必要があります）
- プロット機能を持つ関数のモード依存リターンを準備

アップデート バージョン 0.3.1
--------------------
- tools.segmentation()関数のインデックス範囲外エラーを修正
- hrv.pyでのBioSPPyインポートを修正

アップデート バージョン 0.3
------------------
- ReadTheDocsドキュメントを追加
- 新しい周波数領域メソッド（自己回帰）を追加
- macOSでのヒストグラム図の視覚化の欠如を修正
- 'pyhrv.tools.check_input()'関数で、計算中に入力パラメータが変更される問題を修正
- docstringを更新し、ドキュメントを追加
- 参考文献を追加
- hrv()関数を改善
- nonlinear()関数を改善

アップデート バージョン 0.2
------------------
- ツールボックス名を'pyhrv'に変更
- `pip`を使用したインストールプロセスを追加
- 周波数領域パラメータとメソッド（ウェルチ法とロンブ-スカーグル）を追加
- `frequency_domain()`モジュールレベル関数を追加
- パッケージレベル関数`hrv()`で周波数パラメータの計算を追加
- リポジトリのファイル構造を再配置
- `references.txt`ファイルを追加
- `hrv_report()`関数を改善
- `hrv_keys().json`ファイルを更新
- 小さなバグ修正
- [MIT-BIH NSRDB](https://physionet.org/physiobank/database/nsrdb/)データベースから抽出した50のサンプルNNIシリーズを追加
- サンプルHRVレポートとエクスポートを更新
- `pyhrv.tools.segmentation()`関数のバグを修正（あるセグメントから別のセグメントへのNNIの重複が削除される問題）

アップデート バージョン 0.1.2
--------------------
- 新しい時間領域HRVパラメータを追加 -> 幾何学的パラメータ

  * 三角指数:  _hrv.time_domain.triangular_index()_
  * TINN:  _hrv.time_domain.tinn()_
  * ヒストグラム（NumPyとMatplotlibを利用したヘルパー関数）:  _hrv.time_domain._get_histogram()
  * 幾何学的パラメータ（これらのパラメータは単独で使用されることはほとんどないため、_tinn()_と_triangular_index()_を呼び出す）: _hrv.time_domain.geometrical_parameters()_

- _hrv.time_domain.time_domain()_を更新して、新しい幾何学的パラメータも返すようにした
- 新しい非線形パラメータを追加 -> サンプルエントロピーと傾向変動解析（DFA）

  * サンプルエントロピー:  _hrv.nonlinear_parameters.sample_entrop()_
  * DFA: _hrv.nonlinear_parameters.dfa()_
  * 両方の関数は[nolds](https://github.com/CSchoel/nolds)を利用

- _hrv.nonlinear_parameters.nonlinear()_を更新して、新しい非線形パラメータも返すようにした
- 新しいツール関数を追加 -> HRVレポート
  * 全く新しいHRVレポートジェネレータ:  _hrv.tools.hrv_report()_
  * .txtまたは.csv形式のレポートを生成

- 生成されたHRVエクスポートとHRVレポートの既存ファイルを検出し、既存ファイルの上書きを避けるために自動的に新しいファイル名を生成する_ _check_fname()_関数を追加（例：'Sample.txt'が存在する場合、新しいファイル名を'Sample_1.txt'に「インクリメント」して'Sample.txt'の上書きを避ける）

- './hrv/files/'に'SampleReport.txt'と'SampleReport.csv'を追加
- './hrv/files/'の'SampleExport.json'を更新
- いくつかのツール関数の小さな修正
- Python 3との互換性を向上
- 各モジュールの例セクションを更新

アップデート バージョン 0.1.1
--------------------
- リポジトリ全体を再構成
- _time_domain_、_nonlinear_parameters_、および_tools_モジュールの機能をテストし、結果を検証
- 各モジュールの最後の例スクリプトを修正
- _tools_モジュールに新しい関数を追加: _hrv_import()_、_hrv_export()_、_check_input()_
- _tools.segmentation()_関数のバグを修正

バージョン 0.1
-------------------
- 時間領域関数
- ポアンカレ非線形関数
- HRV関数のための基本ツール
