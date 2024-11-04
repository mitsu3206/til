# 部分的な事前レンダリング(PPR)
Ver.14から追加された比較的新しいレンダリング方式。
ページ単位からUI単位でレンダリング方式を決定する考え方になる。

PPRはStreaming SSRをさらに進化させた技術で、ページをstatic renderingとしつつ、部分的にdynamic renderingにすることが可能なレンダリングモデルである。
SSG・ISRのページの一部にSSRな部分を組み合わせられるようなイメージ、あるいはStreaming SSRのスケルトン部分をSSG/ISRにするイメージ。

まだ実験的に導入された機能ではあるが、今後のデフォルトのレンダリング方式となる可能性がある。

## 実装方法

```ts:next.config.ts
/** @type {import('next').NextConfig} */
 
const nextConfig = {
  experimental: {
    ppr: 'incremental',
  },
};
 
export default nextConfig;
```

```tsx:layout.tsx
import SideNav from '@/app/ui/dashboard/sidenav';
 
export const experimental_ppr = true;
 
// ...
```
