# Python Regex

The regex in this line of code:
```python
model_version = re.findall(r'-?\d+(?:\.\d+)?', x)[0]
```
means: 
`-?` --> optionally lookup if "-" is there, and if so, return it also using findall()[0]
`(?:\.\d+)?` --> means that if you find decimal point value(s) (e.g., `2.2` instead of just `2`), then also match and return that

