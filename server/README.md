# Blockbusters server

This is the server-side for the Blockbuster App

## Running the application in dev mode

You can run your application in dev mode that enables live coding using:
```shell script
./mvnw compile quarkus:dev
```

## Packaging and running the application

The application can be packaged using:
```shell script
./mvnw package
```
It produces the `quarkus-run.jar` file in the `target/quarkus-app/` directory.
Be aware that it’s not an _über-jar_ as the dependencies are copied into the `target/quarkus-app/lib/` directory.

The application is now runnable using `java -jar target/quarkus-app/quarkus-run.jar`.

If you want to build an _über-jar_, execute the following command:
```shell script
./mvnw package -Dquarkus.package.type=uber-jar
```

The application, packaged as an _über-jar_, is now runnable using `java -jar target/*-runner.jar`.

## Creating a native executable

You can create a native executable using: 
```shell script
./mvnw package -Pnative
```

Or, if you don't have GraalVM installed, you can run the native executable build in a container using: 
```shell script
./mvnw package -Pnative -Dquarkus.native.container-build=true
```

You can then execute your native executable with: `./target/blockbusters-server-1.0.0-SNAPSHOT-runner`

If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Testing the application

### REST

You can test the application in Swagger UI

1. Do a `GET` on `/movie/{title}` passing in `The Godfather`

Or in a shell:

```
curl -X 'GET' \
  'http://localhost:8080/movie/The%20Godfather' \
  -H 'accept: application/json'
```

Result:

```
{
  "id": "tt0068646",
  "title": "The Godfather",
  "fullTitle": "The Godfather (1972)",
  "year": 1972,
  "image": "https://imdb-api.com/images/original/MV5BM2MyNjYxNmUtYTAwNi00MTYxLWJmNWYtYzZlODY3ZTk3OTFlXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_Ratio0.6751_AL_.jpg",
  "releaseDate": "1972-03-24",
  "runtimeMins": 175,
  "runtimeStr": "2h 55min",
  "plot": "The Godfather \"Don\" Vito Corleone is the head of the Corleone mafia family in New York. He is at the event of his daughter's wedding. Michael, Vito's youngest son and a decorated WW II Marine is also present at the wedding. Michael seems to be uninterested in being a part of the family business. Vito is a powerful man, and is kind to all those who give him respect but is ruthless against those who do not. But when a powerful and treacherous rival wants to sell drugs and needs the Don's influence for the same, Vito refuses to do it. What follows is a clash between Vito's fading old values and the new ways which may cause Michael to do the thing he was most reluctant in doing and wage a mob war against all the other mafia families which could tear the Corleone family apart.",
  "awards": "Top rated movie #2 | Won 3 Oscars, 31 wins & 30 nominations total",
  "genres": "Crime, Drama",
  "companyList": [
    {
      "id": "co0023400",
      "name": "Paramount Pictures"
    },
    {
      "id": "co0921482",
      "name": "Albert S. Ruddy Productions"
    },
    {
      "id": "co0255097",
      "name": "Alfran Productions"
    }
  ],
  "countries": "USA",
  "languages": "English, Italian, Latin",
  "contentRating": "R",
  "imDbRating": 9.2,
  "boxOffice": {
    "budget": "$6,000,000 (estimated)",
    "openingWeekendUSA": "$302,393",
    "grossUSA": "$136,381,073",
    "cumulativeWorldwideGross": "$250,341,816"
  },
  "tagline": "An offer you can't refuse.",
  "keywordList": [
    "mafia",
    "patriarch",
    "crime family",
    "organized crime",
    "gambling syndicate"
  ],
  "similars": [
    {
      "id": "tt0071562",
      "title": "The Godfather: Part II"
    },
    {
      "id": "tt0111161",
      "title": "The Shawshank Redemption"
    },
    {
      "id": "tt0468569",
      "title": "The Dark Knight"
    },
    {
      "id": "tt0110912",
      "title": "Pulp Fiction"
    },
    {
      "id": "tt0109830",
      "title": "Forrest Gump"
    },
    {
      "id": "tt0108052",
      "title": "Schindler's List"
    },
    {
      "id": "tt0137523",
      "title": "Fight Club"
    },
    {
      "id": "tt0167260",
      "title": "The Lord of the Rings: The Return of the King"
    },
    {
      "id": "tt1375666",
      "title": "Inception"
    },
    {
      "id": "tt0099685",
      "title": "Goodfellas"
    },
    {
      "id": "tt0099674",
      "title": "The Godfather: Part III"
    },
    {
      "id": "tt0133093",
      "title": "The Matrix"
    }
  ]
}
```

