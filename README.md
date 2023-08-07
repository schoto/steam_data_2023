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

