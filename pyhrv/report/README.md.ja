# pyHRVレポート

pyHRVには、計算されたHRV結果から.TXT、.CSV、および.PDF形式（v.0.4で新登場）のレポートを作成するための組み込み機能が付属しています。以下に、異なる出力形式に関する詳細情報を示します。

## .TXTレポート
.TXTレポートを生成するには、以下のコード例に従ってください。サンプルレポートはこちらで確認できます。[TXTレポートの例はこちら](../files/SampleReport.txt)

```python
    # インポート
    import pyhrv

    # 5分間のサンプルNNIシリーズを読み込み
    nni = pyhrv.utils.load_sample_nni()

    # HRVパラメータを計算（表示しない）
    results = pyhrv.hrv(nni, show=False)

    # HRV TXTレポートを作成
    pyhrv.report.hrv_report(results, path='./files/', rfile='SampleReport', file_format='txt')
```

## .CSVレポート
.CSVレポートを生成するには、以下のコード例に従ってください。サンプルレポートはこちらで確認できます。[CSVレポートの例はこちら](../files/SampleReport.csv)

```python
    # インポート
    import pyhrv

    # 5分間のサンプルNNIシリーズを読み込み
    nni = pyhrv.utils.load_sample_nni()

    # HRVパラメータを計算（表示しない）
    results = pyhrv.hrv(nni, show=False)

    # HRV CSVレポートを作成
    pyhrv.report.hrv_report(results, path='./files/', rfile='SampleReport', file_format='csv')
```

## .PDFレポート
#### 要件と依存関係
pyHRV PDFレポートジェネレータは、PDF形式の高品質なレポートを生成できるLaTeXを活用した機能です。[PDFレポートの例はこちら](../files/SampleReport.pdf)。

この機能を使用するには、コンピュータに以下のLaTeXパッケージと共にLaTeX配布物がインストールされている必要があります：

* amsmath
* array
* colorbl
* datetime
* fancyhdr
* geometry
* graphics
* helvet
* hyperref
* layouts
* titlesec
* tikz
* xcolor

お使いのオペレーティングシステム用のLaTeX配布物をダウンロードし、必要なパッケージのインストール方法についての詳細は、[LaTeXプロジェクトウェブサイト](https://www.latex-project.org/get/)をご覧ください。

#### PDFレポートの作成
HRVパラメータを計算してPDFレポートを生成する方法を示す以下の例をご覧ください。

```python
    # インポート
    import pyhrv

    # 5分間のサンプルNNIシリーズを読み込み
    nni = pyhrv.utils.load_sample_nni()

    # HRVパラメータを計算（表示しない）
    results = pyhrv.hrv(nni, show=False)

    # ステップ1：PDFReportオブジェクトを作成し、ECG信号、NNI、またはR-Peaksシリーズと結果を渡す
    report = pyhrv.report.PDFReport(nni=nni, results=results)

    # ステップ2：取得に関する一般情報を設定
    report.set_general_info(subject='Jon Doe',
                            experiment='Sample Report',
                            age=27,
                            gender='male',
                            comment='This is a sample comment in a sample report')

    # ステップ3：PDFレポートを作成
    report.create_report(terminal_output=True)
```

#### 独自のPDFレポートテンプレートの作成
PDFレポート用のLaTeXテンプレートファイルは[pyhrv/report/templates](./templates)フォルダにあります。お好みのLaTeXエディタでこれらのファイルを開いて、独自のレポートテンプレートを作成してください。

HRV結果は[parameters.tex](parameters.tex)ファイルに新しいコマンドとして保存され、レポートテンプレート全体で使用されることに注意してください。テンプレートのみを変更し、parameters.texファイルはそのままにしておくことをお勧めします。

可能であれば、カスタムレポートに参照を残してpyHRVの成長を支援してください。そのためには、この[リポジトリのメインREADME](https://github.com/PGomes92/pyhrv)で提案されている引用形式を使用するか、リポジトリのURLをフッターに注記として追加してください：

```latex
   \lfoot{HRV results \& report generated with pyHRV (v.\version)\\\url{https://github.com/PGomes92/pyhrv}}
```
