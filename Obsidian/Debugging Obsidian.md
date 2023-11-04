# Lage Space between Note Title and text

If you see something like this:
![](./Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104065626.png)
Then disabling this plugin might help:
![](./Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104065706.png)

Also, this "Typewriter Scroll" might be responsible for Obsidian being slow when editing large markdown files.

# Images Appear in The Same Line When Viewing from GitHub

Example:
![](Media/Pasted%20image%2020231104084943.png)

Solution:
Install [this](https://github.com/Gru80/obsidian-regex-replace) plugin from obsidian, then type the following in find:
`(?<!<br>)(\!\[.*?\]\(.*?\.\w{3}\)|\[\[.*?\.\w{3}\]\])(?<!<br>)`
(without the backtick symbols at the start and the end)
and type the following in replace:
`<br>$1<br>`
(without the backtick symbols at the start and the end)

Now, if for some reason, you want to remove the `<br>` tags surrounding images, type this in find:
`(<br>)(\!\[.*?\]\(.*?\.\w{3}\)|\[\[.*?\.\w{3}\]\])(<br>)`
and this in replace:
`$2`

