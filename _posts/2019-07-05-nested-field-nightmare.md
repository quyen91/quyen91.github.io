---
layout: default
title:  "Nested field nightmare"
date:   2019-07-05 15:30:46 +0700
categories: rails
---

Problems:
We have a form with structure like below

```
- user
  - name
  - age
  - estates
    - 1
      - name
      - area
      - size
      - price
    - 2
      - name
      - area
      - size
      - price
    - n....
```

and we will use simple form for implement view form
```
  = simple_form_for :user do |f|
    = f.input :name
    = f.input :age

```
but I want to save estates to json data of user without model Estate. And I must validate input of all fields of Estate object, keep data on input when submit false. I thought about nested fields without model.

Solution:
Create an ruby object:
``` ruby
class Estate
  include ActiveModel::Validations
  # include this calling method .valid? for instance of Estate
end
```


``` ruby
  10.times { @estates << Estate.new }

  # form.html.slim
  = simple_form_for :user do |f|
    = f.input :name
    = f.input :age

    @estates.each do |estate|
      = render partial: 'estate', locals: { f: f, estate: estate }

  # _estate.html.slim
  = fields_for 'estate[]', estate do |e|
    = e.input :name
    = e.input :size

```

Now, when submit form we will see params:
```
params: { user: {
            name: 'xxx',
            age: 'xxx',
            estates: {
              0 => { name: 'xxx', size: 'xxx'},
              1 => { name: 'xxx', size: 'xxx'},
              2 => { name: 'xxx', size: 'xxx'}....
            } }
        }
```
same as nested field with model. Of course, when we submit failed, all input of estates will be keep on form.( remember assign id for every Estate object )

--------
References:

[Create Multiple Objects From Single Form in Rails](https://vicfriedman.github.io/blog/2015/07/18/create-multiple-objects-from-single-form-in-rails/)