ReportGrid Ruby Client Library

Usage
-----
Add the following to your Gemfile 

    git 'git@github.com:softwaregravy/reportgrid-client.git' do  
        gem 'reportgrid' 
     end                 

run `bundle install`

Rails Use 
---------

Note: this is just how I did it, you're free to do it however 

create a file `config/initializers/reportgrid.rb` and add:

    REPORTGRID_TOKEN = ENV['REPORTGRID_TOKEN'] 

    module ReportGrid
      def self.client
          ReportGrid::ReportGrid.new(REPORTGRID_TOKEN) 
      end 
    end 

Wherever you want to track events, you can now do:

    ReportGrid.client.track(PATH, EVENT_NAME, ATTRIBUTES, :rollup => [true|false])

Lets say you have an object called impression:

    ReportGrid.client.track("/tracking_set/#{@impression.common_value}", "impression", @impression.attributes, :rollup => true)

This should let you group stats of impressions by common value, and also show stats rolled up to the tracking set level

