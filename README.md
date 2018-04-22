# heroku-github
Example Node.JS app to deploy Heroku app from Github.

####Create project

    mkdir heroku-github
    cd heroku-github
    npm init

####Install express

    npm install --save express

####Create `index.js`

    const express = require("express");
    const app = express();
    const PORT = process.env.PORT || 3000;

    app.get("/", (req, res) => res.send("Hello World!"));

    app.listen(PORT, () => console.log(`Example app listening on port ${PORT}!`));
Note `process.env.PORT` is necessary to deploy in heroku

####Configure npm start in `package.json`
>heroku will run `npm start` on deploy. You can change this command by setting Procfile : [Heroku Procfile](https://devcenter.heroku.com/articles/procfile)

    "scripts": {
        "start": "node index.js"
    }

####Initialize Git and push to Github
    git init
    git add .
    git commit -am "Inital Commit"
    git remote add origin https://github.com/acc/heroku-github.git
    git push origin master
Replace `https://github.com/acc/heroku-github.git` with the git repository you want

####Initialize heroku
    heroku login
    heroku create heroku-github-deploy
`heroku-github-deploy` is the app name. Change this with desired app name or heroku will generate random name if null

####Set Deployment method
In your newly created `heroku-github-deploy` dashboard, go to 
>Deploy
>Choose `Github` in `Deployment method`
>Type in repository name : in this case `heroku-github`
>Search -> Connect


>Choose Enable Automatic Deploys if you want. `This will set heroku to deploy everytime you push a commit to github`
>Click DeployBranch and done
