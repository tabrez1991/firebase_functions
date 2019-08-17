# Firebase Cloud Functions

## Create a firebase project
1. Go to https://firebase.google.com/
2. Login or signup and go to console.
3. Add project.
4. Enter your project name.
5. Create project.

## Create firebase in your system
1. Open terminal.
2. Go to desktop.<br/>
`cd Desktop`<br/>
3. Make a folder item-list-server.<br/>
`mkdir item-list-server`<br/>
4. Go to the folder.<br/>
`cd item-list-server`<br/>
5. Install the Firebase CLI.<br/>
`npm install -g firebase-tools`<br/>
If command fails use <br/>
`sudo npm install -g firebase-tools`<br/>
6. Run firebase login.<br/>
`firebase login`<br/>
7. Allow firebase to collect anonymous cli usage and error reporting information?<br/>
`yes`<br/>
8. This will open your browser for login with firebase. Choose your account and login.
9. Run firebase init functions.<br/>
`firebase init functions`<br/>
10. This will show a list of all your projects, use the arrow key to select your project.
11. What language would you like to use to write Cloud Functions?<br/>
`Javascript`<br/>
12. Do you want to use ESLint to catch probable bugs and enforce style?<br/>
`n`<br/>
13. Do you want to install dependencies with npm now?<br/>
`y`<br/>
14. This will setup the project and install all the dependencies.
15. Now, go to the functions folder<br/>
`cd functions`<br/>
16. Open the index.js file and insert the following code snippet.
```
const functions = require("firebase-functions");
const cors = require("cors")({ origin: true });
const admin = require("firebase-admin");

admin.initializeApp();

const database = admin.database().ref("/items");

exports.helloWorld = functions.https.onRequest((request, response) => {
  response.send("Hello from a Severless Database!");
});

const getItemsFromDatabase = res => {
  let items = [];

  return database.on(
    "value",
    snapshot => {
      snapshot.forEach(item => {
        items.push({
          id: item.key,
          item: item.val().item
        });
      });
      res.status(200).json(items);
    },
    error => {
      res.status(500).json({
        message: `Something went wrong. ${error}`
      });
    }
  );
};

exports.addItem = functions.https.onRequest((req, res) => {
  return cors(req, res, () => {
    if (req.method !== "POST") {
      return res.status(500).json({
        message: "Not allowed"
      });
    }
    const item = req.body.item;
    database.push({ item });
    getItemsFromDatabase(res);
  });
});

exports.getItems = functions.https.onRequest((req, res) => {
  return cors(req, res, () => {
    if (req.method !== "GET") {
      return res.status(500).json({
        message: "Not allowed"
      });
    }
    getItemsFromDatabase(res);
  });
});

exports.deleteItem = functions.https.onRequest((req, res) => {
  return cors(req, res, () => {
    if (req.method !== "DELETE") {
      return res.status(500).json({
        message: "Not allowed"
      });
    }
    const id = req.query.id;
    admin
      .database()
      .ref(`/items/${id}`)
      .remove();
    getItemsFromDatabase(res);
  });
});
```
17. Run the following command on your terminal.<br/>
``` firebase deploy```

# Now your Firebase Function successfully implemented
 If you want to show where it is. Goto the firebase console. Click on functions. This will show you the list of fuctions that you create. 