**Commit:**

git add .
git commit -m "Initial commit"

**Push:**

git branch -M main
git remote add origin git@github.com:username/your-project-name.git
git push -u origin main


**Pull (new):**

cd ~/coding
git clone git@github.com:username/your-project-name.git



**"normal workflow"**
git pull
# edit with nvim
git add .
git commit -m "what changed"
git push


**Starting server with npm**

1. npm init -y

2. (in package.json file) add:

   "scripts": {
        "start": "node index.js"
    } 

3. Start: npm start

4. Stop: Ctrl + C


**Setting up github**

1. Configure Git (required once for root)
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
Verify:

git config --global --list. 

2. Initialize Git
git init

3. Add a .gitignore
nvim .gitignore

4. Commit your code

5. Create a GitHub repository

On GitHub:

New repository

Same name as your project

Do not initialize with README

Copy the SSH URL, it will look like:

git@github.com:username/your-project-name.git

6. Set up SSH for root (very important)

As root:

ssh-keygen -t ed25519 -C "youremail@example.com"

7. Add key to GitHub:

cat /root/.ssh/id_ed25519.pub

Paste into:

GitHub → Settings → SSH and GPG keys → New SSH keys

8. Push to GitHub
git branch -M main
git remote add origin git@github.com:username/your-project-name.git
git push -u origin main

**Creating new user (not root)**

1. 👉 Create a normal user and stop using root:

adduser yourname
usermod -aG sudo yourname

2. Then:

su - yourname
mkdir ~/coding
