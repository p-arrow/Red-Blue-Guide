## Prerequisites
- `git config --global user.email "you@example.com"`
- `git config --global user.name "Your Name"`

## Create Git Repo
- `mkdir newDir`
- `cd newDir`
- `git init`
- `git add "file"`
- `git commit -m "This is a new file"`
- `git push "repo_name" master`

## Change Git Remote URL
- `git remote -v`: show existing URLs
- `git remote set-url "remote-name" "remote-url"`
   - `git remote set-url heroku https://git.heroku.com/example.git`

## Make Local Repo-Backup
- `cd /your/desired/dir`: move to your backup folder
- `git clone https://github.com/user/project.git`: download your repo
- `cd repoDir` and `git pull`: update your local repo

## Set Up WebService with Heroku
- Check your server code into a new local Git repository
   - `git init`
   - `git add yourFile.py`
   - `git commit -m "Checking in my file!"`
- Sign up for a free Heroku account: [https://signup.heroku.com/dc](https://signup.heroku.com/dc)
- Download the Heroku command-line interface: [https://devcenter.heroku.com/articles/heroku-cli](https://devcenter.heroku.com/articles/heroku-cli)
   - This will make `heroku` available in your shell 
- Authenticate the Heroku CLI with your account. Enter: `heroku login`
   - It will prompt you for your username and password; use the ones that you just set up when you created your account
- Create configuration files:
   - `Procfile`: used by Heroku to specify the command line for running your application ([see here](https://devcenter.heroku.com/articles/procfile))
   - `requirements.txt`: to install dependencies of your application that aren't in the Python standard library
   - `runtime.txt`: tells Heroku what version of Python you want to run
   -  and check them into your Git repository
- Modify your server to listen on a configurable port
   - Add below code to your server file 
   - Then add: `git add yourfile.py` and `git commit -m "Use PORT from environment."`
```
import os

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 8000))
    server_address = ('', port)
    httpd = ThreadHTTPServer(server_address, ClassName)
    httpd.serve_forever()
```
- Create your Heroku app: `heroku create yourAppName`
- Push your code to Heroku with Git: `git push heroku master`
