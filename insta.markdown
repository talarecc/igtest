[x] image du post
[ ] nombre de like
[x] lien du poste
[x] createur
[ ] pouvoir associer à un ou plisuers produits

# Liens utiles
- https://developers.facebook.com/
- https://developers.facebook.com/docs/instagram-basic-display-api/getting-started


# Authentication (dans un navigateur)
https://api.instagram.com/oauth/authorize?client_id=263923504637698&redirect_uri=https://talarecc.github.io/igtest/&scope=user_profile,user_media&response_type=code

- **url de test** : https://talarecc.github.io/igtest/
- **ID** : 263923504637698
- **secret** : f3f7309ed75d069c7e7a20ba583496b9

## result
- **code** : AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw


# Echanger code contre access token (POST) : 
curl -X POST \ https://api.instagram.com/oauth/access_token \ -F client_id=684477648739411 \ -F client_secret=eb8c7... \ -F grant_type=authorization_code \ -F redirect_uri=https://socialsizzle.herokuapp.com/auth/ \ -F code=AQDp3TtBQQ...

- **client_id** : 263923504637698
- **client_secret** : f3f7309ed75d069c7e7a20ba583496b9
- **grant_type** : authorization_code
- **redirect_uri** : https://talarecc.github.io/igtest/
- **code** : AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw

## result : 
```
{
    "access_token": "IGQVJWY0xWSlJVWlNCWXRpVUxYMzV1QVZAlVnA2TkJOM0NBdUZARYWhCTktJM0Q4VDF6SlAwWDhVLU9iS21mbS00dFlVUTFzTGg2LUhmV3hIVk5tU1F0cHZAwSlFRN3FqY285RzlzaTNiZAGRrVFVBcTdBbjFXaUNsNmNmZAzhV",
    "user_id": 17841429603614101
}
```

# Echanger token contre un long lived access token
curl -i -X GET "https://graph.instagram.com/access_token?grant_type=ig_exchange_token&client_secret={instagram-app-secret}&access_token={short-lived-access-token}"

- **grant_type** : ig_exchange_token
- **client_secret** : f3f7309ed75d069c7e7a20ba583496b9
- **access_token** : IGQVJWY0xWSlJVWlNCWXRpVUxYMzV1QVZAlVnA2TkJOM0NBdUZARYWhCTktJM0Q4VDF6SlAwWDhVLU9iS21mbS00dFlVUTFzTGg2LUhmV3hIVk5tU1F0cHZAwSlFRN3FqY285RzlzaTNiZAGRrVFVBcTdBbjFXaUNsNmNmZAzhV

## result 
```
{
    "access_token": "IGQVJXUm9BMDViUzVJallGbmR1VmJIT1c3S0FCcDlrLURUcnhqT2FTUXJyWWg3R2lleU5KMHM0WHRCT05EOGZAiQlluT2JmSVZAoZAzRWcVVFOGlRRWNVeWVESjByamRhNUs1cHk4bE5R",
    "token_type": "bearer",
    "expires_in": 5184000
}
```

# Refresh a long-lived token
curl -i -X GET "https://graph.instagram.com/refresh_access_token?grant_type=ig_refresh_token&access_token={long-lived-access-token}"

- **grant_type** : ig_refresh_token
- **access_token** : IGQVJXUm9BMDViUzVJallGbmR1VmJIT1c3S0FCcDlrLURUcnhqT2FTUXJyWWg3R2lleU5KMHM0WHRCT05EOGZAiQlluT2JmSVZAoZAzRWcVVFOGlRRWNVeWVESjByamRhNUs1cHk4bE5R

## result 
```
{
  "access_token":"{long-lived-user-access-token}",
  "token_type": "bearer",
  "expires_in": 5183944 // Number of seconds until token expires
}
```

# Url d'interrogation du noeud utilisateur (GET) : 
curl -X GET \ 'https://graph.instagram.com/{user-id}?fields=id,username,media_count&access_token={access-token}'
curl -X GET \ 'https://graph.instagram.com/17841429603614101?fields=id,username,media_count&access_token=AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw'

## result :
```
{
    "id": "17841429603614101",
    "username": "rark_twitch",
    "media_count": 5
}
```

# Get media id (GET) :
http://api.instagram.com/oembed?url=http://instagram.com/p/B-XMwrFIVnc/

- **url** : lien du post instagram

## result : 
```
{
    "version": "1.0",
    "title": "PB APRÈS PB, WR APRÈS WR. 🏅",
    "author_name": "rark_twitch",
    "author_url": "https://www.instagram.com/rark_twitch",
    "author_id": 29552810787,
    "media_id": "2276344258009061852_29552810787",
    "provider_name": "Instagram",
    "provider_url": "https://www.instagram.com",
    "type": "rich",
    "width": 658,
    "height": null,
    "html": "html",
    "thumbnail_url": "https://instagram.fcdg1-1.fna.fbcdn.net/v/t51.2885-15/sh0.08/e35/s640x640/91473080_870207096752692_5577804207658831461_n.jpg?_nc_ht=instagram.fcdg1-1.fna.fbcdn.net&_nc_cat=104&_nc_ohc=wnHnGqcA7rkAX_ouNXm&oh=25e514b785d5e8a445acf8a1dd82f80b&oe=5EB65F91",
    "thumbnail_width": 640,
    "thumbnail_height": 640
}
```

