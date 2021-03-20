# video_game_ETL
In this particular ETL, I wanted to compared the popularity of games on Steam with the popularity of the games that are typically streamed on Twitch. These are two heavily used gaming platforms globally, with Steam providing a variety of games and Twitch providing a platform for gamers to interact with streamers, subscribe to channels and stream games. 

I want to be able to compare the games on Steam and the games most popular on Twitch to see where they match and what are some of the notable characteristics of the most popular games. 

# Data Sources
## Steam Kaggle Data
I used the following two sources from Kaggle for the Steam data: 

- [Steam Video Games](https://www.kaggle.com/tamber/steam-video-games)
- [Steam Store Games](https://www.kaggle.com/nikdavis/steam-store-games?select=steam.csv)

## Twitch API Data
Using the Twitch developers platform, I generated a client ID that allowed me access to their API to pull any necessary gaming data that I may need. In order to access the Twitch API I first downloaded the following package

```python
pip3 install python-twitch-client
```
Which then allows you to import TwitchClient from twitch.

- [Additional TwitchClient references](https://python-twitch-client.readthedocs.io/en/latest/basic_usage.html#)

# Cleaning & Transformations
Given that the Steam datasets were in kaggle, they were already relatively clean where the only cleaning was required was to clean any additional columns and reset any column titles as needed.

For the Twitch API, the data required a pprint to be able to appropriately read the data, but was relatively cleaned. The transformation to a dataframe required parsing through the various items for each game to be able to extract each of the names, viewers and channels for the associated games to convert to a dataframe within pandas. 

# Loading
The initial upload required the creation of a new database in postgres, but I used the psycogp2 package in order to create a connection into the postgres server aand create the database rather than using pgAdmin and creating it within that interface. Further steps are noted in the jupyter notebook. 

After closing that connection, I used sqlalchemy to upload and create the tables for each of the dataframes within the gaming_db to upload my data. I had chosen sqlalchemy for it's ease of use and later versatility when I wanted to transform the data or for later updates into the database. 

# Challenges
The biggest challenge of this project was being able to appropriately laod items into the sqlserver where I was unable to use pdAdmin in order to create the database and creating the tables as needed. Ultimately, I neeeded to look into alternative ways in which a postgres connection could be established that would allow me a similar point of access to the server and easily allow for updates. 

This was solved with the psycogp2 that allowed for database creation and later using sqlAlchemy to address any table creation or data creation that was needed. 

Also, the current Twitch API documentatin does not clearly allow for access when using Python or without the need for Oath2 which made it difficult to interpret the ways in which it waqs accessible. Using another search, the additional TwitchClient references (noted above) resolved this issue as well. 

# Additional Notes
Please noted for the Twitch API, you will need your own client ID in order to access the APIs and for the postgres access through sqlalchemy or psycogp2 you will also need to use your own local username, password, host and port as needed. 
