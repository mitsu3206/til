# ルートの定義
ルートを定義するには、appディレクトリ配下にURLのパスとしたい新しいディレクトリを作成し、その中に`page.tsx`ファイルを作成する。

/app/dashboard/page.tsx

```tsx:page.tsx
// 必ずデフォルトエクスポート(export default function)で定義する。。
export default function Page() {
  return <p>Dashboard Page</p>;
}
```

この場合、`https://example.com/dashboard`となる。

さらに、`layout.tsx`という特別なファイルを`/app/dashboard/layout.tsx`に作成すると、その`dashboard`配下のページで共有のUIを作成することができる。

```tsx:layout.tsx
// 必ずデフォルトエクスポート(export default function)で定義する。。
export default function Layout({ children }: { children: React.ReactNode }) {
  return
    <div>
      // ヘッダーやサイドバーなどの共通のUI
    </div>
    <div>
      <div>{children}</div>
    </div>
  );
}
```

注目すべきは、`Layout`コンポーネントに`children`というpropsを受け取っていること。
このように記述することで、配下のページを`{children}`にインポートして`Layout`コンポーネントに自動的にネストされる。
`/app/dashboard/invoices/page.tsx`を作成したとすると、`/app/dashboard`に作成した`layout.tsx`の`{children}`にインポートされる。

## 注意事項
- `page.tsx`や`layout.tsx`は必ずデフォルトエクスポート(export default function)で定義すること。
  - コンパイルエラーとなるため。
