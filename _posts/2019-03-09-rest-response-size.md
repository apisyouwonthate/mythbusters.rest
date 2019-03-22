---
layout: post
title:  "Myth: REST Responses Sizes are massive!"
date:   2019-03-04 19:08:05 +0000
categories: jekyll update
---

One of the biggest complaints people have about REST is that the response size is too big. In reality though, that is not a REST problem, that is a problem with the developers maintaining that endpoint. Let's look at some reasons why and how we can mitigate it. 

## Sending too much data

Thoughtfully developing an API endpoint requires some thought into what data is or is not being sent over the wire. While it takes little effort to add a new field to your response object, it does take some thought into _if_ the field should be added in the first place. One of the best ways to mitigate this is by embracing Hypermedia with your APIS. Lets use an example of a users response object before we add Hypermedia. 

```json
{
  "data": [
    {
      "type": "User",
      "id": 1,
      "attributes": {
        "userId": "11122",
        "name": "Crashy McCrashface",
        "position": "Lead Bike Engineer",
        "yearsAtPosition": 2,
        "previousPosition": "Bike Engineer",
        "managerId": "10109"
      }
    },
    {
      "type": "User",
      "id": 2,
      "attributes": {
        "userId": "11123",
        "name": "Turtle McTurtleface",
        "position": "Lead Swamp Designer",
        "yearsAtPosition": 5,
        "previousPosition": "Junior Swamp Designer",
        "managerId": "10002"
      }
    }
  ];
}
```

Looking at the data above, there is so much included that doesnt need to be in a ```HTTP/2 GET /users``` request. Lets simplify the whole thing. 

```json
{
  "data": [
    {
      "type": "User",
      "id": 1,
      "attributes": {
        "userId": "11122",
        "name": "Crashy McCrashface"
      },
      "relationships": {
        "user": {
          "links": {
            "self": "https://apisyouwonthate.com/api/users/11122/relationships/user",
            "related": "https://apisyouwonthate.com/api/users/11122",
          },
          "data": {
            "type": "User",
            "id": "11122",
          }
        } 
      }
    },
    {
      "type": "User",
      "id": 2,
      "attributes": {
        "userId": "11123",
        "name": "Turtle McTurtleface"
      },
      "relationships": {
        "user": {
          "links": {
            "self": "https://apisyouwonthate.com/api/users/11123/relationships/user",
            "related": "https://apisyouwonthate.com/api/users/11123",
          },
          "data": {
            "type": "User",
            "id": "11123",
          }
        } 
      }
    }
  ];
}
```

While this has more structure to the request, the data being sent back has been cut down and we give the client user instructions to where to find the data they may want next. This is called "discoverability". Now, if we request ```HTTP/2 GET /users/11123``` we would want to return something similar to the first example, like so: 

```json
{
  "data": [
    {
      "type": "User",
      "id": 1,
      "attributes": {
        "userId": "11122",
        "name": "Crashy McCrashface",
        "position": "Lead Bike Engineer",
        "yearsAtPosition": 2,
        "previousPosition": "Bike Engineer",
        "managerId": "10109"
      }
    }
  ];
}
```.

### Wrongly modeled data. 

In conjunction with the above, another reason people complain about REST response sizes being so large is that developers have not modeled the data for the requests. Lets consider the example above. In it, we have two requests we are making, ```/api/users``` and ```/api/users/11122```. In the first request, we should return the least amount of data possible. When making the first GET request, which returns all the resources for the given endpoint, model your data to return the bare minimum. In this case, a userId and a name. 

The idea here is instead of racing to code, take a step back and see what data is truly needed for the endpoint. If you have a users page, an organization chart let's just say, is it useful to have data surrounding their time at the company? Or maybe previous titles? That data is not useful in this case, so instead lets model our data to only return the following:

```json
{
  "data": [
    {
      "type": "User",
      "id": 1,
      "attributes": {
        "userId": "11122",
        "name": "Crashy McCrashface",
        "position": "Lead Bike Engineer",
        "manager": "Stowford Turtle"
      }
    }
  ];
}
```

And that's all you need! Along with hypermedia, the other data is close by but now our response is more concise and easier to use. 