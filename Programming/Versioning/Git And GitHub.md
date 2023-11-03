# Add Large Files To GitHub Repo
([source](https://dev.to/iamtekson/upload-large-file-to-github-37me))

Run the following commands:

```cmd
git lfs install

git lfs track --filename [file path]

git lfs push --all origin main

git add .
git commit -am "add large file"
git push -u origin main
```

note that the last 3 commands you can do from the VS Code interface

# Remove a String From Commit History

Note: this is currently not working; I still see the string in the commit history

```bash
git filter-branch --tree-filter "if [ -f .obsidian/plugins/obsidian-excalidraw-plugin/data.json ]; then sed -i 's/THE-KEY/YOUR-API-KEY/' .obsidian/plugins/obsidian-excalidraw-plugin/data.json; fi" HEAD~10..HEAD
```

or 

```bash
git filter-branch --tree-filter "find . -type f -exec sed -i 's/THE-KEY/YOUR-API-KEY/' {} \;" HEAD~10..HEAD
```

