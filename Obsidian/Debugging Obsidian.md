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

# MathJax/Latex Compatibility with GitHub

check out [commits](https://github.com/OdyAsh/OdyAsh-Notes/commits/main/Mathematics/Linear%20Algebra/Vectors.md) on Nov 4, 2023, on the [Vectors.md](../Mathematics/Linear%20Algebra/Vectors.md) file, what I deduced from all these attempts are the following:

* Probably any equations that contain any form of matrix/vector (square brackets, parentheses. etc.) can NOT be rendered on the same line of text EVEN IF we're using `$$` instead of `$`.
	* In that case, you have to start a new line (that has `newline` before and after the equation), make it use `$$`, and it can NOT be in a bullet point.
* Use `\cr` instead of `\\` to signify `newline` in latex.
* don't add spaces around `$$`, and don't add `newlines` between Latex. Example:
  
  ![](Media-Temp/Pasted%20image%2020231104170701.png)
   
