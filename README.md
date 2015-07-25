# Restaurantly
===============
        Online Course by rubyonrailstutor at: http://rubyonrailstutor.github.io/setup/restaurantly-app-setup/

Initial stumbling blocks to setup a working environment.
--------------------------------------------------------
# time_zone.rb:282: warning: circular argument reference - now
  **DESCRIPTION**: On multiple occasions when executing various commands from video, the above warning displays.
  
  **SOLUTION**: It is fine to ignore.
  
  **SOURCE**: Personal observation.

# PSQL installation
  **CMD**: which psql
  
  **RESULT**: Failure
  
  **SOLUTION**: 
  
            1. Download http://postgresapp.com
  
            2. Include export PATH=$PATH:/Applications/Postgres.app/Contents/Versions/9.4/bin 
                            -> ~/.bash_profile
            
                            -> ~/.zshrc (I work with Terminal 2 with Oh-My-Zshc framework)
                                                                                           
            3. Restart terminal
            
            4. which psql -> /Applications/Postgres.app/Contents/Versions/9.4/bin/psql
# BUNDLE
  **PROBLEM**: Bundler could not find compatible versions for gem "activesupport":
  
  **SOLUTION**: 
  
                1. Delete gemfile.lock
  
                2. bundle install
  
  **SOURCE**: http://stackoverflow.com/questions/8858706/bundler-could-not-find-compatible-versions-for-gem-updating-rails-app
 
# GEMFILE 
  **PROBLEM**: Bundler fails to install debugger 1.6.8
  
  **REASON** : Due to compatibility issues, debugger 1.6.8 does not work on Ruby 2.1 and above.
  
  **SOLUTION**: In GEMFILE towards bottom: change gem 'pry-debugger' -> gem 'pry-byebug'
  
  **SOURCE**: http://stackoverflow.com/questions/24705579/bundler-fails-to-install-debugger-1-6-8 and others

# rails generate rspec:install  (Launching Rails Server)
  **PROBLEM**: undefined method `configure' for #<Restaurantly::Application:0x007fcc763a8348> (NoMethodError)
  
  **DETAILED OUTPUT**:
                      
                      /usr/local/lib/ruby/gems/2.2.0/gems/activesupport-4.0.2/lib/active_support/values/time_zone.rb:282: warning: circular argument reference - now
                      
                      /Users/Coder/Documents/Ruby/restaurantly/restaurantly/config/environments/development.rb:1:in `<top (required)>': undefined method `configure' for #<Restaurantly::Application:0x007fcc763a8348> (NoMethodError)
  
  **SOLUTION**: 
    
                1. Open restaurantly/config/environments/development.rb
                
                2. Change first line: Rails.application.configure do -> Restaurantly::Application.configure do (Take note of capital letter R)
  **SOURCE**: http://stackoverflow.com/questions/22977051/error-launching-rails-server-undefined-method-configure
  
# bundle exec rake db:create
  **PROBLEM**: Output does not correspond to video
  **OUTPUT**: 
                
                restaurantly_dev already exists
                
                restaurantly_test already exists
  
  **SOLUTION**: No need to fix anything. Fine like that.
  
  **SOURCE**: Personal experience.
  
# rails server
  **PROBLEM**: DEPRECATION WARNING: You didn't set config.secret_key_base.
  
  **DESCRIPTION**: When running the command and trying to reach server from localhost:3000, the terminal generates above error.
  
  **SOLUTION**:
                
                Open: restaurantly/config/application.rb
                
                Edit: Add towards bottom: config.secret_key_base = 'blipblapblup'
  
  **SOURCE**: https://github.com/rails-api/rails-api/issues/72
  
# rails server (again)
  **PROBLEM**: undefined method `raise_in_transactional_callbacks=' for #<Class:0x007fbe1b50d030>

  **DESCRIPTION**: After fixing above issue, when running rails server again, localhost:3000 displays a page detailing out NoMethodError
  
  **SOLUTION**: 
  
                Open: restaurantly/config/application.rb (Same as previous file)
                
                Edit: Comment out: config.active_record.raise_in_transactional_callbacks = true
                
  ===
  
  After fixing all above issues, localhost:3000 displays exactly the same page as the one in the video.
  
