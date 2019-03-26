+++
date = "2011-12-01T13:16:52-04:00"
title = "How to Make Foursquare your Bitch"
author = "Jessica Frazelle"
description = "I would just like to preface this by saying I do not condone cheating but I thought of this as a 'challenge' and not so much as cheating."
aliases = [
    "/posts/how-to-make-foursquare-your-bitch.html"
]
+++


I would just like to preface this by saying I do not condone cheating but I thought of this as a "challenge" and not so much as "cheating".


A project I am working on required me to checkin to places on foursquare that I was not currently near (or even close to). Now the answer to this was pretty simple. Checkin through the API using the lat and long of the venue I was "supposedly" at. Boom. Worked without a flaw. Ok I will admit it I am kinda a competitive person and well, the foursquare badges are so pretty I immediately started thinking about how I could check in remotely and collect them all. But surely, surely foursquare must have some sort of catches in place that do not allow this. Because I was ever so curious to find out what they may be (&#8230;and how to get around them) I decided to try.<!--more-->



## Authentication

Let's start with the auth. If a user has not authed your application or is not currently logged into foursquare (assuming you created an app in the <a href="https://developer.foursquare.com/" target="_blank">foursquare for developers dashboard</a>) redirect them as follows.

```php
$clientId = "YOUR-CLIENT-ID";
$redirectUri = "YOUR-REDIRECT-URI";
header("Location:https://foursquare.com/oauth2/authenticate?client_id=" . $clientId ."&response_type=code&redirect_uri=" . $redirectUri);
```

After authenticating, grab the authentication code foursquare redirected the user with.

```php
$code = $_REQUEST['code'];
```

Now start a session and save your access token to it. This way we can easily see if the user is an authenticated app user by checking the session variable. You could also save it as a cookie if you want it to last longer.

```php
session_start();

if (!isset($_SESSION['access_token'])) {
   $app_token_url = "https://foursquare.com/oauth2/access_token?client_id=" . $client_id . "&amp;client_secret=" . $client_secret . "&amp;grant_type=authorization_code&amp;redirect_uri=" . $redirect_uri . "&amp;code=" . $code;

   $ch = curl_init();
   curl_setopt($ch, CURLOPT_URL, $app_token_url);
   curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
   $foursquare_token = curl_exec($ch);
   curl_close($ch);

   $array_token              = json_decode($foursquare_token, true);
   $token                    = $array_token['access_token'];
   $_SESSION['access_token'] = $token;
}
```


## Get Location Data

Ok now you have your token and we can get into the fun part, winning at foursquare! To check into a venue you need to post the following parameters to foursquare: `venueId`, `ll` (latitude, longitude), `llAcc` (accuracy of previous points), `oauth_token`, and `v` (version, which foursquare takes in as todays date in the form "Ymd").


So to make checking into various different venues easier I decided the only thing I want to pass to this function is the venueId, v, and oauth_token. This requires making a function to return the lat and long of the venue from the foursquare api.

```php
function getLatLong($venue_id, $v, $oauth_token) {
   $venue_url = 'https://api.foursquare.com/v2/venues/' . $venue_id . '?oauth_token=' . $oauth_token . '&v=' . $v;

   $response       = file_get_contents($venue_url);
   $venue          = json_decode($response, true);
   $venue_response = $venue['response'];
   $location       = $venue_response['venue']['location'];
   $lat            = $location['lat'];
   $long           = $location['lng'];

   return $lat . ', ' . $long;
}
```


## Checkin

Now we can send this value into the checkin function.

```php
function checkin($venue_id, $v, $oauth_token, $latlong) {
   $checkin_url = "https://api.foursquare.com/v2/checkins/add";

   parameters = array(
       'venueId' => $venue_id,
       'broadcast' => 'private', //now i set this private, but can be public
       'll' => $latlong,
       'llAcc' => '1',
       'oauth_token' => $oauth_token,
       'v' => $v
   );

   $curl = curl_init($checkin_url);
   curl_setopt($curl, CURLOPT_POST, true);
   curl_setopt($curl, CURLOPT_POSTFIELDS, $parameters);
   curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);
   $response = curl_exec($curl);

   return $response;
}
```


## Response

The response from this will be in the following format.

```json
{
    meta: {
        code: 200
    },
    notifications: [
        {
            type: "notificationTray",
            item: {
                unreadCount: 0
            }
        }
    ],
    response: {
        checkin: {
            id: "4d627f6814963704dc28ff94",
            createdAt: 1298300776,
            type: "checkin",
            shout: "Another one of these days. #snow",
            timeZoneOffset: -300,
            user: {
                id: "32",
                firstName: "Dens",
                photo: {
                    prefix: "https://irs0.4sqi.net/img/user/",
                    suffix: "/32_1239135232.jpg",

                },

            },
            venue: {
                id: "408c5100f964a520c6f21ee3",
                name: "Tompkins Square Park",
                contact: {
                    phone: "2123877685",
                    formattedPhone: "(212) 387-7685",

                },
                location: {
                    address: "E 7th St. to E 10th St.",
                    crossStreet: "btwn Ave. A &amp; B",
                    lat: 40.72651075083395,
                    lng: -73.98171901702881,
                    postalCode: "10009",
                    city: "New York",
                    state: "NY",
                    country: "United States",
                    cc: "US",

                },
                categories: [
                    {
                        id: "4bf58dd8d48988d163941735",
                        name: "Park",
                        pluralName: "Parks",
                        shortName: "Park",
                        icon: {
                            prefix: "https://foursquare.com/img/categories_v2/parks_outdoors/park_",
                            suffix: ".png",

                        },
                        primary: true,

                    },

                ],
                verified: true,
                stats: {
                    checkinsCount: 25523,
                    usersCount: 8932,
                    tipCount: 85,

                },
                url: "http://www.nycgovparks.org/parks/tompkinssquarepark",
                likes: {
                    count: 0,
                    groups: [

                    ],

                },
                specials: {
                    count: 0,

                },

            },
            source: {
                name: "foursquare for Web",
                url: "https://foursquare.com/"
            },
            photos: {
                count: 1,
                items: [
                    {
                        id: "4d627f80d47328fd96bf3448",
                        createdAt: 1298300800,
                        prefix: "https://irs3.4sqi.net/img/general/",
                        suffix: "/UBTEFRRMLYOHHX4RWHFTGQKSDMY14A1JLHURUTG5VUJ02KQ0.jpg",
                        width: 720,
                        height: 540,
                        user: {
                            id: "32",
                            firstName: "Dens",
                            photo: {
                                prefix: "https://irs0.4sqi.net/img/user/",
                                suffix: "/32_1239135232.jpg",

                            },

                        },
                        visibility: "priviate"
                    }
                ],

            },
            likes: {
                count: 0,
                groups: [

                ],

            },
            like: false,
            score: {
                total: 1,
                scores: [
                    {
                        points: 1,
                        icon: "https://foursquare.com/img/points/defaultpointsicon2.png",
                        message: "Have fun out there!",

                    },

                ],

            },

        },

    },

}
```


## Summary

So what I found was this:

- You can check into 15-20 places in a loop without loosing points or disabling the chance to win badges, but then you have to take a break for a few hours
- When changing locations over a vast distance (ex. Los Angeles &#8211;> San Francisco), you must wait the amount of time it takes to reasonably cover that distance before checking in or else you will not be able to earn badges.


With these in mind this is how I approached earning as many badges in as little time as possible. Once I was "in" a location area, I looped through a set array of about 15 venues. I made these arrays based off the places most blogs said you needed to win a badge. The expertise badges are easy; checkin to 3 different venues categorized as BBQ Joints, earn the badge. The city badges all have lists in foursquare that house the venues you need to go, hit five and you get the badge.

```php
$windy_city_badge = array(
   '4b876c65f964a520e2be31e3',
   '4b4e0d9ff964a520c0df26e3',
   '4e1e0e65aeb75f77be667547',
   '4e70c1aa814dd2cb962265cb',
   '49dce128f964a520b65f1fe3'
);
```

I would recommend conquering the city badges first because you will probably earn all the expertise badges in the process.


Go get &#8216;em! Haters gonna hate, but you just made foursquare yo biotch.
