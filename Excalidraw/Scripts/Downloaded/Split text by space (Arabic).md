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
	var startOffset = el.x+el.width; // in Arabic, "+" makes text go right. the last Arabic letter is positioned at startOffset location
	var first = 1;
	sentence.forEach((word)=>{
		firstTerm = first*word.length*letterWidth;
		secondTerm = (1-first)*maxWordLetters*letterWidth;
		startOffset -= firstTerm + secondTerm;
		ea.addText(startOffset, el.y, word);
		first = 0;
		//startOffset -= 2*letterWidth;
	});
	
	//for(i=0;i<text.length;i++) {
	//ea.addText(el.x,el.y+i*el.height/text.length,text[i]);
	//}
});
ea.addElementsToView(false,false);
ea.deleteViewElements(elements);