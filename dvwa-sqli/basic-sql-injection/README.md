## DVWA SQL Injection

# Objective

DVWAを利用してSQL Injectionの基本動作を確認する。

# Environment
・DVWA
・Docker
・Firefox

# Security Level
Low

# Test Payload
1' OR '1'='1

# Result 
本来の挙動
・指定したidのユーザー情報の表示
今回の挙動
・全ユーザ情報の表示

# Analysis
アプリケーションでのエスケープ処理、入力値のバリデーション、プリペアードステートメントまたはパラメータ化クエリを使用していない。

SQL分にユーザー入力がそのまま挿入されている可能性が高い
[予想]
SELECT first_name, sur_name FROM users WHERE user_id = '$id';

ペイロードが挿入され条件が常に真となった。

# Countermeasure
idは一意の識別子
→SQL文でLIMITを掛け一人分の情報を返すようにする
入力値をそのまま挿入
→プリペアードステートメント（プレースホルダ及びバインド）に変更

# Lessens Learned
・プリペアードステートメントの重要性
・補助機能としてのエスケープ処理の必要性
・ユーザビリティから返り値がない時のエラー文の必要性