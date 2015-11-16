# geonamesjp_vs_ndlna
[GeoNames.jp](http://geonames.jp/) と[国立国会図書館典拠データ](http://id.ndl.go.jp/auth/ndla) のリンクセット

> このレポジトリのリンクセットは Web NDL Authorities の外部提供インタフェースを用いて作成されました。


## What's this?
GeoNames.jp と国立国会図書館典拠データのURIを [skos:exactMatch](http://www.w3.org/2004/02/skos/core#exactMatch) で結ぶリンクセットです。

このリンクセットのライセンスは  [CC-BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/) です。


## Target
Web NDL Authorities の外部提供インタフェースの SPARQL Endpoint に対して、以下の SPARQL相当のクエリーを実行することで得られた URI を対象としてリンクセットの作成を行っています。

    select ?s ?label ?rel where {
      ?s  <http://www.w3.org/2004/02/skos/core#inScheme> <http://id.ndl.go.jp/auth#geographicNames> ;
          <http://www.w3.org/2000/01/rdf-schema#label> ?label ;
          <http://www.w3.org/2004/02/skos/core#relatedMatch> ?rel . 
          filter regex( ?rel, "^http://id.ndl.go.jp/class/ndlc/GC.*" )
    }

<http://id.ndl.go.jp/auth#geographicNames> に所属する概念であり、かつ、関連する概念として <http://id.ndl.go.jp/class/ndlc/GC??????> が設定されていることを抽出条件としています。NDLC については [国立国会図書館分類表](http://www.ndl.go.jp/jp/data/catstandards/classification_subject/ndlc.html) を参照してください。

なお、当該 SPARQL エンドポイントでは 100 件の上限が設定されているために (2015/11/16現在)、すべてのデータを取得するために別途 OFFSET 句を設定しています。SPARQL エンドポイントの制限については <http://iss.ndl.go.jp/ndla/sparql/> をご確認ください。

## Example

    @prefix skos:  <http://www.w3.org/2004/02/skos/core#> .
    
    <http://geonames.jp/resource/北海道>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00258064> .
    <http://geonames.jp/resource/北海道三石郡三石町>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00367275> .
    <http://geonames.jp/resource/北海道三笠市>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00275209> .
    <http://geonames.jp/resource/北海道上川郡上川町>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00367244> .
    <http://geonames.jp/resource/北海道上川郡下川町>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00366697> .
    <http://geonames.jp/resource/北海道上川郡剣淵町>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00366732> .
    <http://geonames.jp/resource/北海道上川郡和寒町>  skos:exactMatch  <http://id.ndl.go.jp/auth/ndlna/00367250> .
	
## Note
* 3,742 Triples (2015/11/16時点)


