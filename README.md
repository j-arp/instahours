# Teamwork::InstaHours

A Utility to check hours in Teamwork and automatically complete week by submitting your missing hours to a default project.
Useful for folks like me that work primarily on a single support project

# What it Does
* Allows you to see time entries and total hours for a given week
* Allows you to generate all missing time and apply it to a given default project. 

For instance: You look up your weekly hours and you see you logged 30 minutes of work on some project on Tuesday and an hour and half to some otherproject on Wednesday. Fire of the complete command and InstaHours will add 8 hours to your default project on days without any entries, 7 1/2 hours on Tuesday and 6 1/2 hours on Wednesday.

You now have all 40 hours accounted for.

# Requirements:
  * enable TW api key in your account
  * set 3 Env variables on your puter: TW_API_KEY, TW_USER_ID, TW_PROJECT_ID
  * include this class in a script

# METHODS
  * new: pass in date for a week. leave blank for current week
  * entries_for: returns  all time entires for week
  * time_for: returns  total time logged in week
  * time_for_in_hours: same as above but in hours
  * complete: will check hours for each day of the week and add add missing time to default project

# EXAMPLE
  
    require_relative 'instahours'
    
    instahours = InstaHours.new
    #  or instahours = InstaHours.new(Date.new(2016,01,28))
    entries = instahours.entries_for
    time = instahours.time_for_in_hours
    
    puts "Total time logged is  #{time} "
    puts "There are #{entries.count} time entries"
    
    entries.each do | entry |
      puts "#{entry["date"]} | #{entry["project-name"]} >> #{entry["hours"]}h #{entry["minutes"]}m "
    end
    
    instahours.complete
