# BetterHelp-Coding-Challenge

* Run npm install
* Open localhost:3000
* Click on the submit button to see the results. 

Below are the tables and its attributes.
People table
|ID   |NAME   |ADDRESS   |
|:-:|:-:|:-:|
|2  |Austin|752-4834 Nascetur Rd|
|150|Laura|75 Jacobia Road|
|50   |Noel|Ap #654-6960 Nulla Road|
|968  |Olympia|4201 Egestas. Ave|
|571|Amelia|915-3085 Sapien. St|
|438|Ashley|320 Ut, Street


Donations table
|ID   |People ID|DONATION DATE|PARTY|
|:-:|:-:|:-:|:-:|
|1|2|2018-09-19|-1|
|2|2|2018-10-20|-1|
|3|2|2018-11-13|-1|
|4|2|2018-12-11|-1|
|5|2|2020-04-11|1|
|6|2|2020-01-11|1|
|7|2|2019-03-11|1|
|8|150|2019-04-13|-1|
|9|50|2020-02-08|-1|
|10|50|2020-01-07|1|
|11|50|2019-12-21|1|
|12|50|2019-11-10|1|
|13|968|2020-04-26|1|
|14|968|2020-01-26|-1|
|15|968|2019-01-26|1|
|16|44|2019-12-17|1|
|17|571|2020-04-21|-1|
|18|313|2020-03-11|1|
|19|313|2020-03-11|-1|
|19|313|2020-03-11|-1|


Below is the query that returns the name, date of most recent donation, political party and address <br/>
`WITH FINDPARTY AS(
         SELECT Donations.People_ID, SUM(CASE Donations.PARTY WHEN 1 THEN 1 ELSE 0 END) AS D,
         SUM(CASE Donations.PARTY WHEN -1 THEN 1 ELSE 0 END) AS R FROM Donations GROUP BY People_ID),
     FindMajorityParty AS(SELECT FINDPARTY.People_ID,
         (CASE WHEN FINDPARTY.D > FINDPARTY.R THEN "Democrat"
         WHEN FINDPARTY.D < FINDPARTY.R THEN "Republic"
         WHEN FINDPARTY.D = FINDPARTY.R THEN "Undetermined" END) AS MAJORITY_PARTY FROM FINDPARTY GROUP BY FINDPARTY.People_ID),
     FINDDONATIONDATE AS (SELECT Donations.People_ID, MAX(DONATION_DATE) AS MOST_RECENT_DATE FROM Donations GROUP BY Donations.People_ID),
     PEOPLETABLE AS(SELECT People.ID, People.NAME, People.ADDRESS FROM People)
         SELECT PEOPLETABLE.NAME, PEOPLETABLE.ADDRESS, FindMajorityParty.People_ID, FindMajorityParty.MAJORITY_PARTY, MOST_RECENT_DATE
         FROM FindMajorityParty, FINDDONATIONDATE, PEOPLETABLE
         WHERE FindMajorityParty.People_ID = FINDDONATIONDATE.People_ID AND FindMajorityParty.People_ID = PEOPLETABLE.ID
         GROUP BY FindMajorityParty.People_ID;    `


The input will only accept the above query. It will give a 'Request failed: error' when an invalid string is provide as an input. 
