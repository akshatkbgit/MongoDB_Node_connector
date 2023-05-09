// mongodb://127.0.0.1:27017/

const MongoClient = require('mongodb').MongoClient;
const assert = require('assert');

// Connection URL
const uri = 'mongodb://127.0.0.1:27017/';

const client = new MongoClient(uri, {useUnifiedTopology: true});

// Database Name
const dbName = "fruitsDB";
 
async function run() {
  try {
    await client.connect(function(){
      console.log("Connected successfully to server!");
    });
  const database = client.db(dbName);
  
  const collection = database.collection('fruits'); 
 
  const docs = [
  {
    name: 'Apple',
    score: 8,
    review: "Great fruit"
  },
  {
    name: "Orange",
    score: 6,
    review: "Kinda sour"
  },
  {
    name: "Bananna",
    score: 9,
    review: "Great stuff!"
  }
  ];
 
  const options = { ordered: true };
 
  const result = await collection.insertMany(docs, options);
 
  console.log(`${result.insertedCount} documents were inserted.`);
 
  } finally {
    // Ensures that the client will close when you finish/error
    await client.close();
  }
}
run().catch(console.dir);
