### Buck's Ruby ActiveRecord Notes

1. Go to GitHub and fork repository.
2. Go to linux prompt, go to directory above where you want the repository to go.
3. git clone <paste repository fork url>
4. cd into new repository directory
5. ls (or ls -R) to get a feel for directory/file organization
6. gem install bundler (if necessary/desired)
7. bundle install
8. bundle exec rake -T (to refresh memory of the rake tasks I may be about to do)
9. bundle exec db:create # Create two empty database files in the db/ directory, named database.sqlite3 and test-database.sqlite3, if they don't exist
10. bundle exec rake spec # Run the tests located in the spec/ directory, just to see what they're about and how they fail(/pass).

11. If you're getting started creating a new database, or if you're changing an existing database, create a new empty migration.
  
  bundle exec rake generate:migration NAME=<a snake case name that describes this migration, e.g. create_dogs, dog_rename_column_person_owner>

12. Open up the newly-created empty migration file and fill in the #change method with whatever it is you want to create/change

13. Create/Update the database from the migrations (i.e. migrate)

  bundle exec rake db:migrate

14. Seed the database using whatever seed code you put into db/seeds.rb (maybe you used a CSV importer, or maybe you made explicit SQL statements).

  bundle exec rake db:seed

15. Create the empty model

  bundle exec rake generate:model

16. Fill in empty model with associations (e.g. belongs_to, has_many) and validations (validates)

  Associations: http://guides.rubyonrails.org/association_basics.html
  Validations: http://guides.rubyonrails.org/active_record_validations.html

17. You can now query!

  http://guides.rubyonrails.org/active_record_querying.html




Rake Options:

$ bundle exec rake -T
rake console             # Start IRB with application environment loaded
rake db:create           # Create the database
rake db:drop             # Drop the database
rake db:migrate          # Migrate the database
rake db:rollback         # rollback your migration--use STEP=number to step back multiple times
rake db:seed             # populate the database with sample data
rake db:version          # Returns the current schema version number
rake generate:migration  # Create an empty migration in db/migrate, e.g., rake generate:migration NAME=create_tasks
rake generate:model      # Create an empty model in app/models, e.g., rake generate:model NAME=User
rake generate:spec       # Create an empty model spec in spec, e.g., rake generate:spec NAME=user
rake spec                # Run the spec suite
