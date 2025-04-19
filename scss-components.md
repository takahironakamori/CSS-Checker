# SCSS Components Reference（再利用スニペット集）

このドキュメントは、共通で使いまわせるSCSSコンポーネントのコードスニペット集です。BEM設計に基づき、SCSSによるコンポーネント設計を効率化するために活用します。

---

## Button（ボタン）

```scss
.button {
  display: inline-block;
  padding: 0.5em 1.2em;
  font-size: 1rem;
  font-weight: bold;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: $color-primary;
  color: #fff;
  transition: background-color 0.2s;

  &:hover {
    background-color: darken($color-primary, 10%);
  }

  &--secondary {
    background-color: $color-gray-300;
    color: $color-text;

    &:hover {
      background-color: $color-gray-400;
    }
  }

  &--disabled {
    background-color: $color-gray-200;
    color: $color-gray-500;
    cursor: not-allowed;
  }
}
```

---

## Input Field（フォーム入力）

```scss
.input-field {
  display: block;
  width: 100%;
  padding: 0.6em;
  font-size: 1rem;
  border: 1px solid $color-border;
  border-radius: 4px;

  &:focus {
    outline: none;
    border-color: $color-primary;
    box-shadow: 0 0 0 2px rgba($color-primary, 0.2);
  }

  &--error {
    border-color: $color-error;
    background-color: lighten($color-error, 45%);
  }
}
```

---

## Card（カード）

```scss
.card {
  border: 1px solid $color-border;
  border-radius: 6px;
  padding: 1rem;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(#000, 0.05);

  &__title {
    font-size: 1.2rem;
    margin-bottom: 0.5rem;
    font-weight: bold;
  }

  &__content {
    font-size: 1rem;
    color: $color-text;
  }

  &--highlighted {
    border-color: $color-accent;
    background-color: lighten($color-accent, 45%);
  }
}
```

---

## Alert（お知らせ／警告表示）

```scss
.alert {
  padding: 1rem;
  border-left: 5px solid;
  background-color: $color-gray-100;
  margin-bottom: 1rem;

  &--info {
    border-color: $color-info;
    background-color: lighten($color-info, 40%);
  }

  &--success {
    border-color: $color-success;
    background-color: lighten($color-success, 40%);
  }

  &--error {
    border-color: $color-error;
    background-color: lighten($color-error, 40%);
  }
}
```

---

## Utility：clearfix

```scss
@mixin clearfix {
  &::after {
    content: '';
    display: table;
    clear: both;
  }
}
```

---

## コンポーネントの使い方

- それぞれのスニペットは `_components/` フォルダに分割し、必要なものだけインポートして使用
- モディファイア（`--error`, `--highlighted` など）はできるだけ明確な状態に限定
- コンポーネント化せず直書きしがちなスタイルは都度ここに追加・整理

---

## メモ

- プロジェクトに応じて `$color-*` などの変数は差し替えOK
- 基本の命名ルールは `scss-guidelines.md` に従うこと
- 再利用性を優先し、過剰なネストや依存を避ける