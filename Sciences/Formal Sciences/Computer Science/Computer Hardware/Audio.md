Main sources: [source 1](https://www.audiogrounds.com/audio-cable/), [source 2](https://www.pianodreamers.com/audio-cables-guide/), [source 3](https://www.pugetsystems.com/support/guides/trs-and-trrs-oh-and-trrrs-2255)

# Audio Cable Terminologies

## Jacks and Plugs (F/M Connectors/Sockets)

![](Attachments%20-%20Audio/Pasted%20image%2020231129125137.png)

* The fixed part of the connection is called JACK. 
* What you plug into a jack is called PLUG.

## Balanced and Unbalanced Audio Cables

* Audio cables can be:
	* balanced (and unbalanced, [source](https://www.audiogrounds.com/audio-cable/#:~:text=Some%20audio%20cable%20types%20can%20be%20both%20balanced%20and%20unbalanced%2C%20depending%20on%20the%20purpose%2C%20while%20others%20are%20always%20unbalanced))
	* unbalanced
* Unbalanced audio cables (UACs) have 1 wire and shield (ground), while balanced audio cables (BACs) have 2 wires and shield. Visualization:
  
  ![](Attachments%20-%20Audio/Pasted%20image%2020231129130757.png)
  
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
		  
		  ![](Attachments%20-%20Audio/Pasted%20image%2020231129134331.png)
		  
		  At the receiver's BIS: the cold signal is flipped, which effectively eliminates the noise and outputs a clean audio signal:
		  
		  ![](Attachments%20-%20Audio/Pasted%20image%2020231129134349.png)
		  
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

## Analog vs Digital Cables

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
  
    ![](Attachments%20-%20Audio/Pasted%20image%2020231129135600.png)
    
    Other times, the difference is clear, for example ([source](https://emastered.com/blog/audio-cable-types)):
    
    ![](Attachments%20-%20Audio/Pasted%20image%2020231129140239.png)

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

Overview of audio cables ([source](https://www.google.com/search?q=audio+cables+ts+trs+trrs&tbm=isch&ved=2ahUKEwjBgcbj6OiCAxUQVqQEHbnpAW0Q2-cCegQIABAA&oq=audio+cables+ts+trs+trrs&gs_lcp=CgNpbWcQDDoECCMQJzoFCAAQgAQ6CAgAEIAEELEDOgoIABCABBCKBRBDOg0IABCABBCKBRCxAxBDOgYIABAIEB46BwgAEIAEEBhQAFjungJg6a4CaAJwAHgAgAGjAYgBtRiSAQQwLjIymAEAoAEBqgELZ3dzLXdpei1pbWfAAQE&sclient=img&ei=BPpmZcHvB5CskdUPudOH6AY&bih=639&biw=1396#vhid=VL3SpvgWhon5hM&vssid=3981:4zAWe05jEfOr2M)):

![](Attachments%20-%20Audio/Pasted%20image%2020231129104925.png)

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

![](Attachments%20-%20Audio/Pasted%20image%2020231129155954.png)

([source](https://www.google.com/search?q=ts+trs+trrs&sca_esv=586305682&tbm=isch&sxsrf=AM9HkKkPC5MEf561nelVH-rCbs0SF_qtaA:1701266369937&source=lnms&sa=X&ved=2ahUKEwiCu5eNr-mCAxXCaqQEHU5hB3UQ_AUoAXoECAEQAw&biw=1396&bih=639&dpr=1.38#imgrc=V8tNljFapQaPAM))

![](Attachments%20-%20Audio/Pasted%20image%2020231129160042.png)

([source](https://www.google.com/search?q=ts+trs+trrs&sca_esv=586305682&tbm=isch&sxsrf=AM9HkKkPC5MEf561nelVH-rCbs0SF_qtaA:1701266369937&source=lnms&sa=X&ved=2ahUKEwiCu5eNr-mCAxXCaqQEHU5hB3UQ_AUoAXoECAEQAw&biw=1396&bih=639&dpr=1.38#imgrc=uk-OoHC72nOfJM))

# Decibel (dB)

[source 1: soundonsound.com](https://www.soundonsound.com/sound-advice/decibels-explained) [source 2: blog.echobarier.com](https://blog.echobarrier.com/blog/the-decibel-scale-explained)

* The name decibel means a tenth of a bel.
	* The bel part being named after that well‑known inventor of telephones, Alexander Graham Bell (hence the capital B in dB).
* dB scale can be logically compared to the Richter scale, which measures the intensity of earthquakes. 
* The dB scale takes into account the noise very close to the source, as the noise intensity decreases as the distance from the sound source increases.
* Sounds above 85 dB are considered harmful.
* Decibel is simply a convenient way of expressing the ratio between two signal levels. 
	* "convenient" because the nature of the decibel makes it logarithmic, and it just so happens that our ears are also logarithmic in the way they perceive sound level.
	* Since it expresses only general ratios, measured notations of dB were introduced, including:
		* dBm 
			* Measures power.
			* It is a fixed value where 0dBm equates to 1 milliwatt of power.
			* Important in the pioneering days of telephone when small amounts of electrical power needed to be transmitted over long distances.
				* In the world of telephones and 600 ohm line impedances, 0 dBm tended to mean a signal of 0.775 Volts applied to a load of 600 ohms — or 1mW.
					* as $P = \frac{V^2}{R} = \frac{0.775^2}{600} = 0.001W = 1mW$.
			* Not important to the world of modern audio
				* dBm does not signify a signal level of 0.775 Volts unless the load impedance is 600 ohms, but since load impedances are not an issue in modern audio systems, dBu was introduced.
		* dBu
			* Measures voltage.
			* "u" means "unloaded"
			* same as dBv (for voltage), even though the latter is less common.
			* Signifies a signal level of 0.775 volts regardless of the load impedance.
				* This is why it measures voltage only, as it doesn't take resistance (i.e., impedance) into consideration. 
			* However, having 0.775 volts as the reference voltage level can lead to clumsy calculations. Therefore, dBV was introduced.
		* dBV
			* Same definitions as dBu, but the reference voltage level is now 1V, instead of 0.775V.
		* Comparison between dBu and dBV ([source: audiouniversityonline.com](https://audiouniversityonline.com/consumer-vs-professional-audio-levels-what-is-the-difference/)):
		  
		  ![](Attachments%20-%20Audio/Pasted%20image%2020231204131702.png)
		  
* The dB [measurement levels increase](https://www.sciencedirect.com/topics/engineering/decibel-scale) almost exponentially. 
	* 10 dB is 10 times more intense than 0 dB. 
	* A sound that is 1,000 times more intense than 0 dB (near total silence) is 30 dB.
	* Number of dBs = $10 \cdot log_{10} (P_1/P_2)$ where $P_1$ and $P_2$ are the two **powers** being compared.
		* Therefore, 3dB represents a doubling in power.
			* E.g.: 10 watt amplifier has "3 dB more power" than 5, because $10 \cdot log_{10} (10/5)=3$
			* Other examples:
			  
			  ![|350](Attachments%20-%20Audio/Pasted%20image%2020231204125819.png)
			  
	* Number of dBs = $20 \cdot log_{10} (V_1/V_2)$ where $V_1$ and $V_2$ are the two **voltages** being compared.
		* Therefore, 6dB represents a doubling in power.
			* E.g.: 4V has "6 dB more voltage"  than 2V, because $20 \cdot log_{10} (4/2)=6$
			* Other examples:
			  
			  ![|345](Attachments%20-%20Audio/Pasted%20image%2020231204125859.png)
			  
	* Visualizations of dBm as red and dBV as blue respectively:
	  
	  ![](Attachments%20-%20Audio/Pasted%20image%2020231204124819.png)

Visualizations of the decibel scale:

![](Attachments%20-%20Audio/Pasted%20image%2020231203093501.png)

![](Attachments%20-%20Audio/Pasted%20image%2020231203093523.png)

([source: residential-acoustics.com](https://residential-acoustics.com/decibel-levels-sometimes-negative/))

# Analog Levels

There are three levels of signal that are transmitted via a cable:

![](Attachments%20-%20Audio/Pasted%20image%2020231129122940.png)

([source: pianodreamers.com](https://www.pianodreamers.com/keyboard-amplifier-guide/))

Alternative visualization about the difference between mic-level signal, instrument-level signal, line-level signal, and speaker-level signal ([source: blackghostaudio.com](https://www.blackghostaudio.com/blog/audio-signal-levels-explained-mic-instrument-line-and-speaker)):

![](Attachments%20-%20Audio/Pasted%20image%2020231203114737.png)

## Line Level

[source 1: Mixed Signals' YouTube video](https://www.youtube.com/watch?v=Lxq2T0r3Jy4)

* Line level is the standard signal level used in audio systems. 
	* Specifically, it is the voltage level that audio signals are typically transmitted at between audio devices in a studio.
* Devices that operate at line level include:
	* Mixing consoles
	* Compressors
	* Modern synthesizers
	* DJ mixers
	* Hi-fis
	* Consumer electronics such as TVs and MP3 players

![](Attachments%20-%20Audio/Pasted%20image%2020231203154440.png)

## Mic Level

[source 1: Mixed Signals' YouTube video](https://www.youtube.com/watch?v=Lxq2T0r3Jy4)

* Mic level describes the voltage generated by a microphone when it picks up sound, typically just a few thousandths of a volt ([source: shure.com](https://www.shure.com/en-US/performance-production/louder/whats-the-difference-between-line-and-mic-levels#:~:text=A%20mic%2Dlevel%20or%20microphone,in%20sound%20level%20and%20distance.)).
* requires a pre-amplifier to bring it up to line level. 
* Microphone level is usually specified between -60 and -40 dBu. (dBu and dBV are decibel measurements relative to voltage.)

![](Attachments%20-%20Audio/Pasted%20image%2020231203154550.png)

## Instrument Level

[source 1: Mixed Signals' YouTube video](https://www.youtube.com/watch?v=Lxq2T0r3Jy4)

* Instrument level is the signal level produced by electric guitars, basses, and many vintage keyboards and synths.
* Some of the instruments produce voltage on-par with the line level. However, they shouldn't be connected directly to line level equipment due to their high impedance. More on that [here](https://www.youtube.com/watch?v=4GH411St0Vo).
* We can connect instrumental level to line level using:
	* a dedicated instrument preamp
	* a Hi-Z input on a mic preamp
	* a DI box

![](Attachments%20-%20Audio/Pasted%20image%2020231204111151.png)

## Phono Level

[source 1: Mixed Signals' YouTube video](https://www.youtube.com/watch?v=Lxq2T0r3Jy4)

* Weaker than mic level.
* Produced by turntables used to play Vinyl records.

![](Attachments%20-%20Audio/Pasted%20image%2020231204113930.png)

## Speaker Level

[source 1: Mixed Signals' YouTube video](https://www.youtube.com/watch?v=Lxq2T0r3Jy4)

* Strongest audio signal level.
* Produced by power amplifiers driving passive speakers, such as:
	* guitar/bass amps
	* passive studio monitors
	* consumer hi-fi systems
	* 

![](Attachments%20-%20Audio/Pasted%20image%2020231204114729.png)