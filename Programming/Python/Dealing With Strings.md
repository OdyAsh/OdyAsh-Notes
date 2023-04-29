# Tips
## Remove Redundant Whitespaces

![[Pasted image 20230310205337.png|475]]

Notice that if we swapped the replace() functions, then one "|" would remain

## pre-allocate space for strings using ":<" in f-strings

```python
print(f'{var_a:<30}{var_b:<30}{var_c:<30}')
```

# Arabic

## Python Implicitly Reorders RTL

note: RLT == Right To Left

![[Pasted image 20230308200432.png|225]]
so if first element is in arabic, then jupyter notebook actually flips the content of the list when it is displayed, yet the indexing is the based on what was written in the code.

another example:
![[Pasted image 20230308200604.png|275]]
numbers also apply:
![[Pasted image 20230308200702.png|275]]

A little caveat about symbols:
![[Pasted image 20230308201426.png|275]]
but when extending other arabic letters:
![[Pasted image 20230308201503.png|300]]


however, if we introduce a non-arabic letter, notebook displays the continuous blocks of arabic letters from RTL, even though they are still indexed as what is seen in code:
![[Pasted image 20230308200855.png|275]]

This can lead to impossible-to-debug outputs:
![[Pasted image 20230308203432.png|450]]

solution: don't ever use english letters in arabic strings/lists (replace them with symbols or numbers or remove them, for example "a" here is switched to "1"):
![[Pasted image 20230308203518.png|400]]
(now this is kind of debug-able :D)

Other examples:

![[Pasted image 20230308193435.png|200]]


![[Pasted image 20230308193440.png|200]]

![[Pasted image 20230308193444.png|200]]

A more complex example:

![[Pasted image 20230308194442.png]]

![[Pasted image 20230308194953.png]]

output:
![[Pasted image 20230308195032.png]]


but if we remove {score:0.2f}, output will be: