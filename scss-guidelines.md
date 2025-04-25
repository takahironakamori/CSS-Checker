# SCSSコーディングガイドライン

このドキュメントは、私自身のSCSSコーディングルールを整理し、プロジェクト間でのブレをなくすためのリファレンスとして作成したものです。

---

## 命名規則（BEM）

### 基本構造

```
.prefix--block {}
.prefix--block--variation {}
.prefix--block__element {}
.prefix--block--variation__element {}
.prefix--block__element--variation {}
.prefix--block--variation__element--variation {}
```

### prefix（接頭辞）

- プロジェクト名、ページの種類、役割等、ざっくりとした役割を明示するために prefix（接頭辞）をつけることができます。
- 公開用のウェブページ等、prefix をつけないこともできます。

#### 例

- 管理画面のタブ : `admin--tabs`
- エディタのタブ（管理画面のタブとはわけておきたい） : `blog-editor--tabs`
- 公開用ホーム画面のヘッダ（prefix無し） : `header`

### block(かたまり)

- コンポーネント名を block として使用できます。
- 複数の単語でコンポーネント名が構成される場合は、`-` でつなぎます。 

#### 例

- 管理画面のタブ : `admin--tabs`
- 公開用ホームページのお問い合わせフォーム : `contact-form`

#### 「複数」の block の命名規則

| 正しい | 使用不可の例 | 
|-------|-------|
| `--buttons` | `--button-group` |
| `--cards` | `--card-group` |
| `--tabs` | `--tab-group` |
| `--items` | `--list` |


### variation(バリエーション)

- block や element について、バリエーションがある場合は、variation をつけます。
- variation は `A01` のような汎用なものや、`primary` などのラベルをつけることができます。
- variation は block 、element のそれぞれについて複数回使用することはできません。
- 下記の modifiter で使用している状態名を使用することはできません。

#### 例

- 管理画面のタブの別バージョン : `admin--tab--A01`
- お問い合わせフォームの重要なボタン : `contact-form__button--primary`


#### pattern : パターンバリエーション

- 特定の意味を持たせず、デザインの違いだけを区別するためのバリエーションは `--A01`, `--A02` のように命名します。このような記号的バリエーションを **パターンバリエーション** と呼びます。
- 明確な意味を持つ場合は --primary などのラベル付きバリエーションを使います。

```scss
.button--A01 {} // デザインパターン1
.button--A02 {} // デザインパターン2
```


#### style : スタイルバリエーション

- 見た目を変更するバリエーション

```scss
.button--fill {} // 塗りつぶしのボタン
.button--outline {} // 枠線だけのボタン
```


#### size : サイズバリエーション

- 大きさを指定するバリエーション
- ボタンや要素のサイズバリエーションは、命名が長くなりすぎないように **省略表記（略称）を使って統一**します。
- 以下は、推奨されるサイズ略称と、使用を避けるべきフル表記の例です。

| サイズ | 推奨略称（正しい） | 使用不可の例（誤り） |
|--------|--------------------|-----------------------|
| extra-extra-small | `xxs` | `extra-extra-small` |
| extra-small | `xs` | `extra-small` |
| small        | `s`  | `small` |
| medium       | `m`  | `medium` |
| large        | `l`  | `large` |
| extra-large  | `xl` | `extra-large` |
| extra-extra-large | `xxl` | `extra-extra-large` |

```scss
.button--fill--s {}
.button--fill--m {}
.button--fill--l {}
.button--fill--xl {}
.button--fill--xxl {}
```

#### label : ラベルバリエーション

- 特定の意味や状態を示す、ラベル名を持つバリエーションで以下があります。

| ラベルバリエーション | 推奨用途                            | イメージ                         | 対象アクションの例                     |
|----------------------|-------------------------------------|----------------------------------|----------------------------------------|
| `--primary`          | 最重要アクション・ページで1つだけ  | ブランドカラー or 強調されたボタン | フォームの送信 / 次へ進む / 購入する     |
| `--secondary`        | 補助的なアクション（primaryの次に大事） | 落ち着いたカラー / 控えめ         | 戻る / キャンセル / 編集する           |
| `--info`             | 情報の提示や通知                    | 青系カラーで冷静・中立           | 詳細を見る / お知らせ / チュートリアル開始 |
| `--positive`         | 成功・完了など良い結果を強調        | 緑系 / 明るい安心感              | 保存成功 / 完了 / 有効化する            |
| `--notice`           | 注意喚起・軽い警告                  | オレンジ・黄色系で目を引く       | 一部未入力 / 古いデータの確認 / 下書き保存 |
| `--negative`         | 否定・削除・注意の必要なアクション   | 赤系 / 危険・緊急を連想          | 削除 / 退会 / キャンセル確認            |
| `--accent`           | 装飾的・強調目的（機能的ではない）   | 補助カラー / アクセント的使い方   | フィルタータグ / ラベル表示 / 特別扱い要素 |

- ユーザーの行動を誘導する強さ順に： primary > secondary > info / positive<br>
フィードバック的要素： positive, notice, negative<br>
視覚の補助要素： accent

#### バリエーションが複数ある場合

- クラス名は、以下の順番で variation をつけて記述します。
- バリエーションが複数ある場合は、バリエーションごとにクラスを分離して定義・使用する方式を原則とします。
- 順番：`block--[pattern]` `block--[style]` `block--[size]` `block--[label]`

#### 使用例

| バリエーション | 正しい使用例 | 誤りの使用例 |
|--------------------|--------------------|-----------------------|
| `A01`, `fill`, `m`, `primary` | `button--A01` `button--fill` `button--m` `button--primary` | `button--A01--fill--m--primary` |


### element(構成要素)

- コンポーネントを構成する要素を element と使用できます。
- element は入れ子にすることができます。
- element のネスト階層は2階層以内（`__`を使うのは2回まで）が理想だが、明確な意味があり、読みやすさ・保守性に問題がなければ3階層以上も許容します。

#### 例

- 管理画面のタブのラベル : `admin-tab__label`
- ヘッダのロゴ : `header__logo`
- ヘッダーのロゴの画像 : `header__logo__img`


### modifier(状態)

- modifier は、以下に明記されたもののみ使用することができます。
- modifier は、必ず "--" で始まります。
- modifier は必ず別のクラスとして使用します（半角スペースで区切ってください）。
- 同時に複数の modifier を使用することができます。

#### 選択されている状態

| 正しい | 使用不可の例 | 
|-------|-------|
| `--active` | `--is-active`, `--selected`, `--checked` |

#### エラーがある状態

| 正しい | 使用不可の例 | 
|-------|-------|
| `--error` | `--is-error`, `--has-error` |

#### 開いている状態

| 正しい | 使用不可の例 | 
|-------|-------|
| `--open` | `--is-open`, `--opened` |

#### アニメーションで表示する

- 【正】まず `--on` を加え、すぐ（10ms）に `--show` を加える。
- 【誤】`--show` だけを加える。
- 【誤】`--visible` を使用する。

#### アニメーションで非表示する

- 【正】あらかじめ `--on --show` をつけておき、まず `--show` を消して、数秒（250ms）後に `--on` を消す。
- 【誤】まず `--hide` を加え、数秒後に `--off` を加える。

#### 使用不可

| 正しい | 使用不可の例 | 
|-------|-------|
| `--disabled` | `--is-disabled`, `--disable`, `--none` |

#### 非表示

| 正しい | 使用不可の例 | 
|-------|-------|
| `--hidden` | `--is-hidden`, `--invisible`, `--hide` |

#### ローディング中

| 正しい | 使用不可の例 | 
|-------|-------|
| `--loading` | `--is-loading`, `--load`, `--spinner` |

#### 操作不能

| 正しい | 使用不可の例 | 
|-------|-------|
| `--readonly` | `--read-only`, `--no-edit` |

#### フォーカス中

| 正しい | 使用不可の例 | 
|-------|-------|
| `--focus` | `--focused`, `--is-focus` |

#### ホバー中

| 正しい | 使用不可の例 | 
|-------|-------|
| `--hover` | `--hovered`, `--is-hover` |

---

### utility(例外処理)

- utility を使用して例外的に表示を変更することができます。
- utility は、必ず "u--" で始まり、基本構造は u--block--variation です。
- utility は必ず別のクラスとして使用します（半角スペースで区切ってください）。
- 同時に複数の utility を使用することができます。

#### 例

- 段落の余白（下）を大きくする : `paragraph--m n--mb--l`

## SCSS構造とファイル分割

