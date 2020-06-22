I was initally having a hard time trying to figure out how to import a repo from a local machine into Azure Devops. After some searching I found out that the following commands will do the trick (must be done from the local directory):

```
git init
git remote add origin <URL for Azure Git repo>
git add .
git commit -m 'initial commit'
git push -u origin master
```
'origin' must also be changed to something unique like 'upstream', 'myorigin', etc.

