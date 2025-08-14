(i).One to One Relation
    <!-- (I).  Embedding  -->
      <!-- users collection -->
      {
        "_id":   ObjectId("user1"),
        "name":  "Lakshay",
        "email": "lakshay@example.com",
        "profile": {                                    <!-- Embedded related document inside main document -->
          "age": 28,
          "gender": "male",
          "bio": "Human from earth"
        }
      }
    <!-- (II). Referencing  -->
      <!-- users collection -->
      {
        "_id": ObjectId("user1"),                     
        "name": "Lakshay",
        "email": "lakshay@example.com",
        "profile_id": ObjectId("profile1")                <!-- Use a foreign key reference to another collection -->
      }
      <!-- profiles collection -->
      {
        "_id": ObjectId("profile1"),
        "age": 28,
        "gender": "male",
        "bio": "Human from earth"
      }


(ii).One to Many Relation
    <!-- (I).  Embedding  -->
      <!-- authors collection -->
      {
        "_id": ObjectId("author1"),
        "name": "Lakshay G",
        "books": [                                          <!-- Embedded array of subdocuments in the book field -->
          { "title": "title_01", "year": 1949 },
          { "title": "title_02", "year": 1945 }
        ]
      }
    <!-- (II). Referencing  -->
      <!-- authors collection ("one") -->
      {
        "_id": ObjectId("author1"),                           <!-- "one" document object id -->
        "name": "Lakshay G"
      }
      <!-- books collection ("many") -->
      {
        "_id": ObjectId("book1"),
        "title": "title_01",
        "year": 1949,
        "author_id": ObjectId("author1")                      <!-- Store reference to the "one" document -->
      }
      {
        "_id": ObjectId("book2"),
        "title": "title_02",
        "year": 1945,
        "author_id": ObjectId("author1")                      <!-- Store reference to the "one" document -->
      }