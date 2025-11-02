# SSH mirror from forgejo to remote repo

1. edit conf
   `nano /forgejo/gitea/conf/app.ini`
2. add

```
[migrations]
ALLOWED_DOMAINS = *.github.com,github.com,gitlab.com
```

3. add ssh url from remote repo to settings of forgejo repo
4. username and password leave empty
5. check: use ssh auth
6. check: sync when commits are pushed
7. add pushed mirror

Sources
https://forgejo.org/docs/latest/user/repo-mirror/#pushing-to-a-remote-repository
https://github.com/go-gitea/gitea/issues/19966
https://docs.gitea.com/next/administration/config-cheat-sheet
