# defer
`defer`を通過しないと、`defer`された`function`は実行されない。
`defer`の前に`os.Exit()`した場合は、その`function`は実行されない。
`defer`した`function`を実行したいのであれば、エラーハンドリングの前に`defer`を記述しなければならない。
