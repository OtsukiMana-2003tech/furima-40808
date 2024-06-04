# テーブル設計

## users テーブル

| Column             | Type     | Options                   |
| ------------------ | -------- | ------------------------- |
| nickname           | string   | null: false               |
| email              | string   | null: false, unique: true |
| encrypted_password | string   | null: false               |
| front_name         | string   | null: false               |
| back_name          | string   | null: false               |
| front_name_kana    | string   | null: false               |
| back_name_kana     | string   | null: false               |
| birth_date         | date     | null: false               |


### Association

- has_many :items
- has_many :sales

## items テーブル

| Column           | Type       | Options                        |
| ---------------- | ---------- | ------------------------------ |
| item_name        | string     | null: false                    |
| description      | text       | null: false                    |
| price            | integer    | null: false                    |
| category_id      | integer    | null: false                    |
| condition_id     | integer    | null: false                    |
| delivery_fee_id  | integer    | null: false                    |
| shipping_area_id | integer    | null: false                    |
| shipping_time_id | integer    | null: false                    |
| user             | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one :sale
- belongs_to_active_hash :category
- belongs_to_active_hash :condition
- belongs_to_active_hash :delivery_fee
- belongs_to_active_hash :shipping_area
- belongs_to_active_hash :shipping_time

## sales テーブル

| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| user               | references | null: false, foreign_key: true |
| item               | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- belongs_to :item
- has_one :delivery

## deliveries テーブル

| Column           | Type       | Options                        |
| -----------------| ---------- | ------------------------------ |
| postal_code      | string     | null: false                    |
| city             | string     | null: false                    |
| street_address   | string     | null: false                    |
| building         | string     |                                |
| phone_number     | string     | null: false                    |
| shipping_area_id | integer    | null: false                    |
| sale             | references | null: false, foreign_key: true |

### Association

- belongs_to :sale
- belongs_to_active_hash :shipping_area

## ActiveHash モデル

### categories テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### conditions テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### delivery_fees テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### shipping_areas テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### shipping_times テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |