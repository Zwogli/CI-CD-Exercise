# CI/CD Test

In this particular repository I'm taking my first steps in continuous integration and continuous development, using git-ftp as well.

## Simple CI/CD Practice with none Framework on Windows

1. Create a `up.bat` in your working-folder
2. Open your `up.bat` file and write without @Rem:

```
git pull                @Rem Pull your Repository
git add .               @Rem Add all changes to your stage
git commit -m "%*"      @Rem Write a commit message. %* is a Variable on Windows
git push                @Rem Push your changes in your repository
git ftp push            @Rem Update your ftp-server
```
