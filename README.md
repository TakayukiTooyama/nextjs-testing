## Project setup : Nextjs+React-testing-library+TypeScript+Tailwind CSS

## 1. Nextjs Project 新規作成

### 1-1. create-next-app

    npx create-next-app . --use-npm

#### Node.js version 10.13 以降が必要です。 -> ターミナル `node -v`で ver 確認出来ます。

### 1-2. 必要 module のインストール

    npm i axios msw swr

### 1-3. prettier の設定 : package.json

```
    "prettier": {
        "singleQuote": true,
        "semi": false
    }
```

## 2. React-testing-library の導入

### 2-1. 必要 module のインストール

    npm i -D jest @testing-library/react @types/jest @testing-library/jest-dom @testing-library/dom babel-jest @testing-library/user-event jest-css-modules

### 2-2. Project folder 直下に".babelrc"ファイルを作成して下記設定を追加

    touch .babelrc

```
    {
        "presets": ["next/babel"]
    }
```

### 2-3. package.json に jest の設定を追記

```
    "jest": {
        "testPathIgnorePatterns": [
            "<rootDir>/.next/",
            "<rootDir>/node_modules/"
        ],
        "moduleNameMapper": {
            "\\.(css)$": "<rootDir>/node_modules/jest-css-modules"
        }
    }
```

### 2-4. package.json に test script を追記

```
    "scripts": {
        ...
        "test": "jest --env=jsdom --verbose"
    },
```

## 3. TypeScript の導入

https://nextjs.org/learn/excel/typescript/create-tsconfig

### 3-1. 空の tsconfig.json 作成

    touch tsconfig.json

### 3-2. 必要 module のインストール

    npm i -D typescript @types/react @types/node

### 3-3. 開発 server 起動

    npm run dev

### 3-4. \_app.js, index.js -> tsx へ拡張子変更

### 3-5. AppProps 型追記

```
    import { AppProps } from 'next/app'

    function MyApp({ Component, pageProps }: AppProps) {
        return <Component {...pageProps} />
    }

    export default MyApp
```

## 4. Tailwind CSS の導入

https://tailwindcss.com/docs/guides/nextjs

### 4-1. 必要 module のインストール

    npm i tailwindcss@latest postcss@latest autoprefixer@latest

### 4-2. tailwind.config.js, postcss.config.js の生成

    npx tailwindcss init -p

### 4-3. tailwind.config.js の purge 設定追加

```
module.exports = {
    purge: ['./pages/**/*.tsx', './components/**/*.tsx'],
    darkMode: false,
    theme: {
        extend: {},
    },
    variants: {
        extend: {},
    },
    plugins: [],
}
```

### 4-4. globals.css の編集

```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## 5. 動作確認

### 5-1. index.tsx の編集

```
const Home: React.FC = () => {
  return (
    <div className="flex justify-center items-center flex-col min-h-screen font-mono">
      Hello Nextjs
    </div>
  )
}
export default Home
```

#### npm run dev -> Tailwind CSS が効いているかブラウザで確認

### 5-2. `__tests__`フォルダと`Home.test.tsx`ファイルの作成

```
import { render, screen } from '@testing-library/react'
import '@testing-library/jest-dom/extend-expect'
import Home from '../pages/index'

it('Should render hello text', () => {
  render(<Home />)
  expect(screen.getByText('Hello Nextjs')).toBeInTheDocument()
})
```

#### npm test -> テストが PASS するか確認

```
 PASS  __tests__/Home.test.tsx
  ✓ Should render hello text (20 ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.728 s, estimated 2 s
```

## コミットメッセージ

🐛 バグ修正  
👍 機能改善  
✨ 部分的な機能追加  
🎉 盛大に祝うべき大きな機能追加  
♻️ リファクタリング  
🚿 不要な機能・使われなくなった機能の削除  
💚 テストや CI の修正・改善  
🎨 Lint エラーの修正やコードスタイルの修正  
🚀 パフォーマンス改善  
🆙 依存パッケージなどのアップデート  
🔒 新機能の公開範囲の制限  
👮 セキュリティ関連の改善
