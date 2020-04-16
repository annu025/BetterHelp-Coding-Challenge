# BetterHelp-Coding-Challenge

Below are the tables and its attributes.
People table
|ID   |NAME   |ADDRESS   |
|:-:|:-:|:-:|
|2  |Austin|752-4834 Nascetur Rd|
|150 |NoelAB|Ap #1654-6960 Nulla Road|
|50   |Noel|Ap #654-6960 Nulla Road|
|968  |Olympia|4201 Egestas. Ave|
|571|Amelia|915-3085 Sapien. St|
|438|Ashley|320 Ut, Street


Donations table
|ID   |People ID|DONATION DATE|PARTY|
|:-:|:-:|:-:|:-:|
|1|2|2020-04-11|1|
|1|2|2020-01-11|1|
|1|2|2019-03-11|1|
|2|150|2019-04-13|-1|
|3|50|2020-02-08|-1|
|4|968|2020-04-26|1|
|4|968|2020-01-26|-1|
|4|968|2019-01-26|1|
|5|44|2019-12-17|1|
|6|571|2020-04-21|-1|
|7|313|2020-03-11|1|

Below is the query that returns the name, date of most recent donation, political party and address <br/>
`SELECT People.NAME, MAX(Donations.DONATION_DATE) as DONATIONS, Donations.PARTY, People.ADDRESS FROM People JOIN Donations ON People.ID = Donations.People_ID GROUP BY People.NAME`

