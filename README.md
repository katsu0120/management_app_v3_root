# ポートフォリオ紹介
[https://management-app-v3-front.herokuapp.com](https://management-app-v3-front.herokuapp.com)

Mgt_App(マネジメントアップ)はプロジェクトを社内で共有可能なプロジェクト管理ツールです。<br>
Projectを作成し、達成目標を「プロジェクトタイトル」として記載。<br>
その内容を「プロジェクト内容」として書き込みます。<br>
そして、そのプロジェクトを達成する為のタスクをTASK欄に追加して行き、<br>
全てのTASKが完了となったら、PROJECTを完了させるという設計です。<br>

#### トップページ
![top_image](https://user-images.githubusercontent.com/87424854/177262116-e8f4c3b8-ef8d-48d2-b2f3-b3e8bdb477ad.png)

### プロジェクト管理方法
Mgt_Appでは2つのプロジェクト管理方法があります。

<br>
<br>  

### カンパニープロジェクト

カンパニープロジェクトとは、カンパニー参加ユーザーと共有するプロジェクトの事です。<br>
チームでプロジェクトの完了を目指す場合に使用します。
![company_project_image](https://user-images.githubusercontent.com/87424854/177258825-6c5f5e0c-ea8b-4f15-a43a-4ce2a3ca21f4.png)


### パーソナルプロジェクト

パーソナルプロジェクトとは、他者と共有しない個人のプロジェクトの事です。<br>
個人でプロジェクトの完了を目指す場合に使用します。
![company_project_image](https://user-images.githubusercontent.com/87424854/177264416-6aa1bba6-3e21-4c5d-b933-211e63e4df88.png)




#### レスポンシブ対応

スマホ利用も想定したUI設計。

<img width="273" alt="image" src="https://user-images.githubusercontent.com/87424854/177299244-b3fc7376-834f-4806-abcf-0485e3b77bd6.png">
# ポートフォリオに使用した技術

#### 各バージョン

- Ruby 2.7.4
- Rails(API) '6.1.3.1
- Nuxt.js(SPA) 2.15.8
- Vuetify 1.12.1
- docker-compose 1.29.2

#### フロントエンド
| 名称 | 説明 |
| ---- | ---- |
| Nuxt.js (SPA mode) | フロントエンドフレームワーク |
| Vuetify | UIコンポーネント |
| Authentication | JWTを用いたサインイン・ログイン・ログアウト |
| EsLint | Linter |

- Vuetifyコンポーネントを導入することで、スマホ利用を想定したレスポンシブデザインを実現。

- Vuexストアでステート管理。

- 未ログイン状態でアクセスして欲しくないページ（ /users/editなど ）へのアクセス対策には、Nuxt.jsのmiddlewareを活用することで自動的にリダイレクトするようにしました。

- ログイン状態でアクセスして欲しくないページ （ログインページ, 新規作成ページ） へのアクセスも同じくリダイレクトします。


#### バックエンド
| 名称 | 説明 |
| ---- | ---- |
| Rails (API mode) | APIサーバーとして利用 |
| PostgreSQL | データベース |

- RailsはAPIサーバーとして利用しており、フロントエンドコンテナからのリクエストに対してJSONデータを返しています。

- ログインパスワードなどはJWTで暗号化しています。

- Sing in時, メールアドレス変更時, パスワードを忘れた時などのメール認証は連動させているGメールから認証メールが届く仕様になっています。

#### テストコード
| 名称 | 説明 |
| ---- | ---- |
| Jest | フロントエンドテスト, Vuexストアの動作を少しだけ |
| RSpec | バックエンドテスト, バリデーションとアソシエーションのテスト, コントローラーテスト, ログイン認証テスト |

#### インフラ
| 名称 | 説明 |
| ---- | ---- |
| Docker, Docker-compose | コンテナ環境 |
| Github | バージョン管理 |
| Heroku | 本番環境 |

#### ER図

- シンプルなER設計になっております。
projectデーブルが持つcompany_idはCompanyテーブルのidをFKとしているのですが、nullを許容しています。
nullの場合は「パーソナルプロジェクト」に振り分けられ、
company_idがある場合は「カンパニープロジェクト」として振り分ける様にコントローラーで設計しているので、
シンプルに見えるER図の中でも高度に設計されております。

![Mgt_App_ER_drawio](https://user-images.githubusercontent.com/87424854/177291323-1d15c083-82b1-4444-8056-d49d2a748b31.png)

# アプリの機能紹介

### 機能一覧
| 機能名 | 説明 |
| ---- | ---- |
| ユーザー機能 | サインイン、ログイン、ログアウト、ゲストログイン、登録情報の編集(名前,profile,メールアドレス,パスワード)、パスワード忘れたら？機能 |
| カンパニー機能 | カンパニーの作成、カンパニーの削除(カンパニー作成ユーザーのみ)、カンパニーネームの編集(カンパニー作成ユーザーのみ)、ユーザーの検索機能(nameは一意性なのでnameで検索)、参加ユーザーの追加、参加ユーザーの削除(カンパニー作成ユーザーのみ) |
| プロジェクト機能 | カンパニー(共有)プロジェクトの作成、カンパニープロジェクトの最終更新者の表示機能、パーソナル(個人)プロジェクトの作成、プロジェクトの編集機能(編集、完了、削除、未完了に戻す) |
| タスク機能 | taskの作成機能(プロジェクト毎に作成)、taskの編集機能(編集、完了、削除、未完了に戻す))、CompanyProjectのtaskの最終更新者表示機能
