# CI/CD exercise

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

> [!IMPORTANT]
>
> - Linux / Mac shelsript, create a `up.sh` file in your working-folder
> - Windows command prompt, create a `up.bat` file in your working-folder

### 3.1 Simple CI/CD script

Now you can open your command prompt file to add following script:

> [!IMPORTANT]
> To create a commit message we need a variable in `git commit -m ""`.
>
> - Linux / Mac -> `$git commit -m "$*"`
> - Windows -> `$git commit -m "%*"`

```
git pull
git add .
git commit -m "%*"
git push
git ftp push
```

- `$git pull` Pull your Repository
- `$git add .` Add all changes to your stage
- `$git commit -m "%*"` Write a commit message. `%*` is a Variable on Windows
- `$git push Push` your changes in your repository
- `$git ftp push` Update your ftp-server

### 3.2 CI/CD script with Angular Framework

1. Create a Angular Project
2. Create in your Angular Project following files:

- `up.bat` for windows, `up.sh` for Linux/Mac
- `.git-ftp-include`

3. Edit `.git-ftp-include`:

```
!./dist/ci-cd-test
```

4. Edit `up.bat`

```
git pull
git add .
git commit -m "%*"
git push
call ng build
call git ftp push     Update your ftp-server
```

- `$call ng build` "call" waits for the current project to be build
- `$call git ftp push` Update your ftp-server

### 3.2 CI/CD script with via SSH

We need the following points for an SSH push:

1. a server on which we want to push
2. an account for the SSH connection

- Account name
- Account password

3. the server address

```
git add .
git commit -m "%*"
git push
ssh `"account-name"`@`"ip-address"` "cd da-services && sudo git pull && sudo ./env/bin/pip install -r requirements.txt"
```

> [!Note]
> Example: `ssh janedoe@34.65.211.91 "cd da-services && sudo git pull && sudo ./env/bin/pip install -r requirements.txt"`
>
>- `ssh`: Secure shell is a Internet Protocol
>- `janedoe`: Account name
>- `34.65.211.91`: Server ip address
>- `cd da-services`: navigate to destination folder
>- `sudo git pull`: super user do ...
>- `sudo ./env/bin/pip install -r requirements.txt`: installs your development environment

## 4. Run your "up.bat" or "up.sh"

1. Open your console
2. Navigate to your project folder
3. Write `$up "commit message"`, without ""
