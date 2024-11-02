# リンクとナビゲーション
`<Link />`コンポーネントを使用して、アプリケーション内のページをリンクできる。
`<a>`タグの代わりに`<Link>`を利用する。

```tsx:nav.tsx
import Link from 'next/link';

export default function NavLinks() {
  return (
    <>
      <Link>
      </Link>
    </>
  );
}
```

`<a>`タグの場合にはページ全体をレンダリングしていた動作が、`<Link>`コンポーネントでは一部のレンダリングのみで済む。

- メリット
  - 非常に高速なページ遷移を実現できる

## アクティブなリンクを表示する
`usePathname()`というフックを使用すると、ユーザーの現在のパスを取得することができる。
フックを使用するためには、クライアントコンポーネントに変換する必要がある。
クライアントコンポーネントに変換するためには、ファイルの先頭に`'use client';`を記述する。

```tsx:nav.tsx
import Link from 'next/link';
import { usePathname } from 'next/navigation';
import clsx from 'clsx';

export default function NavLinks() {
  return (
    <>
      <Link
        className={clsx(
          '/*共通のスタイル*/',
          {
            '/*アクティブなメニューのスタイル*/': pathname === link.href,
          },
        )}
      >
      </Link>
    </>
  );
}
```

## 注意事項
- クライアントコンポーネントは極力使わない
  - ユースケース
    - Hooksを利用するとき
    - イベントハンドラを利用するとき
    - ブラウザAPIを利用するとき
    - クライアント操作が多いコンポーネント
