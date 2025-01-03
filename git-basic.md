---
marp: true
theme: uncover
class:
  - lead
---

![](https://miro.medium.com/v2/resize:fit:640/format:webp/0*pUHGatJv-HzVc2ZZ.jpg)

---

### Why do we need version control?

1. Collaboration
2. Backup
3. History
4. Experimentation
5. Deployment
6. Code review

---

## Config

```bash
git config --global user.name "Your Name"
git config --global user.email "your@mail"
```

---

## Create / Clone

```bash
git init
# OR
git clone <url>
```

---

## Remote

![bg left:60% 100%](https://git-scm.com/book/en/v2/images/remote-branches-2.png)

```bash
git remote add origin <url>
git push -u origin master
```

---

## Staging area

```bash
git add .
git add <file>
```

---

## Viewing File changes

```bash
git status
git diff
```

---

## Commit

```bash
git commit -m "message"
```

1. Add prefixes to commit message (fix, feat, config, other).

   Example: `feat: Carousel component added.`

2. Multiline commit message for multiple changes.
   Example:
   ```
   feat: Carousel component added.
   fix: Header text overflow.
   ```

---

## Log

```bash
git log
```

---

## Branches

```bash
git branch
git branch <branch-name>
git checkout <branch-name>
# Create and checkout
git checkout -b <branch-name>
```

---

## Fetch, pull, push

```bash
git fetch
git pull
git push
```

---

## Merge

```bash
git merge <branch-name>
```

---

## Cherry pick

```bash
git cherry-pick <commit-hash>
```

---

## Conflicts

---

VS code extensions

[GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
[Git Graph](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)
[Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
[Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)

---

## Azure devops practices in PRO

1. Branch policies
2. Pull request
   - Add Work Items.
   - Add Prefix in title.
   - Add Description on what to test.
   - Add Reviewers
   - Set Auto complete.
3. Code review
4. CI/CD
5. Work items

<style style="display:none">
:root {
    --color-background: #000;
    --color-foreground: #fff;
    --color-background-code: #00000088;
    --color-highlight: #f00;
    --color-dimmed: #f00;
  }
  section{
    background-image: url('https://images.unsplash.com/photo-1618556450991-2f1af64e8191?q=80&w=1964&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D');
  }
  a{
    color:#fff;
    border-bottom: 1px dotted #fff;
  }
</style>
