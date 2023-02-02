# MongoDB

<div align="center">
<i>Practice with mongoDB<i>
</div>

## Tasks

**1.** Write a MongoDB query to display all the documents in the collection restaurants.

```js
db.restaurants.find()
```

---

<br>
<br>

**2.** Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine for all the documents in the collection restaurant.

```js
db.restaurants.find({}, {restraunt_id: 1, name: 1, borough: 1, cuisine: true})
```

---

<br>
<br>

**3.** Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine, but exclude the field _id for all the documents in the collection restaurant.
```js
db.restaurants.find({}, {"_id": 0, restraunt_id: 1, name: 1, borough: 1, cuisine: true})
```

---

<br>
<br>

**4.** Write a MongoDB query to display the fields restaurant_id, name, borough and zip code, but exclude the field _id for all the documents in the collection restaurant.
```js
db.restaurants.find({}, {restraunt_id: 1, name: 1, borough: 1, "address.zipcode": 1})
```

---

<br>
<br>

**5.** Write a MongoDB query to display all the restaurant which is in the borough Bronx. 
```js
db.restaurants.find({borough: "Bronx"})
```

---

<br>
<br>

**6.** Write a MongoDB query to display the first 5 restaurant which is in the borough Bronx.
```js
db.restaurants.find({borough: "Bronx"}).limit(5)
```

---

<br>
<br>

**7.** Write a MongoDB query to display the next 5 restaurants after skipping first 5 which are in the borough Bronx. 
```js
db.restaurants.find({"borough": "Bronx"}).skip(5).limit(5)
```

---

<br>
<br>

**8.** Write a MongoDB query to find the restaurants who achieved a score more than 90.
```js
db.restaurants.find({grades : { $elemMatch : {"score" : {$gt : 90}}}})
```

---

<br>
<br>

**9.** Write a MongoDB query to find the restaurants that achieved a score, more than 80 but less than 100. 
```js
db.restaurants.find({grades : {$elemMatch : {score : {$gt : 80, $lt : 100}}}})
```

---

<br>
<br>

**10.** Write a MongoDB query to find the restaurants which locate in latitude value less than -95.754168.
```js
***1st***
db.restaurants.find({"address.coord" : {$lt : -95.754168}})
// check all values in massiv and compare with -95.754168
***2nd***
db.restaurants.find({"address.coord.0" : {$lt : -95.754168}})
// check solely 1st elem of massive due to coord [-180 - 0, 0 - 180] -> no need check 2nd value
```

---

<br>
<br>

**11.** Write a MongoDB query to find the restaurants that do not prepare any cuisine of 'American' and their grade score more than 70 and latitude less than -65.754168. 
```js
db.restaurants.find(
      {$and : 
          [
              {cuisine : {$ne : "American "}},
              {grades : {$elemMatch : {score : {$gt : 70}}}},
              {"address.coord.0" : {$lt : -65.754168}}
          ]
      })
```

---

<br>
<br>

**12.** Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American' and achieved a score more than 70 and located in the longitude less than -65.754168.

***Note : Do this query without using $and operator.***
```js
  db.restaurants.find(
      {
          cuisine : {$ne : "American "},
          grades : {$elemMatch : {score : {$gt : 70}}},
          "address.coord.0" : {$lt : -65.754168}
      })
```

---

<br>
<br>

**13.** Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American' and achieved a grade point 'A' not belongs to the borough Brooklyn. The document must be displayed according to the cuisine in descending order. 
```js
db.restaurants.find(
      {
          cuisine : {$ne : "American "},
          grades : {$elemMatch : {grade : {$eq : "A"}}},
          borough : {$ne : "Brooklyn"}
      })
        .sort({cuisine : -1})
```

---

<br>
<br>

**14.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'Wil' as first three letters for its name. 
```js
db.restaurants.find(
  {
      name : {$regex : /^Wil/}    // or name : /^Wil/ instead of $regex
  }, {
      restaurant_id : 1,
      name : 1,
      borough : 1,
      cuisine : 1
  })
```

---

<br>
<br>

**15.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'ces' as last three letters for its name. 
```js
db.restaurants.find(
  {
      name : {$regex : /ces$/}    // or name : /ces$/ instead of $regex
  }, {
      restaurant_id : 1,
      name : 1,
      borough : 1,
      cuisine : 1
  })
```

---

<br>
<br>

**16.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'Reg' as three letters somewhere in its name.
```js
db.restaurants.find({
          name: {$regex: /.*Reg.*/}
      }, {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
```

---

<br>
<br>

**17.** Write a MongoDB query to find the restaurants which belong to the borough Bronx and prepared either American or Chinese dish. 
```js
//1st
db.restaurants.find({
          borough : {$eq : "Bronx"},
          cuisine : {$in : ["American ", "Chinese"]}
      }, {
          name: 1,
          borough: 1,
          cuisine: 1
      })
      
//2nd
db.restaurants.find({
          borough: {$eq: "Bronx"},
          $or : [
              {cuisine: "American "},
              {cuisine: "Chinese"}
              ]
      }, {
          name: 1,
          borough: 1,
          cuisine: 1
      })
```

---

<br>
<br>

**18.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which belong to the borough Staten Island or Queens or Bronxor Brooklyn.
```js
db.restaurants.find({
      borough: {$in : 
          [
              "Staten Island",
              "Queens",
              "Bronx",
              "Brooklyn"
          ]}
      }, {
          restaurant_id: 1,
          name: 1,
          borough: 1, 
          cuisine: 1
      })
```

