Run:

git fetch origin
git log origin/beta-release --oneline --all --grep="alphasense obo"

You can also check whether your commit exists in beta-release:

git branch -r --contains 4dc38b2
