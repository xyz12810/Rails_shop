# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
#at begin run 
rails db:seed  
bundle install #restart server
 
rails test:integration  #集成测试
#rails g mailer Order received shipped
#rails  g integration_test user_stories
#TODO 订单确认邮件 没发出去 待排查  test:integration
#bin/rails generate scaffold User name:string password:digest

sqlite3 -line db/development.sqlite3 "select * from users
 It turns out that it’s easy to implement using the Rails
callback facility   过滤器 限制访问
#
> bin/rails console
Loading development environment.
>> User.create(name: 'dave', password: 'secret', password_confirmation: 'secret')
=> #<User:0x2933060 @attributes={...} ... >
>> User.count
=> 1
#其实begin相当于java的try
#rescue相当于java的catch
#ensure相当于java的finaly
#raise相当于java的throw

usercontrol :it’s still possible for two administrators
each to delete the last two users if their timing is right. Fixing this
would require more database wizardry than we have space for here.


TODO playtime task I   fix test error
=======
TODO playtime task I  broadcast don't work   当数据库中product.price change orderitem中price不change
http://url.cn/4115TZ8   Task K playtime

rails db:setup RAILS_ENV="production"

https://ruby-china.org/topics/26185
https://www.phusionpassenger.com/library/install/apache/install/oss/osx/
部署服务器时 使用capistrano 时修改 apach服务器的config  DocumentRoot
/home/rubys/deploy/depot/current/public/
<Directory
/home/rubys/deploy/depot/current/public>
Apache 启动问题
http://www.cnblogs.com/snandy/archive/2012/11/13/2765381.html
http://vin-zhou.github.io/2014/10/27/%E5%90%AF%E7%94%A8Mac%E8%87%AA%E5%B8%A6%E7%9A%84Apache/ 

你的apache还是很顽固地403、403，那么，你就应该考虑网站目录的权限问题了，首先是目录的基本权限，apache要求目录具有执行权限，也就是x，而其中要注意的，你的目录树都应该拥有这些权限，目前我设置的是755，网上有文章说705就可以搞定，我还没具体测试，比如我的网站根目录是/usr/local/site/test，那么，你要保证/usr、/usr/local、/usr/local/site、/usr/local/site/test这四个层级的目录都是755权限，而我本人就只注意到最末的子目录test，却忽视了site层级，就悲催地弄了许久....

    chmod 755 /usr/local/site　　　　　　　　　　　　　　　　　 　　　　　　　　　　

    chmod 755 /usr/local/site/test　　　　　　　　　　　　　　　　　　　　　　　　　

　　小提示：上面这两段命令可以简化成（不过这样设置之后，文件夹中的所有文件都会是755权限，所以请在网站目录内还没有文件时进行此设置）：

cap deploy:setup
cap deploy:check
cap deploy:migrations
cap production deploy
cap production deploy:rollback


<VirtualHost *:80>
    ServerName www.railshop.com
    DocumentRoot "/Users/Expand/Documents/rubyshop/Rails_shop/public/"
    RailsEnv development 
    SetEnv SECRET_KEY_BASE "0123456789abcdef"
      ErrorLog "/private/var/log/apache2/www.railshop.com-error_log"
   CustomLog "/private/var/log/apache2/www.railshop.com-access_log" common
        <Directory "/Users/Expand/Documents/rubyshop/Rails_shop/public">
            AllowOverride all
            Options -MultiViews
            Require all granted
        </Directory>
</VirtualHost>
    chmod -R 755 /usr/local/site*　　　


bin/rails generate controller Admin::Book action1 action2 # controller 分组
config/initializers/inflections.rb  #修改词形变化文件  另一种方式是在model 的class中设置self.table_name="xxxz"
数据库表扩充字段 rails 有据可查  比其他的更便捷
# Doesn't work
User.where( "name like '?%'", params[:name])
#Works
User.where("name like ?", params[:name]+"%")
#order
orders= Order.where(name:'Dave').order("pay_type,shipped_at DESC")
orders= Order.where(name:'Dave').order("pay_type,shipped_at DESC").limit(10)
list= Talk.select("title,speaker,recorded_on")
ineItem.select('li.quantity').where("pr.title= 'Programming Ruby 1.9'").joins("as li inner join products as pr on li.product_id= pr.id")

summary = LineItem.select( "sku, sum(amount) as amount").group("sku")
#lock 锁
Account.transaction do
	ac = Account.where(id: id).lock("LOCKIN SHAREMODE").firstac.balance-= amount if ac.balance> amount
	ac.save
end
#writing our own sql 
Order.find_by_sql("select * from orders")

　　　　　　　 　　　　　　　　　

