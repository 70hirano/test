# Githubの設定確認テスト

## ブランチ設定
**1. Require a pull request before merging**
  * PR経由のみマージを許可する
  * ONにすることでmainやstgなどの重要ブランチを直接いじらせず、安全なPR経由だけに限定することができる

**2. Require approvals**
  * PRにレビューが必要かどうかを設定する
  * ON：レビュー必須、承認者の人数を設定可能
  * ー：レビュー必要なし　　　

**3. Dismiss stale pull request approvals when new commits are pushed**
  * PRに対して承認済だがマージ前の状態で、同じソースに対して修正を加えて、追加pushした際の「承認」をどう扱うかを制御する
  * ON：前の承認が無効となる　→　UI上もApproveが消え、再承認が必要になる。再承認後にマージが可能となる
  * ー：前の承認が残る

**4. Require review from Code Owners**
  * CODEOWNERS ファイルに指定された人の承認が必須となる

**5. Require approval of the most recent reviewable push**
  * PRに対して承認済だがマージ前の状態で、同じソースに対して修正を加えて、追加pushした際の「マージ」の動きを制御する
  * ON：最新のpushが承認されるまで、マージ不可
  * ー：マージは可能

## テストリポジトリ
* https://github.com/70hirano/test

## テストユーザー
* 70meth01：リーダー
* 70meth02：開発者
  

## テストケース
* mainリポジトリに対して、以下設定を行い各ケースのシナリオを実行した
 1. Require a pull request before merging　→　ON
 2. Require approvals　→　ON＋承認者数=1
 3. Dismiss stale pull request approvals when new commits are pushed　→　テストケースに合わせて変更
 4. Require review from Code Owners　→　ー
 5. Require approval of the most recent reviewable push　→　テストケースに合わせて変更

### ケース1　ブランチ設定　3：ON　5：ON　の場合
* ~~1-1 開発者：ファイルを修正し、開発リーダーにPRを投げる~~
* ~~1-2 リーダー：承認し、マージ可能な状態となる（マージは未だ行わない）~~
* ~~1-3 開発者：ファイルを追加修正しpushする~~
* ~~1-4 リーダー：追加pushにより承認が消える（無効化される）。マージ不可の状態となる~~
* ~~1-5 リーダー：再承認を行い、マージ可能な状態となる~~
* ~~1-6 リーダー：マージする~~
<br /><img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/7bea8c4a-a32a-4d0b-8136-0ff2ece549c9" /><br />

### ケース2　ブランチ設定　3：ー　5：ー　の場合
* ~~2-1 開発者：ファイルを修正し、開発リーダーにPRを投げる~~
* ~~2-2 リーダー：承認し、マージ可能な状態となる（マージは未だ行わない）~~
* ~~2-3 開発者：ファイルを追加修正しpushする~~
* ~~2-4 リーダー：追加pushがあっても承認状態のまま、マージも可能な状態のまま~~
* ~~2-5 リーダー：マージする~~
<br /><img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/3438229d-16e2-42f9-9966-e37424e55437" /><br />
　
### ケース3　ブランチ設定　3：ON　5：ー　の場合
* 3-1 開発者：ファイルを修正し、開発リーダーにPRを投げる
* 3-2 リーダー：承認し、マージ可能な状態となる（マージは未だ行わない）
* 3-3 開発者：ファイルを追加修正しpushする
* 3-4 リーダー：追加pushにより承認が消える（無効化される）。ただしマージは可能な状態となる　**※ 矛盾した状態となる**
* **↑　マージ不可となる可能性あり（最新のpushに対して承認されていないため）　※テスト結果で判断する**
* ======================================================
* 3-5 リーダー：再承認を行い、マージ可能な状態となる
* 3-6 リーダー：マージする
* ======================================================

### ケース4　ブランチ設定　3：ー　5：ON　の場合
* ~~4-1 開発者：ファイルを修正し、開発リーダーにPRを投げる~~
* ~~4-2 リーダー：承認し、マージ可能な状態となる（マージは未だ行わない）~~
* ~~4-3 開発者：ファイルを追加修正しpushする~~
* 4-4 リーダー：追加pushがあっても承認状態のまま、ただしマージは不可の状態となる　**※ UIと矛盾した状態となる**
    <br /><img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/f9c90e05-a076-4372-9c12-54123e7d3313" /><br />
* **開発者＆開発リーダーからみたPRの状態　→　承認は一度通ったが（Verified）、更にレビューが必要＆マージも未だ**
　　＜br /><img width="50%" height="50%" alt="image" src="https://github.com/user-attachments/assets/b422de74-19e3-4c44-9604-fb8c6fe547ab" /><br />
* **開発リーダーの場合は、直近のみ変更を確認することができる**
    <br /><img width="1161" height="858" alt="image" src="https://github.com/user-attachments/assets/c29dad66-801d-4db5-8b40-1049a639e223" /><br />



