# Mongoose
elegant mongodb object modeling for node.js.

Official site: https://mongoosejs.com/


# Installation 
*First be sure you have <b>MongoDB</b> and <b>Node.js</b> installed.*

You can install the package with the command:
```cmd
npm install mongoose --save
```

# Usage
## Connector
To create a connector, you can paste the code bellow in a file `connection.js`:
```js
require(`dotenv`).config()

const mongoose = require('mongoose')

const URI = process.env.DB_STRING; // Setted in your .env file

//if localhost : const URI = 'mongodb://user:pass@hostname:27017/'

const connectDB = async() =>{
    await mongoose.connect(URI, {
        useUnifiedTopology: true,
        useNewUrlParser: true
    });
    console.log('db connected successfully')
}

module.exports = connectDB
```
After that, you can initialize the connection at the top of your `app.js` (for example).
```js
const connectDB = require('./db/connection');
connectDB();
```

## Model
To create a model, you have to define a schema of the model. Let's says we want to create a model of a user in a file `model/User.js`:
```js
const mongoose = require('mongoose');

const UserSchema = new mongoose.Schema(
    {
        "firstname": {
            type: String,
            required: true
        },
        "lastname": {
            type: String,
            required: true
        },
        "login": {
            type: String,
            unique: true,
            required: true
        },
        "password": {
            type: String,
            required: true
        },
    },
    {
        collection: "user"
    }
);
```
To define a model based on this schema, you just have to add at the bottom of `model/User.js`
```js
const User = mongoose.model('User', UserSchema);

module.exports = User;
```

## CRUD
### Create 
To write a data in the database, you have to use `save()`
```js
const newUser = new User({
    "firstname": "Joe",
    "lastname": "Mama",
    "login": "joe",
    "password": "mama"
});
newUser.save().then(() => {
    // DO something when the save is done
}).catch((e) => {
    console.log(`Error ${e.message}`, e);
});
```