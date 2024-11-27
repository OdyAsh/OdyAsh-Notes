
When reading articles or documentations, you'll see that sometimes, "tokens" and "chunks" are treated as synonyms, but usually they represent different granularity levels. Demonstration by definitions:

Tokens:
* A token is the smallest unit of data that the NLP model processes, <mark style="background: #D2B3FFA6;">such as a sentence, a word, or a character</mark> (s1).
* It's a way to break down and analyze text into manageable components (s2).

Chunks:
* A chunk is a group of tokens ([s3](https://medium.com/@jeevanchavan143/nlp-tokenization-stemming-lemmatization-bag-of-words-tf-idf-pos-7650f83c60be#6f4c))
* For example, if we have this text: "Hello there! My name is OdyAsh     (new paragraph)    I like astronomy!", then depending on how you want to process this text, you might have one of these configurations:
	* tokens ⟺ sentences, chunks ⟺ paragraphs
	* tokens ⟺ words, chunks ⟺ sentences
	* tokens ⟺ words, chunks ⟺ group of nouns only (i.e., process the tokens so that they are grouped into chunks of noun phrases. Example: [s4](https://medium.com/greyatom/learning-pos-tagging-chunking-in-nlp-85f7f811a8cb#3049).
	* tokens ⟺ characters, chunks ⟺ words
	* tokens ⟺ characters, chunks ⟺ chunk size (i.e., 200 characters)
	* Examples: here: [s5](https://medium.com/@abdallahashraf90x/tokenization-in-nlp-all-you-need-to-know-45c00cfa2df7)

So, one might treat a chunk as a unit of data which the NLP model gains useful info from ([s4](https://medium.com/greyatom/learning-pos-tagging-chunking-in-nlp-85f7f811a8cb#3049)), and by chunking down, we get to the details of each chunk, i.e., the tokens which form this chunk (s6).

To summarize:
* Usually:
	* A chunk: a unit of data with a low granularity level.
	* A token: a unit of data with a high granularity level.
* Occasionally:
	* They are treated as the same thing.

# Sources

* s1: https://www.functionize.com/blog/understanding-tokens-and-parameters-in-model-training
* s2: https://www.quora.com/What-is-a-token-in-NLP
* s3: https://medium.com/@jeevanchavan143/nlp-tokenization-stemming-lemmatization-bag-of-words-tf-idf-pos-7650f83c60be
* s4: https://medium.com/greyatom/learning-pos-tagging-chunking-in-nlp-85f7f811a8cb
* s5: https://medium.com/@abdallahashraf90x/tokenization-in-nlp-all-you-need-to-know-45c00cfa2df7
* s6: https://excellenceassured.com/nlp-training/nlp-training-courses-online/how-can-nlp-help-me/chunking-chunking-chunking-across