2. Do a `GET` on `/movie/cast/{id}` passing in id from the result above.

Or in a shell:

```
curl -X 'GET' \
  'http://localhost:8080/movie/cast/tt0068646' \
  -H 'accept: application/json'
```

Result:

```
{
  "imDbId": "tt0068646",
  "directors": {
    "items": [
      {
        "id": "nm0000338",
        "name": "Francis Ford Coppola"
      }
    ]
  },
  "writers": {
    "items": [
      {
        "id": "nm0701374",
        "name": "Mario Puzo"
      },
      {
        "id": "nm0000338",
        "name": "Francis Ford Coppola"
      },
      {
        "id": "nm0701374",
        "name": "Mario Puzo"
      }
    ]
  },
  "actors": [
    {
      "id": "nm0000008",
      "name": "Marlon Brando",
      "image": "https://imdb-api.com/images/original/MV5BMTg3MDYyMDE5OF5BMl5BanBnXkFtZTcwNjgyNTEzNA@@._V1_Ratio1.2727_AL_.jpg",
      "asCharacter": "Don Vito Corleone"
    },
    {
      "id": "nm0000199",
      "name": "Al Pacino",
      "image": "https://imdb-api.com/images/original/MV5BMTQzMzg1ODAyNl5BMl5BanBnXkFtZTYwMjAxODQ1._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Michael"
    },
    {
      "id": "nm0001001",
      "name": "James Caan",
      "image": "https://imdb-api.com/images/original/MV5BMTI5NjkyNDQ3NV5BMl5BanBnXkFtZTcwNjY5NTQ0Mw@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Sonny"
    },
    {
      "id": "nm0144710",
      "name": "Richard S. Castellano",
      "image": "https://imdb-api.com/images/original/MV5BMjI2MzA3MjQ5N15BMl5BanBnXkFtZTcwMzY5NDYwOA@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Clemenza (as Richard Castellano)"
    },
    {
      "id": "nm0000380",
      "name": "Robert Duvall",
      "image": "https://imdb-api.com/images/original/MV5BMjk1MjA2Mjc2MF5BMl5BanBnXkFtZTcwOTE4MTUwMg@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Tom Hagen"
    },
    {
      "id": "nm0001330",
      "name": "Sterling Hayden",
      "image": "https://imdb-api.com/images/original/MV5BMjE0MTk1NjkzN15BMl5BanBnXkFtZTcwMzA1MjE1Mg@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Capt. McCluskey"
    },
    {
      "id": "nm0549134",
      "name": "John Marley",
      "image": "https://imdb-api.com/images/original/MV5BMjk0NjY1MjAyMl5BMl5BanBnXkFtZTcwNzY5NDYwOA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Jack Woltz"
    },
    {
      "id": "nm0002017",
      "name": "Richard Conte",
      "image": "https://imdb-api.com/images/original/MV5BNzE0MzU0MzY3OF5BMl5BanBnXkFtZTcwMjE2MjYwOA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Barzini"
    },
    {
      "id": "nm0504803",
      "name": "Al Lettieri",
      "image": "https://imdb-api.com/images/original/MV5BOWUxYTJkY2MtYmZmZi00ZjBmLWJmM2ItMmU3YWI2YzBhZDUwXkEyXkFqcGdeQXVyNjUxMjc1OTM@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Sollozzo"
    },
    {
      "id": "nm0000473",
      "name": "Diane Keaton",
      "image": "https://imdb-api.com/images/original/MV5BMTY5NDI5OTEyOF5BMl5BanBnXkFtZTgwMzU4NDI1NzM@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Kay Adams"
    },
    {
      "id": "nm0001820",
      "name": "Abe Vigoda",
      "image": "https://imdb-api.com/images/original/MV5BMjE1MDk5NzMyN15BMl5BanBnXkFtZTYwMjA4Mjg1._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Tessio"
    },
    {
      "id": "nm0001735",
      "name": "Talia Shire",
      "image": "https://imdb-api.com/images/original/MV5BMTkwMzc0NjQzNV5BMl5BanBnXkFtZTYwNzM0NTk3._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Connie"
    },
    {
      "id": "nm0751625",
      "name": "Gianni Russo",
      "image": "https://imdb-api.com/images/original/MV5BNTgyMTgxODM4MV5BMl5BanBnXkFtZTcwNDg5NDYwOA@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Carlo"
    },
    {
      "id": "nm0001030",
      "name": "John Cazale",
      "image": "https://imdb-api.com/images/original/MV5BMTUzMTM1MjI5NV5BMl5BanBnXkFtZTcwMTM5NTM1Mw@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Fredo"
    },
    {
      "id": "nm0094036",
      "name": "Rudy Bond",
      "image": "https://imdb-api.com/images/original/MV5BNWY2ZGQxMDctNWUyYS00NzYyLTk0MjMtZWY4MWY2YzQ1ZGRiXkEyXkFqcGdeQXVyNjUwNzk3NDc@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Cuneo"
    },
    {
      "id": "nm0553887",
      "name": "Al Martino",
      "image": "https://imdb-api.com/images/original/MV5BMjMyMDk4MzYyMl5BMl5BanBnXkFtZTcwNzg5NDYwOA@@._V1_Ratio0.8182_AL_.jpg",
      "asCharacter": "Johnny Fontane"
    },
    {
      "id": "nm0455088",
      "name": "Morgana King",
      "image": "https://imdb-api.com/images/original/MV5BODg5OTAxNDQzMl5BMl5BanBnXkFtZTgwOTM3ODIxNjM@._V1_Ratio1.0000_AL_.jpg",
      "asCharacter": "Mama Corleone"
    },
    {
      "id": "nm0598926",
      "name": "Lenny Montana",
      "image": "https://imdb-api.com/images/original/MV5BMjFmMjQ4ODMtNDZmZC00NzQ3LTlmODEtOTBlMGIzMzUxY2Q4XkEyXkFqcGdeQXVyNjUxMjc1OTM@._V1_Ratio0.9545_AL_.jpg",
      "asCharacter": "Luca Brasi"
    },
    {
      "id": "nm0553908",
      "name": "John Martino",
      "image": "https://imdb-api.com/images/original/MV5BMTUzNTgzNTg5MV5BMl5BanBnXkFtZTgwOTMzODU3NjE@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Paulie Gatto"
    },
    {
      "id": "nm0181128",
      "name": "Salvatore Corsitto",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Bonasera"
    },
    {
      "id": "nm0109175",
      "name": "Richard Bright",
      "image": "https://imdb-api.com/images/original/MV5BODZmNzZhMTgtMDdhMC00YzRhLWJlYzQtZWI0OGQ4YzI1ZDA3XkEyXkFqcGdeQXVyMjUyNDk2ODc@._V1_Ratio1.5000_AL_.jpg",
      "asCharacter": "Neri"
    },
    {
      "id": "nm0733678",
      "name": "Alex Rocco",
      "image": "https://imdb-api.com/images/original/MV5BMTk3MTMyNTkxOF5BMl5BanBnXkFtZTcwMDA4NTAzMQ@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Moe Greene"
    },
    {
      "id": "nm0320413",
      "name": "Tony Giorgio",
      "image": "https://imdb-api.com/images/original/MV5BMTQ2ODY2NzktOTQ5Zi00MTA3LWE4NTAtZGFjNjdjOGU2ZTE5XkEyXkFqcGdeQXVyMjUyNDk2ODc@._V1_Ratio1.7727_AL_.jpg",
      "asCharacter": "Bruno Tattaglia"
    },
    {
      "id": "nm0780005",
      "name": "Vito Scotti",
      "image": "https://imdb-api.com/images/original/MV5BMTY4MzMwOTU3Ml5BMl5BanBnXkFtZTcwNTE0MzkxOA@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Nazorine"
    },
    {
      "id": "nm0515372",
      "name": "Tere Livrano",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Theresa Hagen"
    },
    {
      "id": "nm0719353",
      "name": "Victor Rendina",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Philip Tattaglia"
    },
    {
      "id": "nm0512642",
      "name": "Jeannie Linero",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Lucy Mancini"
    },
    {
      "id": "nm0339589",
      "name": "Julie Gregg",
      "image": "https://imdb-api.com/images/original/MV5BNDIyODY0NTE4NV5BMl5BanBnXkFtZTgwNTM0NTg1MDI@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Sandra Corleone"
    },
    {
      "id": "nm0792132",
      "name": "Ardell Sheridan",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Mrs. Clemenza"
    },
    {
      "id": "nm0824940",
      "name": "Simonetta Stefanelli",
      "image": "https://imdb-api.com/images/original/MV5BMTQ2NjYxNzYxMl5BMl5BanBnXkFtZTcwMDA4NzkxOA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Apollonia - Sicilian Sequence"
    },
    {
      "id": "nm0408636",
      "name": "Angelo Infanti",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Fabrizio - Sicilian Sequence"
    },
    {
      "id": "nm0301403",
      "name": "Corrado Gaipa",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Don Tommasino - Sicilian Sequence"
    },
    {
      "id": "nm0162948",
      "name": "Franco Citti",
      "image": "https://imdb-api.com/images/original/MV5BMjIxMDg5MDA1MV5BMl5BanBnXkFtZTcwMzIyOTUzOA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Calo - Sicilian Sequence"
    },
    {
      "id": "nm0882237",
      "name": "Saro Urzì",
      "image": "https://imdb-api.com/images/original/MV5BMjIyNDQyNzc0OF5BMl5BanBnXkFtZTcwNTMzMTMwNw@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Vitelli - Sicilian Sequence"
    },
    {
      "id": "nm0025702",
      "name": "Chris Anastasio",
      "image": "https://imdb-api.com/images/original/MV5BMTc2NzkyNTI5Nl5BMl5BanBnXkFtZTYwNTQ3MDky._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Policeman (uncredited)"
    },
    {
      "id": "nm5981184",
      "name": "Norm Bacchiocchi",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Luca Brasi's Assassin (uncredited)"
    },
    {
      "id": "nm0104967",
      "name": "Max Brandt",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Extra in Furniture-Moving Scene (uncredited)"
    },
    {
      "id": "nm0012736",
      "name": "Tybee Brascia",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Dancer in Wedding Scene (uncredited)"
    },
    {
      "id": "nm13397629",
      "name": "Garrett Cassell",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Chef (uncredited)"
    },
    {
      "id": "nm0178874",
      "name": "Carmine Coppola",
      "image": "https://imdb-api.com/images/original/MV5BMjk1MTY2MjA5OF5BMl5BanBnXkFtZTgwODYxNTcxMDE@._V1_Ratio1.4545_AL_.jpg",
      "asCharacter": "Piano Player in Montage (uncredited)"
    },
    {
      "id": "nm0178887",
      "name": "Gian-Carlo Coppola",
      "image": "https://imdb-api.com/images/original/MV5BMDFjOGUzODgtZDQzNC00MDY2LWJmMjYtZDdlNGM2NTI2MzMyXkEyXkFqcGdeQXVyNjUwNzk3NDc@._V1_Ratio0.8182_AL_.jpg",
      "asCharacter": "Baptism Observer (uncredited)"
    },
    {
      "id": "nm0178889",
      "name": "Italia Coppola",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Extra in Wedding Scene (uncredited)"
    },
    {
      "id": "nm0178910",
      "name": "Roman Coppola",
      "image": "https://imdb-api.com/images/original/MV5BMTU2OTE2MDkzOF5BMl5BanBnXkFtZTYwOTgyMDgz._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Boy on Street Who Attended Funeral (uncredited)"
    },
    {
      "id": "nm0001068",
      "name": "Sofia Coppola",
      "image": "https://imdb-api.com/images/original/MV5BMTcxODIwMDMzOF5BMl5BanBnXkFtZTgwMDE5MTU0MDE@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Michael Francis Rizzi (uncredited)"
    },
    {
      "id": "nm0182539",
      "name": "Don Costello",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Don Victor Stracci (uncredited)"
    },
    {
      "id": "nm0196872",
      "name": "Robert Dahdah",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Crowd (uncredited)"
    },
    {
      "id": "nm5217597",
      "name": "Richard Fass",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Tom Hagen's Son (uncredited)"
    },
    {
      "id": "nm0292875",
      "name": "Gray Frederickson",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Cowboy on the Set at Woltz's Studio (uncredited)"
    },
    {
      "id": "nm0003003",
      "name": "Ron Gilbert",
      "image": "https://imdb-api.com/images/original/MV5BZjMwOWJjZmYtYTNhNy00ZWMzLTljOTMtMzdjMzVjZGIzNTNlXkEyXkFqcGdeQXVyMTcxNDMwOTg@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Usher in Bridal Party (uncredited)"
    },
    {
      "id": "nm0332630",
      "name": "Anthony Gounaris",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Anthony Vito Corleone (uncredited)"
    },
    {
      "id": "nm0342519",
      "name": "Joe Lo Grippo",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Sonny's Bodyguard (uncredited)"
    },
    {
      "id": "nm0343780",
      "name": "Sonny Grosso",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Cop Outside Hospital (uncredited)"
    },
    {
      "id": "nm0348927",
      "name": "Louis Guss",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Don Zaluchi (uncredited)"
    },
    {
      "id": "nm0837665",
      "name": "Bobra Harris",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Woman (uncredited)"
    },
    {
      "id": "nm2361496",
      "name": "Merril E. Joels",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Toll Both Collector (uncredited)"
    },
    {
      "id": "nm0432921",
      "name": "Randy Jurgensen",
      "image": "https://imdb-api.com/images/original/MV5BMjEwMDMzMTUxOV5BMl5BanBnXkFtZTcwMTQ3ODU5NA@@._V1_Ratio1.5000_AL_.jpg",
      "asCharacter": "Sonny's Killer #1 (uncredited)"
    },
    {
      "id": "nm0268094",
      "name": "Tony King",
      "image": "https://imdb-api.com/images/original/MV5BMTc5MTY4Nzg1NF5BMl5BanBnXkFtZTcwMTUwOTA0NA@@._V1_Ratio1.2273_AL_.jpg",
      "asCharacter": "Tony - Stablehand (uncredited)"
    },
    {
      "id": "nm0483279",
      "name": "Paul Lambert",
      "image": "https://imdb-api.com/images/original/MV5BNTQ5MDNjOTUtYWZlNS00MWRlLTkzMTQtMzg0MTBlMDgxN2EzL2ltYWdlL2ltYWdlXkEyXkFqcGdeQXVyOTA4NDY2Mw@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Mobster at Funeral with Barzini (uncredited)"
    },
    {
      "id": "nm1711180",
      "name": "Peter Lemongello",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Singer (uncredited)"
    },
    {
      "id": "nm0513401",
      "name": "Tony Lip",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Wedding Guest (uncredited)"
    },
    {
      "id": "nm0553778",
      "name": "Lou Martini Jr.",
      "image": "https://imdb-api.com/images/original/MV5BMjQ1Y2QzMGItZjkxYy00YWFjLWI0MzktMjk1ZDg2ZDRkOGJlXkEyXkFqcGdeQXVyMTI4ODQ5Ng@@._V1_Ratio1.3182_AL_.jpg",
      "asCharacter": "Boy at Wedding (uncredited)"
    },
    {
      "id": "nm0553937",
      "name": "Raymond Martino",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Corleone Family Member (uncredited)"
    },
    {
      "id": "nm0575453",
      "name": "Joseph Medaglia",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Priest at Baptism (uncredited)"
    },
    {
      "id": "nm0605866",
      "name": "Carol Morley",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Night Nurse (uncredited)"
    },
    {
      "id": "nm6586677",
      "name": "Dave Moskin",
      "image": "https://imdb-api.com/images/original/MV5BOWQxMzNjOTgtMmFmZi00Y2U5LWFhYmQtZTVhOWRjYjdkZGYxXkEyXkFqcGdeQXVyMTI4NzM2MA@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Child (uncredited)"
    },
    {
      "id": "nm0678385",
      "name": "Rick Petrucelli",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Lou - Sollozzo's Driver (uncredited)"
    },
    {
      "id": "nm0678393",
      "name": "Joe Petrullo",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Pallbearer (uncredited)"
    },
    {
      "id": "nm0723997",
      "name": "Burt Richards",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Floral Designer (uncredited)"
    },
    {
      "id": "nm0724319",
      "name": "Sal Richards",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Drunk (uncredited)"
    },
    {
      "id": "nm0727004",
      "name": "Chuck Riley",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Narrator of Theatrical Trailer (voice) (uncredited)"
    },
    {
      "id": "nm0743159",
      "name": "Tom Rosqui",
      "image": "https://imdb-api.com/images/original/MV5BOTdkMTJmNjktZjE3NS00NjJlLTk3NTEtMGQyOGQ2ZjU1ZTliXkEyXkFqcGdeQXVyMTcyODY2NDQ@._V1_Ratio1.3182_AL_.jpg",
      "asCharacter": "Rocco Lampone (uncredited)"
    },
    {
      "id": "nm0744351",
      "name": "Giacomo Rossi Stuart",
      "image": "https://imdb-api.com/images/original/MV5BMTM0ODM3MTM4MF5BMl5BanBnXkFtZTcwNTU5ODg0NA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "G.I. (uncredited)"
    },
    {
      "id": "nm0749429",
      "name": "Nino Ruggeri",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Mobster at Funeral with Barzini (uncredited)"
    },
    {
      "id": "nm0803370",
      "name": "Frank Sivero",
      "image": "https://imdb-api.com/images/original/MV5BMTkzNDQxMTcxMF5BMl5BanBnXkFtZTcwNTU0NDgyMQ@@._V1_Ratio0.7273_AL_.jpg",
      "asCharacter": "Street Extra (uncredited)"
    },
    {
      "id": "nm0816628",
      "name": "Filomena Spagnuolo",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Extra in Wedding Scene (uncredited)"
    },
    {
      "id": "nm0818874",
      "name": "Joe Spinell",
      "image": "https://imdb-api.com/images/original/MV5BYjc4ZjA0NTQtYWFlMC00ZjkwLWIyMjYtY2U3MzI5YTQ0NmQ4XkEyXkFqcGdeQXVyNjUxMjc1OTM@._V1_Ratio0.8182_AL_.jpg",
      "asCharacter": "Willi Cicci (uncredited)"
    },
    {
      "id": "nm0868442",
      "name": "Gabriele Torrei",
      "image": "https://imdb-api.com/images/original/MV5BMjNhZjNhN2QtMGRlOC00NWNkLWI1MmEtNDU5YzhkM2ZhNDFkXkEyXkFqcGdeQXVyMTcyODY2NDQ@._V1_Ratio1.5000_AL_.jpg",
      "asCharacter": "Enzo the Baker (uncredited)"
    },
    {
      "id": "nm0885014",
      "name": "Nick Vallelonga",
      "image": "https://imdb-api.com/images/original/MV5BMDIwYmVmOGEtNzhjZi00Zjg0LTlmMDQtOTczMGU4YjdiYzJlXkEyXkFqcGdeQXVyNjY5NDE1MDM@._V1_Ratio0.8636_AL_.jpg",
      "asCharacter": "Wedding Party Guest (uncredited)"
    },
    {
      "id": "nm0796439",
      "name": "Ed Vantura",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Wedding Guest (uncredited)"
    },
    {
      "id": "nm2096458",
      "name": "Ron Veto",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Extra in Hospital Scene (uncredited)"
    },
    {
      "id": "nm1417330",
      "name": "Matthew Vlahakis",
      "image": "https://imdb-api.com/images/original/MV5BYTE5OWUwMjMtZmFiMy00ODE0LWI0MWQtYTk4MGE3MWY0ZjUwXkEyXkFqcGdeQXVyMjU2NjM3MA@@._V1_Ratio0.7727_AL_.jpg",
      "asCharacter": "Clemenza's Son (uncredited)"
    },
    {
      "id": "nm0945192",
      "name": "Conrad Yama",
      "image": "https://imdb-api.com/images/original/nopicture.jpg",
      "asCharacter": "Fruit Vendor (uncredited)"
    }
  ]
}
```

