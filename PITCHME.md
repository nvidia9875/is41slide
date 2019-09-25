---?color=#FDF5E6

IS41　セキュリティ課題発表<br><br>
『CFT』<br><br>
チームさかい
---?color=#FDF5E6
### 「 CTF 」とは 
<br>
- Capture The Flag（旗取りゲーム）の略<br><br>
- 情報セキュリティの技術を競う競技・ゲーム<br><br>
- 隠された答え（Flag）をセキュリティスキルを用いて探し、答えをサーバへ送信するクイズ形式が多い

+++?color=#FDF5E6

### 基本ルール
<br>
制限時間以内に得点を多く獲得したチームが勝利
- 制限時間：だいたい12h~48h(大会による)
- 検索 : オンライン，オフライン問わず可

+++?color=#FDF5E6

### 禁止事項
<br>
- 競技時間内の他チームのとのフラグ・解法の共有

---?color=#343434 
### 主な出題分野
<br>

@color[#FF8C00](・Reverse engineering, Binary) <br> 
@color[#FF8C00](・Network)<br>
@color[#FF8C00](・Forensics) <br>
@color[#FF8C00](・Pwn -脆弱性調査- ) <br>
@color[#FF8C00](・Web) <br>
@color[#FF8C00](・Cipher -暗号-) <br>
@color[#FF8C00](・programming)

---?color=#343434 
### Forensics
<br>

@color[#EEE](物理メモリのイメージファイルを解析し，必要な情報を得ること)<br> <br>
@color[#EEE](例えば犯罪捜査で)<br>
@color[#EEE](● 消えたファイルを特定) <br> 
@color[#EEE](● 一部が壊れたデータの復元) <br> 
@color[#EEE](● ファイルのタイムスタンプを調査) <br> 

---?color=#343434 
### Pwn
<br>

@color[#EEE](プログラムの脆弱性を突いてフラグを獲得する問題) <br> <br> 
@color[#EEE](どうやって解くの？) <br><br> 
@color[#EEE](1, プログラムは配布されるので、手元で解析) <br> 
@color[#EEE](2, 解析結果からファイルへアクセスする処理を行うコードを作成) <br> 
@color[#EEE](3, 実際に攻撃をしてフラグをゲット！) <br> 

---?color=#343434 
### 試しに解いてみよう

---?color=#343434

![](./assets/image01.png "ksnctf")


---?color=#343434

![](./assets/image02.png "ksnctf")

---?color=#343434

```
$ mv paper.docx paper.zip
$ mkdir ./ctf && unzip paper.zip -d ./ctf
$ cd ctf
$ ls

total 24
drwxr-xr-x   7 shunsuke  staff   224B Sep 25 16:28 .
drwx------+ 22 shunsuke  staff   704B Sep 25 18:24 ..
-rw-r--r--@  1 shunsuke  staff   6.0K Sep 25 16:28 .DS_Store
-rw-r--r--@  1 shunsuke  staff   2.4K Jan  1  1980 [Content_Types].xml
drwxr-xr-x@  3 shunsuke  staff    96B Sep 25 16:23 _rels
drwxr-xr-x@  4 shunsuke  staff   128B Sep 25 16:23 docProps
drwxr-xr-x@ 19 shunsuke  staff   608B Sep 25 16:23 word
```

---?color=#343434

```
$ cd word
$ ll
total 256
drwxr-xr-x@ 3 shunsuke  staff    96B Sep 25 16:23 _rels
-rw-r--r--@ 1 shunsuke  staff    42K Jan  1  1980 document.xml
-rw-r--r--@ 1 shunsuke  staff   1.4K Jan  1  1980 endnotes.xml
-rw-r--r--@ 1 shunsuke  staff   2.0K Jan  1  1980 fontTable.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 footer1.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 footer2.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 footer3.xml
-rw-r--r--@ 1 shunsuke  staff   1.4K Jan  1  1980 footnotes.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 header1.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 header2.xml
-rw-r--r--@ 1 shunsuke  staff   1.2K Jan  1  1980 header3.xml
drwxr-xr-x@ 3 shunsuke  staff    96B Sep 25 16:23 media
-rw-r--r--@ 1 shunsuke  staff   3.0K Jan  1  1980 settings.xml
-rw-r--r--@ 1 shunsuke  staff    16K Jan  1  1980 styles.xml
-rw-r--r--@ 1 shunsuke  staff    17K Jan  1  1980 stylesWithEffects.xml
drwxr-xr-x@ 3 shunsuke  staff    96B Sep 25 16:23 theme
-rw-r--r--@ 1 shunsuke  staff   428B Jan  1  1980 webSettings.xml


//これは見つからなかった
$ grep -r "flag" -i document.xml

```

---?color=#343434
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<w:document xmlns:wpc="http://schemas.microsoft.com/office/word/2010/wordprocessingCanvas" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" xmlns:o="urn:schemas-microsoft-com:office:office" xmlns:r="http://schemas.openxmlformats.org/officeDocument/2006/relationships" xmlns:m="http://schemas.openxmlformats.org/officeDocument/2006/math" xmlns:v="urn:schemas-microsoft-com:vml" xmlns:wp14="http://schemas.microsoft.com/office/word/2010/wordprocessingDrawing" xmlns:wp="http://schemas.openxmlformats.org/drawingml/2006/wordprocessingDrawing" xmlns:w10="urn:schemas-microsoft-com:office:word" xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main" xmlns:w14="http://schemas.microsoft.com/office/word/2010/wordml" xmlns:wpg="http://schemas.microsoft.com/office/word/2010/wordprocessingGroup" xmlns:wpi="http://schemas.microsoft.com/office/word/2010/wordprocessingInk" xmlns:wne="http://schemas.microsoft.com/office/word/2006/wordml" xmlns:wps="http://schemas.microsoft.com/office/word/2010/wordprocessingShape" mc:Ignorable="w14 wp14"><w:body><w:p w:rsidR="00433D93" w:rsidRPr="000E7386" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/><w:jc w:val="center"/><w:rPr><w:sz w:val="48"/></w:rPr></w:pPr><w:bookmarkStart w:id="0" w:name="_GoBack"/><w:bookmarkEnd w:id="0"/><w:r w:rsidRPr="000E7386"><w:rPr><w:rFonts w:hint="eastAsia"/><w:sz w:val="48"/></w:rPr><w:t>P is equal to NP</w:t></w:r></w:p><w:p w:rsidR="00433D93" w:rsidRPr="00E22D59" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/><w:jc w:val="center"/></w:pPr></w:p><w:p w:rsidR="00433D93" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/><w:jc w:val="center"/></w:pPr><w:r><w:rPr><w:rFonts w:hint="eastAsia"/></w:rPr><w:t>No Author Given</w:t></w:r></w:p><w:p w:rsidR="00433D93" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/><w:jc w:val="center"/></w:pPr><w:r><w:rPr><w:rFonts w:hint="eastAsia"/></w:rPr><w:t>No Institute Given</w:t></w:r></w:p><w:p w:rsidR="00433D93" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/></w:pPr></w:p><w:p w:rsidR="00433D93" w:rsidRDefault="00433D93" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/></w:pPr><w:r w:rsidRPr="00CE5FAA"><w:rPr><w:rFonts w:hint="eastAsia"/><w:b/></w:rPr><w:t>Abstract.</w:t></w:r><w:r><w:rPr><w:rFonts w:hint="eastAsia"/></w:rPr><w:t xml:space="preserve"> In this paper, we prove that the complexity classes P and NP are equal by showing that the 3-SAT problem can be solved in deterministic polynomial time.</w:t></w:r></w:p><w:p w:rsidR="00433D93" w:rsidRDefault="002653CD" w:rsidP="00433D93"><w:pPr><w:spacing w:line="360" w:lineRule="auto"/></w:pPr><w:r><w:rPr><w:rFonts w:hint="eastAsia"/><w:b/><w:noProof/><w:sz w:val="24"/><w:szCs w:val="28"/></w:rPr><w:drawing><wp:anchor distT="0" distB="0" distL="114300" distR="114300" simplePos="0" relativeHeight="251658240" behindDoc="0" locked="0" layoutInCell="1" allowOverlap="1" wp14:anchorId="2060EB98" wp14:editId="413AD905"><wp:simplePos x="0" y="0"/><wp:positionH relativeFrom="column"><wp:posOffset>3958590</wp:posOffset></wp:positionH><wp:positionV relativeFrom="paragraph"><wp:posOffset>194945</wp:posOffset></wp:positionV><wp:extent cx="1548765" cy="1409700"/><wp:effectExtent l="0" t="0" r="0" b="0"/><wp:wrapSquare wrapText="bothSides"/><wp:docPr id="2" name="図 2" descr="C:\Users\FLxAG_NTSCFTTKP5ZDDW\Documents\paper\P is equal to NP\remove_x\200px-Complexity_subsets_pspace.svg.png"/><wp:cNvGraphicFramePr><a:graphicFrameLocks xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main" noChangeAspect="1"/></wp:cNvGraphicFramePr><a:graphic xmlns:a="http://schemas.openxmlformats.org/drawingml/2006/main"><a:graphicData uri="http://schemas.openxmlformats.org/drawingml/2006/picture"><pic:pic xmlns:pic="http://schemas.openxmlformats.org/drawingml/2006/picture"><pic:nvPicPr><pic:cNvPr id="0" name="Picture 2" descr="C:\Users\FLxAG_NTSCFTTKP5ZDDW\Documents\paper\P is equal to 
```
---?color=#343434
```
descr="C:\Users\FLxAG_NTSCFTTKP5ZDDW\Documents\paper\P is equal to 
```
---?color=#343434

```
//フラグっぽいぞ〜！？
FLxAG_NTSCFTTKP5ZDDW
```

---?color=#343434

![](./assets/image05.png "ksnctf")

---?color=#343434

```
//FLxAGのxを消してみる
FLxAG_NTSCFTTKP5ZDDW
        ↓
FLAG_NTSCFTTKP5ZDDW
```

---?color=#343434

![](./assets/image06.png "ksnctf")

---?color=#343434

