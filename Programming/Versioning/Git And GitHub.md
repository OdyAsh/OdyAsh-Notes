# Add Large Files To GitHub Repo
([source](https://dev.to/iamtekson/upload-large-file-to-github-37me))

Run the following commands:

```cmd
git lfs install

git lfs track

git lfs push --all origin main

git add .
git commit -am "add large file"
git push -u origin main
```

note that the last 3 commands you can do from the VS Code interface

