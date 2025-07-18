# フロントエンドのテスト入門

これは「フロントエンド開発のためのテスト入門」の第３章〜第６章で解説する、トレーニングリポジトリです。対象読者は、初めてフロントエンドのテストに取り組まれる方を想定しており、Jestの基本的な使用方法から解説しています。

- 第３章 はじめの単体テスト
    - 条件分岐のテスト
    - 閾値と例外処理のテスト
        - 例外のスローを検証
        - エラーメッセージの検証
        - instanceof を使ったエラークラスの検証
    - 用途別マッチャー
        - 真偽値
            - toBeTruthy
            - toBeFalsy
        - 数値の検証
            - toBe
            - toEqual
            - toBeGreaterThan
            - toBeGreaterThanOrEqual
            - toBeLessThan
            - toBeLessThanOrEqual
            - toBeCloseTo
        - 配列の検証
            - toContain:配列に特定のprimitive値が含まれているか
            - toContainEqual:配列に特定のオブジェクトが含まれているか
            - arrayContaining:引数に与えられた配列要素が含まれているか
        - オブジェクトの検証
            - toMatchObject:オブジェクトの部分一致
            - toHaveProperty:オブジェクトに特定のキーが存在するか
            - objectContaining:オブジェクトの部分一致
    - 非同期の検証
        - Promiseのreturn値を検証する
        - Promiseのrejectを検証する
        - async/awaitを使った非同期の検証
- 第４章 モック
    - jest.mockでモック関数を作成しスタブを行う
        - スタブの目的は代用です。
    - jest.spyOnでのスタブ
        - スタブとは対象のオブジェクトを置き換え
        - jest.spyOnができること
            - データ取得成功を再現する
            - データ取得失敗を再現する
    - jest.fnを使ってモック関数を作成しスパイをする
        - スパイの目的は記録を行うことです。
        - jest.fnで検証できること
            - 実行されたことの検証
            - 実行された回数の検証
            - 実行時引数の検証
            - 実行時引数のオブジェクト検証
- 第５章 UI コンポーネントテスト
  - 必要ライブラリ
    - jest-environment-jsdom: DOM APIの提供
    - @testing-library/react: React向けのテストライブラリ
    - @testing-library/jest-dom: DOMの検証でJestの標準マッチャーでは不十分のため。
    - @testing-library/user-event: ユーザー操作のシミュレート
  - render関数: UIコンポーネントのレンダリング
  - 要素の取得
    - screen.getTextBy: 一致する文字列を持つDOM要素の取得
    - screen.getByRole('button'): Buton要素の取得をロールで行う
    - screen.getByRole('list'): ul要素の取得をロールで行う
    - screen.getByRole('listitem'): li要素の取得をロールで行う
  - 要素の取得の絞り込み
    - within: 取得した要素を絞り込んで検証を行う
  - アサーション
    - toBeIntTheDocument: 要素がドキュメントに存在することの確認
    - toHaveLength: 要素がドキュメントに個数存在することの確認
  - テストの実例
    - 記事一覧(5-4)
      - アイテムが存在する場合、一覧表示
      - アイテムが存在しない場合、一覧表示されないこと
    - 新規アカウント登録Form要素の操作・状態チェック(5-5)
      - 単体テスト
        - fileldnのアクセシブルネームは、legendを引用していることの検証
          - divはロールを持たない。アクセシビリティ上でひとまとまりのグループとして使えない
          - アクセシビリティを考慮してlegend要素、group要素を使う
        - 初期状態でチェックボックスはチェックが入っていないことの検証
        - メールアドレス欄の存在の検証
        - パスワード欄の存在の検証 
          - type="password"はロールを持たないので、getByPlaceholderTextを使う
      - 統合テスト:登録フォーム全体をテスト
        - 文字入力の再現はtesting-libraryのfireEventでもできるが、よりユーザー操作に近いuserEventを使う
        - 検証項目
          - サインアップボタンが非活性
          - 利用同意チェックボックスを押下すると、サインアップボタンが活性化
          - formのアクセシブルネームは、見出しを引用しているか検証
            - HTMLのId属性をuseIdを使い、生成する
            - アクセシブルネームを適用するとForm要素はロールが適用される
              ください。
    - フォームの統合テスト(5-6)
      - 仕様
        - 過去に買い物をした履歴のないユーザーは「お届け先」を入力します。
        - 過去に買い物をした履歴のあるユーザーは「過去のお届け先」が選べますが「新しいお届け先」を入力指定することも可能です。
      - 便利な機能
        - Formイベントをモックするためのモック関数
        - 入力操作をまとめるインタラクション関数
      - 検証対象
        - Formコンポーネント
          - 検証項目
            - 過去のお届けがない場合のテスト
              - お届け先入力欄があることの検証
              - 入力、送信すると、入力内容が送信されることの検証
            - 過去のお届けがある場合のテスト
              - 設問に答えるまで、お届け先を選べないことの検証
                - 新しいお届け先を登録しますか？存在検証
                  - はい、いいえ
                - 過去のお届け先の存在検証
              - いいえを選択し、入力、送信すると、入力内容が送信されることの検証
              - はい選択し、入力、送信すると、入力内容が送信されることの検証
        - RegisterAddressコンポーネント
          - 検証項目
            - 登録成功時の検証
            - 登録失敗時の検証
            - バリデーションエラー時の検証
            - 不明なエラー時の検証

- 第６章 カバレッジレポートの読み方

## 第３章 はじめの単体テスト

Jest を使用したテストコードを解説します。はじめてテストに取り組まれる方にとって、最適な内容です。

【サンプルコード】`src/03/**/*.test.ts`

```
$ npm test
```

## 第４章 モック

テストを実施するうえで、必要不可欠な「モック」について解説します。Jest は標準でモック機能を備えています。

【サンプルコード】`src/04/**/*.test.ts`

```
$ npm test
```

## 第５章 UI コンポーネントテスト

Node.js には DOM API がありませんが、jsdom という DOM API をシュミレートするテスト環境を用意することで、実際のブラウザでテストするのと同じようなテストが「高速に」実施できます。Testing Library は、そのテスト環境において、UIコンポーネントテストをサポートするライブラリです。

【サンプルコード】`src/05/**/*.test.tsx`

```
$ npm test
```

## 第６章 カバレッジレポートの読み方

単体テスト・結合テストに慣れたら、カバレッジレポートを確認して、不足しているテストを見つけてみましょう。カバレッジレポートを確認することで、テストコードを書くポイントがはっきりします。

【サンプルコード】`src/06/**/*.test.{ts,tsx}`

```
$ npm test
```
