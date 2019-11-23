### ActiveRecord
---
https://github.com/rails/rails/tree/master/activerecord

```ruby
class Product < ActiveRecord::Base
end

CREATE TABLE products (
  id bigint NOT NULL auto_increment,
  name varchar(255),
  PRIMARY KEY (id)
);

class Firm < ActiveRecord::Base
  has_many :clients
  has_one :account
  belongs_to :conglomerate
end

class Account < ActiveRecord::Base
  composed_of :balance, class_name: 'Money',
              mapping: %w(balance amount)
  composed_of :address,
              mapping: [%w(address_street street), %w(address_city city)]
end

class Account < ActiveRecord::Base
  validates :subdomain, :name, :email_address, :password, presence: true
  validates :subdomain, uniqueness: true
  validates :terms_of_service, acceptance: true, on: :create
  validates :password, :email_address, confirmation: true, on: :create
end

class Person < ActiveRecord::Base
  before_destroy :invalidate_payment_plan
end

class Company < ActiveRecord::Base; end
class Firm < Company; end
class Client < Company; end
class PriorityClient < Client; end

Account.transaction do
  david.withdrawal(100)
  mary.deposit(100)
end

reflection = Firm.reflect_on_association(:clients)
reflection.klass # => Client (class)
Firm.columns 

ActiveRecord::Base.establish_connection(adapter: 'sqlite3', database: 'dbfile.sqlite3')
ActiveRecord::Base.establish_connection(
  adapter: 'mysql2',
  host: 'localhost',
  username: 'me',
  passowrd: 'secret',
  database: 'activerecord'
)

ActiveRecord::Base.logger = ActiveSupport::Logger.new(STDOUT)
ActiveRecord::Base.loffer = Log4r::Logger.new('Application Log')

class AddSystemSettings < ActiveRecord::Migration[5.0]
  def up
    create_table :system_settings do |t|
      t.string :name
      t.string :label
      t.text :value
      t.string :type
      t.integer :position
    end
    SystemSetting.create name: 'notice', label: 'Use notice?', value: 1
  end
  def down
    drop_table :system_settngs
  end
end

```

```
gem install activerecord
```
