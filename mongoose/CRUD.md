### Create

```javascript
// Import the express framework
const express = require("express");
// Create an instance of the express application
const app = express();

// Import the body-parser middleware (not used in this code, but typically for parsing JSON, URL-encoded data, etc.)
const bodyParser = require("body-parser");

// Import the mongoose library for MongoDB interaction
const mongoose = require("mongoose");

// Connect to a local MongoDB instance with the database named "Abhinish"
mongoose.connect("mongodb://127.0.0.1:27017/Abhinish");

// Define a schema for the Student collection with 'name' and 'age' fields
const studentSchema = new mongoose.Schema({
  name: String,
  age: Number,
});

// Create a model based on the student schema, representing documents in the 'students' collection
const Student = mongoose.model("Student", studentSchema);

// Create a new instance of the Student model (a new document)
const doc = new Student();

// Set the 'name' and 'age' fields for the document
doc.name = "Ayasha";
doc.age = 22;

// Save the document to the MongoDB database
doc.save();

// Start the express server and listen on port 3300
app.listen(3300);


```
















