# CI/CD Test

In this particular repository I'm taking my first steps in continuous integration and continuous development, using git-ftp as well.

## Git-ftp -- uploads to FTP servers the Git way

> If you use Git and you need to upload your files to an FTP server, Git-ftp can save you some time and bandwidth by uploading only those files that changed since the last upload.

> It keeps track of the uploaded files by storing the commit id in a log file on the server. It uses Git to determine which local files have changed.

> You can easily deploy another branch or go back in the Git history to upload an older version.

```
# Setup
git config git-ftp.url "ftp://ftp.example.net:21/public_html"
git config git-ftp.user "ftp-user"
git config git-ftp.password "secr3t"

# Upload all files
git ftp init

# Or if the files are already there
git ftp catchup

# Work and deploy
echo "new content" >> index.txt
git commit index.txt -m "Add new content"
git ftp push
# 1 file to sync:
# [1 of 1] Buffered for upload 'index.txt'.
# Uploading ...
# Last deployment changed to ded01b27e5c785fb251150805308d3d0f8117387.
```

## CI/CD Practice with none Framework on Windows

1. Create a `up.bat` in your working-folder
2. Open your `up.bat` file and write without @Rem:

```
git pull                @Rem Pull your Repository
git add .               @Rem Add all changes to your stage
git commit -m "%*"      @Rem Write a commit message. %* is a Variable on Windows
git push                @Rem Push your changes in your repository
git ftp push            @Rem Update your ftp-server
```

## CI/CD Practice with Angular Framework on Windows

1. Create a Angular Project
2. Create in yout Angular Project following files:

- up.bat
- .git-ftp-include

3. Edit ".git-ftp-include":

```
!./dist/ci-cd-test
```

4. Edit "up.bat"

```
git pull              @Rem Pull your Repository
git add .             @Rem Add all changes to your stage
git commit -m "%*"    @Rem Write a commit message. %* is a Variable on Windows
git push              @Rem Push your changes in your repository
call ng build         @Rem "call" waits for the current project to be build
call git ftp push     @Rem Update your ftp-server
```
