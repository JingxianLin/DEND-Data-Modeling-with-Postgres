#1. A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.
Your role is to create a database schema and ETL pipeline for this analysis.
#2. Database Schema:
To complete the project, create a star schema optimized for queries on song play analysis. This includes the following tables.

#Fact Table
songplays - records in log data associated with song plays i.e. records with page NextSong
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#Dimension Tables
users - users in the app
user_id, first_name, last_name, gender, level

songs - songs in music database
song_id, title, artist_id, year, duration

artists - artists in music database
artist_id, name, location, latitude, longitude

time - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday

#In addition to the data files, six more files are included:

test.ipynb displays the first few rows of each table to let you check your database.
create_tables.py drops and creates tables. You run this file to reset your tables before each time you run your ETL scripts.
etl.ipynb reads and processes a single file from song_data and log_data and loads the data into your tables.
etl.py reads and processes files from song_data and log_data and loads them into your tables.
sql_queries.py contains all your sql queries, and is imported into the last three files above.
README.md provides discussion on the project.

#Steps to Follow:
Write CREATE statements in sql_queries.py to create each table.
Write DROP statements in sql_queries.py to drop each table if it exists.
Run in console: python create_tables.py
Run test.ipynb to confirm the creation.
Follow instructions in the etl.ipynb notebook to develop ETL processes for each table.
Run test.ipynb to confirm that records were successfully inserted into each table.
Implement etl.py, run and verify.

#ETL Pipeline:
Process song_data to create the songs and artists dimensional tables by inserting song record and artist record.
song_data = [song_id, title, artist_id, year, duration]
artist_data = [artist_id, artist_name, artist_location, artist_latitude, artist_longitude]
Process log_data to create the time and users dimensional tables, as well as the songplays fact table: For time table, filter records by NextSong action, extract the timestamp, hour, day, week of year, month, year, and weekday from the ts column, and insert time data records; for users table, select columns for user ID, first name, last name, gender and level, and insert user records; for songplays table, find songs by using the query
song_select = ("""SELECT song_id, artists.artist_id FROM songs JOIN artists ON songs.artist_id = artists.artist_id WHERE songs.title = %s AND artists.name = %s AND duration = %s
""")
select the timestamp, user ID, level, song ID, artist ID, session ID, location, and user agent, and insert songplay record.