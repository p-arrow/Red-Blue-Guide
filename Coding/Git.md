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
