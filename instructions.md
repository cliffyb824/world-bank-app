In this exercise, you'll deploy a web app to Heroku. The files you'll need are in the 5_deployment folder.

## RUN THE APP LOCALLY
1. Start the local server:
```bash
cd 5_deployment
python worldbank.py
```

2. Verify in the browser: In the terminal, use this command to get the link for vieweing the app:
```
env | grep WORK
```
The link wil be:
http://<WORKSPACESPACEID>-3001.<WORKSPACEDOMAIN> replacing WORKSPACEID and WORKSPACEDOMAIN with your values. Head to the deployment only if your app is running successfully locally. 



## DEPLOYMENT TO HEROKU PLATFORM
Create the Heroku account: Go to www.heroku.com and create an account if you haven't already. Then, follow the process given in the previous video:

1. Open a new terminal, and create the application folder:
```
cd 5_deployment/
mkdir web_app
mv -t web_app/ data/ worldbankapp/ worldbank.py  wrangling_scripts/ requirements.txt runtime.txt
```


2. Verify the Heroku installation:
```
heroku --version
curl https://cli-assets.heroku.com/install-ubuntu.sh | sh
```


3. Log into Heroku using the command:
```
heroku login -i
```


4. Remove app.run() from the worldbank.py file. Go into the 5_deployment folder with:

```
cd 5_deployment/web_app
touch Procfile
```

Put the following in the Procfile
```
web gunicorn worldbank:app
```

NOTE: For workspace users, the requirements.txt is already available in the exercise folder. In addition, we have also provided a runtime.txt file in the exercise folder, that declares the exact Python version number to use on the Heroku platform.


5. Initialize a git repository with the following ONE-TIME commands:
```
git init
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

Whenever you make any changes to your web_app folder contents, you will have to run git add and git commit commands.
```
git add .
git status
git commit -m "your message"
```


6. Create a uniquely named Heroku app. Use this command:
```
heroku create my-app-name --buildpack heroku/python
```
If you get a message that the app name is already taken, try again with a different app name until you find one that is not taken. Check that heroku added a remote repository with this command:
```
git remote -v
```

7. Set any environment variable to pass along with the push. Finally, push the app to Heroku:
```
heroku config:set SLUGIFY_USES_TEXT_UNIDECODE=yes
heroku config:set AIRFLOW_GPL_UNIDECODE=yes
heroku config
git push heroku master
```

Go to the link for your web app to see if it's working. The link should be https://app-name.heroku.com
