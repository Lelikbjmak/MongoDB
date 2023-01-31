# MongoDB

<div align="center">
<i>Practice with mongoDB<i>
</div>

## Tasks

1. Write a MongoDB query to display all the documents in the collection restaurants.

```js
db.restaurants.find()
```

2. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine for all the documents in the collection restaurant.

```js
db.restaurants.find({}, {restraunt_id: 1, name: 1, borough: 1, cuisine: true})
```

3. Write a MongoDB query to display the fields restaurant_id, name, borough and cuisine, but exclude the field _id for all the documents in the collection restaurant.
```js
db.restaurants.find({}, {"_id": 0, restraunt_id: 1, name: 1, borough: 1, cuisine: true})
```

4. Write a MongoDB query to display the fields restaurant_id, name, borough and zip code, but exclude the field _id for all the documents in the collection restaurant.
```js
db.restaurants.find({}, {restraunt_id: 1, name: 1, borough: 1, "address.zipcode": 1})
```

5. Write a MongoDB query to display all the restaurant which is in the borough Bronx. 
```js
db.restaurants.find({borough: "Bronx"})
```

6. Write a MongoDB query to display the first 5 restaurant which is in the borough Bronx.
```js
db.restaurants.find({borough: "Bronx"}).limit(5)
```

7. Write a MongoDB query to display the next 5 restaurants after skipping first 5 which are in the borough Bronx. 
```js
db.restaurants.find({"borough": "Bronx"}).skip(5).limit(5)
```

8. Write a MongoDB query to find the restaurants who achieved a score more than 90.
```js
db.restaurants.find({grades : { $elemMatch : {"score" : {$gt : 90}}}})
```

9. Write a MongoDB query to find the restaurants that achieved a score, more than 80 but less than 100. 
```js
db.restaurants.find({grades : {$elemMatch : {score : {$gt : 80, $lt : 100}}}})
```

10. Write a MongoDB query to find the restaurants which locate in latitude value less than -95.754168.
```js
***1st***
db.restaurants.find({"address.coord" : {$lt : -95.754168}})
// check all values in massiv and compare with -95.754168
***2nd***
db.restaurants.find({"address.coord.0" : {$lt : -95.754168}})
// check solely 1st elem of massive due to coord [-180 - 0, 0 - 180] -> no need check 2nd value
```

11. Write a MongoDB query to find the restaurants that do not prepare any cuisine of 'American' and their grade score more than 70 and latitude less than -65.754168. 
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

12. Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American' and achieved a score more than 70 and located in the longitude less than -65.754168.

***Note : Do this query without using $and operator.***
```js
  db.restaurants.find(
      {
          cuisine : {$ne : "American "},
          grades : {$elemMatch : {score : {$gt : 70}}},
          "address.coord.0" : {$lt : -65.754168}
      })
```

13. Write a MongoDB query to find the restaurants which do not prepare any cuisine of 'American' and achieved a grade point 'A' not belongs to the borough Brooklyn. The document must be displayed according to the cuisine in descending order. 
```js
db.restaurants.find(
      {
          cuisine : {$ne : "American "},
          grades : {$elemMatch : {grade : {$eq : "A"}}},
          borough : {$ne : "Brooklyn"}
      })
        .sort({cuisine : -1})
```

14. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'Wil' as first three letters for its name. 
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

15. Write a MongoDB query to find the restaurant Id, name, borough and cuisine for those restaurants which contain 'ces' as last three letters for its name. 
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




