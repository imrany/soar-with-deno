# soar-with-deno
Before you head over to the final step, install the VSCode plugin, SQLite Viewer. You can use this SQLite Viewer plugin to observe the changes in the database while you follow the instructions below.

#### 1 Generate a new TOKEN.

Run the following command.
```bash
deno run generateToken.ts
```
Paste the token to the `.env` to `API_KEY="TOKEN"`

#### 2 Start backend server
```bash
deno run -A main.ts
```

#### 3 Open a new terminal. Register a user with your StackUp username using curl command. Replace "StackUpUsername" with your StackUp username before running the command below.

```bash
curl -i -XPOST -d '{"username": "StackUpUsername", "password": "123"}' --url http://127.0.0.1:5555/register 
```

#### 4 Login the new user that has your StackUp Username

```bash
curl -i -XPOST -d '{"username": "StackUpUsername", "password": "123"}' --url http://127.0.0.1:5555/login --cookie-jar cookie.cookie
```
There will be a file created called cookie.cookie. Open the file. Copy the JWT signature from the cookie. See screenshot below for what it looks like. You must copy the WHOLE string.

#### 5 Update the user's username by appending "-Ready-For-Submission" e.g. 
"StackUpUsername-Ready-For-Submission". Replace "yourJWTString" with your JWT signature you copied previously before running the command below.
```bash
curl -i -XPUT -d '{"username": "StackUpUsername-Ready-For-Submission", "password": "123"}' --url http://127.0.0.1:5555/auth/update --cookie cookie.cookie -H "Authorization: Bearer yourJWTString"
```
You have to relogin after this with the new username. Replace "StackUpUsername" with your StackUp username before running the command below.
```bash
curl -i -XPOST -d '{"username": "StackUpUsername-Ready-For-Submission", "password": "123"}' --url http://127.0.0.1:5555/login --cookie-jar cookie.cookie
```
Copy the new JWT signature in cookie.cookie.

#### 6 Delete the user by calling the appropriate route path. 
Replace "yourJWTString" with your JWT signature you copied previously before running the command below.
```bash
curl -i -XDELETE --url "http://127.0.0.1:5555/auth/delete" --cookie cookie.cookie -H "Authorization: Bearer yourJWTString"
```
