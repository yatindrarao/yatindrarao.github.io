---
layout: post
comments: true
---

## Why use polymorphic association?

What if you want to create a model which you can use in more than one models. There are many
problems in real world where we want to create common interface between models. For example
let's say you are implementing comment feature on site and you want it to for Users, Vendors and Agents model.

<!-- more -->

One possible solution is to create seperate models for each of them which is not an optimized solution. Instead
we can use polymorphic assoication provided by Rails.

## How to use it?
Let's conitue with Comment model. The association can be defined as follow:
```
class Comment < ApplicationRecord
  belongs_to :commentable, polymorphic: true
end

class Vendor < ApplicationRecord
  has_many :comments, as: :commentable
end

class Agent < ApplicationRecord
  has_many :comments, as: :commentable
end
```
Required table structure can be achieved by following migration:

```
class CreateComments < ActiveRecord::Migration[5.0]
  def change
    create_table :comments do |t|
      t.text :body
      t.references :commentable, polymorphic: true, index: true
      t.timestamps
    end
  end
end
```
Now we are ready to use them. We can perform following opeartions on comment model such as:
- Create user comment
  ```
  @user.comments.create(body: "Very Good!")
  ```
  This will store comment with `commentable_type` as `"user"` and `commentable_id` as `@user.id`.
- Find all comments by user
  ```
  @user.comments
  ```  

## When to use them?
Whenever you want to share functionality between many models.

For more details please visit [Rails Guide](http://guides.rubyonrails.org/association_basics.html#polymorphic-associations)
