# Java Cheat Sheet
※Java初学者のチートシートです
※Claude Codeと壁打ちしながらやっています。時折調べていますがもしかしたらハルシネーションを起こしている可能性もあります、ご注意ください。

## Directory structure
```
java/
├─ notebooks/ # 文法まとめ(.ipynb + JJava)
├─ src/ # クラスを使ったソースコード(.java)
├─ .gitignore
└ README.md
```

## Contents


## Environment
|項目|バージョン|
|---|---|
|JDK|Eclipse Temurin 25（LTS）|
|エディタ|VS Code|
|拡張|Extension Pack for Java / Jupyter #どちらもMicrosoft|
|Python|3.14 #Jupyter用|
|Javaカーネル|JJava 1.0-a8|

## Environment setup(as of October 31,2026)
1. JDKを入れる
    ```PoworShell
    winget install EclipseAdoptium.Temurin.25.JDK
    ```
    開き直す、または別のタブで以下のコマンドを打つ
    ```PowerShell
    java -version        # openjdk version "25.x.x" ならOK
    where.exe java       # Temurinが一番上に来ているか
    echo $env:JAVA_HOME  # Temurin 25のフォルダを指しているか
    ```
2. VS Codeの拡張を入れる
    `Ctrl + Shift + X`か拡張機能のアイコンから2つの拡張機能を導入する
    - Extension Pack for Java
    - Jupyter
3. Python仮想環境を作ってJupyterを入れる
    ```PowerShell
    mkdir notebooks, src
    py -m venv .venv
    .venv\Scripts\python -m pip install jupyter
    .venv\Scripts\jupyter --version   # 一覧が出ればOK
    ```
    ※`activate`を使わず、`.venv\Scripts\python`を直接呼ぶとPowerShellの実行ポリシーで止まらない
4. JJavaカーネルを入れる
    1. [JJavaのRelease](https://github.com/dflib/jjava/releases)から最新の`jjava-x.x-kernelspec.zip`をダウンロード
    2. 解凍して、`kernel.json`があるフォルダを指定して登録する
    ```PowerShell
    .venv\Scripts\jupyter kernelspec install <解凍したフォルダ> --user --name=java
    .venv\Scripts\jupyter kernelspec list   # java が出ればOK
    ```
5. VS Codeで動作確認
    1. `notebooks/`に`.ipynb`ファイルを作る
    2. 右上の「Select Kernel」→「Jupyter Kernel」→「Java(jjava)」
    3. セルを実行 # `Shift + Enter` or `左のボタン`
   ```java
   var list = new ArrayList<String>(List.of("b", "a", "c"));
   Collections.sort(list);
   list
   ```
   [a,b,c](notebooks\test.ipynb)と出れば成功

## 注意点
- VS CodeのJava拡張はJDK 21以上が必要で、今後25以上に上がる予定。LTSの25を使っておけば安全
- JJavaはまだアルファ版。古い記事で紹介されている「IJava」はメンテが止まっているので使わない
- PyPIの jjava は古い版なので、GitHubのReleasesから入れる
- `src/`のクラスは`javac -d out src\*.java`でコンパイルし、ノートブックで`%classpath ../out`と書けば読み込める
