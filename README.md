# An Express wrapper for React App
Express renders a React App by reading it's compiled public/index.html as a _static file_. All the development and design takes place withing the React App. The Express app (containing the React App) is then deployed to Heroku via GitHub.

The result is a ultra fast Single Page Application, in this case a music app. Simple, but able to scale into a fullstack MERN application as needed. 

### Development Style
Stand up the application end-to-end first, then build out the design. Instead of finishing the application on localhost and _then_ trying (and failing) to deploy it, scaffold and assure the deployment first.

### Development Environment
Open VScode, Bash terminal, and Chrome. Update Node and npm by downloading the LTS https://nodejs.org/en/ 

## Stand up Express
`mkdir website` begin in a workfolder
`npx express-generator nirvana` the app will be called "nirvana 

`cd nirvana`   
`npm install`  
`npm audit fix --force` run multiple times until complete

`npm start` runs the application from localhost on port 3000. You should see an Express welcome screen in the browser. Go ahead and stop the server

## Push to GitHub
`git add .`
`git commit -m 'initial commit`

Create a new GitHub repository called nirvana  
`git remote add origin git@github.com:dylannirvana/jj.git`  
`git push origin master`

You should see code in the repo

## Create a Heroku Pipeline
Create a new pipeline in Heroku containing a staging app and a production app, `nirvana-stage` and `nirvana-production`

Associate `nirvana-stage` with the `nirvana` repo on GitHub  

Turn on Automatic Deploys. And _deploy master_. You should see the Express welcome app on Staging. Go ahead and _promote_ it to Production

In the Pipeline, turn on Review App (built from `pull request`). This completes the first end-to-end with an Express application

## Stand up React App
`npx create-react-app@latest client` in nirvana directory  

`cd client`  You're in the nirvana/client directory now
`npm install`  
`npm audit fix --force` run multiple times until complete  

`npm start` runs the application from localhost on port 3000. Provided you stopped the previous process, you should see the React App welcome screen in the browser. Go ahead and stop the server 

## Get Express to render React App
Go back to the Express app
`cd ../`  you're now in the `nirvana` directory  

### bin/www  
Line 15, change port from 3000 to 5000 so it will render a proxy

### app.js
Comment out lines 13-14 on views  
line 20 static file 
lines 22-23 on routers  

line 22 add:  
<code>
  app.use(express.static(path.join(__dirname, 'client/build')));
  
  app.get('*', function(req, res) {
    res.sendFile(path.join(__dirname, 'client/build', 'index.html'));
  });
</code>

This will associate the React App's static file with Express  

### package.json
Make sure there is a start statement  
<code> 
  "scripts": {
    "start": "node ./bin/www"
  }, 
  </code>  

 > You _might_ need an engine statement 
  <code> 
  "engines": {
    "node": "18.x"
  }, 
  </code> 

### Stand React App up in Express
`npm start` in client to see React App on port 3000   

In another terminal window  
`cd ../` to nirvana  
`npm start` in nirvana to see Express on port 5000  
_You should see the React App from both ports in separate windows_  
   
### Push to GitHub and run in Heroku
Run this change end-to-end  
`git add .`
`git commit -m 'initial commit`
`git push origin master`

You should see an automatic deployment of the React App on `nirvana-stage`. Promote the app to `nirvana-production` 

_You are now running React App in an Express wrapper in Heroku_

### Tidy Up (optional)
`rm -R public/ routes/ views/` from nirvana  
`mv app.js server.js`  
line 7 in bin/www, change ../app to ../server  

***  

### Build the components/scenes
lorem

### Add content, assets, widgets
Add all copy, music widgets, video, ConvertKit, etc..

### Design the app with sass  
lorem

### Add agents, trackers
Facebook pixel  
Google Analytics  

## Change the DNS and Go Live 
Change the DNS and go live






