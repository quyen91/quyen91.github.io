---
layout: default
title:  "Basic authen for mount route in rails app!"
date:   2020-04-02 15:30:46 +0700
categories: rails
---

# Problem
- Mình sẽ có một số trường hợp dùng mount route, như docs, sidekiq, rails-admin.

``` ruby
# route.rb
unless Rails.env.production?
  mount Rswag::Ui::Engine => '/api-docs'
  mount Rswag::Api::Engine => '/api-docs'
  mount Sidekiq::Web => '/sidekiq'
end
```

# Solution (cho trường hợp dùng rswag)
#### Đối với trường hợp user cần phải login
 - thì sẽ rất dễ, chỉ cần authen với Devise gem là được . Nếu chưa login sẽ redirect tới màn login.

```ruby
# route.rb
authenticate :user, ->(user) { user.admin? } do
    mount Sidekiq::Web => '/sidekiq'
end
```

#### Đối với những trường hợp không có login, làm sao authen
  - mong muốn có thể show popup nhập username/password kiểu basic authen
  - Dùng constraint (vẫn chưa tìm được cách)
