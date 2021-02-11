# Project Purpose

Sparkify, a music streaming app startup, wants to leverage songs and user data that they have been collecting from the app by analyzing and finding relevant patterns. In particular, the analytics team wants to know what are the songs that the users are listening to. However, within the current setup, it is difficult for them to make sense of the data as it resides in directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app, which is not suitable for quering at all. The objective of this project is to create a Postgres database along with a database schema and ELT pipeline for optimized queries and subsequent analysis. Here is the outline of the project:

a) define fact and dimension tables for a star schema with a particular analytic focus
b) create database and tables. 
c) write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.
d) Test to to confirm the creation of your tables with the correct columns and  to confirm records were successfully inserted into each table. 

# Schema Design
For this project, we have implemented this following star schema: 
![image](https://drive.google.com/uc?export=view&id=1YHwDVf6w8NjPOizaoTqAJjyJK33z-HNd)
![image](https://drive.google.com/uc?export=view&id=1913oZeBZPBNiUuk8gu3ZSbLBA2l_VQtG)

As the fact table contains a 1 to many relationship to each of the dimensions in the data, we thought that it is appropriate to use a star schema. This database will enable the Analytics team to create recommendations to the users based on query data. Especially, they can capture live playback behavior such as song plays, artist plays, time when it is played, and more and use this behavioral data to recommend personalize playlists.

## Script Usage
For this project, the following scripts have been developed: 

1. **sql_queries.py**: contains all SQL queries of the project for creating, dropping and quering tables.
2. **create_tables.py**: has functions to create and drop table.

     #### Functions within the Script:
    **create_database**: Creates and connects to the sparkify database

    **drop_tables**: Drops each table using the queries in `drop_table_queries` list. 

    **create_tables**: Creates each table using the queries in `create_table_queries` list.
    
     **main**: Drops (if exists) and Creates the sparkify database.Establishes connection with the sparkify database and gets
    cursor to it. Drops all the tables. Creates all tables needed. Finally, closes the connection. 
    
    
3. **etl.ipynb**: reads and processes a single file from song_data and log_data and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.

4. **etl.py**:   read  and process files from song_data and log_data and load them to tables. 
    #### Functions and its importance:
   
    **process_song_file**: read the song files and to insert song and artist records

    **process_log_file**: read the log files and insert details with selected columns 
   
    **process_data**: collect all the file paths and then call the above two functions. Thereafter, show status of files processed.

    **main**: call the process_data function.

5. **test.py**: displays the first few rows of each table to let you check your database.

## Sample Queries 

SELECT songplays.location, songplays.level, songs.title,songs.duration, time.year, time.week, artists.name as Artist_Name, users.gender as User_Gender \
From songplays Left join songs on songplays.song_id = songs.song_id \
Left join time on songplays.start_time = time.start_time \
Left join artists on songplays.artist_id = artists.artist_id \
Left join users on songplays.user_id = users.user_id \
where songplays.song_id = 'SOZCTXZ12AB0182364' ;

![image](https://drive.google.com/uc?export=view&id=1y2Yba-hy8UkyDWRmIS1baQxX_4dHW-lT)












