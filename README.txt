This is submission for Upgrad Cricket Challenge. Here is the approach documentation --
1.Data Gathering --

	Espn cricinfo website url was hit using R's xml2 package. The resultant html was parsed to get the details. 
	In each url call, 200 records were fetched. This was repeated till the pages existed.

	Below are the details gathered --
	australia batsman stats -- details of each and every batting innings playerwise played by australia
	australia bowler stats  -- details of each and every bowler innings playerwise played by australia
	australia series stats  -- details of each series played by australia result wise
	australia team stats    -- details of each and every match played by australia result wise
	india batsman stats     -- details of each and every batting innings playerwise played by india
	india bowler stats      -- details of each and every bowler innings playerwise played by india
	india series stats      -- details of each series played by india result wise
	india team stats        -- details of each and every match played by india result wise

	All the code for url data scraping is in the below files (this was run once for team2 aus and again for team6 india) --
	cricinfo_batsman_stats.R
	cricinfo_bowler_stats.R
	cricinfo_series_stats.R
	cricinfo_team_stats.R

	At the end, all the data obtained was written to csv's and is available in the same directory by the below names --
	australia_batsman_stats.csv
	australia_bowler_stats.csv
	australia_series_stats.csv
	australia_team_stats.csv
	india_batsman_stats.csv
	india_bowler_stats.csv
	india_series_stats.csv
	india_team_stats.csv

	page= parameter in the url was changed while running -- team2 in the R files's urls mean Australia and team6 means India

2. Every venue which has seen a match between india and australia was mapped manually to their home countries --
	
	venue_to_hometeam_mapping.csv

	Eg - This file will map Delhi to India and Dubai to UAE.
	Based on the above, a new KPI was built to tell if a match happened in the teams home country

************************************************************************************
Data preparation and modelling

For every prediction, linear model, random forest and gradientboosted rf were tried. 
The best one was picked based on rmse/accuracy and predictions were made for the 5 ODIs

************************************************************************************
	
3. predicting runs for batsmen	
	
	The following metrics were derived and used to build a model for each batsman --	
	'opposition'							-- opposition team - india and australia
	'ratio_of_matches_played_last_year'     -- a player might have been dropped from the team. This metric tell how many times the player played in last 1 year
	'runs_scored_last_year'                 -- runs scored last year 
	'avg_last_year'                         -- average runs per match in last year
	'centuries_last_year'                   -- no of centuries scored last year
	'half_centuries_last_year'              -- no of half centuries scored last year
	'month'                                 -- month when match was played
	'total_runs_scored'                     -- total runs scored till the match date
	'sixes_till_date'                       -- total sixes hit till the match date
	'fours_till_date'                       -- total 4s hit till the match date
	'is_home_venue'                         -- if the match was played on teams home ground
	'is_opposition_home_venue'              -- if the match was played on oppositions home ground

4.	predicting wickets for bowlers

	The following metrics were derived and used to build a model for each batsman --	
	'wickets'								-- wickets taken in the match
	'opposition'							-- opposition team - india and australia
	'ratio_of_matches_played_last_year'     -- a player might have been dropped from the team. This metric tell how many times the player played in last 1 year
	'total_wickets_taken'                   -- wickets taken till that match
    'total_overs_bowled'                    -- overs bowled till that match
	'total_maidens_bowled'                  -- maidens bowled till that match
	'total_runs_given'                      -- runs given till that match
	'wickets_taken_last_year'               -- wickets taken in last 1 year
    'avg_wickets_last_year'                 -- average no of wickets per match in last year
	'is_home_venue'                         -- if the match was played on teams home ground
	'is_opposition_home_venue'              -- if the match was played on oppositions home ground

	
5. predicting maximum 4s/6s --
	
	The following metrics were derived and used to build a model for each batsman --	
	'runs'									-- runs scored in the match (used from earlier runs prediction model)
	'opposition'							-- opposition team - india and australia
	'ratio_of_matches_played_last_year'     -- a player might have been dropped from the team. This metric tell how many times the player played in last 1 year
	'runs_scored_last_year'                 -- runs scored last year 
	'avg_last_year'                         -- average runs per match in last year
	'centuries_last_year'                   -- no of centuries scored last year
	'half_centuries_last_year'              -- no of half centuries scored last year
	'month'                                 -- month when match was played
	'total_runs_scored'                     -- total runs scored till the match date
	'sixes_till_date'                       -- total sixes hit till the match date
	'fours_till_date'                       -- total 4s hit till the match date
	'is_home_venue'                         -- if the match was played on teams home ground
	'is_opposition_home_venue'              -- if the match was played on oppositions home ground

6. predicting winning team match by match --

	The following metrics were derived and used to build a model for each batsman --	
	'opposition'							-- opposition team - india and australia
	'is_home_venue'                         -- if the match was played on teams home ground
	'is_opposition_home_venue'              -- if the match was played on oppositions home ground
	'loss_ratio_last_year'                  -- ratio of matches lost to played last year
	'odi_loss_ratio_last_year'              -- ratio of odi matches lost to played last year
	'last_year_odi_loss_ratio_against_aus'  -- ratio of odi matches lost against aus to played last year
	'overall_odi_loss_ratio_against_aus'    -- ratio of odi matches lost against aus across all years
	'overall_odi_loss_ratio'                -- ratio of odi matches lost across all years
	'last_tournament_lost_flag'             -- did the team lose the last tournament
	'last_match_lost_flag'                  -- did the team lose the last match
	'result'                                -- win or loss result

7. Sequence in which code should be run --

	cricinfo_batsman_stats.R
	cricinfo_bowler_stats.R
	cricinfo_series_stats.R
	cricinfo_team_stats.R
	australian_player_run_prediction.R
	australian_player_wicket_prediction.R
	indian_player_run_prediction.R
	indian_player_wicket_prediction.R
	india_4s_6s_prediction.R
	australia_4s_6s_prediction.R
	series_win_predictions.R
	
******************************************************************************************************************************************************
Predictions
******************************************************************************************************************************************************
Match results 
Match 1 - India
Match 2 - India
Match 3 - India
Match 4 - India
Match 5 - India	

Most runs --
S Dhawan followed by Dhoni, Kohli and Maxwell

Most wickets --
JA Richardson followed by Zampa, Bhumbrah, Shami and Yadav

Most 6s --
Rohit Sharma and Maxwell are tied

Most 4s --
S Dhawan and Maxwell are tied
	
	
	
	
	
	
	
	
	