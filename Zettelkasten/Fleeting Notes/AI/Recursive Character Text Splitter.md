#ai #nlp #chunking
# Explanation by Example

Example text:

```python
text = """What I Worked On

February 2021

Before college the two main things I worked on, outside of school, were writing and programming. I didn't write essays. I wrote what beginning writers were supposed to write then, and probably still are: short stories. My stories were awful. They had hardly any plot, just characters with strong feelings, which I imagined made them deep.

The first programs I tried writing were on the IBM 1401 that our school district used for what was then called "data processing." This was in 9th grade, so I was 13 or 14. The school district's 1401 happened to be in the basement of our junior high school, and my friend Rich Draves and I got permission to use it. It was like a mini Bond villain's lair down there, with all these alien-looking machines — CPU, disk drives, printer, card reader — sitting up on a raised floor under bright fluorescent lights.
"""
```


For our text splitter, we'll consider a chunk size of 100 characters and the order of the characters used for splitting will be `my_splitter_order = ['\n\n', '\n', ' ', '' ]`.

Overview logic of recursive splitting:
1. Get all the text (for later consistency, let's call it a "level-0 (L0) substring", where this substring == the whole string):
   
   ![](Media-Temp/Pasted%20image%2020240606211822.png)
   
2. Sequentially merge these L0 substrings as long as their size is less than `chunk_size` parameter.
	2. Now, since this L0 substring is more than `chunk_size` (i.e., 100) characters, we won't merge it with any other substrings.
		1. Side note: I know there aren't "any other substrings" in the first place, I'm just explaining the algorithm, since this logic will repeat in future steps, so bear with me :].
3. For each of the L0 substrings (which is only one) we split it based on the first character in `my_splitter_order` (i.e., `\n\n`) into level-1 (L1) substrings :
   
   ![](Media-Temp/Pasted%20image%2020240606204544.png)
   
4. Sequentially merge these L1 substrings as long as their size is less than `chunk_size` parameter (i.e., 100):
   
   ![](Media-Temp/Pasted%20image%2020240606204705.png)
   
	1. As we can see, ***if*** we have added the third L1 substring (i.e., `\n\nBefore college the ...`), ***then*** the merged string would've been > 100, ***so we stopped*** at merging ***the first two*** L1 substrings.
5. For each of the other L1 substrings, apply the character splitter next in order of `my_splitter_order` (i.e., `\n`) to get L2 substrings:
   
   ![](Media-Temp/Pasted%20image%2020240606205145.png)
   
6. Sequentially merge these L2 substrings as long as their size is less than `chunk_size` parameter.
	1. As you can deduce, no merging will occur, since each L2 substring is already more than `chunk_size` characters.
7. For each of the L2 substrings, apply the character splitter next in order of `my_splitter_order` (i.e., whitespace: ` `) to get L3 substrings:
   
   ![](Media-Temp/Pasted%20image%2020240606210017.png)
   
8. Sequentially merge these L3 substrings as long as their size is less than `chunk_size` parameter:
   
   ![](Media-Temp/Pasted%20image%2020240606210235.png)
   
9. For each of the L3 substrings, apply the character splitter next in order of `my_splitter_order` (i.e., empty string) to get L4 substrings.
	1. Note: basically, when we choose an empty string as a splitting character, we're basically saying "split everything into single characters. For example: potato will be `[p,o,t,a,t,o]`". 
	2. However, since all L3 substrings (of the two L2 substrings) are <= `chunk_size`, therefore we won't split any further.
10. Finally, concatenate all of these L3 substrings with the L1 substring previously mentioned to get these final chunks:
   
   ![](Media-Temp/Pasted%20image%2020240606211129.png)
   

## Visualized Summary

![](Media-Temp/Pasted%20image%2020240606225909.png)


Draft (incomplete and might be inaccurate) (TODO):
The steps above can be summarized in the following points:
1. Check if <= `chunk_size`
	1. If yes, move to step 2.
	2. If no, split into substrings based on the `i-th` special character splitter next in line.
	3. `i += 1`
	4. Merge substrings as long as <= `chunk_size`
	5. For each of these merged substrings, repeat 1.1 till 1.5.
2. 

# Sources

s1: https://dev.to/eteimz/understanding-langchains-recursivecharactertextsplitter-2846