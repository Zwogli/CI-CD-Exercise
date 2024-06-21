# CI/CD Test

In this particular repository I'm taking my first steps in continuous integration and continuous development, using git-ftp as well.

## 1. Install git-ftp

Install git-ftp Install git-ftp by following the instructions at (https://github.com/git-ftp/git-ftp/tree/master).

## 2. Git-ftp setup

Follow up to the Declaration (https://github.com/git-ftp/git-ftp/tree/master).
Below are the code snippets:

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

## 3. CI/CD Practice with command prompt file

In the first Step you must create a command prompt file in your project. There are differences depending on the operating system:

### Linux / Mac shelscript

Create a `up.sh` in your working-folder

### Windows command prompt

Create a `up.bat` in your working-folder

## 4. CI/CD Script

Now you can open your command prompt file to add following script:

> [!IMPORTANT]
> To create a commit message we need a variable in git commit -m "".
> - Linux / Mac -> $git commit -m "$_"
> - Windows -> $git commit -m "%_"

```
git pull
git add .
git commit -m "%*"
git push
git ftp push
```

- $git pull Pull your Repository
- $git add . Add all changes to your stage
- $git commit -m "%_" Write a commit message. %_ is a Variable on Windows
- $git push Push your changes in your repository
- $git ftp push Update your ftp-server

## CI/CD Practice with Angular Framework on Windows

1. Create a Angular Project
2. Create in yout Angular Project following files:

- up.bat
- .git-ftp-includeöö

3. Edit ".git-ftp-include":

```
!./dist/ci-cd-test
```

4. Edit "up.bat"

```
git pull              > Pull your Repository
git add .             > Add all changes to your stage
git commit -m "%*"    > Write a commit message. %* is a Variable on Windows
git push              > Push your changes in your repository
call ng build         > "call" waits for the current project to be build
call git ftp push     > Update your ftp-server
```

## Run your "up.bat"

1. Open your console
2. Navigate to your project folder
3. Write $up "commit message", without ""
