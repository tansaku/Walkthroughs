Payments with Stripe
---------------

* nice and easy to use for developers

* used to take a long time (couple of weeks) - keeping credit cards required a lot of due diligence 

* not going to be able to test since stripe locks us out of that

* today we are going to use the complete checkout solution (less complete solutions also available)

* going to create an admin user who can see all the payments that have taken place

* first up we need the concept of an admin user - could use existing table with an admin column, or we could use a completely different table, which is what we'll do now

* create an admin_feature_spec.rb

```ruby
require 'rails_helper'

describe 'admins' do
  it 'cannot sign up' do
    visit '/admins/sign_up'
    expect(page).not_to have_content 'Sign up'
  end
end
```

* watch this fail: "No route matches [GE] '/admins/sign_up'"

[Note: we might need to add if post.picture.exists? if image links are breaking our tests]

* to fix this let's generate a new devise model for admins:

bin/rails g devise Admin

and migrate

* change the error message to "expected not to find text 'Sign up'"

* in order to fix this - let's remove :registrable from Admin model and adjust test:

```ruby
require 'rails_helper'

describe 'admins' do
  it 'cannot sign up' do
    expect{visit '/admins/sign_up'}.to raise_error
  end
end
```
* tests should pass

* now need to create admins via seed file, e.g. in seeds.rb

Admin.delete_all
Admin.create(email: 't@t.com', password: '12345678', password_confirmation: '12345678')

* run `rake db:seed` and we'll have an admin account we can use to log into development

* so let's create an order feature spec

```ruby
require 'rails_helper'

describe 'orders page' do
  let(:post)(create(:post))
  let(:user)(create(:user))
  let(:admin)(create(:admin))

  context 'logged in as admin' do
    context 'no orders' do
      it 'sees a message' do
         visit '/orders'
         expect(page).to have_content 'No orders yet'
      end 
    end
  end

  context 'not logged in as admin' do
    it 'prompts to sign in' do
      visit '/orders'
      expect(page).to have_content 'sign up'
    end
  end


```

* should get complaint about routes

* add resource :orders in routes.rb

* then we get error about controller

* generate an orders controller

* get view about error

* add blank view

* to login as an admin we need:

```ruby
  context 'logged in as admin' do
    before do
      login_as admin, scope: admin
    end
```

[Note: need factory girl?]

* tests should now pass

```ruby

```ruby
require 'rails_helper'

describe 'orders page' do
  let(:post)(create(:post, title: 'Pretty picture'))
  let(:user)(create(:user, email: 'customer@blah.com'))
  let(:admin)(create(:admin))

  context 'logged in as admin' do

    context 'with orders' do
      before do 
        login_as admin, scope: admin
        christmas_day = Date.new(2013, 12, 25)

        Order.create(id: 1, post: post, user: user, created_at: christmas_day)
        visit '/orders'
      end

      it 'displays the product' do
        expect(page).to have_link 'Pretty picture'
      end

      it 'displays the customer email' do
        expect(page).to have_content 'customer@blah.com'
      end

      it 'displays an order number' do
        expect(page).to have_content '2512130001'
      end
  end
```

* tests should now fail - uninitialised constant order

* generate our order model

`bin/rails g model Order post:belongs_to user:belongs_to`

* migrate

* tests should now have new error about page contents

* grab orders from database in controller

* fill out view

```html
<% if @orders.any? %>
  <% orders.each do |order| %>
    <%= order.user.email %>
    <%= link_to order.post.title, '/posts' %>
    <%# order.number %>
  <% end %>
<% else %>
  No orders yet
<% end %>
```
* some tests will now pass, but order number test will fail

* need to update order.rb

```ruby
class Order < ActiveRecord::Base
  belongs_to :user
  belongs_to :post

  def number
    date_section = created_at.strftime('%d%m%y')
    number_section = "%04d" % id 

    date_section + number_section
  end

end
```
* and remote comment from view:

```html
<% if @orders.any? %>
  <% orders.each do |order| %>
    <%= order.user.email %>
    <%= link_to order.post.title, '/posts' %>
    <%= order.number %>
  <% end %>
<% else %>
  No orders yet
<% end %>
```

* and tests should all now pass



















