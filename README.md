<h1>Hello again, Kazbek here!</h1>

<h4>For this project I decided to go and work with Steam Data dataset with all Steam games ranked from 2023. Especially I will clean data and transform it.</h4>

DATA: steamspy_data.csv <br/>
STACK: BigQuery <br/>

The dataset looks like this for instance : <br/>

![BigQuery-–-My-First-Project-–-Console-Google-Cloud](https://github.com/schoto/steam_data_2023/assets/69323411/67f54898-acf8-4120-a334-e3c922b261be)
				
Let's say I'm not gonna need <b>owners,average_forever,average_2weeks, median_forever, median_2weeks, ccu (concurrent user), score_rank and tags columns</b>, because some of them are empty or we simply don't need them.

I'm gonna go ahead and select all I need with the following SQL query:

```
SELECT
  appid AS `Game Id`,
  name AS `Game Name`,
  developer AS Developer,
  publisher AS Publisher,
  score_rank AS `Score Rank`,
  positive AS Positive,
  negative AS Negative,
  userscore AS `User Score`,
  price AS Price,
  initialprice AS `Initial Price`,
  discount AS Discount,
  languages AS Languages,
  genre AS Genre
FROM
  `steam_data_2023.steamdata2023`;
```

and then I will save the result as a new CSV file so I can re-upload it to BigQuery. I could've save it as a new table though


![Créer-une-table-–-BigQuery-–-My-First-Project-–-Console-Google-Cloud](https://github.com/schoto/steam_data_2023/assets/69323411/4baa7baa-e22c-4009-b411-f66d13198aa5)

I have now more accurate information in this table

[screen record.webm](https://github.com/schoto/steam_data_2023/assets/69323411/57dfc440-ea0c-4b14-b38f-53cf63a47bd3)

Now I'm going to see if I have any double records on Game_Name column (normally we have 999 games in this dataset)

```
select count(distinct Game_name) AS nb_of_unique_names
from astral-outpost-382214.steam_data_2023.clean_data_steam;
```

And after executiong the query I see:

![BigQuery-–-My-First-Project-–-Console-Google-Cloud](https://github.com/schoto/steam_data_2023/assets/69323411/807ec280-c62c-4615-b19c-a955e637d326)

It means there's no doubles

Now we are going to check if in any columns of our dataset we have NULL values

```
SELECT
  COUNTIF(Game_Id IS NULL) AS Game_Id_null_count,
  COUNTIF(Game_Name IS NULL) AS Game_Name_null_count,
  COUNTIF(Developer IS NULL) AS Developer_null_count,
  COUNTIF(Genre IS NULL) AS Genre_null_count,
  COUNTIF(Publisher IS NULL) AS Publisher_null_count,
  COUNTIF(Positive IS NULL) AS Positive_null_count,
  COUNTIF(Negative IS NULL) AS Negative_null_count,
  COUNTIF(Price IS NULL) AS Price_null_count,
  COUNTIF(Initial_Price IS NULL) AS Initial_Price_null_count,
  COUNTIF(Discount IS NULL) AS Discount_null_count,
  COUNTIF(Languages IS NULL) AS Languages_Price_null_count,
FROM astral-outpost-382214.steam_data_2023.clean_data_steam;
```

We have 4 NULL values in all dataset: 1 in Developer column and 3 in Genre column

![Bienvenue-–-My-First-Project-–-Console-Google-Cloud](https://github.com/schoto/steam_data_2023/assets/69323411/3daf17fa-c967-4411-a475-19a9b4c0f006)

