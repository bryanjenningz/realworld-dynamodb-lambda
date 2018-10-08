```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-ja2rbo@email.com",
    "username": "author-ja2rbo",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-ja2rbo@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1qYTJyYm8iLCJpYXQiOjE1MzkwMjMyMTksImV4cCI6MTUzOTE5NjAxOX0.l-dGIBVbIl8GKwo7sovqvsy5GOHMiHnBqflvoofTNm0",
    "username": "author-ja2rbo",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-b4hswf@email.com",
    "username": "authoress-b4hswf",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-b4hswf@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy1iNGhzd2YiLCJpYXQiOjE1MzkwMjMyMTksImV4cCI6MTUzOTE5NjAxOX0.PPuZDgTGUJwR8Bn-H4tTv6k1za5-G5EuTOOWvS_8ZYM",
    "username": "authoress-b4hswf",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-p0qset@email.com",
    "username": "non-author-p0qset",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-p0qset@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3ItcDBxc2V0IiwiaWF0IjoxNTM5MDIzMjE5LCJleHAiOjE1MzkxOTYwMTl9.N0Dq3jMRxUuqIBW9CC4UBrR57-IAHawCSgY1LjH3vJw",
    "username": "non-author-p0qset",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bpjwa9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023219924,
    "updatedAt": 1539023219924,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3thtrh",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023219974,
    "updatedAt": 1539023219974,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-bpjwa9
```
```
200 OK

{
  "article": {
    "createdAt": 1539023219924,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-bpjwa9",
    "updatedAt": 1539023219924,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-3thtrh
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1539023219974,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-3thtrh",
    "updatedAt": 1539023219974,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/9lk8m5
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [9lk8m5]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-3thtrh

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1539023219974,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-3thtrh",
    "updatedAt": 1539023219974,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-3thtrh

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1539023219974,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-3thtrh",
    "updatedAt": 1539023219974,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-3thtrh

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1539023219974,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-3thtrh",
    "updatedAt": 1539023219974,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-3thtrh

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-3thtrh

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-3thtrh

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-3thtrh

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-3thtrh]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-3thtrh

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-ja2rbo]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-bpjwa9/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1539023219924,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-bpjwa9",
    "updatedAt": 1539023219924,
    "favoritedBy": [
      "non-author-p0qset"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-bpjwa9
```
```
200 OK

{
  "article": {
    "createdAt": 1539023219924,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-bpjwa9",
    "updatedAt": 1539023219924,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-bpjwa9/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-bpjwa9_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-bpjwa9_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-bpjwa9/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1539023219924,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-bpjwa9",
    "updatedAt": 1539023219924,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-bpjwa9
```
```
200 OK

{}
```
```
GET /articles/title-bpjwa9
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-bpjwa9]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-3thtrh
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-ja2rbo]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "nm1oqy",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4o7zbw",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221008,
    "updatedAt": 1539023221008,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "nm1oqy",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "j4eeb4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-2zou2v",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221031,
    "updatedAt": 1539023221031,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "j4eeb4",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "s594xj",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mag1xu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221060,
    "updatedAt": 1539023221060,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "s594xj",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "n6j4zk",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title--zdxdop",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221087,
    "updatedAt": 1539023221087,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "n6j4zk",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "18x4ac",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lwk81b",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221111,
    "updatedAt": 1539023221111,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "18x4ac",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "zidz5e",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-b0ym0k",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221138,
    "updatedAt": 1539023221138,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "zidz5e",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "w6ivvx",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ep4dwe",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221166,
    "updatedAt": 1539023221166,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "w6ivvx",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ks2al5",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-tr3kwm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221192,
    "updatedAt": 1539023221192,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ks2al5",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "kgqv5e",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qkmhmv",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221221,
    "updatedAt": 1539023221221,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "kgqv5e",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5kzcrx",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-wurnhy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221246,
    "updatedAt": 1539023221246,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5kzcrx",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c8bzlj",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-s2lygf",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221277,
    "updatedAt": 1539023221277,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c8bzlj",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dpidw5",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-3ao82m",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221301,
    "updatedAt": 1539023221301,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dpidw5",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "f7xjlu",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dao56a",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221323,
    "updatedAt": 1539023221323,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "f7xjlu",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ppv9ms",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7y02ae",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221348,
    "updatedAt": 1539023221348,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ppv9ms",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "l3id20",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4mzyla",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221373,
    "updatedAt": 1539023221373,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "l3id20",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "x10gf8",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-phyl2y",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221399,
    "updatedAt": 1539023221399,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "x10gf8",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "26euyz",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qxr2n1",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221427,
    "updatedAt": 1539023221427,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "26euyz",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "elky7o",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-n6zw2c",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221468,
    "updatedAt": 1539023221468,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "elky7o",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "j6wz",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-oltflb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221494,
    "updatedAt": 1539023221494,
    "author": {
      "username": "authoress-b4hswf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "j6wz",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "rwb873",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gqhvzs",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023221544,
    "updatedAt": 1539023221544,
    "author": {
      "username": "author-ja2rbo",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "rwb873",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rwb873",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221544,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gqhvzs",
      "updatedAt": 1539023221544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j6wz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221494,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oltflb",
      "updatedAt": 1539023221494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "elky7o",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221468,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6zw2c",
      "updatedAt": 1539023221468,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "26euyz",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221427,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qxr2n1",
      "updatedAt": 1539023221427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x10gf8"
      ],
      "createdAt": 1539023221399,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-phyl2y",
      "updatedAt": 1539023221399,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppv9ms",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221348,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7y02ae",
      "updatedAt": 1539023221348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7xjlu",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221323,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dao56a",
      "updatedAt": 1539023221323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dpidw5",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221301,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ao82m",
      "updatedAt": 1539023221301,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c8bzlj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221277,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s2lygf",
      "updatedAt": 1539023221277,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5kzcrx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221246,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wurnhy",
      "updatedAt": 1539023221246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ks2al5",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221192,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tr3kwm",
      "updatedAt": 1539023221192,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w6ivvx"
      ],
      "createdAt": 1539023221166,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ep4dwe",
      "updatedAt": 1539023221166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zidz5e"
      ],
      "createdAt": 1539023221138,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b0ym0k",
      "updatedAt": 1539023221138,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "18x4ac",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221111,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lwk81b",
      "updatedAt": 1539023221111,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n6j4zk",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221087,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--zdxdop",
      "updatedAt": 1539023221087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j4eeb4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221031,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2zou2v",
      "updatedAt": 1539023221031,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nm1oqy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221008,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4o7zbw",
      "updatedAt": 1539023221008,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ks2al5",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221192,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tr3kwm",
      "updatedAt": 1539023221192,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "elky7o",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221468,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6zw2c",
      "updatedAt": 1539023221468,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dpidw5",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221301,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ao82m",
      "updatedAt": 1539023221301,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zidz5e"
      ],
      "createdAt": 1539023221138,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b0ym0k",
      "updatedAt": 1539023221138,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-b4hswf
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "j6wz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221494,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oltflb",
      "updatedAt": 1539023221494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "26euyz",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221427,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qxr2n1",
      "updatedAt": 1539023221427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7xjlu",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221323,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dao56a",
      "updatedAt": 1539023221323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c8bzlj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221277,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s2lygf",
      "updatedAt": 1539023221277,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w6ivvx"
      ],
      "createdAt": 1539023221166,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ep4dwe",
      "updatedAt": 1539023221166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "18x4ac",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221111,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lwk81b",
      "updatedAt": 1539023221111,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nm1oqy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221008,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4o7zbw",
      "updatedAt": 1539023221008,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-p0qset
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-ja2rbo&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rwb873",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221544,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gqhvzs",
      "updatedAt": 1539023221544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "elky7o",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221468,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6zw2c",
      "updatedAt": 1539023221468,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-ja2rbo&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x10gf8"
      ],
      "createdAt": 1539023221399,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-phyl2y",
      "updatedAt": 1539023221399,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppv9ms",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221348,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7y02ae",
      "updatedAt": 1539023221348,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rwb873",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221544,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gqhvzs",
      "updatedAt": 1539023221544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j6wz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221494,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oltflb",
      "updatedAt": 1539023221494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "elky7o",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221468,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6zw2c",
      "updatedAt": 1539023221468,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "26euyz",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221427,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qxr2n1",
      "updatedAt": 1539023221427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x10gf8"
      ],
      "createdAt": 1539023221399,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-phyl2y",
      "updatedAt": 1539023221399,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppv9ms",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221348,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7y02ae",
      "updatedAt": 1539023221348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7xjlu",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221323,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dao56a",
      "updatedAt": 1539023221323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dpidw5",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221301,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ao82m",
      "updatedAt": 1539023221301,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c8bzlj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221277,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s2lygf",
      "updatedAt": 1539023221277,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5kzcrx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221246,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wurnhy",
      "updatedAt": 1539023221246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ks2al5",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221192,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tr3kwm",
      "updatedAt": 1539023221192,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w6ivvx"
      ],
      "createdAt": 1539023221166,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ep4dwe",
      "updatedAt": 1539023221166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zidz5e"
      ],
      "createdAt": 1539023221138,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b0ym0k",
      "updatedAt": 1539023221138,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "18x4ac",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221111,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lwk81b",
      "updatedAt": 1539023221111,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n6j4zk",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221087,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--zdxdop",
      "updatedAt": 1539023221087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j4eeb4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221031,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2zou2v",
      "updatedAt": 1539023221031,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nm1oqy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221008,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4o7zbw",
      "updatedAt": 1539023221008,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-b4hswf/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-b4hswf",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "j6wz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221494,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oltflb",
      "updatedAt": 1539023221494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "26euyz",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221427,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qxr2n1",
      "updatedAt": 1539023221427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7xjlu",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221323,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dao56a",
      "updatedAt": 1539023221323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c8bzlj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221277,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s2lygf",
      "updatedAt": 1539023221277,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w6ivvx"
      ],
      "createdAt": 1539023221166,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ep4dwe",
      "updatedAt": 1539023221166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "18x4ac",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221111,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lwk81b",
      "updatedAt": 1539023221111,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nm1oqy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221008,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4o7zbw",
      "updatedAt": 1539023221008,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-ja2rbo/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-ja2rbo",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "rwb873",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221544,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gqhvzs",
      "updatedAt": 1539023221544,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j6wz",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221494,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oltflb",
      "updatedAt": 1539023221494,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "elky7o",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221468,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6zw2c",
      "updatedAt": 1539023221468,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "26euyz",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221427,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qxr2n1",
      "updatedAt": 1539023221427,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "x10gf8"
      ],
      "createdAt": 1539023221399,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-phyl2y",
      "updatedAt": 1539023221399,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "l3id20",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221373,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mzyla",
      "updatedAt": 1539023221373,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ppv9ms",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221348,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7y02ae",
      "updatedAt": 1539023221348,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f7xjlu",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221323,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dao56a",
      "updatedAt": 1539023221323,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dpidw5",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221301,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-3ao82m",
      "updatedAt": 1539023221301,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c8bzlj",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221277,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-s2lygf",
      "updatedAt": 1539023221277,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5kzcrx",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221246,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-wurnhy",
      "updatedAt": 1539023221246,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kgqv5e",
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221221,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qkmhmv",
      "updatedAt": 1539023221221,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ks2al5",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221192,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-tr3kwm",
      "updatedAt": 1539023221192,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0",
        "w6ivvx"
      ],
      "createdAt": 1539023221166,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ep4dwe",
      "updatedAt": 1539023221166,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2",
        "zidz5e"
      ],
      "createdAt": 1539023221138,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b0ym0k",
      "updatedAt": 1539023221138,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "18x4ac",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221111,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lwk81b",
      "updatedAt": 1539023221111,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n6j4zk",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221087,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title--zdxdop",
      "updatedAt": 1539023221087,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "s594xj",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1539023221060,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mag1xu",
      "updatedAt": 1539023221060,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "j4eeb4",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1539023221031,
      "author": {
        "username": "author-ja2rbo",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-2zou2v",
      "updatedAt": 1539023221031,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "nm1oqy",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1539023221008,
      "author": {
        "username": "authoress-b4hswf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4o7zbw",
      "updatedAt": 1539023221008,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "f7xjlu",
    "tag_12",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "nm1oqy",
    "tag_0",
    "18x4ac",
    "tag_4",
    "tag_mod_3_1",
    "dpidw5",
    "tag_11",
    "tag_mod_2_1",
    "tag_mod_3_2",
    "c8bzlj",
    "tag_10",
    "j4eeb4",
    "tag_1",
    "tag_6",
    "w6ivvx",
    "tag_15",
    "x10gf8",
    "l3id20",
    "tag_14",
    "26euyz",
    "tag_16",
    "ks2al5",
    "tag_7",
    "kgqv5e",
    "tag_8",
    "n6j4zk",
    "tag_3",
    "ppv9ms",
    "tag_13",
    "rwb873",
    "tag_19",
    "5kzcrx",
    "tag_9",
    "s594xj",
    "tag_2",
    "j6wz",
    "tag_18",
    "tag_a",
    "tag_b",
    "elky7o",
    "tag_17",
    "tag_5",
    "zidz5e"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-mlx9r5@email.com",
    "username": "author-mlx9r5",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-mlx9r5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1tbHg5cjUiLCJpYXQiOjE1MzkwMjMyMjIsImV4cCI6MTUzOTE5NjAyMn0.lvOnyeXP12hiNYG23NEPGYm2tz_SNP9Po5ApbA0B9Hg",
    "username": "author-mlx9r5",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-gze77r@email.com",
    "username": "commenter-gze77r",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-gze77r@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1nemU3N3IiLCJpYXQiOjE1MzkwMjMyMjIsImV4cCI6MTUzOTE5NjAyMn0.4uhD1wkJIqNT7UEv73yzSVguM0FyrQHWoawCjYcWNJw",
    "username": "commenter-gze77r",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-n04o14",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1539023222939,
    "updatedAt": 1539023222939,
    "author": {
      "username": "author-mlx9r5",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment gtc2pl"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e0573d21-6545-4a67-9f6c-d166e860b2fe",
    "slug": "title-n04o14",
    "body": "test comment gtc2pl",
    "createdAt": 1539023222976,
    "updatedAt": 1539023222976,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment aovnix"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "db882f19-30f0-4842-bfc3-b2629c7adb30",
    "slug": "title-n04o14",
    "body": "test comment aovnix",
    "createdAt": 1539023223015,
    "updatedAt": 1539023223015,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment fifaso"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "f668123b-b63d-4b4a-a445-ad05fcf4cb95",
    "slug": "title-n04o14",
    "body": "test comment fifaso",
    "createdAt": 1539023223050,
    "updatedAt": 1539023223050,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment mj8xq3"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "20796950-b2b7-4dca-a9f1-a333e3e4abf4",
    "slug": "title-n04o14",
    "body": "test comment mj8xq3",
    "createdAt": 1539023223083,
    "updatedAt": 1539023223083,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment bv9yol"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "72e2965d-60b8-495c-ab13-daa057888833",
    "slug": "title-n04o14",
    "body": "test comment bv9yol",
    "createdAt": 1539023223117,
    "updatedAt": 1539023223117,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment jkngqe"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "31a451ca-ff53-4901-bc2f-6fcb2203f4ed",
    "slug": "title-n04o14",
    "body": "test comment jkngqe",
    "createdAt": 1539023223156,
    "updatedAt": 1539023223156,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment y3z7tp"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "61f93352-783f-47cc-90d1-10a26ccab64a",
    "slug": "title-n04o14",
    "body": "test comment y3z7tp",
    "createdAt": 1539023223192,
    "updatedAt": 1539023223192,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment uwexro"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "58eeadfa-d8fb-41b8-948d-91195d1c7b74",
    "slug": "title-n04o14",
    "body": "test comment uwexro",
    "createdAt": 1539023223230,
    "updatedAt": 1539023223230,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment 611it3"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "711e2a7c-c8d0-4792-bfb5-0f30de2ae599",
    "slug": "title-n04o14",
    "body": "test comment 611it3",
    "createdAt": 1539023223261,
    "updatedAt": 1539023223261,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-n04o14/comments

{
  "comment": {
    "body": "test comment dbvnox"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "5aae724e-3e57-4dd5-9911-0855ae718b62",
    "slug": "title-n04o14",
    "body": "test comment dbvnox",
    "createdAt": 1539023223295,
    "updatedAt": 1539023223295,
    "author": {
      "username": "commenter-gze77r",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-n04o14/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-n04o14/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment n3yved"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-n04o14/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1539023222976,
      "id": "e0573d21-6545-4a67-9f6c-d166e860b2fe",
      "body": "test comment gtc2pl",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023222976
    },
    {
      "createdAt": 1539023223295,
      "id": "5aae724e-3e57-4dd5-9911-0855ae718b62",
      "body": "test comment dbvnox",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223295
    },
    {
      "createdAt": 1539023223261,
      "id": "711e2a7c-c8d0-4792-bfb5-0f30de2ae599",
      "body": "test comment 611it3",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223261
    },
    {
      "createdAt": 1539023223230,
      "id": "58eeadfa-d8fb-41b8-948d-91195d1c7b74",
      "body": "test comment uwexro",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223230
    },
    {
      "createdAt": 1539023223083,
      "id": "20796950-b2b7-4dca-a9f1-a333e3e4abf4",
      "body": "test comment mj8xq3",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223083
    },
    {
      "createdAt": 1539023223050,
      "id": "f668123b-b63d-4b4a-a445-ad05fcf4cb95",
      "body": "test comment fifaso",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223050
    },
    {
      "createdAt": 1539023223117,
      "id": "72e2965d-60b8-495c-ab13-daa057888833",
      "body": "test comment bv9yol",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223117
    },
    {
      "createdAt": 1539023223156,
      "id": "31a451ca-ff53-4901-bc2f-6fcb2203f4ed",
      "body": "test comment jkngqe",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223156
    },
    {
      "createdAt": 1539023223015,
      "id": "db882f19-30f0-4842-bfc3-b2629c7adb30",
      "body": "test comment aovnix",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223015
    },
    {
      "createdAt": 1539023223192,
      "id": "61f93352-783f-47cc-90d1-10a26ccab64a",
      "body": "test comment y3z7tp",
      "slug": "title-n04o14",
      "author": {
        "username": "commenter-gze77r",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1539023223192
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-n04o14/comments/e0573d21-6545-4a67-9f6c-d166e860b2fe
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-n04o14/comments/db882f19-30f0-4842-bfc3-b2629c7adb30
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-gze77r]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-n04o14/comments/db882f19-30f0-4842-bfc3-b2629c7adb30
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-n04o14/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "username": "user1-0.sr5avd6kd2",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU",
    "username": "user1-0.sr5avd6kd2",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "username": "user1-0.sr5avd6kd2",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.sr5avd6kd2]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.sr5avd6kd2@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.sr5avd6kd2@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU",
    "username": "user1-0.sr5avd6kd2",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.aehe6xqiczt",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.aehe6xqiczt]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "password": "0.g5kzo7wposa"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.sr5avd6kd2@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU",
    "username": "user1-0.sr5avd6kd2",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.sr5avd6kd2
```
```
200 OK

{
  "profile": {
    "username": "user1-0.sr5avd6kd2",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.x0h0rwhhn6o
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.x0h0rwhhn6o]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1MzkwMjMyMjMsImV4cCI6MTUzOTE5NjAyM30.gvxEJ0LP3BRV5vgh8jCfWJtWwNnSA3SHGuroXA3R2gw",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.s1yxqole3p",
    "email": "user2-0.s1yxqole3p@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.s1yxqole3p@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuczF5eHFvbGUzcCIsImlhdCI6MTUzOTAyMzIyNCwiZXhwIjoxNTM5MTk2MDI0fQ.WtdbewYCB2a2tA9mAzh04cnBO9I2pbcqMFx7gXtfvFY",
    "username": "user2-0.s1yxqole3p",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.sr5avd6kd2@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.sr5avd6kd2",
    "email": "updated-user1-0.sr5avd6kd2@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.sr5avd6kd2",
    "email": "updated-user1-0.sr5avd6kd2@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.sr5avd6kd2",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.sr5avd6kd2",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuc3I1YXZkNmtkMiIsImlhdCI6MTUzOTAyMzIyMywiZXhwIjoxNTM5MTk2MDIzfQ.1dxfUYqLzbPABHhqzK2b9d_Gn4fW2kbD2A8BK0ih6gU"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.dn3bjknkfr@email.com",
    "username": "user2-0.dn3bjknkfr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.dn3bjknkfr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuZG4zYmprbmtmciIsImlhdCI6MTUzOTAyMzIyNCwiZXhwIjoxNTM5MTk2MDI0fQ.oYe3Y3UbHFCkKBb4ImM1Kl6T9BOjCixPLji6QyTYMTQ",
    "username": "user2-0.dn3bjknkfr",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.dn3bjknkfr@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.dn3bjknkfr@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2018-10-08T18:27:04.378Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