### GraphQL

Do a Query:

```
{
  movie(title:"The Godfather"){
  	title:fullTitle
    tagline
    contentRating
    keywords:keywordList
    rating:imDbRating
    image
    year
    castMembers{
      mainActors(limit:3){
        name
        image
        asCharacter
      }
    }
  }
}
```

Results:

```
{
  "data": {
    "movie": {
      "title": "The Godfather (1972)",
      "tagline": "An offer you can't refuse.",
      "contentRating": "R",
      "keywords": [
        "mafia",
        "patriarch",
        "crime family",
        "organized crime",
        "gambling syndicate"
      ],
      "rating": 9.2,
      "image": "https://imdb-api.com/images/original/MV5BM2MyNjYxNmUtYTAwNi00MTYxLWJmNWYtYzZlODY3ZTk3OTFlXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_Ratio0.6751_AL_.jpg",
      "year": 1972,
      "castMembers": {
        "mainActors": [
          {
            "name": "Marlon Brando",
            "image": "https://imdb-api.com/images/original/MV5BMTg3MDYyMDE5OF5BMl5BanBnXkFtZTcwNjgyNTEzNA@@._V1_Ratio1.2727_AL_.jpg",
            "asCharacter": "Don Vito Corleone"
          },
          {
            "name": "Al Pacino",
            "image": "https://imdb-api.com/images/original/MV5BMTQzMzg1ODAyNl5BMl5BanBnXkFtZTYwMjAxODQ1._V1_Ratio0.7273_AL_.jpg",
            "asCharacter": "Michael"
          },
          {
            "name": "James Caan",
            "image": "https://imdb-api.com/images/original/MV5BMTI5NjkyNDQ3NV5BMl5BanBnXkFtZTcwNjY5NTQ0Mw@@._V1_Ratio0.7273_AL_.jpg",
            "asCharacter": "Sonny"
          }
        ]
      }
    }
  }
}
```

