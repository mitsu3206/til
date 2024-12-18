# 検索とページネーション
## 検索
以下のクライアントフックを使用する。

- useSearchParams
  - 現在のURLのパラメータにアクセスできる
  - `?page=1&query=pending`であれば、`{page: '1', query: 'pending'}`となる
- usePathname
  - 現在のURLのパス名を取得できる
- useRouter
  - クライアントコンポーネント内のルート間のナビゲーションをプログラムで有効にする

```tsx:search.tsx
'use client';

import { useSearchParams, usePathname, useRouter } from 'next/navigation';
 
export default function Search() {
  const searchParams = useSearchParams();
  const pathname = usePathname();
  const { replace } = useRouter();
 
  function handleSearch(term: string) {
    const params = new URLSearchParams(searchParams);
    if (term) {
      params.set('query', term);
    } else {
      params.delete('query');
    }
    replace(`${pathname}?${params.toString()}`);
  }
  return (
    <div>
      // ...
      <input
        className=""
        placeholder={placeholder}
        onChange={(e) => {
          handleSearch(e.target.value);
        }}
        defaultValue={searchParams.get('query')?.toString()}
      />
      // ...
    </div>
  );
}
```

### ベストプラクティス debounce
上記のコードの状態だと、入力のたびにデータベースがクエリされる。
デバウンスは関数が実行される頻度を制御する手法である。

```tsx:search.tsx
// ...
import { useDebouncedCallback } from 'use-debounce';
 
// Inside the Search Component...
const handleSearch = useDebouncedCallback((term) => {
  console.log(`Searching... ${term}`);
 
  const params = new URLSearchParams(searchParams);
  if (term) {
    params.set('query', term);
  } else {
    params.delete('query');
  }
  replace(`${pathname}?${params.toString()}`);
}, 300);
```

