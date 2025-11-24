# create repo locally
mkdir mta-sts && cd mta-sts
git init
# create .well-known folder and mta-sts file
mkdir -p .well-known
cat > .well-known/mta-sts.txt <<'EOF'
version: STSv1
mode: enforce
mx: mx.example.com
max_age: 604800
EOF

# create staticwebapp.config.json
cat > staticwebapp.config.json <<'EOF'
{
  "routes": [
    {
      "route": "/.well-known/mta-sts.txt",
      "serve": "/.well-known/mta-sts.txt"
    }
  ]
}
EOF

git add .
git commit -m "Initial mta-sts files"
# create remote repo on GitHub (you can use gh CLI or create on web UI)
# using gh (optional): gh repo create yourusername/mta-sts --public --source=. --remote=origin
git remote add origin git@github.com:YOURUSER/mta-sts.git
git push -u origin main
