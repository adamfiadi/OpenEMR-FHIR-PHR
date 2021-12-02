**INSTALLATION :**

1. Clone the PHR Repository from https://github.com/lhncbc/phr

2. This should give you the def directory, which will contain the following:
- a bashrc.def file
- a bin subdirectory, which should contain a file and multiple softlinks. The softlinks are mostly set to point to the packages subdirectory, which is where the softlinks should     be adjusted to match your installation. The following softlinks are found in the bin subdirectory:
       1. bundle - points to the ruby bundle script
       2. gem - points to the ruby gem script
       3. irb - points to the ruby irb script
       4. node - points to your node directory
       5. npm - points to your npm directory
       6. rails - points to the rails script in your ruby/bin directory
       7. rake - points to the rake script in your ruby/bin directory
       8. ruby - points to the ruby script in your ruby/bin directory
       9. mysql - points to your mysql executable - and is the only link that does not depend on links in the packages subdirectory

    The git file, which is found the bin subdirectory is a script that we use to control how git commands are run.

- a cshrc.def file, which we use to set up various development environment variables. You will certainly need to modify this for your environment.
- a dependencies.yaml file, which shows which versions various packages are using for the current code.
- a packages subdirectory, which will be empty. This subdirectory will need to be populated with a combination of third-party package directories and softlinks to third-party       packages, which you will need to supply as you install the packages:
       1. autocomp - either the top-level directory of the autocomp-phr package or a softlink to it;
       2. javascript-stacktrace - either the top-level directory of the javascript-stacktrace code or a softlink to it;
       3. jquery - either the top-level directory of the jquery-1.9.1 code or a softlink to it;
       4. jquery-mobile - either the top-level directory of the jquery-mobile-1.4.2 code or a softlink to it;
       5. jquery-ui - either the top-level directory of the jquery-ui-1.10.1 code or a softlink to it;
       6. node - either the top-level directory of the node.js code or a softlink to it;
       7. node_modules - either the top-level directory of the node.js modules or a softlink to it; and
       8. ruby - either the top-level directory of the ruby code or a softlink to it.
- a proto1 sudirectory, which contains the bulk of the PHR code, and follows the Rails directory hierarchy conventions.

**Third-party Packages to be Installed**
1. MySQL or some other SQL database 
   - http://www.mysql.com
   - You can use MySQL version 5.6.45 (linux)
   - the def/bin directory contains a mysql softlink to the mysql executable. If this is not correct for your installation, update that softlink.
   - make sure you set up a user before installing other packages
   - we recommend specifying a secure installation, since the PHR system deals with sensitive information

2. A webserver such as Apache
   - http://httpd.apache.org
   - version 2.4.6

3. RubyOnRails
   - http://rubyonrails.org
   - installation order that works ]]:
        - install ruby
        - manually install the ruby gem named bundler
        - move the Gemfile from the def directory to your ruby directory
        - issue the bundle install command to install the gems listed in the Gemfile. When the installation completes successfully, you should have a Gemfile.lock file in your             ruby directory (in addition to the Gemfile). 
   - create a softlink ruby in the def/packages directory that points to your ruby directory
   - update the proto1/config/database.yml file as appropriate for your database.

4. node.js
   - http://nodejs.org
   - You can use:
        - node-v8.11.3-linux-x64
   - create a softlink node in the def/packages directory that points to your node directory
   - create a softlink node_modules in the def/packages directory that points to your node_modules directory. The node_modules should include prototype v0.0.5
   - npm - use the version that comes with your node.js distribution

**CONFIGURATION :**
**Elements Flagged for Change**
Places where changes are needed are flagged with some variation of TBD - change for your installation. Basically, searching for TBD in the following files should show you places where tailoring is required.
    - app/models/def_mailer.rb
    - app/models/installation_change.rb
    - app/views/def_mailer/verify_reg_email.html.erb
    - app/views/form/index.rhtml.erb
    - app/views/help_text/index.html.erb
    - config/app_settings.rb
    - config/constants.rb
    - config/database.yml
    - config/environments/development.rb
    - config/environments/test.rb
    - config/environments/production.rb
    - config/error_email.yml
    - config/installation/alternate/installation_config.rb
    - config/installation/default/installation_config.rb
    - lib/js_server/config.json
    - lib/loinc_preparation.rb
    - lib/tasks/def.rake
    - script/postNotice
    - test/selenium/0accounts.sel
    - test/unit/captcha_presenter_test.rb
   
Full-file Changes
Two files that support the ability to switch between installations basically need to be tailored in their entirety, i.e., every constant defined needs to be tailored. Luckily they are not big files. They are:
    - config/installation/alternate/installation_config.rb; and
    - config/installation/default/installation_config.rb

**Database tables that require tailoring**
A few table rows in the database also require some tailoring.

field_descriptions - 2 rows
    - Terms & Conditions on the registration form:
        1. You'll need to get the id of the signup form in the forms table (the_form_id = Form.where(form_name: 'signup'))
        2. Then get the row in the field_descriptions table that contains the terms & conditions text that is shown on the signup form (FieldDescription.where(form_id:                      the_form_id, target_field: 'instructions2')). The default_value column of that row contains the HTML for the terms and conditions for your site. Replace what's in                that column with your own text.
    - Suport email address on the login_answer form
        1. Get the id of the login_answer form in the forms table.
        2. Get the row in the field_descriptions table that contains a PHR support email address (FieldDescription.where(form_id: the_form_id, target_field: 'login_instr4')).              The default_value column of that row contains an email address for PHR support. Right now it is set to TBD@YOUR.SUPPORT.EMAIL. You'll want to change that.

installation_changes
    This table contains rows used to change from a default installation to an alternate installation. Each row in that table (there will usually be 3 rows in that table, but there might be 6) needs to be changed. 








