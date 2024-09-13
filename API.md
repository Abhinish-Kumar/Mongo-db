## API

```javascript
const express = require("express");
const app = express();
const bodyParser = require("body-parser");
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }));

// parse application/json
app.use(bodyParser.json());

const mongoose = require("mongoose");
mongoose.connect("mongodb://127.0.0.1:27017/amazone");
const clientSchema = new mongoose.Schema({
  name: String,
  age: Number,
  city: String,
});

//Clients collection create hoga jisme sare document save honge is se create kie gae

const Client = new mongoose.model("Client", clientSchema);

//post api at end point /client
app.post("/client", (req, res) => {
  console.log(req.body);
  let createdClient = new Client({
    name: req.body.name,
    age: req.body.age,
    city: req.body.city,
  });
  createdClient
    .save()
    .then((savedCLient) => {
      console.log("User saved:", savedCLient);
    })
    .catch((error) => {
      console.log("Error saved user:", error);
    });
  res.send("Your data is received");
});

//api to get users at end point /clients

app.get("/client", async (req, res) => {
  let data = await Client.find();
  res.send({ data: data });
});

app.get("/client/:name", async (req, res) => {
  let nameParam = req.params.name;
  let data = await Client.findOne({ name: nameParam });
  res.send({ data: data });
});

app.put("/client/:name", async (req, res) => {
  let nameParam = req.params.name;
  let data = await Client.findOneAndUpdate(
    { name: nameParam },
    { name: "Abhinish Kumar" },
    { new: true }
  );
  res.send({ data: data });
});

//Delete route to delete by id

app.delete("/client/:name", async (req, res) => {
  let nameParam = req.params.name;
  let data = await Client.findOneAndDelete({ name: nameParam },{ new: true });
  res.send({ data: data });
});




app.listen(4400, () => {
  console.log("Your server is running at port 4400");
});

```