def sales_graph
	png_data = Sales.plot_for(Date.today.month)
	send_data(png_data, type: "image/png", disposition: "inline")
end

def send_secret_file
	send_file("/files/secret_list")
	headers["Content-Description"] = "Top secret"
end
#objects in a session must be
#serializable (using Ruby’s Marshal functions).
<!-- session_store = :cookie_store #4kb default
If you have a high-volume site, keeping the size of the session data small and
going with cookie_store is the way to go
session_store = :active_record_store
session_store = :drb_store
session_store = :mem_cache_store
session_store = :memory_store
session_store = :file_store -->

# If you’d like an easier way of dealing with uploading and storing images, take
#TODO use  Paperclip4 attachment_fu5 plugins 
#helpers method rails 
http://doc.rubyfans.com/rails/api/v4.1.0/

<%= link_to(image_tag("delete.png", size: "50x22"),
product_path(@product),
data: { confirm: "Are you sure?" },
method: :delete)
%>

<%= mail_to("support@pragprog.com", "Contact Support",
subject: "Support question from #{@user.name}",
encode: "javascript") %>

render(partial: 'article',
object: @an_article,
locals: { authorized_by: session[:user_name],
from_ip: request.remote_ip })


<%= render(partial: "product",collection: @products) %>

#spacer_template  option
The optional :spacer_template parameter lets you specify a template that will be
rendered between each of the elements in the collection. For example, a view
might contain the following:
rails50/e1/views/app/views/partial/_list.html.erb
<%= render(partial: "animal",
collection: %w{ ant bee cat dog elk },
spacer_template: "spacer")
%>
This uses _animal.html.erb to render each animal in the given list, rendering the
partial _spacer.html.erb between each. If _animal.html.erb contains this:
rails50/e1/views/app/views/partial/_animal.html.erb
<p>The animal is <%= animal %></p>

 _spacer.html.erb contains this:
rails50/e1/views/app/views/partial/_spacer.html.erb
<hr />
your users would see a list of animal names with a line between each



<%= render partial: "user", layout: "administrator" %>
<%= render layout: "administrator" do %>
# ...
<% end %>
Partial layouts are to be found directly in the app/views directory associated
with the controller, along with the customary underbar prefix, such as
app/views/users/_administrator.html.erb.

chapter 22
 this chapter, you'll see:
• Naming migration files  # ls db/migrate
• Renaming and columns
• Creating and renaming tables
• Defining indices and keys
• Using native SQL

bin/rails db:migrate:redo STEP=3
By default, redo will roll back one migration and rerun it. To roll back multiple
migrations, pass the STEP= parameter

rename_column :orders, :e_mail, :customer_email
As rename_column() is reversible, separate up() and down() methods are not required
in order to use it

#change column
def up
change_column :orders, :order_type, :string
end
However, the opposite transformation is problematic. We might be tempted
to write the obvious down() migration:
def down
change_column :orders, :order_type, :integer
end

#we want to create a one-way migration—one 
#that cannot be reversed—we’ll want to stop the down migration from being applied. In this #case, Rails provides a special exception that we can throw

class ChangeOrderTypeToString < ActiveRecord::Migration
def up
change_column :orders, :order_type, :string, null: false
end
def down
raise ActiveRecord::IrreversibleMigration
end
end

#Generally the call to drop_table() is not needed, as create_table() is reversible.
#rename table 
class RenameOrderHistories < ActiveRecord::Migration
def change
rename_table :order_histories, :order_notes
end
end

#
add_index :orders, :name

#overload id  sqlite3 db/development.sqlite3 ".schema tickets"
#create_table :tickets, primary_key: :number do |t|

#Tables with No Primary Key
create_table :authors_books, id: false do |t|
t.integer :author_id, null: false
t.integer :book_id, null: false
end
#https://github.com/matthuhiggins/foreigner
And, if you’d like to make your life even easier, someone has written a plugin1
that automatically handles adding foreign key constraints.)

#Custom Messages and Benchmarks
def up
say_with_time "Updating prices..." do
Person.all.each do |p|
p.update_attribute :price, p.lookup_master_price
end
end
end
say_with_time() prints the string passed before the block is executed and prints
the benchmark after the block completes.


#Schema Manipulation Outside Migrations

def run_with_index(*columns)
	connection.add_index(:orders, *columns)
	begin
		yield
	ensure
		connection.remove_index(:orders, *columns)
	end
end


def get_city_statistics
		run_with_index(:city) do
		# .. calculate stats
		
		end
	end

	#However,that index isn’t needed during the day-to-day running of the application, and  tests have shown that maintaining it slows the application appreciably


