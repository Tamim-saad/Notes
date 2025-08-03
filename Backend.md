# Backend Notes by me

### Two types of dependency in node:

#### normal dependency:

		using \--save  
		ex: $npm i express \--save  
		Package.json e always thakbe,amra use korte parbo  
		—save na dile boro project e package e jhamela hoy, dile git pull korle local machine e same dependency install hobe

#### Dev dependency:

Production e lagbe na, for development purpose only	  
		ex: $npm i express \--save-dev

### commands

***$node \-v***  
***$npm \-v***  
***$code .***  
***$npm init***  
***$npm init \-y (for not answering any question)***  
***$npm i express —save***  
***$npm run start (main command $node server.js,jeta server.js file ta k execute kore, but package.json e eta start diye configure kora)***

### Initial code explanation

const express \= require('express');  
const app \= express();

* **Import Express**: `express` is required to create a web server.  
* **Initialize App**: `app` is an instance of the Express application.

//? Check Connection  
app.get('/', (req, res) \=\> {  
  res.json({ message: 'welcome' });  
});

* **Route Definition**: Defines a GET route for `/`.  
* **Request Handler**: When `/` is accessed, the server responds with a JSON object: `{ message: 'welcome' }`.  
* **Purpose**: Useful for a basic health check of the server (confirming it's running and responding). It is a **route handler**, not middleware.

const port \= process.env.PORT || 3000;

* **Port Configuration**:  
  * `process.env.PORT`: Retrieves the port number from the environment variables (useful for deployment, where the hosting platform specifies the port).  
  * `|| 3000`: Falls back to port `3000` if no environment variable is set (e.g., during local development).

app.listen(port, () \=\> {  
  console.log(\`Server running on port ${port}\`);  
});

* **Start the Server**:  
  * app.listen(port, callback): Starts the Express server, listening on the specified port.  
  * The callback function logs a message to the console when the server starts successfully.

### To install nodemon:

***$npm i nodemon –save-dev***  
Then package.json \=\> scripts \=\> {”dev”: “nodemon server.js”}  
To apply changes on the fly, give following command instead of “**$npm run start**”  
	**$npm run dev**

### To run debugger:

\- make sure that following two line is included in  “package.json-\>{}scripts”  
	  **$"start": "node server.js”**  
 **$"dev": "nodemon server.js"**  
\- click debug icon above script function  
\- click on dev from {start,test,dev} options.  
\- it will run a new javascript debug terminal

### To make API call in postman:

- Click new(left upper one) \-\> click collection \-\> add request \-\> GET \[address\]

### **CRUD** operation:

*\-create \[POST\] {ex: linkedin account creation}*  
*\-read \[GET\] {view profile}*  
*\-update \[PUT/PATCH\] {add info}*  
*\-delete \[DELETE\] {delete account}*

#### Request er body pete hole

*npm er body-parser package namaste hobe”*  
		***$npm i body-parser —save***  
	*Surute body-parser require korte hobe*

#### Routes Overview

| HTTP Method | Endpoint | Description |
| ----- | ----- | ----- |
| **POST** | /users | Create a new user |
| **GET** | /users | Retrieve all users |
| **GET** | /users/:id | Retrieve a user by ID |
| **PUT** | /users/:id | Update a user's details |
| **DELETE** | /users/:id | Delete a user by ID |

#### 

## To run debugger:

In terminal, give the command-  
$npm run dev  
Then server will start.  
The line you want to debug, just add a breakpoint.  
Reload from user end.  
Then debug environment will appear with some floating options,use them to debug.

Remember: after yellow box appear around breakpoint, postman api call doesn’t work. Remove the breakpoint to make api call again from postman

## Route Implementations WIthout DB

### Create a User (POST /users)

app.post('/users', (req, res) \=\> {  
  const user \= req.body; // Extract user data from the request body  
  user.id \= \++lastid;    // Assign a unique ID to the new user  
  users.push(user);      // Add the user to the users array (in-memory storage)  
  res.status(201).json(user);  // Respond with the created user and HTTP status 201  
});

### Get All Users (GET /users)

app.get('/users', (req, res) \=\> {  
  res.json(users);  
});

### Get a User by ID (GET /users/:id)

app.get('/users/:id', (req, res) \=\> {  
  const id \= parseInt(req.params.id);  
  const user \= users.find(u \=\> u.id \=== id);  
  user ? res.json(user) : res.status(404).json("user not found");  
});

### Update a User (PUT /users/:id)

app.put('/users/:id', (req, res) \=\> {  
  const id \= parseInt(req.params.id); // Extract ID from the URL and convert it to an integer  
  const index \= users.findIndex(u \=\> u.id \=== id); // Find the index of the user with the given ID

  if (index \=== \-1) return res.status(404).json("user not found"); // If user not found, return 404

  users\[index\] \= { ...users\[index\], ...req.body }; // Merge existing user data with updated data

  res.json(users\[index\]); // Respond with the updated user data  
});

### Delete a User (DELETE /users/:id)

app.delete('/users/:id', (req, res) \=\> {  
  const id \= parseInt(req.params.id); // Extract user ID from URL and convert it to an integer  
  const index \= users.findIndex(u \=\> u.id \=== id); // Find the index of the user with the given ID

  if (index \=== \-1) return res.status(404).json("user not found");

  users.splice(index, 1); // Remove the user from the array  
  res.json({ message: "user deleted" }); // Send success response  
});

### Middleware

To parse JSON request bodies:

app.use(express.json());

### Mongodb-compass and mongoose installation

### TO SEE INSTALLATION OF MONGODB-Compass AND CONNECT MONGOOSE to vscode(google by mongoose npm) SEE VIDEO no 045

### To install mongoose:

	***\&npm i mongoose –save***

## Route Implementations WIth DB

### Folder Structure:

### ![][image1] 

### 

### /server.js:

const express \= require('express');  // Import Express framework to create server and handle routing  
const app \= express();  // Initialize an Express application instance  
const bodyParser \= require('body-parser');  // Import body-parser to parse incoming request bodies  
const connectDB \= require('./config/db');  // Import the database connection function

//? Parse Request Body Middleware  
app.use(bodyParser.json());  
// Middleware that allows the app to parse JSON request bodies, enabling access via req.body

//? Connect to MongoDB  
connectDB();  
// Calls the function to establish a connection with the MongoDB database

//? API Routes  
app.use('/api/users', require('./routes/api/users'));  
// This line mounts the user routes (CRUD operations on users) under the '/api/users' endpoint

//? Check Connection Endpoint  
app.get('/', (req, res) \=\> {  
  res.json({ message: 'welcome' });  
  // Sends a JSON response to the root URL ('/') to confirm the server is running  
});

//? Server Port Configuration  
const port \= process.env.PORT || 3000;  
// Sets the server to listen on the port specified in the environment variable or defaults to 3000

app.listen(port, () \=\> {  
  console.log(\`Server running on port ${port}\`);  
  // Starts the server and logs a message indicating the port it's running on  
});

### /config/db.js:

const mongoose \= require('mongoose');  // Import Mongoose for database interaction

const uri \= 'mongodb+srv://nodejs-c1:nodejs-c1@nodejs-c1.530gk.mongodb.net/';  // MongoDB connection URI

const connectDB \= async () \=\> {  
  try {  
    await mongoose.connect(uri);  // Connect to MongoDB using the provided URI  
    console.log('Mongoose Connect');  // Log success message if connection succeeds  
  }  
  catch (error) {  
    console.error(error.message);  // Log the error message if the connection fails  
  }  
}

module.exports \= connectDB;  // Export the connectDB function to be used elsewhere in the application

### /models/User.js:

const mongoose \= require('mongoose');  // Import Mongoose to interact with MongoDB

const UserSchema \= new mongoose.Schema({  
  fname: {  
    type: String  // Field 'fname' should be of type String  
  },  
  lname: {  
    type: String  // Field 'lname' should be of type String  
  },  
  email: {  
    type: String  // Field 'email' should be of type String  
  }  
}, {  
  timestamps: true  // Automatically adds 'createdAt' and 'updatedAt' fields to the schema  
});

module.exports \= mongoose.model('User', UserSchema);  // Export the Mongoose model named 'User'

### /routes/api/users.js: 

const express \= require('express');  // Import Express framework to handle routing functionalities.  
const router \= express.Router();  // Create an instance of the Express router to define API routes.  
const User \= require('../../models/User');  // Import the User model to interact with the MongoDB collection.

//? Create a new user (POST request)  
router.post('/', async (req, res) \=\> {  
  try {  
    // Extract user details from the request body.  
    // Why: This helps to separate the incoming data and prepare it for database storage.  
    const userObj \= {  
      fname: req.body.fname,  // First name is extracted from the request body.  
      lname: req.body.lname,  // Last name is extracted from the request body.  
      email: req.body.email,  // Email is extracted from the request body.  
    };

    // Create a new user instance using the Mongoose model.  
    // Why: This step helps in ensuring data adheres to the defined schema before saving.  
    const user \= await User(userObj);

    // Save the new user to the database.  
    // How: The \`save()\` function writes the new user to the database.  
    await user.save();

    // Send a response with HTTP status 201 (Created) and return the created user.  
    // Why: HTTP 201 indicates successful resource creation.  
    return res.status(201).json(user);  
  }  
  catch (err) {  
    // Handle any errors and respond with a generic message.  
    // Why: To avoid exposing sensitive error details to the client.  
    res.status(500).json({ message: "Something went wrong" });  
  }  
});

//? Get all users (GET request)  
router.get('/', async (req, res) \=\> {  
  try {  
    // Retrieve all users from the database.  
    // How: The \`find({})\` method fetches all documents from the collection.  
    const users \= await User.find({});

    // Return all users with HTTP status 200 (OK).  
    // Why: HTTP 200 indicates a successful data retrieval.  
    return res.status(200).json(users);  
  }  
  catch (err) {  
    // Handle any errors that occur during database query execution.  
    res.status(500).json({ message: "Something went wrong" });  
  }  
});

//? Get a specific user by ID (GET request)  
router.get('/:id', async (req, res) \=\> {  
  try {  
    // Extract the user ID from the request parameters.  
    // How: \`req.params.id\` retrieves the ID from the URL.  
    const id \= req.params.id;

    // Find the user by ID in the database.  
    // How: \`findById(id)\` searches the collection for a matching document.  
    const user \= await User.findById(id);

    if (user) {  
      // If user is found, return the user data.  
      return res.json(user);  
    } else {  
      // If no user is found, return a 404 (Not Found) status.  
      return res.status(404).json("user not found");  
    }  
  }  
  catch {  
    // Catch block to handle any unexpected errors.  
    res.status(500).json({ message: "Something went wrong" });  
  }  
});

//? Update an existing user (PUT request)  
router.put('/:id', async (req, res) \=\> {  
  try {  
    // Extract the user ID from the request parameters.  
    // Why: The ID is needed to identify which record to update.  
    const id \= req.params.id;

    // Extract updated user data from the request body.  
    const userBody \= req.body;

    // Find the user by ID and update with new data.  
    // How: \`findByIdAndUpdate\` takes ID, new data, and \`{ new: true }\` to return updated data.  
    const updatedUser \= await User.findByIdAndUpdate(id, userBody, { new: true });

    // Optional comments to clarify update options  
    // Only update \`fname\` field: \`User.findByIdAndUpdate(id, { fname: req.body.fname }, { new: true })\`  
    // Show old values after update: \`User.findByIdAndUpdate(id, { fname: req.body.fname })\`

    if (updatedUser) {  
      // If update is successful, return the updated user data.  
      return res.json(updatedUser);  
    } else {  
      // If no user is found, return a 404 (Not Found) response.  
      return res.status(404).json("user not found");  
    }  
  }  
  catch {  
    // Handle any errors that might occur during the update process.  
    res.status(500).json({ message: "Something went wrong" });  
  }  
});

//? Delete a user  
router.delete('/:id', async (req, res) \=\> {  
  try {  
    const id \= req.params.id;  // Extract the user ID from the request URL parameter

    // Attempt to delete the user by ID from the database  
    const deletedUser \= await User.findByIdAndDelete(id);

    if (deletedUser) {  
      // If user is found and deleted, return success message with deleted user details  
      return res.json({ "following user deleted": deletedUser });  
    } else {  
      // If no user is found with the given ID, return 404 Not Found status  
      return res.status(404).json("user not found");  
    }  
  } catch (err) {  
    // Handle any errors that may occur during the operation and respond with 500 Internal Server Error  
    res.status(500).json({ message: "Something went wrong", error: err.message });  
  }  
});

module.exports \= router;  // Export the router to be used in the main server file.

##  Some Explanation

#### 1\. Understanding `async` and `await`:

#### **`async` (Asynchronous Function)**

* The `async` keyword is used to define a function that returns a **Promise** implicitly.  
* It allows the function to handle asynchronous operations in a readable way.  
* Functions declared with `async` can contain the `await` keyword.

#### **`await`**

* The `await` keyword is used inside an `async` function to pause execution until the Promise is resolved.  
* It ensures that the function waits for an asynchronous operation to complete before moving to the next line of code.  
* Instead of using traditional `.then()` promise chains, `await` makes the code look synchronous and cleaner.

#### **Example:**

async function fetchData() {  
  const data \= await someAsyncFunction();  // Waits until someAsyncFunction resolves  
  console.log(data);  
}

**How it works:**

1. The function is marked `async` to indicate it contains asynchronous operations.  
2. `await` makes the function wait until `someAsyncFunction()` completes, then assigns the result to `data`.  
3. The next line executes only after the Promise resolves.

#### 

#### 2\. `findByIdAndUpdate()` Function Structure

#### **Syntax:**

Model.findByIdAndUpdate(id, updateObject, options);

#### **Explanation of Parameters:**

1. `id`: The unique identifier (usually `_id`) of the document to be updated.  
2. `updateObject`: An object containing the fields to be updated.  
3. `options` (optional):  
   * `{ new: true }`: Returns the updated document instead of the old one.  
   * `{ upsert: true }`: If the document does not exist, create a new one.  
   * `{ runValidators: true }`: Runs schema validators before updating.

#### **Example:**

const updatedUser \= await User.findByIdAndUpdate(  
  "65a3b4cde78",  // Example document ID  
  { fname: "Updated Name" },  // Fields to update  
  { new: true, runValidators: true }  // return updated data and validate  
);

**How it works:**

* The method searches for a user by the given ID.  
* If found, it updates the `fname` field with "Updated Name".  
* It returns the updated document because of `{ new: true }`.

#### 3\. `find({})` Function Structure

#### **Syntax:**

Model.find(query, projection, options);

#### **Explanation of Parameters:**

1. `query`: An object that specifies conditions to filter documents (empty `{}` means no filters, returning all documents).  
2. `projection` (optional): Specifies which fields to include/exclude.  
3. `options` (optional): Additional query options such as sorting, limiting, and pagination.

#### **Example:**

const users \= await User.find({}, "fname lname", { limit: 5 });

**How it works:**

* `{}` as query means all records will be retrieved.  
* `"fname lname"` projection means only `fname` and `lname` fields are returned.  
* `{ limit: 5 }` option means only 5 records will be returned.

#### 4\. Clarifying `const users = await User.find({})`

#### **Why it uses `User.find({})` and not `users.find({})`?**

* In your code:

const users \= await User.find({});

**Explanation:**

* `User` is the **Mongoose model**, which represents the MongoDB collection.  
* The `find({})` method is called on the `User` model to retrieve data from the `users` collection in the database.  
* The result of this query is stored in the variable `users`, which contains the list of retrieved user documents.

#### **Why not `users.find({})`?**

* The variable `users` only stores the data returned by `User.find({})`, but it does not have access to Mongoose methods like `.find()`.  
* The correct syntax is always `Model.find()` where `Model` is the schema model, such as `User` in this case.

#### **Example Breakdown:**

const users \= await User.find({});  
console.log(users); // Array of user objects from the database

**Step-by-step explanation:**

1. `User.find({})` → Fetches all records from the database.  
2. The result is stored in the variable `users`.

`users` now contains an array of all user documents, e.g.:  
\[  
  { \_id: '1', fname: 'John', lname: 'Doe' },  
  { \_id: '2', fname: 'Jane', lname: 'Doe' }  
\]

3. If you tried `users.find({})`, it would result in an error because `users` is just an array, not a Mongoose model.

| Concept | Explanation |
| ----- | ----- |
| `async` | Declares an asynchronous function that returns a Promise implicitly. |
| `await` | Waits for an asynchronous operation to complete before continuing. |
| `findByIdAndUpdate()` | Updates a document by ID and returns the updated document if `{ new: true }` is passed. |
| `find({})` | Retrieves documents from the database based on filter criteria (empty `{}` returns all). |
| `User.find({})` | Correct usage, because `User` is the Mongoose model that interacts with the database. |

### To install dotenv:

	**$npm i dotenv –save**

### To install encryption package to protect password:

	**$npm i bcrypt –save**

### To install jsonwebtoken to generate token to access password:

	**$npm i jsonwebtoken –save**

### Bcrypt Password Encryption \- Key Notes

1\. Why Encrypt Passwords?

* Protects against unauthorized access.  
* Prevents rainbow table and brute-force attacks.  
* Ensures passwords are stored securely (hashed, not plain text).

---

2\. Steps in Password Encryption

Step 1: Generate Salt  
const salt \= await bcrypt.genSalt(10);

* Adds randomness to prevent duplicate hashes.  
* 10 is the salt round (higher \= more secure, but slower).

Step 2: Hash the Password  
const hashedPassword \= await bcrypt.hash(req.body.password, salt);

* Combines salt with password and applies hashing.  
* Hashed password stored securely in the database.

---

3\. Password Verification

**`const isMatch = await bcrypt.compare(req.body.password, storedHashedPassword);`**

* **Compares input password with stored hash.**  
* **Returns `true` if they match, else `false`.**

---

4\. Key Benefits of Bcrypt

* **Adaptive hashing (slows down with increasing computation power).**  
* **Automatic salting (no need to manually add salt).**  
* **Slowness for security (mitigates brute-force attacks).**

---

5\. Important Considerations

* **Always use `app.use(express.json());` to parse request bodies.**  
* **Never store plain-text passwords.**  
* **Recommended salt rounds: 10-12 for a balance between security and performance.**  
* **Use async/await to avoid blocking the server.**

## Authentication:  /routes/api/users.js: 

const express \= require('express');  
const router \= express.Router();  
const User \= require('../../models/User')  
const bcrypt \= require('bcrypt');  
const jwt \= require('jsonwebtoken');

//? Create a new user  
router.post('/', async (req, res) \=\> {  
  try {  
    // 🔐 Password Security Steps:  
    // 1\. Make random 'salt' to mix with password (like special seasoning)  
    const salt \= await bcrypt.genSalt(10); // 10 \= security strength

    // 2\. Hash password \= password \+ salt → scrambled text  
    const password \= await bcrypt.hash(req.body.password, salt);

    // 📦 Prepare user data package  
    const userObj \= {  
      fname: req.body.fname,  
      lname: req.body.lname,  
      email: req.body.email,  
      password: password, // Store HASHED password, never raw password\!  
    }

    // 💾 Save to database  
    const user \= await User(userObj) // Create new user document  
    await user.save(); // Actually save to database

    // ⚠️ SECURITY WARNING: We're sending back hashed password\!  
    // Should remove password before sending response  
    return res.status(201).json(user) // 201 \= Created success status

  } catch (err) {  
    // 🚨 Handle errors (like duplicate email or database issues)  
    res.status(500).json({ message: "Something wrong " }); // 500 \= Server error  
  }  
});

// 1\. Route Setup  
// router.post('/', async (req, res) \=\> {  
// What it does: Handles POST requests to the website's root URL (/)  
// Like: A registration form submission handler

// 2\. Password Security (Most Important Part\!)  
// const salt \= await bcrypt.genSalt(10);  
// const password \= await bcrypt.hash(req.body.password, salt);  
// Step 1: Makes a "salt" \- random data for password protection  
// genSalt(10) \= Security level (higher number \= more secure but slower)  
// Step 2: Mixes the user's password with the salt to create a secure hash  
// Why: Never store passwords as plain text\!

// 3\. Building the User  
// const userObj \= {  
//   fname: req.body.fname,  
//   lname: req.body.lname,  
//   email: req.body.email,  
//   password: password, // This is the hashed password now  
// }  
// What's happening: Creates a user object with:  
// First name  
// Last name  
// Email  
// Securely hashed password (not the real password\!)

// 4\. Saving to Database  
// const user \= await User(userObj)  
// await user.save();  
// Step 1: User(userObj) creates a new user document  
// Step 2: user.save() stores it in the database

// 5\. Success Response  
// return res.status(201).json(user)  
// 201 Status: "Created" success message  
// Sends back: The created user data (but we'll talk about this later)

// 6\. Error Handling  
// catch (err) {  
//   res.status(500).json({ message: "Something wrong " });  
// }  
// Catches: Any errors that happen in the process  
// Responds: Generic error message (500 \= Internal Server Error)

//? Login  
router.post('/login', async (req, res) \=\> {  
  try {  
    const { type, email, password, refreshToken } \= req.body;

    // Currently only handling email/password login  
    if (type \=== 'email') {  
      // 🔍 Find user by email (like looking up in phonebook)  
      const user \= await User.findOne({ email: email });

      if (\!user) {  
        return res.status(404).json({ message: "user not found" }); // 404 \= Not found  
      }  
      else {  
        // 🔑 Verify password & handle login  
        await handleEmailLogin(password, user, res)  
      }  
    }  
    else {  
      if (\!refreshToken) {  
        return res.status(404).json({ message: "Refresh token not found" });  
      }  
      else {  
        await handleRefreshToken(refreshToken, res);  
      }  
    }  
  } catch (error) {  
    res.status(500).json({ message: "Something wrong " });  
  }  
});

// This is a login route handler:  
// router.post('/login', async (req, res) \=\> {  
// It handles POST requests to the /login URL  
// async means it contains asynchronous operations (like database queries)  
// req is the incoming request, res is the response we'll send back

// Getting user input:  
// const { type, email, password, refreshToken } \= req.body;  
// Extracts data from the request body (what the user sent)  
// Possible fields: type, email, password, refreshToken

// Check the login type:  
// if (type \=== 'email') {  
// The code currently only handles email/password login  
// There might be other types (like 'google' or 'facebook') in the future

// Find the user:  
// const user \= await User.findOne({ email: email });  
// Searches the database for a user with this email  
// await means we wait for the database response before continuing

// Handle user not found:  
// if (\!user) {  
//   return res.status(404).json({ message: "user not found" });  
// }  
// If no user exists with that email:  
// Send back 404 status (Not Found)  
// Return a JSON error message  
// return stops further execution

// Handle existing user:  
// else {  
//   await handleEmailLogin(password, user, res)  
// }  
// If user exists, call a helper function handleEmailLogin  
// This function would typically:  
// Compare passwords  
// Generate authentication tokens  
// Send response back to client

// Error handling:  
// } catch (error) {  
//   res.status(500).json({ message: "Something wrong " });  
// }  
// Catches any errors that occur in the try block  
// Sends a generic 500 error (Internal Server Error)  
// Note: In real applications, you might want to log the actual error

//?Get user profile  
router.get('/profile', authenticateToken, async (req, res) \=\> {  
  try {  
    // Step 1: Get the user's ID from the authenticated request  
    const id \= req.user.\_id;

    // Step 2: Find the user in the database using their ID  
    const user \= await User.findById(id);

    // Step 3: If the user exists, return their profile  
    if (user) {  
      return res.json(user);  
    }  
    // Step 4: If the user doesn't exist, return a 404 error  
    else {  
      return res.status(404).json("user not found");  
    }  
  }  
  // Step 5: Handle any unexpected errors  
  catch {  
    res.status(500).json({ message: "Something went wrong" });  
  }  
});

//? Get all users  
router.get('/', async (req, res) \=\> {  
  try {  
    const users \= await User.find({})  
    return res.status(200).json(users)  
  }  
  catch (err) {  
    res.status(500).json({ message: "Something went wrong" });  
  }  
})

//?Get one user  
router.get('/:id', async (req, res) \=\> {  
  try {  
    const id \= req.params.id  
    const user \= await User.findById(id)  
    if (user) {  
      return res.json(user)  
    }  
    else {  
      return res.status(404).json("user not found")  
    }  
  }  
  catch {  
    res.status(500).json({ message: "Something went wrong" });  
  }  
})

//? Update 1 user  
router.put('/:id', async (req, res) \=\> {  
  try {  
    const id \= req.params.id;  
    const userBody \= req.body  
    const updatedUser \= await User.findByIdAndUpdate(id, userBody, { new: true })  
    // only fname update korte chaile (id, fname, {new: true})  
    // update kore old value e dekhate chaile (id, fname)

    if (updatedUser) {  
      return res.json(updatedUser)  
    }  
    else {  
      return res.status(404).json("user not found")  
    }  
  }  
  catch {  
    res.status(500).json({ message: "Something went wrong", error: err.message });  
  }  
})

//? Delete a user  
router.delete('/:id', async (req, res) \=\> {  
  try {  
    const id \= req.params.id;  
    const deletedUser \= await User.findByIdAndDelete(id)  
    if (deletedUser) {  
      return res.json({ "following user deleted": deletedUser })  
    }  
    else {  
      return res.status(404).json("user not found")  
    }  
  } catch (err) {  
    res.status(500).json({ message: "Something went wrong", error: err.message });  
  }  
});

module.exports \= router

// 🔑 Helper function for email/password login  
async function handleEmailLogin(password, user, res) {  
  // 🔐 Compare user input with stored hash  
  const isValidPassword \= await bcrypt.compare(password, user.password)

  if (isValidPassword) {  
    // ✅ Correct password: Create token package  
    const userObj \= await generateUserObj(user)  
    return res.json(userObj);  
  }  
  else {  
    // ❌ Wrong password: Unauthorized access  
    return res.status(401).json({ message: "login failed" }); // 401 \= Unauthorized  
  }  
}  
// What it does:  
// Takes the password you entered and the user's stored password (which is encrypted)  
// Uses bcrypt.compare() to check if they match  
// If correct: Creates a special user object with security tokens  
// If wrong: Sends "login failed" error (401 \= Unauthorized)  
// Key Concepts:  
// Never store passwords as plain text (always encrypted/hashed)  
// bcrypt is a library for safe password comparison

// 🎟️ Token Creation Helpers  
function generateUserObj(user) {  
  // Create access/refresh tokens (like special event tickets)  
  const { accessToken, refreshToken } \= generateToken(user);

  // Convert MongoDB user document to plain object  
  const userObj \= user.toJSON()

  // Add tokens to user object  
  userObj\['accessToken'\] \= accessToken // Short-lived token (1 day)  
  userObj\['refreshToken'\] \= refreshToken // Long-lived token (20 days)

  return userObj;  
}  
// What it does:  
// Gets security tokens from generateToken()  
// Converts database user data to a simple JSON object  
// Adds the tokens to this object  
// Returns the final package ready to send to the client  
// Why this matters:  
// Tokens act like temporary digital keys for accessing protected features  
// Separates database data from what we send to the client

// 🔏 Token Generation (JWT)  
function generateToken(user) {  
  // Access Token (daily use)  
  const accessToken \= jwt.sign(  
    { email: user.email, \_id: user.id }, // Payload (user info)  
    process.env.JWT\_SECRET, // Secret key (like password for tokens)  
    { expiresIn: '1d' } // Expires in 1 day  
  );

  // Refresh Token (for getting new access tokens)  
  const refreshToken \= jwt.sign(  
    { email: user.email, \_id: user.id },  
    process.env.JWT\_SECRET,  
    { expiresIn: '20d' } // Expires in 20 days  
  );

  return { accessToken, refreshToken };  
}

// What it does:  
// Uses jsonwebtoken (JWT) library to create two tokens:  
// Access Token: Short-lived (1 day) for daily use  
// Refresh Token: Long-lived (20 days) to get new access tokens  
// Key Concepts:  
// jwt.sign(payload, secret, options) creates a token  
// Tokens are like digital ID cards with expiration dates  
// process.env.JWT\_SECRET is a secret key stored in your server's environment (like a password for your tokens)

function handleRefreshToken(refreshToken, res) {  
  jwt.verify(refreshToken, process.env.JWT\_SECRET, async (err, payload) \=\> {  
    if (err) {  
      return res.status(401).json({ message: "UnauthorizedError" })  
    }  
    else {  
      const user \= await User.findById(payload.\_id);  
      if (user) {  
        const userObj \= generateUserObj(user);  
        return res.status(200).json(userObj);  
      } else {  
        return res.status(401).json({ message: "UnauthorizedError" })  
      }  
    }  
  })  
}

###  What the “jwt\_secret” actually do?

**What is JWT\_SECRET?**  
It’s a secret key (like a password) that only your server knows.  
It’s used to sign and verify JWTs.  
Example: "mySuperSecretKey123\!" (but much longer and more random in real apps).

**What does JWT\_SECRET actually do?**  
The JWT\_SECRET has two main jobs:

**1\. Signing Tokens (Creating JWTs)**  
When a user logs in, the server creates a JWT using the JWT\_SECRET.  
The JWT\_SECRET is used to generate a signature for the token.  
The signature ensures the token hasn’t been tampered with.

Example:  
const token \= jwt.sign(  
  { email: "alice@example.com" }, // Payload (user data)  
  process.env.JWT\_SECRET, // Secret key  
  { expiresIn: '1d' } // Expires in 1 day  
);

**2\. Verifying Tokens (Validating JWTs)**  
When the client sends a JWT back to the server, the server uses the JWT\_SECRET to verify the token.  
The server checks:  
Is the token’s signature valid? (Was it signed with the correct JWT\_SECRET?)  
Has the token expired?  
Has the token been tampered with?

Example:  
const decoded \= jwt.verify(token, process.env.JWT\_SECRET);  
**How does JWT\_SECRET work under the hood?**

**Step 1: Creating a JWT**  
The server takes the payload (user data, e.g., email, ID).  
It adds a header (describes the token type and algorithm).  
It combines the header and payload into a string.  
It uses the JWT\_SECRET to generate a signature for the string.  
The final JWT is a combination of:

Header  
Payload  
Signature

Example JWT:

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImFsaWNlQGV4YW1wbGUuY29tIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV\_adQssw5c

**Step 2: Verifying a JWT**  
The server receives the JWT from the client.  
It splits the JWT into its three parts:

Header  
Payload  
Signature

It uses the JWT\_SECRET to re-calculate the signature for the header and payload.  
It compares the re-calculated signature with the signature in the JWT:  
If they match → The token is valid.  
If they don’t match → The token is invalid (tampered with or signed with the wrong key).

**Why is JWT\_SECRET necessary?**

Prevents Tampering:  
Without the JWT\_SECRET, anyone could modify the payload (e.g., change the email or ID) and create a fake token.  
The signature ensures the token hasn’t been altered.

Ensures Authenticity:  
Only your server knows the JWT\_SECRET, so only your server can create valid tokens.  
Clients can’t forge tokens.

Stateless Authentication:  
The server doesn’t need to store tokens. Instead, it embeds user info in the token and verifies it using the JWT\_SECRET.

**Real-World Analogy:**  
Imagine you’re issuing tickets for a concert:  
JWT\_SECRET: Your special ink stamp.  
Token: A ticket with:  
Header: "This is a valid ticket."  
Payload: "Alice can enter until 8 PM."  
Signature: Your stamp on the ticket.  
Verification:  
At the door, the bouncer checks:  
Is the stamp real? (Uses JWT\_SECRET to verify the signature.)  
Is the ticket still valid? (Checks the expiration time.)

### Use of access token:

We can view users profile by using access token which is generated at login time

### Differentiate between guest and registered user by access token

Explanation of Access Tokens for Guest and Registered Users

What is an Access Token?

An access token is a digital credential (like a temporary key) that grants a user permission to interact with specific resources or services in an application. It is often used in APIs and web services for authentication and authorization.  
---

Why Access Tokens Are Needed

| User Type | Purpose of Access Token | Example Use Cases |
| :---- | :---- | :---- |
| **Registered Users** | Grants full access to personalized resources after authentication (e.g., account data). | \- Viewing profiles \- Making purchases \- Accessing private data |
| **Guest Users** | Provides limited access for basic interactions (no authentication required). | \- Browsing public content \- Adding items to a cart \- Accessing trial features |

---

Key Differences

| Feature | Registered Users | Guest Users |
| :---- | :---- | :---- |
| **Token Scope** | Full access to personal data and features. | Limited access to public/unrestricted features. |
| **Token Lifespan** | Long-lived (e.g., hours/days). | Short-lived (e.g., minutes/hours). |
| **Security Level** | High (linked to user identity). | Low (anonymous, no personal data). |

---

How It Works

1. **Registered Users**:  
   * **Step 1**: Log in with email/password.  
   * **Step 2**: Server issues an access token (e.g., JWT).  
   * **Step 3**: Token is sent with every request to access protected resource

// Example: Token generation for registered users  
**const token \= jwt.sign(**  
  **{ userId: "123", role: "user" },**  
  **process.env.JWT\_SECRET,**  
  **{ expiresIn: "1d" });**

2. **Guest Users**:  
   * **Step 1**: Visit the app without logging in.  
   * **Step 2**: Server issues a temporary guest token (optional).  
   * **Step 3**: Token allows limited actions (e.g., browsing

// Example: Token generation for guests  
**const guestToken \= jwt.sign(**  
  **{ sessionId: "abc", role: "guest" },**  
  **process.env.JWT\_SECRET,**  
  **{ expiresIn: "1h" });**  
---

Why Guests Might Need Tokens

* **Session Management**: Track guest activity (e.g., cart items).  
* **Rate Limiting**: Prevent abuse of public APIs.  
* **Security**: Enforce token-based policies even for anonymous users.

### /middleware/auth.js:

// Import the jsonwebtoken library to work with JWTs (JSON Web Tokens)  
const jwt \= require('jsonwebtoken');

// Export a middleware function that will be used to authenticate requests  
module.exports \= function (req, res, next) {  
  // Step 1: Check if the request has an Authorization header  
  const authHeader \= req.headers.authorization;

  // If there's no Authorization header, block the request  
  if (\!authHeader) {  
    // Send a 401 Unauthorized response with an error message  
    res.status(401).json({ message: 'Invalid authorization' });  
  }  
  // If the Authorization header exists, proceed to extract the token  
  else {  
    // Step 2: Extract the token from the Authorization header  
    // The header usually looks like: "Bearer \<token\>"  
    // Split the header by spaces and take the second part (the actual token)  
    const token \= authHeader && authHeader.split(' ')\[1\];

    // Step 3: Check if the token exists  
    if (token) {  
      // Step 4: Verify the token using the JWT\_SECRET  
      // jwt.verify() checks if the token is valid and not tampered with  
      jwt.verify(token, process.env.JWT\_SECRET, (err, payLoad) \=\> {  
        // If there's an error (e.g., token is expired or invalid), block the request  
        if (err) {  
          // Send a 401 Unauthorized response with an error message  
          res.status(401).json({ message: 'Invalid authorization' });  
        }  
        // If the token is valid, proceed to the next step  
        else {  
          // Step 5: Attach the payload (user data) to the request object  
          // The payload contains the user's information (e.g., userId, email)  
          req.user \= payLoad;

          // Step 6: Call next() to pass control to the next middleware or route handler  
          next();  
        }  
      });  
    }  
    // If the token doesn't exist, block the request  
    else {  
      // Send a 401 Unauthorized response with an error message  
      res.status(401).json({ message: 'Invalid authorization' });  
    }  
  }  
};

### Explanation:

Step 1: Check for the Authorization Header

const authHeader \= req.headers.authorization;

* **What**: The client sends a token in the `Authorization` header (e.g., `Bearer eyJhbGci...`).  
* **Why**: This is the standard way to send tokens in HTTP requests.  
* **How**: Extract the header value to check for a token.

Step 2: Handle Missing Token

if (\!authHeader) {  
  res.status(401).json({ message: 'Invalid authorization' });

}

* **What**: If there’s no token, block the request.  
* **Why**: No token \= No proof of identity.  
* **How**: Send a `401 Unauthorized` error.

---

Step 3: Extract the Token

const token \= authHeader.split(' ')\[1\];

* **What**: Split the header value to get the token.  
  * Example: `Bearer abc123` → `abc123`.  
* **Why**: The token is prefixed with `Bearer` by convention.  
* **How**: Split the string by spaces and take the second part.

---

Step 4: Verify the Token

jwt.verify(token, process.env.JWT\_SECRET, (err, payload) \=\> { ... });

* **What**: Use the server’s secret key (`JWT_SECRET`) to validate the token.  
* **Why**: Ensures the token wasn’t tampered with and is still valid.  
* **How**:  
  * `jwt.verify` decodes the token.  
  * If valid → `payload` contains user data (e.g., `userId`, `email`).  
  * If invalid → `err` explains why (expired, fake, etc.).

---

Step 5: Grant or Deny Access

if (err) {  
  res.status(401).json({ message: 'Invalid authorization' });  
} else {  
  req.user \= payload; // Attach user data to the request  
  next(); // Allow access to the protected route  
}

* **Valid Token**:  
  * Attach the user’s data to `req.user` (e.g., `req.user.email`).  
  * `next()` passes control to the next middleware or route handler.  
* **Invalid Token**:  
  * Block access with a `401 Unauthorized` error.

---

Key Concepts Explained

What is a JWT?

* A **JSON Web Token** (JWT) is a secure way to transmit user data between the client and server.  
* Structure: `Header.Payload.Signature`  
  * **Header**: Algorithm used (e.g., `HS256`).  
  * **Payload**: User data (e.g., `userId`, `email`).  
  * **Signature**: Ensures the token is valid (created using `JWT_SECRET`).

What is `JWT_SECRET`?

* A secret key **only the server knows** (stored in `.env`).  
* Used to:  
  * **Sign tokens**: Create the token’s signature.  
  * **Verify tokens**: Confirm the token is authentic.

Why Use `Bearer` in the Header?

* It’s a convention to prefix tokens with `Bearer` to indicate the type of authentication.  
* Example: `Authorization: Bearer abc123`.

---

Example Flow

1. **User Logs In**:  
   * Server creates a JWT and sends it to the client.  
2. **User Requests Protected Data**:  
   * Client sends the JWT in the `Authorization` header.  
3. **Middleware Checks Token**:  
   * Valid token → Access granted.  
   * Invalid token → Access denied.

---

Common Questions

Q: What if the token expires?

* The `jwt.verify` check will fail, and the user must log in again.

Q: Where is `JWT_SECRET` stored?

* In a `.env` file (never in code\!) to keep it secure:  
* env  
* Copy  
* JWT\_SECRET=your\_super\_secret\_key\_here

Q: Why attach `payload` to `req.user`?

* So downstream routes/middleware can access the user’s data (e.g., `req.user.email`).

### Clarification:

#### Why attach payload to req.user?

The line `req.user = payload;` is a crucial part of the middleware. It attaches the **decoded payload** (user data) from the JWT to the `req.user` object. Let’s break down **why this is done** and **how it works** in simple terms.

---

What is `payload`?

* The `payload` is the **decoded data** from the JWT.  
* It typically contains user information, such as:

{  
  "userId": "123",  
  "email": "user@example.com",  
  "role": "user"

* }  
* This data is embedded in the JWT when the token is created (e.g., during login).

---

Why Attach `payload` to `req.user`?

1\. Share User Data Across Middleware and Routes

* In Express, the `req` object is passed through all middleware and route handlers.  
* By attaching the `payload` to `req.user`, you make the user’s data available to any subsequent middleware or route handler.  
* Example:

app.get('/profile', (req, res) \=\> {  
  console.log(req.user); // { userId: "123", email: "user@example.com" }  
  res.send(\`Welcome, ${req.user.email}\!\`);

* });

2\. Avoid Repeated Token Decoding

* Without attaching `payload` to `req.user`, you’d need to decode the JWT in every route handler that requires user data.  
* Example of **bad practice**:

app.get('/profile', (req, res) \=\> {  
  const token \= req.headers.authorization.split(' ')\[1\];  
  const payload \= jwt.verify(token, process.env.JWT\_SECRET); // Decode again  
  res.send(\`Welcome, ${payload.email}\!\`);

* });  
* This is inefficient and redundant.

3\. Simplify Access Control

* You can use `req.user` to check permissions or roles in downstream middleware or routes.  
* Example:

app.get('/admin', (req, res) \=\> {  
  if (req.user.role \=== 'admin') {  
    res.send('Welcome, Admin\!');  
  } else {  
    res.status(403).send('Access Denied');  
  }

* });

---

How Does It Work?

1. **Token Verification**:  
   * The middleware decodes the JWT using `jwt.verify`.  
   * If valid, the `payload` contains the user’s data.  
2. **Attach Payload to `req.user`**:  
3. req.user \= payload;  
   * This adds the user’s data to the `req` object.  
4. **Use `req.user` in Routes**:  
   * Any route handler or middleware after this can access `req.user`.

####  why this ?

    const id \= req.user.\_id;  
why not:  
    const id \= req.user.id;??

Great question\! The difference between req.user.\_id and req.user.id depends on how the JWT payload is structured and how your database schema is designed. Let’s break it down:

**1\. Why req.user.\_id?**  
In MongoDB (and Mongoose), the unique identifier for a document is stored in the \_id field by default.  
When you create a JWT payload, it’s common to include the user’s \_id from the database:

const token \= jwt.sign(  
  { \_id: user.\_id, email: user.email }, // Payload  
  process.env.JWT\_SECRET,  
  { expiresIn: '1d' }  
);

So, when the token is decoded in the middleware, req.user will contain:  
req.user \= { \_id: "123", email: "user@example.com" };  
Therefore, you access the user’s ID using req.user.\_id.

**2\. Why req.user.id?**  
Some developers prefer to use id instead of \_id in the JWT payload for simplicity.  
If the payload is structured like this:  
const token \= jwt.sign(  
  { id: user.\_id, email: user.email }, // Payload  
  process.env.JWT\_SECRET,  
  { expiresIn: '1d' }  
);

Then, when the token is decoded, req.user will contain:  
req.user \= { id: "123", email: "user@example.com" };  
In this case, you would use req.user.id.

**Which One Should You Use?**  
It depends on how the JWT payload is created:  
If the payload uses \_id:  
Use req.user.\_id.  
If the payload uses id:  
Use req.user.id.

**Best Practice**  
Be consistent with how you structure your JWT payload.  
If you’re using MongoDB/Mongoose, it’s common to use \_id because that’s the default field name for the unique identifier in the database.  
Example:  
const token \= jwt.sign(  
  { id: user.\_id, email: user.email }, // Payload  
  process.env.JWT\_SECRET,  
  { expiresIn: '1d' }  
);

Then, in your route:  
const id \= req.user.\_id; // Access \_id

**Why Not Both?**  
You can include both \_id and id in the payload if you want flexibility:  
const token \= jwt.sign(  
  { \_id: user.\_id, id: user.\_id, email: user.email }, // Include both  
  process.env.JWT\_SECRET,  
  { expiresIn: '1d' }  
);

Then, you can use either req.user.\_id or req.user.id in your code.

### Auth Flow:

![][image2]

### 

### Example for using another Object Reference:

We should write like this:  
**productId: {**  
        **type: mongoose.Types.ObjectId,**  
        **ref: "Product",**  
      **},**

The `ref: "Product"` establishes a relationship between the `Order` schema and the `Product` schema

const mongoose \= require("mongoose");

const OrderSchema \= new mongoose.Schema(  
  {  
    qty: {  
      type: Number,  
    },  
    total: {  
      type: Number,  
    },  
    userId: {  
      type: mongoose.Types.ObjectId,  
      ref: "user",  
    },  
    // productId: {  
    //   type: mongoose.Types.ObjectId,  
    //   ref: "Product",  
    // },  
    deliveryLocation: {  
      type: String,  
    },  
    expectedDeliveryDate: {  
      type: Date,  
    },  
    purchaseDate: {  
      type: Date,  
    },  
    deliveryStatus: {  
      type: String,  
      enum: \["delivered", "cancelled", "in-progress"\],  
      default: "in-progress",  
    },  
  },  
  {  
    timestamps: true,  
  }  
);

module.exports \= mongoose.model("Order", OrderSchema);

### **Multer Definition:**  Multer is a middleware for handling `multipart/form-data`, primarily used for uploading files in Node.js applications.

**Key Features:**

* Works with Express.js

* Supports single and multiple file uploads

* Allows file filtering and size limits

* Stores files in memory or disk

**Installation:**

`npm install --save multer`

**Basic Usage:**

// Configure storage settings for multer  
const storage \= multer.diskStorage({  
  // Set the destination folder for uploaded files  
  destination: function (req, file, cb) {  
    // Save files in the "/tmp/my-uploads" directory  
    cb(null, "/tmp/my-uploads");  
  },  
  // Define the naming convention for uploaded files  
  filename: function (req, file, cb) {  
    // Generate a unique suffix using the current timestamp and a random number  
    const uniqueSuffix \= Date.now() \+ "-" \+ Math.round(Math.random() \* 1e9);  
    // Set the file name as the field name plus the unique suffix  
    cb(null, file.fieldname \+ "-" \+ uniqueSuffix);  
  },  
});

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>