# Initialize Git repository
git init

# Add a README file
echo "# Chatbot Project" > README.md

echo "This is a chatbot project using NLP and AI technologies." >> README.md

git add README.md

git commit -m "Initial commit with README"

# Create a .gitignore file
echo "# Ignore system files
.DS_Store
*.log
node_modules/
__pycache__/
.env
" > .gitignore

git add .gitignore

git commit -m "Added .gitignore file"

# Create project folders
mkdir backend frontend assets

touch backend/server.py frontend/index.html

echo "print('Chatbot server running')" > backend/server.py

echo "<html><body><h1>Chatbot Interface</h1></body></html>" > frontend/index.html

# Add all files to Git
git add .
git commit -m "Initial project structure"

# Instructions to push to GitHub
echo "
To push your project to GitHub:
1. Create a repository on GitHub.
2. Run: git remote add origin <your-repo-url>
3. Run: git branch -M main
4. Run: git push -u origin main
"
