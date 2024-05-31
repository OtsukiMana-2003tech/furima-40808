# テーブル設計

## users テーブル

| Column             | Type   | Options                   |
| ------------------ | ------ | ------------------------- |
| nickname           | string | null: false               |
| email              | string | null: false, unique: true |
| password           | string | null: false               |
| front_name         | string | null: false               |
| back_name          | string | null: false               |
| front_name_kana    | string | null: false               |
| back_name_kana     | string | null: false               |


### Association

- has_many :items
- has_many :sales
- has_many :deliveries

## items テーブル

| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| item_name          | string     | null: false                    |
| description        | text       | null: false                    |
| price              | integer    | null: false                    |
| user               | references | null: false, foreign_key: true |

### Association

- belongs_to :user
- has_one :sale

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

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| delivery_address   | text    | null: false               |
| postal_code        | string  | null: false               |
| city               | string  | null: false               |
| street_address     | string  | null: false               |
| building           | string  | null: true                |
| phone_number       | integer | null: false               |

### Association

- belongs_to :user
- belongs_to :sale