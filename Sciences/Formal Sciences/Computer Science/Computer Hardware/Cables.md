Main sources: [source 1](https://www.audiogrounds.com/audio-cable/), [source 2](https://www.pianodreamers.com/audio-cables-guide/), [source 3](https://www.pugetsystems.com/support/guides/trs-and-trrs-oh-and-trrrs-2255)

# Terminologies

## Jacks and Plugs (F/M Connectors/Sockets)

![](Attachments%20-%20Cables/Pasted%20image%2020231129125137.png)

* The fixed part of the connection is called JACK. 
* What you plug into a jack is called PLUG.

## Balanced and Unbalanced Audio Cables

* Audio cables can be:
	* balanced (and unbalanced, [source](https://www.audiogrounds.com/audio-cable/#:~:text=Some%20audio%20cable%20types%20can%20be%20both%20balanced%20and%20unbalanced%2C%20depending%20on%20the%20purpose%2C%20while%20others%20are%20always%20unbalanced))
	* unbalanced
* Unbalanced audio cables (UACs) have 1 wire and shield (ground), while balanced audio cables (BACs) have 2 wires and shield. Visualization:
  
  ![](Attachments%20-%20Cables/Pasted%20image%2020231129130757.png)
  
* A BAC requires devices with balanced output/input stages ([source](https://www.eetimes.com/cross-coupled-output-stages-for-balanced-audio-interfaces/#:~:text=At%20the%20source%2C%20a%20balanced,difference%20between%20the%20two%20signals.)).
	* At the source, a *balanced output stage (BOS)* **differentially drives** two signal wires
		* with equal and opposite signal voltage waveforms (theoretically). 
	* At the receiver, a *balanced input stage (BIS)* **extracts the difference** between the two signals.
* In BACs, the 2 wires transmit the same audio signal, such that:
	* The original signal is called hot signal (+)
	* The other one has a 180° phase shift, and thus, it has multiple terms:
		* cold signal (-)
		* reverse polarity signal
		* phase-shifted signal
	* Any noise signals resulting from electric interference (e.g., [EMI, RFI](https://www.eastcoastshielding.com/difference-between-emi-shielding-rfi-shielding.php), etc.) is almost completely induced.
		* This happens as the receiver's BIS cancels the identical noise signals in both wires, while it amplifies the audio signals in the 2 wires (as $x - (-x) = 2x$) ([source](https://www.audiogrounds.com/audio-cable/#:~:text=While%20the%20signal%20travels,for%20most%20home%20applications.)). Visualization:
		  
		  At the source's BOS:
		  
		  ![](Attachments%20-%20Cables/Pasted%20image%2020231129134331.png)
		  
		  At the receiver's BIS: the cold signal is flipped, which effectively eliminates the noise and outputs a clean audio signal:
		  
		  ![](Attachments%20-%20Cables/Pasted%20image%2020231129134349.png)
		  
		* The "noise-free" sound that BACs provide is apparent if the cable is more than 3 meters. Otherwise, UACs provide a similar "noise-free" experience.
* BAC is relatively more expensive than UACs.

Cable examples of BACs vs UACs:

|BALANCED AUDIO CABLES|UNBALANCED AUDIO CABLES|
|---|---|
|¼” or 3.5mm TRS (mono audio)|¼” TS|
|XLR|¼” and 3.5mm TRS (stereo audio)|
|¼” and 3.5mm TRRS (stereo, no mic)|¼” and 3.5mm TRRS (stereo + mic)|
||RCA|
|Balanced Headphone Cables|SpeakON|
|4-Pin XLR||
|Dual 3-Pin XLR||
|2.5mm TRRS Cable||
|4.4mm 5-Pole Pentaconn (Sony)|

Note: some of these cable types will be explained later.

More information about BACs vs UACs is provided [here](https://www.youtube.com/watch?v=rgfZb1pEIrU).

## Analog vs Digital

* Analog cables (AC) ([source](https://www.pianodreamers.com/audio-cables-guide/))
	* Work by sending information via a stream of electricity (an electrical signal/impulse) from one point to another.
	* Can be further categorized based on its balance state and level.
* Digital cables (DC)
	* Work by sending information via a stream of binary code (1s and 0s) from one point to another.
	* Examples: MIDI, USB, Thunderbolt, Firewire, Optical, etc.
* Both audio cable types are designed for specific purposes and shouldn’t be mixed. Mixing them won't damage your equipment, but the results won’t be perfect. ([source](https://www.audiogrounds.com/audio-cable/#:~:text=damage%20your%20equipment%2C%20but%20the%20results%20won%E2%80%99t%20be%20perfect.)) 
	* In some scenarios, using digital cables (DCs) instead of analog cables (ACs) can give surprisingly clean results!
	* However, using ACs instead of DCs will cause audio jitters/distortion due to the presence of relatively high impedance in DCs' [jacks](#Jacks%20and%20Plugs%20(F/M%20Connectors/Sockets)).
* Some digital and analog cables may look the same at first glance. For example:
  
    ![](Attachments%20-%20Cables/Pasted%20image%2020231129135600.png)
    
    Other times, the difference is clear, for example ([source](https://emastered.com/blog/audio-cable-types)):
    
    ![](Attachments%20-%20Cables/Pasted%20image%2020231129140239.png)

Examples of ACs vs DCs:

|ANALOG CABLES|DIGITAL AUDIO CABLES|
|---|---|
|TS Cables|S/PDIF Optical TOSLINK Cable|
|TRS Cables|S/PDIF Digital Coaxial Cable|
|TRRS Cables|USB Cables|
|RCA Cables|HDMI Cables|
|Speaker Cables|MIDI Cables|
|XLR Cables|ADAT Cables|
|SpeakON Cables|AES/EBU|

### Analog Cable Types

#### TS Cable

* Tip-Sleeve.
* Connects instruments.
* Transmits mono audio signals only.
* Is always [unbalanced](#Balanced%20and%20Unbalanced%20Audio%20Cables).

#### TRS Cable

* Tip-Ring-Sleeve.
* Can transmit:
	* balanced mono signals
		* used for microphones.
	* unbalanced stereo signals
		* used for headphones.

#### TRRS Cable

* Tip-Ring-Ring-Sleeve.
* Can transmit:
	* balanced stereo signals
		* this will have 4 wires: three audio signal wires, and shielding. 
	* unbalanced stereo signals + mono mic signal
		* this is more common.
		* this will have 4 wires: two audio signal wires, one mic signal, and shielding. 

#### TS vs TRS vs TRRS (and TRRRS)

|TYPE|UNBALANCED|BALANCED|STEREO|MONO|MIC|
|---|---|---|---|---|---|
|TS|Yes|No|No|Yes|No|
|TRS|Yes|Yes|Yes (Unbalanced)|Yes (Bal.)|No|
|TRRS|Yes|Yes|Yes (Bal. w/o mic)|Yes (Bal.)|Yes|

Finally, there's a balanced TRRRS with a matching 4.4mm TRRRS connector called Pentaconn. This connector was developed by [NIPPON DICS](https://www.ndics.com/en/products/pentaconn/), and it’s currently used by SONY and [Sennheiser headphones](https://www.audiogrounds.com/pair-sennheiser-headphones/), headphone amps, and digital audio players.

More details are in [this](https://www.youtube.com/watch?v=m4hy63fEgA0) video.

![](Attachments%20-%20Cables/Pasted%20image%2020231129155954.png)

([source](https://www.google.com/search?q=ts+trs+trrs&sca_esv=586305682&tbm=isch&sxsrf=AM9HkKkPC5MEf561nelVH-rCbs0SF_qtaA:1701266369937&source=lnms&sa=X&ved=2ahUKEwiCu5eNr-mCAxXCaqQEHU5hB3UQ_AUoAXoECAEQAw&biw=1396&bih=639&dpr=1.38#imgrc=V8tNljFapQaPAM))

![](Attachments%20-%20Cables/Pasted%20image%2020231129160042.png)

([source](https://www.google.com/search?q=ts+trs+trrs&sca_esv=586305682&tbm=isch&sxsrf=AM9HkKkPC5MEf561nelVH-rCbs0SF_qtaA:1701266369937&source=lnms&sa=X&ved=2ahUKEwiCu5eNr-mCAxXCaqQEHU5hB3UQ_AUoAXoECAEQAw&biw=1396&bih=639&dpr=1.38#imgrc=uk-OoHC72nOfJM))



## Analog Levels: Mic, Line, Instrument

There are three levels of signal that are transmitted via a cable:

![](Attachments%20-%20Cables/Pasted%20image%2020231129122940.png)



# Overview of Audio Cables

![](Attachments%20-%20Cables/Pasted%20image%2020231129104925.png)

([source](https://www.google.com/search?q=audio+cables+ts+trs+trrs&tbm=isch&ved=2ahUKEwjBgcbj6OiCAxUQVqQEHbnpAW0Q2-cCegQIABAA&oq=audio+cables+ts+trs+trrs&gs_lcp=CgNpbWcQDDoECCMQJzoFCAAQgAQ6CAgAEIAEELEDOgoIABCABBCKBRBDOg0IABCABBCKBRCxAxBDOgYIABAIEB46BwgAEIAEEBhQAFjungJg6a4CaAJwAHgAgAGjAYgBtRiSAQQwLjIymAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=BPpmZcHvB5CskdUPudOH6AY&bih=639&biw=1396#vhid=VL3SpvgWhon5hM&vssid=3981:4zAWe05jEfOr2M))

## TS vs TRS vs TRRS



* TRS: T