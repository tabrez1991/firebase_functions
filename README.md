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
`cd Desktop`
3. Make a folder item-list-server.<br/>
`mkdir item-list-server`
4. Go to the folder.<br/>
`cd item-list-server`
5. Install the Firebase CLI.<br/>
`npm install -g firebase-tools`
If command fails use <br/>
`sudo npm install -g firebase-tools`
6. Run firebase login.<br/>
`firebase login`
7. Allow firebase to collect anonymous cli usage and error reporting information?<br/>
`yes`
8. This will open your browser for login with firebase. Choose your account and login.
9. Run firebase init functions.<br/>
`firebase init functions`
10. This will show a list of all your projects, use the arrow key to select your project.
11. What language would you like to use to write Cloud Functions?<br/>
`Javascript`
12. Do you want to use ESLint to catch probable bugs and enforce style?<br/>
`n`
13. Do you want to install dependencies with npm now?<br/>
`y`
14. This will setup the project and install all the dependencies.
15. Now, go to the functions folder<br/>
`cd functions`
16. Open the index.js file and insert the following code snippet.
