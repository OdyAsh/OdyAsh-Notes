# Tips
## Remove Redundant Whitespaces

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230310205337.png)

Notice that if we swapped the replace() functions, then one "|" would remain

## pre-allocate space for strings using ":<" in f-strings

```python
print(f'{var_a:<30}{var_b:<30}{var_c:<30}')
```

# Arabic

## Python Implicitly Reorders RTL

note: RLT == Right To Left

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308200432.png)
so if first element is in arabic, then jupyter notebook actually flips the content of the list when it is displayed, yet the indexing is the based on what was written in the code.

another example:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308200604.png)
numbers also apply:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308200702.png)

A little caveat about symbols:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308201426.png)
but when extending other arabic letters:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308201503.png)


however, if we introduce a non-arabic letter, notebook displays the continuous blocks of arabic letters from RTL, even though they are still indexed as what is seen in code:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308200855.png)

This can lead to impossible-to-debug outputs:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308203432.png)

solution: don't ever use english letters in arabic strings/lists (replace them with symbols or numbers or remove them, for example "a" here is switched to "1"):
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308203518.png)
(now this is kind of debug-able :D)

Other examples:

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308193435.png)


![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308193440.png)

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308193444.png)

A more complex example:

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308194442.png)

![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308194953.png)

output:
![](Attachments%20-%20Dealing%20with%20Strings/Pasted%20image%2020230308195032.png)


but if we remove {score:0.2f}, output will be: