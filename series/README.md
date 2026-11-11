# 安全なAI社会形成に関する三段階研究

**日本語** · [English](README.en.md)

自動車社会で安全を支えてきた制度の機能を整理し、AIが人から仕事を任され、外部システムに働きかける社会に必要な要件と参照設計へつなげます。以下のリンクから、原稿を再構成した公開編集版を読めます。日英で公開範囲をそろえています。

| 読む順番 | 各論文の役割 |
| --- | --- |
| [第001論文｜歴史的根拠](paper-001/README.md) · [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/series/paper-001/editions/MGL-REF-002-v1.0.0-ja.pdf) | 登録・資格・継続検査などの制度を調べ、他の領域でも検討できる機能を抽出する |
| [第002論文｜要求工学](paper-002/README.md) · [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/series/paper-002/editions/MGL-REF-003-v1.0.0-ja.pdf) | 抽出した機能を、識別、権限委任、証跡、失効、復旧などの要件に変換する |
| [第003論文｜参照アーキテクチャ](paper-003/README.md) · [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/series/paper-003/editions/MGL-REF-004-v1.0.0-ja.pdf) | 要件を、信頼境界、実行時の制御点、証跡、検証項目に対応づける |
| [統合版 v1.1｜セキュリティ付録](security-annex/README.md) · [PDF v1.0.0](https://github.com/masaogatelabs-dev/mgl-research/blob/792de6c54073e8fe19a86e7544672f5f668ca709/series/security-annex/editions/MGL-REF-005-v1.0.0-ja.pdf) | プロンプトインジェクションや過剰な権限などを例に、どの対策がどの段階を受け持つかを整理する |

たとえば「資格の失効」という制度上の機能から、AIに委任した権限を取り消せるという要件を導きます。参照設計では、その要件を「失効後の操作を実行時に拒否できるか」という検証項目につなげます。

[政策・技術提言](../proposals/README.md) · [事案分析・適用例](../cases/README.md) · [トップ](../README.md)

