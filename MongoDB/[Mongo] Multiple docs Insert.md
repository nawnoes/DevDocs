# Mongoose 여러 데이터 Insert 하기
: 객체의 배열로 Insert할 데이터를 만들고, .insert를 사용해 여러 데이터에 대해 insert 한다

**요약**
```js
    // documents array
    var books = [{ name: 'Mongoose Tutorial', price: 10, quantity: 25 },
                    { name: 'NodeJS tutorial', price: 15, quantity: 5 },
                    { name: 'MongoDB Tutorial', price: 20, quantity: 2 }];
 
    // save multiple documents to the collection referenced by Book Model
    Book.collection.insert(books, function (err, docs) {
      if (err){ 
          return console.error(err);
      } else {
        console.log("Multiple documents inserted to Collection");
      }
    });
```

**전체 코드**
```js
 
var mongoose = require('mongoose');
 
// make a connection
mongoose.connect('mongodb://localhost:27017/tutorialkart');
 
// get reference to database
var db = mongoose.connection;
 
db.on('error', console.error.bind(console, 'connection error:'));
 
db.once('open', function() {
    console.log("Connection Successful!");
    
    // define Schema
    var BookSchema = mongoose.Schema({
      name: String,
      price: Number,
      quantity: Number
    });
 
    // compile schema to model
    var Book = mongoose.model('Book', BookSchema, 'bookstore');
 
    // documents array
    var books = [{ name: 'Mongoose Tutorial', price: 10, quantity: 25 },
                    { name: 'NodeJS tutorial', price: 15, quantity: 5 },
                    { name: 'MongoDB Tutorial', price: 20, quantity: 2 }];
 
    // save multiple documents to the collection referenced by Book Model
    Book.collection.insert(books, function (err, docs) {
      if (err){ 
          return console.error(err);
      } else {
        console.log("Multiple documents inserted to Collection");
      }
    });
    
});
 
```

# Ref
https://www.tutorialkart.com/nodejs/mongoose/insert-multiple-documents-to-mongodb/