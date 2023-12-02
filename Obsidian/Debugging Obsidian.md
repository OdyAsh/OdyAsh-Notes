# Dealing with GitHub and OneDrive setup

If you're working on one device, decide to commit and push, then kindly WAIT a while for the second device to sync the files (using OneDrive), THEN when OneDrive says everything is up to date, you can use `git pull` on the second device. This should tell you `Everything is up to date`.

# Lage Space between Note Title and text

If you see something like this:
![](./Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104065626.png)
Then disabling this plugin might help:
![](./Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104065706.png)

Also, this "Typewriter Scroll" might be responsible for Obsidian being slow when editing large markdown files.

# Images Appear in The Same Line When Viewing from GitHub

Example:
![](Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104084943.png)

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

check out [commits](https://github.com/OdyAsh/OdyAsh-Notes/commits/main/Mathematics/Linear%20Algebra/Vectors.md) on Nov 4, 2023, on the [Vectors.md](../Sciences/Formal%20Sciences/Mathematics/Linear%20Algebra/Vector.md) file, what I deduced from all these attempts are the following:

* Probably any equations that contain any form of matrix/vector (square brackets, parentheses. etc.) can NOT be rendered on the same line of text EVEN IF we're using `$$` instead of `$`.
	* In that case, you have to start a new line (that has `newline` before and after the equation), make it use `$$`, and it can NOT be in a bullet point.
* Use `\cr` instead of `\\` to signify `newline` in latex.
* don't use `{` and `}`, and use `\lbrace` and `\rbrace` instead.
* don't use `\vec{r}_{1}`, use `\vec{r}_1` instead.
* don't add spaces around `$$`, and don't add `newlines` between Latex. Example:
  
  ![](Attachments%20-%20Debugging%20Obsidian/Pasted%20image%2020231104170701.png)
More details about GitHub problems with MathJax is mentioned in [this](https://nschloe.github.io/2022/05/20/math-on-github.html) article.