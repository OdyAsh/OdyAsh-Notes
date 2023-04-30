/*
## requires Excalidraw 1.5.1 or higher

```javascript
*/
elements = ea.getViewSelectedElements().filter((el)=>el.type==="text");
elements.forEach((el)=>{
	ea.style.strokeColor = el.strokeColor;
	ea.style.fontFamily  = el.fontFamily;
	ea.style.fontSize    = el.fontSize;
	const sentence = el.text.split(" ");
	
	var totalLetters = sentence.length; // number of whitespaces
	var maxWordLetters = 0;
	sentence.forEach((word)=>{
	  totalLetters += word.length;
	  maxWordLetters = maxWordLetters > word.length ? maxWordLetters : word.length;
	});
	
	// letterWidth <=> approximate width of letter in sentence
	var letterWidth = el.width / totalLetters;
	var startOffset = el.x; // in English, "+" makes text go right. the first English letter is positioned at startOffset location
	sentence.forEach((word)=>{
		ea.addText(startOffset, el.y, word);
		wordLength = maxWordLetters*letterWidth;
		startOffset += wordLength;
		//startOffset -= 2*letterWidth;
	});
	
	//for(i=0;i<text.length;i++) {
	//ea.addText(el.x,el.y+i*el.height/text.length,text[i]);
	//}
});
ea.addElementsToView(false,false);
ea.deleteViewElements(elements);