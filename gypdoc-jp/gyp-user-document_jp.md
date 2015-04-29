\# GYP(Generate Your Project) User Documentation 日本語訳  
原文ステータス: Draft(as of 2009-05-19)  
原文著者:  Mark Mentovai mark@chromium.org, Steven Knight sgk@chromium.org et al.  
原文更新日: 2009-05-19  
翻訳ステータス: 未完成
翻訳者: underdolphin(masato sueda) underdolphin@users.noreply.github.com  
翻訳更新日: 2015-04-29
###コンテンツ

* イントロダクション
* 日本語訳にあたって
* Chromiumにおけるgypファイルの例
* 実行可能形式ターゲットにおける標準的なgypファイルの例
* ライブラリを作成する標準的なgypファイルの例
* ユースケース
    * 新しいソースファイルの追加
    * 新しい実行可能形式プログラムのための設定の追加
    * ターゲットへの設定の追加
    * クロスコンパイル
    * 新しいライブラリの追
    * ターゲット間の依存関係
    * Mac OS Xバンドルのためのサポート
    * ファイルの移動(リファクタリング)
    * カスタムビルドステップ
    * ビルドフレーバー  

###イントロダクション  
 このドキュメントは、GYPのユーザーレベルにおけるガイドを提供する目的のものです。ここではとしては特定のタスクを想定しGYPを使用することに重点を置き、具体的な技術や言語仕様については説明しません。(そのためには、[LanguageSpecification](https://chromium.googlesource.com/external/gyp/+/HEAD/docs/LanguageSpecification.md)を参照してください。)  
 このドキュメントでは、.gypファイル自体の構造の概要、実行可能形式への設定の概要、ライブラリ形式への設定の概要の説明から始まります。  
 概要の説明の後に、異なる一般的なユースケースのための例を記述しています。

###日本語訳にあたって
このドキュメントの原文は以下のリンク先にあります。  
[GYP User Documentation](https://chromium.googlesource.com/external/gyp/+/HEAD/docs/UserDocumentation.md)  
リンク先は変更されている可能性があります。ご容赦ください。  
また原文のライセンスが不明ではありますが、一応翻訳文書は[CC BY-SA 4.0](http://creativecommons.org/licenses/by-sa/4.0/) にて配布するのものとします。

###Chromiumにおけるgypファイルの例  

下にあるのはChromiumにおける典型的な.gypファイルの記述例です。  

```python
{
    'variables': {  
    .
    .
    .
    },
    'includes': [
      '../build/common.gypi',
    ],
    'target_defaults': {
      .
      .
      .
    },
    'targets': [
      {
        'target_name': 'target_1',
          .
          .
          .
      },
      {
        'target_name': 'target_2',
          .
          .
          .
      },
    ],
    'conditions': [
      ['OS=="linux"', {
        'targets': [
          {
            'target_name': 'linux_target_3',
              .
              .
              .
          },
        ],
      }],
      ['OS=="win"', {
        'targets': [
          {
            'target_name': 'windows_target_4',
              .
              .
              .
          },
        ],
      }, { # OS != "win"
        'targets': [
          {
            'target_name': 'non_windows_target_5',
              .
              .
              .
          },
      }],
    ],
  }
```  
