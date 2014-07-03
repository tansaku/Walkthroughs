devise:

(get rid of pending stuff?)
* currently anyone can edit/delete - you did user sign up and login in sinatra
* in rails we have the devise gem
----> only signed in users can see the edit/delete links
----> clicking "create restaurant" takes you to sign in page --> add that link

* adding contexts to handle being logged in and logged out
* comment out logged in ones to focus on logged out
---> note for reviews: expect(page).not_to have_field 'Thoughts'


* devise
--- devise install
--- generate user
--- changing document root
--- adding alert --> for failing to log in
--- rake db:migrate

* check we can log in 
* add forms to sign up https://github.com/plataformatec/devise/wiki/How-To:-Add-sign_in,-sign_out,-and-sign_up-links-to-your-layout-template
* devise controller is hidden 

* RESTful thinking
* only show review form and links if user signed in --> if user_signed_in?
* for create new restaurant do in controller --> authenticate_user!
* then also authenticate_user! in other controller actions
* can DRY out with before_action --> before_action :authenticate_user!, except: [:index]
* logging in with tests … --> add warden config to rails_helper.rb
* adding log in operation to test:

    before do
      user = User.create email: 'tansaku@gmail.com', password: '12345678', password_confirmation: '12345678'
      login_as user
    end

* follow up - only allowing user to edit/delete restaurants they created - only one review per user …

Notes for Alex - no poltergeist yet?