# Url d'interrogation de media (GET) : 
curl -X GET \ 'https://graph.instagram.com/{media-id}?fields={fields}&access_token={access-token}}'
curl -X GET \ 'https://graph.instagram.com/2276344258009061852_29552810787?fields=id,media_type,media_url,username,timestamp&access_token=AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw'
curl -X GET \ 'https://graph.facebook.com/2276344258009061852_29552810787?fields=id,media_type,media_url,username,timestamp&access_token=AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw'
curl -X GET \ 'https://graph.instagram.com/2276344258009061852_29552810787?fields=id,media_type,media_url,username,timestamp&access_token=AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw'


 "https://graph.facebook.com/v3.2/2276344258009061852_29552810787?fields=username&access_token=AQAfvACPkBX6xoppB-3lFXsoBHNbvLjQfIl0pXzXR2UZoCIdsk6VK8QHpLEOluwj8Oeu054Gd0-sE9uXRhKsDODxw0Fu_SC8K7sgxOEo9Vzm3wqhp5LSnOtgXWMReuGacuJ4V2_r7gsyZykqVIosoe8AEPNrEeoc9Wgm2o9gRwRYw5H01kBLSKoTHJqq6Zgc-P7SrqNLP78sFqOWL1DAPko_f832JwUSL_fsL_jZ4td-Bw"



# Get all media (GET)
https://graph.instagram.com/me/media?fields=id,media_type,media_url,username,timestamp&access_token=IGQVJWY0xWSlJVWlNCWXRpVUxYMzV1QVZAlVnA2TkJOM0NBdUZARYWhCTktJM0Q4VDF6SlAwWDhVLU9iS21mbS00dFlVUTFzTGg2LUhmV3hIVk5tU1F0cHZAwSlFRN3FqY285RzlzaTNiZAGRrVFVBcTdBbjFXaUNsNmNmZAzhV

- **fields** : id,mediatype,media_url,username,timestamp
- **access_token** : IGQVJWY0xWSlJVWlNCWXRpVUxYMzV1QVZAlVnA2TkJOM0NBdUZARYWhCTktJM0Q4VDF6SlAwWDhVLU9iS21mbS00dFlVUTFzTGg2LUhmV3hIVk5tU1F0cHZAwSlFRN3FqY285RzlzaTNiZAGRrVFVBcTdBbjFXaUNsNmNmZAzhV

## result
```
{
    "data": [
        {
            "id": "17859819646794796",
            "media_type": "IMAGE",
            "media_url": "https://scontent.fcdg1-1.fna.fbcdn.net/v/t51.2885-15/91473080_870207096752692_5577804207658831461_n.jpg?_nc_cat=109&_nc_sid=8ae9d6&_nc_oc=AQmL62Oyq2-RUYWxoOUAqU2YiHuX3EqG3N76m1MGpCf-regCOI_T5A10WBRYch8qUE8&_nc_ht=scontent.fcdg1-1.fna&oh=4b0e60826ce4c6debe0508b017015b77&oe=5EB24309",
            "username": "rark_twitch",
            "timestamp": "2020-03-30T15:16:43+0000"
        },
        {
            "id": "17852971849811878",
            "media_type": "IMAGE",
            "media_url": "https://scontent.fcdg1-1.fna.fbcdn.net/v/t51.2885-15/84256140_2227551500874046_5747565521381721533_n.jpg?_nc_cat=100&_nc_sid=8ae9d6&_nc_oc=AQnh9LcTU-s4PVSZVZ018p6LOxXCBRQiOYfmPw6YZI_SnVeMXu6ANBj_1azMH8uq9NM&_nc_ht=scontent.fcdg1-1.fna&oh=a87307df4de4095f668296a4cf0c813e&oe=5EB24FBA",
            "username": "rark_twitch",
            "timestamp": "2020-02-05T07:52:56+0000"
        }
    ],
    "paging": {
        "cursors": {
            "before": "QVFIUmZA4WnNUOXU3R0xWbU5RU0VuQklVUENwWnNrYmhzSlFNM2lnX1Etb3o3alRLYkt2QXc4N2YxWi0zUzg1MDNkdm13YnVaaEF5WGY2ZAGRMWW1qcHNFa1hR",
            "after": "QVFIUl9veTlIdjhWUng5djExQXVzZAW1iaWZA1ZAnBpa2o4bjdMT2txa2lDR3JYN0FPbHF1QTJsOHhtdnk4X3NmVDBvNE13TlBndE5BQ2VzU1pGMS1kdGhLeXN3"
        }
    }
}  
```