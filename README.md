# テーブル設計

## users テーブル

| Column             | Type    | Options                                           |
| ------------------ | ------- | ------------------------------------------------- |
| nickname           | string  | null: false                                       |
| email              | string  | null: false, unique: true                         |
| encrypted_password | string  | null: false                                       |
| front_name         | string  | null: false                                       |
| back_name          | string  | null: false                                       |
| front_name_kana    | string  | null: false                                       |
| back_name_kana     | string  | null: false                                       |
| birth_year_id      | integer | null: false, foreign_key: true, active_hash: true |
| birth_month_id     | integer | null: false, foreign_key: true, active_hash: true |
| birth_day_id       | integer | null: false, foreign_key: true, active_hash: true |


### Association

- has_many :items
- has_many :sales
- belongs_to_active_hash :birth_years
- belongs_to_active_hash :birth_months
- belongs_to_active_hash :birth_days

## items テーブル

| Column               | Type       | Options                                           |
| -------------------- | ---------- | ------------------------------------------------- |
| item_name            | string     | null: false                                       |
| description          | text       | null: false                                       |
| price                | integer    | null: false                                       |
| category_id          | integer    | null: false, foreign_key: true, active_hash: true |
| condition_id         | integer    | null: false, foreign_key: true, active_hash: true |
| delivery_fee_id      | integer    | null: false, foreign_key: true, active_hash: true |
| shipping_area_id     | integer    | null: false, foreign_key: true, active_hash: true |
| shipping_time_id     | integer    | null: false, foreign_key: true, active_hash: true |
| user                 | references | null: false, foreign_key: true                    |

### Association

- belongs_to :user
- has_one :sale
- belongs_to_active_hash :categories
- belongs_to_active_hash :conditions
- belongs_to_active_hash :delivery_fees
- belongs_to_active_hash :shipping_areas
- belongs_to_active_hash :shipping_times

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

| Column             | Type      | Options                                           |
| ------------------ | --------- | ------------------------------------------------- |
| delivery_address   | string    | null: false                                       |
| postal_code        | string    | null: false                                       |
| city               | string    | null: false                                       |
| street_address     | string    | null: false                                       |
| building           | string    |                                                   |
| phone_number       | string    | null: false                                       |
| prefecture_id      | integer   | null: false, foreign_key: true, active_hash: true |
| sale               | reference | null: false, foreign_key: true                    |

### Association

- belongs_to :sale
- belongs_to_active_hash :prefectures

## ActiveHash モデル

### birth_years テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### birth_months テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

### birth_days テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |

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

### prefectures テーブル

| Column      | Type    | Options                   |
| ----------- | ------- | ------------------------- |
| id          | integer | null: false, primary key  |
| name        | string  | null: false               |