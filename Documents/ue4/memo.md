# ■ 開発メモ

## ■ ソースファイルのエンコーディング
* windows(visual studio) の場合は sjis or BOM 付き utf-8 が利用（ビルド）可能。
* ただし、ソースファイル内に日本語は基本的に非推奨。
	* どうしても日本語を使いたい場合（動作確認のため一時的にログを仕込みたい、など）は utf-8 のほうがいい。
	* sjis のままだとどうなるか？
		* ログ(UE_LOG など)や widget （スレートなど）が文字化けする。
		* おそらくツールが utf-8 の想定で動作している。
* 文字列リテラルはソースに含めない。
	* 表示用のテキストは通常 LOCTEXT を利用する。


## ■ リソース名
* プロパティの名前取得方法
	* FText SPropertyEditorAsset::OnGetAssetName() const
		* UEdGraphNode からは遠いから難しいかも？
	* void SFindInMaterial::MatchTokens(const TArray<FString> &Tokens)
		* 検索の実装なので、名前を取る方法などがわかるかも



----
以上。
