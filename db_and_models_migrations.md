## Generating and Running Migrations

#### What are migrations?

Migrations lets you alter the database schema over time. Each migration is a new version of the database. A schema starts with nothing in it, each migration would add/remove new columns, tables, entries to the schema.

#### What is a schema?
A schema is the structure of the database, it defines the tables, fields, relationships, etc as well as any constraints for the data. 

#### Where are migrations stored in a rails app?
db/migrate

#### How to generate a migration?
Migration name matters. Here are a few used most often: 

1. If the migration name is of the form "**CreateXXX**" and is followed by a list of column names and types, (string is the default datatype so we can omit, in below example, name), then a migration creating the table XXX with the columns listed will be generated. Example: 

		$ bin/rails generate migration CreateBacheloretteTable name age:integer
this would generate
		
		class CreateBacheloretteTable < ActiveRecord::Migration
  			def change
    			create_table :bachelorettes do |t|
      				t.string :name
      				t.integer :age
          		end
  			end
		end	

2. If the migration name is of the form "**AddXXXToYYY**" or "**RemoveXXXFromYYY**" and is followed by a list of column names and type, then a migration containing the appropriate add_column and remove_column will be created. Example: 
	
	to add a column: 
	
		$ bin/rails generate migration AddPartNumberToProducts part_number:string

	this would generate

		class AddPartNumberToProducts < ActiveRecord::Migration
  			def change
    			add_column :products, :part_number, :string
  			end
		end

	to remove a column:

		$ bin/rails generate migration RemovePartNumberFromProducts part_number:string
		
	this would generate

		class RemovePartNumberFromProducts < ActiveRecord::Migration
  			def change
    			remove_column :products, :part_number, :string
  			end
		end
		
 		
### How to edit a migration after we have created it?
You can always edit the migration file that you've just created, but after you have ran `rake db:migrate` you will have to create another migration and run that one.

#### How to run a migration?
`rake db:migrate` if you have already created the database

`rake db:create db:migrate` if you haven't created the database yet

#### How to roll back a migration?
We all make mistakes, if we wish to rollback the last migration, we'd do the following:

`rake db:rollback`

If we wish to undo more than one migration, the following might help

`rake db:rollback STEP=3`
this example reverts the last 3 migrations

#### How to generate a new model?
Example:

		$ bin/rails generate model Product name:string description:text
this generates:
		
		class CreateProducts < ActiveRecord::Migration
  			def change
    			create_table :products do |t|
      				t.string :name
      				t.text :description
      				t.timestamps
    			end
  			end
		end