```
/ styles
  ├── style.scss                ... ウェブページが読み込むファイル。app 以下必要なSCSSを読み込む。
  ├── app                       ... ページ別の scss。 値は themes ディレクトリ内で指定しているものしか使えない。
  │   ├── app.scss              ... アプリ全体で使用する scss。
  │   └── [page_name].scss      ... ページ個別で使用する scss（例:home, category, single, login, page）。
  ├── components                ... コンポーネント別の scss。値は themes ディレクトリ内で指定しているものしか使えない。
  │   ├── ui                    ... UIパーツ別の scss。
  │   │   └── [ui_name].scss    ... UIパーツのCSS。Headless UI の scss（例:tab, dialog, dropdown, button）。
  │   └── [component_name].scss ... コンポーネント個別で使用する scss（例:header, footer, card, appNav）。
  ├── themes                    ... テーマ用 scss。
  │   ├── _common.scss          ... テーマ共通 scss。
  │   ├── _dark.scss            ... ダークカラーテーマ用 scss。
  │   ├── _light.scss           ... 標準カラーテーマ用 scss。
  │   └── _themes.scss          ... app.scss が読み込むファイル。すべてのテーマ用CSSを束ねる。
  └── tokens                    ... cssの値を指定している scss。
      ├── aliases
      │   ├── _common.scss      ... values/color 以外の values 内の scss を束ねる。
      │   ├── _dark.scss        ... ダークカラーテーマ用の色に関する scss を束ねる。 
      │   ├── _light.scss       ... 標準カラーテーマ用の色に関する scss を束ねる。  
      │   └── _static.scss      ... 固定カラーテーマ用の色に関する scss を束ねる。  
      └── values
          ├── color             ... 色に関する値を指定する。
          │   ├── _dark.scss    ... ダークカラーテーマ用の色の値を指定する scss。 
          │   ├── _light.scss   ... 標準カラーテーマ用の色の値を指定する scss。   
          │   └── _static.scss  ... 固定カラーテーマ用の色の値を指定する scss。  
          ├── _background.scss  ... background に関する値を指定する scss。
          ├── _border.scss      ... border に関する値を指定する scss。
          ├── _box-shadow.scss  ... box-shadow に関する値を指定する scss。   
          ├── _box-sizing.scss  ... box-sizing に関する値を指定する scss。
          ├── _clear.scss       ... clear に関する値を指定する scss。
          ├── _cursor.scss      ... cursor に関する値を指定する scss。    
          ├── _display.scss     ... display に関する値を指定する scss。
          ├── _float.scss       ... float に関する値を指定する scss。
          ├── _font.scss        ... font に関する値を指定する scss。   
          ├── _image.scss       ... image に関する値を指定する scss。
          ├── _list.scss        ... list に関する値を指定する scss。
          ├── _margin.scss      ... margin に関する値を指定する scss。    
          ├── _overflow.scss    ... overflow に関する値を指定する scss。
          ├── _padding.scss     ... padding に関する値を指定する scss。
          ├── _position.scss    ... position に関する値を指定する scss。   
          ├── _table.scss       ... table に関する値を指定する scss。
          ├── _text.scss        ... text に関する値を指定する scss。
          ├── _transition.scss  ... transition に関する値を指定する scss。 
          ├── _visibility.scss  ... visibility に関する値を指定する scss。 
          └── _z-index.scss     ... z-index に関する値を指定する scss。    
```

---

## スタイルの設定

- app, components ディレクトリ内の各 scss ファイルでのスタイルは、以下のように変数で設定します。
- 色に関する変数は themes/_dark.scss, _light.scss の両方で指定されている変数名を指定します。
- 色以外に関する変数は themes/common.scss で指定されている変数名を指定します。

### 誤っている例（値を指定している）
```
.page {
  margin: 0;
  background: rgb(255, 255, 255);
}
```

### 正しい例（変数名を指定している）
```
.page {
  margin: var(--margin--none);
  background: var(--background-color--default);
}
```

---

## 禁止事項

- `!important` の多用
- `id`セレクタでのスタイリング
- JavaScriptの状態クラスと整合しない命名

---

## メンテナンス時のチェックポイント

- クラス名に意味があるか？
- コンポーネントが再利用しやすくなっているか？
- スタイルがコンポーネント単位で閉じているか？
- 古い変数や未使用スタイルが混在していないか？
- tokens 内以外の scss ファイルで値を直接指定していないか？

---