---

<br>
<br>

**19.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which are not belonging to the borough Staten Island or Queens or Bronxor Brooklyn. 
```js
db.restaurants.find({
      borough: {$nin: 
          [
              "Staten Island",
              "Queens",
              "Bronx",
              "Brooklyn"
          ]}
      }, {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
```

---

<br>
<br>

**20.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which achieved a score which is not more than 10. (?)
```js
      
//incorrect      
db.restaurants.find({
      grades: {$elemMatch:     // or grades: {$elemMatch : {score : {$not : {$gt : 10}}}}
          {score :
              {$lte : 10}
          }
      }}, 
      {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
      
//or
      
// incorrect      
db.restaurants.find({
      "grades.score" : {$lte : 10}},          // or "grades.score" : {$not : {$gt : 10}}
      {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
      
//CORRECT ANSWER
db.restaurants.find({
      "grades.score" : {$not :
          {$gt: 10}}
      }, {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
```

---

<br>
<br>

**21.** Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which prepared dish except 'American' and 'Chinees' or restaurant's name begins with letter 'Wil'. (?)
```js
db.restaurants.find({
      $or: [
              {name: {$regex: /^Wil/}},
              {$and: [
                  {cuisine: {$ne: "American "}},
                  {cuisine: {$ne: "Chinise"}}
                  ]
              }
           ]
      }, {
          restaurant_id: 1,
          name: 1,
          borough: 1,
          cuisine: 1
      })
      
// Doesn't word -?      
db.restaurants.find($or: [
  {name: {$regex: /^Wil/}},
  {cuisine: {$nin: ["American ", "Chinise"]}}
  ])
      
```

---

<br>
<br>

**22.** Write a MongoDB query to find the restaurant Id, name, and grades for those restaurants which achieved a grade of "A" and scored 11 on an ISODate "2014-08-11T00:00:00Z" among many of survey dates.. 
```js
db.restaurants.find({
      $and: [
              {"grades.grade": {$eq: "A"}},
              {"grades.score": {$eq: 11}},
              {"grades.date": {$eq: ISODate("2014-08-11T00:00:00Z")}}
            ]
      }, {
          restaurant_id: 1,
          name: 1,
          grades: 1
      })
```

---

<br>
<br>

**23.** Write a MongoDB query to find the restaurant Id, name and grades for those restaurants where the 2nd element of grades array contains a grade of "A" and score 9 on an ISODate "2014-08-11T00:00:00Z". 
```js
db.restaurants.find({
  "grades.1.grade": {$eq: "A"},
  "grades.1.score" : {$eq: 9},
  "grades.1.date": {$eq: ISODate("2014-08-11T00:00:00Z")}
}, {
  restaurant_id: 1,
  name: 1,
  gardes: 1
})
```

---

<br>
<br>

**24.** Write a MongoDB query to find the restaurant Id, name, address and geographical location for those restaurants where 2nd element of coord array contains a value which is more than 42 and upto 52.. 
```js
db.restaurants.find({
  $and: [
    {"address.coord.1": {$gt: 42}},     // or "address.coord.1": {$gt: 42, $lte: 52}
    {"address.coord.1": {$lte: 52}}
    ]
}, {
  restaurant_id: 1,
  name: 1,
  "address.street": 1,
  "address.coord": 1
})
```

---

<br>
<br>

**25.** Write a MongoDB query to arrange the name of the restaurants in ascending order along with all the columns. 
```js
db.restaurants.find().sort({"name": 1});     
```

---

<br>
<br>

**26.** Write a MongoDB query to arrange the name of the restaurants in descending along with all the columns.
```js
db.restaurants.find().sort({"name": -1});     
```

---

<br>
<br>

**27.** Write a MongoDB query to arranged the name of the cuisine in ascending order and for that same cuisine borough should be in descending order. 
```js
db.restaurants.find().sort({
  cuisine: 1,
  borough: -1
})
```

---

<br>
<br>

**28.** Write a MongoDB query to know whether all the addresses contains the street or not. 
```js
db.restaurants.find({
      "address.street": {$exists: 1}
      })
```

---

<br>
<br>

**29.** Write a MongoDB query which will select all documents in the restaurants collection where the coord field value is Double.
```js
db.restaurants.find({
      "address.coord": {$type: "double"}
      })
```

---

<br>
<br>

**30.** Write a MongoDB query which will select the restaurant Id, name and grades for those restaurants which returns 0 as a remainder after dividing the score by 7. 
```js
db.restaurants.find({
  "grades.score": {$mod: [7, 0]}
}, {
  restaurant_id: 1,
  name: 1,
  gardes: 1
})
```

---

<br>
<br>

**31.** Write a MongoDB query to find the restaurant name, borough, longitude and attitude and cuisine for those restaurants which contains 'mon' as three letters somewhere in its name.
```js
db.restaurants.find({
    name : { $regex : ".*mon.*", $options: "i" } 
    }, {
         "name":1,
         "borough":1,
         "address.coord":1,
         "cuisine" :1
    })
```

---

<br>
<br>

**32.** Write a MongoDB query to find the restaurant name, borough, longitude and latitude and cuisine for those restaurants which contain 'Mad' as first three letters of its name.
```js
db.restaurants.find({
      name: { $regex : /^Mad/i, } // the same as $options: "i"
      }, {
         "name":1,
         "borough":1,
         "address.coord":1,
         "cuisine" :1
      })
```

---
