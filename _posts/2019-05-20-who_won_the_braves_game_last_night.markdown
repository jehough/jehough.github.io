---
layout: post
title:      "Who won the Braves game last night?"
date:       2019-05-21 01:47:31 +0000
permalink:  who_won_the_braves_game_last_night
---


I'm an avid baseball fan.  So when it came time to build a personal project, the natural direction was to use baseball.  In this project I wanted to be able to pull information from a website and be able to use the data to print out some outputs.  I didn't want to use straight data, but rather put them into an object in order to use the data more efficiently.

I honestly wanted to grab more statistics than I was able to grab.  Most of the websites that offer sports data (ESPN, CBSSports, etc) use javascript to put live stats and things on the pages.  I also had trouble finding api's that would work for the project because apparently, sports data is a hot commodity that everyone wants to be paid for.  

I finally settled on getting data from baseball-reference.com.  While many of their stats are still by javascript, they had enough information for me to scrape and use for my project.  I chose to grab all the team names, scores and winning/losing pitchers.  The process of scraping the data was pretty straight forward.  All the information was in tables, so I simple iterated through the tables and grabbed what I needed and put the data for each game in a hash and all of the hashes in an array.

Using the array to create objects in a Game class, I was able to manipulate all the data.  
```
    def initialize(team1, team2, game)
        @game = "#{team1} vs #{team2}"
        attrs_from_hash(game)
        find_winner
        @@all << self
        @@winners << self.winner
        @@losers << self.loser
    end
    def self.create_from_array(games)
        games.each do |game|
        team1 = game[:away_team]
        team2 = game[:home_team]
        self.new(team1, team2, game)
        end
    end
```

It seems like it may be a little wordy and it probably puts to much in initialize, but I wanted to make sure all the information got to the right places.  My goal was to not just put out the simple game score, but to also print out a list of winners and losers.  After creating this class and the CLI class I had a working program....until the next day.

The day after I completed the program I pulled it up and got a strange error that .css was not a function for Nilclass.  Apparrently the day before a game occured where there was no winning/losing pitcher.  That table became nil and broke my program.  It took me a while of fiddling around to find exactly what was wrong.  Once I did, the best way to get around that was to rewrite the pitching portion to test for a nil table before scraping for the pitchers.  I tried it inside my map block and it did not like that.  I finally settled on the following.
```
    games = []
    @@site.css('div.game_summaries').css('div.game_summary').map do |game|
      hash = {
      :away_team => game.css('table.teams').css('tr').first.css('td').css('a')[0].text.chomp,
      :away_score => game.css('table.teams').css('tr').first.css('td.right').first.text.to_i,
      :home_team => game.css('table.teams').css('tr').last.css('td').css('a').text.chomp,
      :home_score => game.css('table.teams').css('tr').last.css('td.right').first.text.to_i}
      if game.css('table')[1] == nil
        hash[:winning_pitcher] = ''
        hash[:losing_pitcher] = ''
      else
        hash[:winning_pitcher] = game.css('table')[1].css('tr')[0].css('td')[1].text
        hash[:losing_pitcher] = game.css('table')[1].css('tr')[1].css('td')[1].text
      end
      games << hash
    end
```

By creating the array separately I could play with the hash after I closed it and add the whole thing back to the array.
Again, it seems overly wordy, but it worked.

