# ストリーミング
準備が整ったコンポーネントから段階的にUIやデータを提供すること。

## 実装方法
### ページ全体のストリーミング
`loading.tsx`をページ単位で配置する。

`/app/dashboard`フォルダに`loading.tsx`ファイルを作成する。

```tsx:loading.tsx
export default function Loading() {
  return <div>Loading...</div>;
}
```

- `loading.tsx`は`Suspense`上に構築された特別なファイル
- ページの読み込みを待たずに、別のページへ移動できる(中断可能なナビゲーション)

### ロードスケルトン
コンテンツがロード中であることを表すプレースホルダーとして使用される。追加したUIは`loading.tsx`の一部として埋め込まれ、最初に送信される。

```tsx:loading.tsx
import DashboardSkeleton from '@/app/ui/skeletons';
 
export default function Loading() {
  return <DashboardSkeleton />;
}
```

`dashboard`フォルダに直接`loading.tsx`を配置すると、その配下のページ全てに適用される。
概要にのみ適用する場合、`(overview)`フォルダを作成し、`loading.tsx`および`page.tsx`ファイルをフォルダ内に移動する。
ダッシュボードの概要ページにのみ適用される。括弧`()`を使用してフォルダを作成すると、URLパスに含まれない。

### コンポーネントのストリーミング
`Suspense`を使用すると、より細かく特定のコンポーネントをストリーミングすることもできる。
`Suspense`は何かしらの条件を満たすまで、レンダリングを延期できる。動的コンポーネントを`Suspense`でラップし、動的コンポーネントをロード中に表示するフォールバックコンポーネントを渡す。

```tsx:page.tsx
import RevenueChart from '@/app/ui/dashboard/revenue-chart';
import { Suspense } from 'react';
import { RevenueChartSkeleton } from '@/app/ui/skeletons';

export default async function Page() {
  return (
    // ...
    <Suspense fallback={<RevenueChartSkeleton />}>
      <RevenueChart />
    </Suspense>
    // ...
  );
}
```

```tsx:revenue-chart.tsx
import { fetchRevenue } from '@/app/lib/data';
// ...

export default async function RevenueChart() { // Make component async, remove the props
  const revenue = await fetchRevenue(); // Fetch data inside the component
  // ...

  return (
    // ...
  );
}
```

### コンポーネントのグループ化
ラッパーコンポーネントを作成して、個々のコンポーネントをグループ化する。

```tsx:page.tsx
// import { Card } from '@/app/ui/dashboard/cards'; // 個々のカードコンポーネントは削除する
import CardWrapper from '@/app/ui/dashboard/cards';
// ...
import {
  CardsSkeleton,
} from '@/app/ui/skeletons';

export default async function Page() {
  return (
    // ...
    // 個々のカードコンポーネントは削除する
    // ラッパーされたCardWrapperコンポーネントを使用する
    // <Card title="Collected" value={totalPaidInvoices} type="collected" />
    // <Card title="Pending" value={totalPendingInvoices} type="pending" />
    // <Card title="Total Invoices" value={numberOfInvoices} type="invoices" />
    <Suspense fallback={<CardsSkeleton />}>
      <CardWrapper />
    </Suspense>
    // ...
  );
}
```

## ベストプラクティス
- データフェッチをそれを必要とするコンポーネントまで移動し、それらのコンポーネントをサスペンスでラップするのが良い方法
