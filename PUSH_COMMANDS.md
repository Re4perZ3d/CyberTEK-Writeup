# Push commands

After creating a new GitHub repo named `CyberTEK-Writeup`, run:

```bash
git clone https://github.com/Re4perZ3d/CyberTEK-Writeup.git
cd CyberTEK-Writeup
cp -r /path/to/extracted/CyberTEK-Writeup/* .
git add .
git commit -m "Add Operation GhostVein writeup"
git push origin main
```

Or with GitHub CLI:

```bash
gh repo create Re4perZ3d/CyberTEK-Writeup --public --description "Operation GhostVein — CyberTEK DFIR writeup"
git init
git add .
git commit -m "Add Operation GhostVein writeup"
git branch -M main
git remote add origin https://github.com/Re4perZ3d/CyberTEK-Writeup.git
git push -u origin main
```
