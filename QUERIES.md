# MongoDB Queries Practice

Write a MongoDB query to:

1. Display all the documents in the restaurants collection.
```
db.restaurants.find({})

```

2. Display the fields restaurant_id, name, borough and cuisine for all the documents in the collection.
```
db.restaurants.find({}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

3. Display the fields restaurant_id, name, borough and cuisine, but exclude the field _id for all the documents in the collection.
```
db.restaurants.find({}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1, _id: 0 })

``` 

4. Display the fields restaurant_id, name, borough and zip code, but exclude the field _id for all the documents in the collection.
```
db.restaurants.find({}, { restaurant_id: 1, name: 1, borough: 1, "address.zipcode": 1, _id: 0 })

``` 

5. Display all the restaurants which are in the borough Bronx.
```
db.restaurants.find({ borough: "Bronx" })

```

6. Display the first 5 restaurants which are in the borough Bronx.
```
db.restaurants.find({ borough: "Bronx" }).limit(5)

```

7. Display the next 5 restaurants after skipping first 5 which are in the borough Bronx.
```
db.restaurants.find({ borough: "Bronx" }).skip(5).limit(5)

``` 

8. Find the restaurants who achieved a score more than 90.
```
db.restaurants.find({ "grades.score": { $gt: 90 } })

```

9. Find the restaurants that achieved a score, more than 80 but less than 100.
```
db.restaurants.find({ "grades.score": { $gt: 80, $lt: 100 } })

```

10. Find the restaurants which are located in latitude value less than -95.754168.
```
db.restaurants.find({ "address.coord": { $lt: -95.754168 } })

```

11. Find the restaurants that do not prepare any cuisine of 'American' and their grade score is more than 70 and latitude less than -65.754168.
```
db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.score": { $gt: 70 },
  "address.coord": { $lt: -65.754168 }
})

```

12. Find the restaurants which do not prepare any cuisine of 'American' and achieved a score more than 70 and are located in the longitude less than -65.754168.

db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.score": { $gt: 70 },
  "address.coord.0": { $lt: -65.754168 }
})


13. Find the restaurants which do not prepare any cuisine of 'American' and achieved a grade point 'A' and does not belong to the borough Brooklyn. The document must be displayed according to the cuisine in descending order.
```
db.restaurants.find({
  cuisine: { $ne: "American" },
  "grades.grade": "A",
  borough: { $ne: "Brooklyn" }
}).sort({ cuisine: -1 })

```

14. Find the restaurant_id, name, borough and cuisine for those restaurants which contain 'Wil' as first three letters in its name.
```
db.restaurants.find({ name: /^Wil/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

15. Find the restaurant_id, name, borough and cuisine for those restaurants which contain 'ces' as last three letters in its name. 
```
db.restaurants.find({ name: /ces$/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

16. Find the restaurant_id, name, borough and cuisine for those restaurants which contain 'Reg' as three letters somewhere in its name.
```
db.restaurants.find({ name: /Reg/ }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

17. Find the restaurants which belong to the borough Bronx and prepare either American or Chinese cuisine.
```
db.restaurants.find({
  borough: "Bronx",
  $or: [
    { cuisine: "American" },
    { cuisine: "Chinese" }
  ]
})

``` 

18. Find the restaurant_id, name, borough and cuisine for those restaurants which belong to the boroughs Staten Island or Queens or Bronx or Brooklyn.
```
db.restaurants.find({
  borough: { $in: ["Staten Island", "Queens", "Bronx", "Brooklyn"] }
}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

19. Find the restaurant_id, name, borough and cuisine for those restaurants which don't belong to the boroughs Staten Island or Queens or Bronx or Brooklyn.
```
db.restaurants.find({
  borough: { $nin: ["Staten Island", "Queens", "Bronx", "Brooklyn"] }
}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

20. Find the restaurant_id, name, borough and cuisine for those restaurants which achieved a score that is not more than 10.
```
db.restaurants.find({ "grades.score": { $not: { $gt: 10 } } }, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

21. Find the restaurant_id, name, borough and cuisine for those restaurants which either prepare dishes except 'American' and 'Chinese' or has a name which begins with the letters 'Wil'.
```
db.restaurants.find({
  $or: [
    { cuisine: { $nin: ["American", "Chinese"] } },
    { name: /^Wil/ }
  ]
}, { restaurant_id: 1, name: 1, borough: 1, cuisine: 1 })

```

22. Find the restaurant_id, name, and grades for those restaurants which achieved an A grade and scored 11 on the date "2014-08-11T00:00:00Z" among many of survey dates.
```
db.restaurants.find({
  "grades.grade": "A",
  "grades.score": 11,
  "grades.date": ISODate("2014-08-11T00:00:00Z")
}, { restaurant_id: 1, name: 1, grades: 1 })

```

23. Find the restaurant_id, name and grades for those restaurants where the 2nd element of grades array contains a grade of "A" and score 9 on an ISODate "2014-08-11T00:00:00Z".
```
db.restaurants.find({
  "grades.1.grade": "A",
  "grades.1.score": 9,
  "grades.1.date": ISODate("2014-08-11T00:00:00Z")
}, { restaurant_id: 1, name: 1, grades: 1 })

```

24. Find the restaurant_id, name, address and geographical location for those restaurants where 2nd element of coord array contains a value which is more than 42 and upto 52.
```
db.restaurants.find({
  "address.coord.1": { $gt: 42, $lte: 52 }
}, { restaurant_id: 1, name: 1, address: 1, "address.coord": 1 })

```

25. Arrange the name of the restaurants in ascending order along with all the columns.
```
db.restaurants.find().sort({ name: 1 })

```

26. Arrange the name of the restaurants in descending along with all the columns.
```
db.restaurants.find().sort({ name: -1 })

```

27. Arrange the restaurants in ascending order of cuisines and descending order of boroughs.
```
db.restaurants.find().sort({ cuisine: 1, borough: -1 })

```

28. Check whether all the resturant addresses contain the street or not.
```
db.restaurants.find({ "address.street": { $exists: false } })

```

29. Display all documents in the restaurants collection where the coord field value is a Double.
```
db.restaurants.find({ "address.coord": { $type: "double" } })

```

30. Display the restaurant_id, name and grades for those restaurants which have a grade divisible by 7.
```
db.restaurants.find({ "grades.grade": { $mod: [7, 0] } }, { restaurant_id: 1, name: 1, grades: 1 })

```

31. Find the restaurant name, borough, longitude and latitude and cuisine for those restaurants which contain 'mon' as three letters somewhere in its name.
```
db.restaurants.find({ name: /mon/ }, { name: 1, borough: 1, "address.coord": 1, cuisine: 1 })

```