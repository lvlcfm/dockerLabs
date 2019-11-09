# README

# This is a Rails 6 Docker Setup

## System Requirements
- Make sure you have Docker and docker-compose installed
- https://hub.docker.com/

## Running This Repo
- Clone this repository
- Have your terminal out/git bash
- Have two windows open as we'll be feeding commands from one terminal window to the other
### Window 1
- cd into the the repository
- execute the command `docker-compose build`
  - This will build an image (all the contents that are necessary to run our rails application)
  - The last line of this output should be `Successfully tagged dockerlabs_webpacker:latest`
- execute the command `docker-compose up`
  - the last line that will signal success will be `Listening on tcp://0.0.0.0:3000`
  - but don't go to that link yet! We'll need to create our database first before that route works
  - this is when we open up the second window
### Window 2
- run the following command
  - `docker-compose run web rails db:create`
    - this command will create the database for the application
    - it should say
      - `Created database myapp_development`
      - `Created database myapp_test`
    - once successful you should now be able to visit `localhost:3000`

### Workflow
  - To shutdown the application -- on Window 2 type `docker-compose down --volumes`
  - To rebuild the application -- on Window 1 type `docker-compose up --build`

### Adding Gems
  - Add gems through the Gemfile in your local environment
  - You will then have to shutdown the application and then rebuild it

### Running Rails Commands Do it Through Window #2
  - To run any Rails commands like `rails generate` do it through Window #2 through the following command
  - `docker-compose run web rails <your command>`
  - example
    - `docker-compose run web rails db:create`
    - `docker-compose run web rails g model workshop description:string`
    - `docker-compose run web rails db:migrate`


## Caveats to this setup
When you run rails commands, it will generate all the files in your local environment so that you can edit them and your edits will be reflected in the contents that the rails server shows.

But this does not apply for the gem install command. If you add a gem through gem install, through window #2, the Gemfile or Gemfile.lock in your local environment will not be changed and when you commit your changes the gem install will not be reflected. So please add your gems through your local environment and rebuild your app.