Map support

```
{
  movie(title:"The Godfather"){
    id
  	title:fullTitle
    tagline
    contentRating
    keywords:keywordList
    rating:imDbRating
    image
    year
    castMembers{
      mainActors(limit:3){
        id
        name
        image
        asCharacter
      }
    }
    ratings(key:rottenTomatoes){
      rottenTomatoes:value
    }
  }
}
```

```
{
  "data": {
    "movie": {
      "id": "tt0068646",
      "title": "The Godfather (1972)",
      "tagline": "An offer you can't refuse.",
      "contentRating": "R",
      "keywords": [
        "mafia",
        "patriarch",
        "crime family",
        "organized crime",
        "gambling syndicate"
      ],
      "rating": 9.2,
      "image": "https://imdb-api.com/images/original/MV5BM2MyNjYxNmUtYTAwNi00MTYxLWJmNWYtYzZlODY3ZTk3OTFlXkEyXkFqcGdeQXVyNzkwMjQ5NzM@._V1_Ratio0.6751_AL_.jpg",
      "year": 1972,
      "castMembers": {
        "mainActors": [
          {
            "id": "nm0000008",
            "name": "Marlon Brando",
            "image": "https://imdb-api.com/images/original/MV5BMTg3MDYyMDE5OF5BMl5BanBnXkFtZTcwNjgyNTEzNA@@._V1_Ratio1.2727_AL_.jpg",
            "asCharacter": "Don Vito Corleone"
          },
          {
            "id": "nm0000199",
            "name": "Al Pacino",
            "image": "https://imdb-api.com/images/original/MV5BMTQzMzg1ODAyNl5BMl5BanBnXkFtZTYwMjAxODQ1._V1_Ratio0.7273_AL_.jpg",
            "asCharacter": "Michael"
          },
          {
            "id": "nm0001001",
            "name": "James Caan",
            "image": "https://imdb-api.com/images/original/MV5BMTI5NjkyNDQ3NV5BMl5BanBnXkFtZTcwNjY5NTQ0Mw@@._V1_Ratio0.7273_AL_.jpg",
            "asCharacter": "Sonny"
          }
        ]
      },
      "ratings": [
        {
          "rottenTomatoes": 97
        }
      ]
    }
  }
}
```

Mutation

```
mutation rate {
  rate(id:"tt0068646",rating:9.5){
    key
    value
  }
}
```

```
{
  "data": {
    "rate": [
      {
        "key": "imDb",
        "value": 9.2
      },
      {
        "key": "theMovieDb",
        "value": 8.7
      },
      {
        "key": "metacritic",
        "value": 100
      },
      {
        "key": "blockbuster",
        "value": 9.5
      },
      {
        "key": "rottenTomatoes",
        "value": 97
      },
      {
        "key": "filmAffinity",
        "value": 9
      }
    ]
  }
}
```

Security

```
mutation rate {
  rate(id:"tt0068646",rating:9.5){
    key
    value
  }
}
```

Subscription

```
subscription ratingChanged {
  listenForRateChanges{
    rating
  }
}
```

Non-Blocking

```
{
  movie(title:"The Godfather"){
    id
  	title:fullTitle
    reviews {
      review{
        title
        content
      }
    }
  }
}
```

In the log file:

```
>>>>>>> MOVIE :vert.x-worker-thread-0
>>>>>>> REVIEW :vert.x-eventloop-thread-2

```