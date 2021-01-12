# Match Service

Spring boot microservice designed to maintain and modify information about ten man matches

## Dependencies
---
* Spring Boot
* Spring Boot Web
* Spring Data MongoDb
* Lombok

## Additional Technologies Used
---
* Docker

## Data Model
---
| Property              | Data Type                     | Description                                                                                                                  | Hashed? |
| --------------------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------- |
| id                    | Long                          | Unique match identified                                                                                                      | false   |
| game                  | String                        | Game played in the match                                                                                                     | false   |
| format                | Int/String                    | Format of the match (bo1, bo3, bo5)                                                                                          | false   |
| state*                 | String                        | Current state of the match                                                                                                   | false   |
| participants*         | Map<Long, Int>                | Map of player ids and their respective teams                                                                                 | false   |
| stages                | Map<String, Map<String, Int>> | Map of stages played in the match, whith the value being metadata for which team selected the map and which team won the map | false   |
| player pick sequence  | String                        | Sequence for which players are picked by team captains                                                                       | false   |
| map pick ban sequence | String                        | Sequence for which maps are picked and banned by team captains                                                               | false   |
| date started | String | Timestamp representing when the match was started | false |

\* - Probably works better as a number (enum)

## Request Mapping
---
> /matches
> 
## Endpoints
---
> **GET** /matches/{id}

Returns match data for the match with the specified id

Example:
```
/matches/1512
{
    "id": 1512,
    "game": "CSGO",
    "format": "bo3",
    "state": "completed",
    "participants": {
        "1543": 0,
        "5123": 1,
        "1235": 1,
        "6123": 0, 
        "1761": 0,
        "1714": 3,
        "8171": 0,
        "7354": 1,
        "2142": 2,
        "7242": 1,
    },
    "stages": {
        "overpass": 1,
        "vertigo": 0,
        "mirage": 0
    }
    "player_pick_sequence": "0110101010",
    "map_pick_ban_sequence": "0x1x0p1p0x1x",
    "date_started": 1610426519000
}
```