**Git Book**: [https://git-scm.com/book/en/v2](https://git-scm.com/book/en/v2)

## Prerequisites
- `git config --global user.email "you@example.com"`
- `git config --global user.name "Your Name"`

## Create Git Repo
- `mkdir newDir`
- `cd newDir`
- `git init`
- `git add "file"`
- `git commit -m "This is a new file"`
- `git puhs` or `git push "repo_name" master`

## Commands within your Repo
- `git show [commit]`: show details of commit  (you need to use the commit hash)
```
#Example: `git show 58ace0476093d04023f84d7816adacfa7b879c43
#Output:
tree 58ace0476093d04023f84d7816adacfa7b879c43

css/
favicon.ico
footer.php
header.php
index.php
```
- `git cat-file -p [commit]`: get list of commit hashes
```
#git cat-file -p 58ace0476093d04023f84d7816adacfa7b879c43
#Output:
040000 tree b352dde43705f193d2c1d4e6f6a133321186869f    css
100644 blob f303c6a7797f5e7a0d5bd31d39a7149366bbf873    favicon.ico
100644 blob 5adab1a1c52dc009d4f26bbce30dacc4c93eea33    footer.php
100644 blob c3646db7f9c7e6f126c75900fdcce16d50e1da82    header.php
100644 blob 88beb94b5e1fc48e1625c89f892b04bffb58225c    index.php
```
- `git log --diff-filter=D --summary`: get ovewview of deleted commits
- `git show [deleted_commit]`: Show details of deleted commits

## Change Git Remote URL
- `git remote -v`: show existing URLs
- `git remote set-url "remote-name" "remote-url"`
   - `git remote set-url heroku https://git.heroku.com/example.git`

## Make Local Repo-Backup
- `cd /your/backup/dir`: move to your backup folder
- `git clone https://github.com/user/example`: download your repo
- If you need to update your local backup: `cd your/backup/dir` and `git pull https://github.com/user/example` 

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
   - Then enter: `git add yourfile.py` and `git commit -m "Use PORT from environment."`
```
import os

if __name__ == '__main__':
    port = int(os.environ.get('PORT', 8000))
    server_address = ('', port)
    httpd = ThreadHTTPServer(server_address, ClassName)
    httpd.serve_forever()
```
- Create your Heroku app: `heroku create yourAppName`
   - For instance, if you name your app silly-pony, it will appear on the web at https://silly-pony.herokuapp.com/ 
- Push your code to Heroku with Git: `git push heroku master`
- If something goes wrong with your server then check out the log file
   - `https://dashboard.heroku.com/apps/xxx/logs`, but replace "xxx" with your own app's name

## Retrieve Web Site Source Code
- `wget -r http://example.com/.git`: -r = recursively
- If you are lucky, directory listing is enabled and you can easily search through the git repository
- Otherwise you need to download subdirectories via trial&error
- Example: `wget -r http://example.com/.git/HEAD` or `wget -r http://example.com/.git/objects`
- Once you retrieve a commit you can look for its details at subdirectory "objects"
  - Example: `commit 58ace0476093d04023f84d7816adacfa7b879c43` may lead to `wget -r http://example.com/.git/objects/58/ace0476093d04023f84d7816adacfa7b879c43`
