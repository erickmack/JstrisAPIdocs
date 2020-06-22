# Introduction

Welcome to the Jstris API! You can use our API to retrieve Leaderboards or specific user's data like live games, sprint time, survival pb, and more.

# Leaderboards

This endpoint retrieves Jstris Sprint, Cheese, Survival, and Ultra leaderboards (20TSD and PC Mode not currently supported)

## HTTP Request

`GET http://jstris.jezevec10.com/api/leaderboard/<game>?mode=<mode>`

## Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
game | none | What game's leaderboard you want to retrieve: `1 = sprint, 3 = cheese, 4 = survival, 5 = ultra`
mode | none | Game mode to retrieve, for games that have more than 1 mode like Sprint and Cheese,`1 = 40L/10L, 2 = 20L/18L, 3 = 100L, 4 = 1000L` for any other game, mode should be 1   
offset | 0 | Offset of the games retrieved, this endpoint sends 500 users at a time to see the next 500 users you add `offset=500` in your next API request

<!-- tabs:start -->
#### ** JavaScript **
```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://jstris.jezevec10.com/api/leaderboard/1?mode=1&offset=0", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
#### ** Python **
```python
import requests

url = "https://jstris.jezevec10.com/api/leaderboard/1?mode=1&offset=0"

payload = {}
headers= {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
<!-- tabs:end -->


> The above command returns JSON structured like this:

```json
[
    {
        "id": 16008204,
        "pos": 1,
        "game": 15.654,
        "ts": "2020-05-27 10:25:10",
        "name": "Vince_HD"
    },
    {
        "id": 640128,
        "pos": 2,
        "game": 16.954,
        "ts": "2018-06-26 04:18:16",
        "name": "MicroBlizz"
    }
]
```
# Maps
This endpoint returns state, name, queue, finish condition, and data of the specified map

## HTTP Request
`GET https://jstris.jezevec10.com/maps/api/<ID>`

## URL Parameters
Parameter | Description
----------|------------
ID | ID of the map you want to retrieve information from

<!-- tabs:start -->
#### ** JavaScript **
```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://jstris.jezevec10.com/maps/api/14079", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
#### ** Python **
```python
import requests

url = "https://jstris.jezevec10.com/maps/api/14079"

payload = {}
headers = {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))

```
<!-- tabs:end -->

> The above command returns JSON structured like this:

```json
{
    "id": 14079,
    "state": 0,
    "name": "skin tests",
    "queue": "OJJILJITLO",
    "finish": 1,
    "data": "AAAAAAAAAAAAABI0VnAIEjRWcAgSNFZwCBI0VnAIEjRWcAgSNFZwCBI0VnAIEjRWcAgSNFZwCBI0VnAIEjRWcAgSNFZwCBI0VnAIEjRWcAgSNFZwCBI0VnAIEjRWcAgSNFZwCA==",
    "boardMD5": "e580ed4ea61836c9"
}
```

# Users

## Live games

This endpoint retrieves a user's last 50 live games.

### HTTP Request

`GET https://jstris.jezevec10.com/api/u/<username>/live/<games>`

### URL Parameters

Parameter | Description
--------- | -----------
username | Username of the player
games | (optional) If omitted the API will return overall statistics from the requested user
offset | If you want to see the next 50 games, increase the offset by 50 in every API request 

<!-- tabs:start -->
#### ** JavaScript **
```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://jstris.jezevec10.com/api/u/FireStorm/live/games?offset=0", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
#### ** Python **
```python
import requests

url = "https://jstris.jezevec10.com/api/u/FireStorm/live/games?offset=0"

payload = {}
headers= {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```
<!-- tabs:end -->


> The above command returns JSON structured like this:

```json
[
    {
        "id": 65123482,
        "gid": "YRPUKA",
        "cid": 29932097,
        "gametime": 147.82,
        "sent": 70,
        "attack": 120,
        "rep": "3",
        "pcs": 145,
        "players": 5,
        "r1v1": 0,
        "pos": 2,
        "vs": "jovili",
        "gtime": "2020-06-17 23:21:12"
    },...
]
```

## Singleplayer

This endpoint returns best and worst time as well as average, sum, total games played, statistical mode and days since last PB. 


### HTTP Request

`GET https://jstris.jezevec10.com/api/u/<username>/records/<game>?mode=<mode>rule=<rule>`

### URL Parameters

Parameter | Description
--------- | -----------
username | Name of the player
game | (number) What game you want `1 = sprint, 3 = cheese, 4 = survival, 5 = ultra, 7 = 20TSD, 8 = PC Mode`
mode | Game mode to retrieve, for games that have more than 1 mode like Sprint and Cheese `1 = 40L/10L, 2 = 20L/18L, 3 = 100L, 4 = 1000L` for any other game, mode should be 1
best | If included the API will return the ID, Gametime, and Timestamp of the user's PB
rule | Game mode rules `MPH` `big` `pentomino` if excluded it will return the default rule

<!-- tabs:start -->
#### ** JavaScript **
```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://jstris.jezevec10.com/api/u/Erickmack/records/1?mode=1&best", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
#### ** Python **
```python
import requests

url = "https://jstris.jezevec10.com/api/u/Erickmack/records/1?mode=1&best"

payload = {}
headers= {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```

<!-- tabs:end -->

> The above command returns JSON structured like this:

```json
{
    "name": "Erickmack",
    "min": 33.19,
    "max": 10795.1,
    "avg": 66.057,
    "sum": 451433.689,
    "games": 6834,
    "mode": {
        "0.1": [
            "55.4-55.5",
            29
        ],
        "1": [
            "56-57",
            196
        ]
    },
    "days": 443
}
```
## Game Data
This endpoint returns gametime, finesse, blocks, and replay of a game. Replay will return false if the replay was not saved.

### HTTP Request
`GET https://jstris.jezevec10.com/api/record/<ID>`

### URL Parameters
Parameter | Description
----------|------------
ID | ID of the game

<!-- tabs:start -->
#### ** JavaScript **
```javascript
var requestOptions = {
  method: 'GET',
  redirect: 'follow'
};

fetch("https://jstris.jezevec10.com/api/record/6245003", requestOptions)
  .then(response => response.text())
  .then(result => console.log(result))
  .catch(error => console.log('error', error));
```
#### ** Python **
```python
import requests

url = "https://jstris.jezevec10.com/api/record/6245003"

payload = {}
headers= {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```

<!-- tabs:end -->

> The above command returns JSON structured like this:

```json
{
    "id": 6245003,
    "gametime": 35.988,
    "finesse": 22,
    "blocks": 102,
    "replay": true
}
```