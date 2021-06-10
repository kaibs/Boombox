# WIP! This project still is in an early stage

## 3D printed two-way Boombox

Repository for a fully 3D-printed two-way Bluetooth-speaker.<br/><br/>
<b>REMARK:</b> <i>This is just the documentation of my personal build and in no way a complete instruction to follow along. I provide everything I used to finish this build as an orientation for similar projects</i>


## specifications:
* size: 280x145x125mm (LxWxH)
* fully printed speaker-enclosure
* 2x 2" full range chassis for mids and higher frequencies
* 1x 3" chassis in own subwoofer-compartment for lower frequencies
* digital crossover and equalizer via a ADAU1401 DSP
* digital volume- (rotary encoder) and tone-control (potentiometers)
* APTX Bluetooth connectivity via a CSR64215 which communicates digitally (I<sup>2</sup>S) with the DSP
* 6s Li-Ion battery pack with BMS and USB-C charging (PD 20V) 

## details:

The goal of this project was to design a fully 3D-printable portable Bluetooth-speaker.
The enclosure consists out of 7 parts which can be printed without supports (some screw-holes might be better with) on a 300x300x150mm build-volume. As a material I used simple PLA, although PETG might be a better choice due to its thermal resistance (amplifiers and DC-DCs might get hot).<br/><br/>
The enclosure contains three seperated chambers, one for each speaker-driver. The big subwoofer-compartment in the middle of the casing has a looped horn-like opening and holds a 3" speaker for lower frequencies (50-250Hz). The two side-compartments contain each a 2" full-range chassis for mids and highs.
Each driver currently has its own amplifier (TPA3310, 30W), but replacing two of them with a 2x15W TDA3110 ([like this](https://de.aliexpress.com/item/32969057168.html?spm=a2g0s.9042311.0.0.27424c4dnLOET4)) for the two 2" would probably make more sense.<br/><br/>
The battery of the speaker consists out of six 18650-cells () which are connected in series to a 6s-BMS. The charging happens over an USB-C adapter with a Power-Delivery chip, which delivers an output-voltage of 20V. This way the attaching DC-DC-converter has only to go up by 5.2V, which results in lower heat loss. The downside is that you can only use USB-PD-chargers to power the speaker.<br/><br/>
The "brain" of the speaker is resembled by an ADAU1401 DSP from Analog Devices and a sound-providing CSR64215 Bluetooth-receiver.
The ADAU1401 is a small, self-booting DSP with 4 DACs, so each of the speaker-chassis can have it's own channel. This way, digital audio-processing like EQ, crossovers and other balancing, can happen completely in software. The board also allows using it's GPIOs for manipulating parameters. Volume- and tone-control is realized with rotary-encoders and potentiometers.
The Bluetooth-receiver is connected as a slave via I<sup>2</sup>S to the DSP to avoid any loss in quality due to unnecessary ADC-DAC-conversions.





## drivers and software
* [Drivers for the EZ-USB](https://www.diyaudio.com/forums/digital-line-level/269111-low-cost-usbi-programmer-using-cypress-cy7c68013a-board-post5536992.html) (DSP programmer)
* [Analog Devices Sigma Studio](https://www.analog.com/en/design-center/evaluation-hardware-and-software/software/ss_sigst_02.html#software-overview) (DSP dev-tool)

The software necessary for programming the CSR64215 Bluetooth-module (setting name, I<sup>2</sup>S-mode, sampling freq etc.) is a little hard to get. Offically this tools aren't made for the consumer-market and therefore only available for business-clients ([csrsupport.com](http://www.csrsupport.com/)).
However the software is often shared in forums like in [this](http://www.hifi-forum.de/index.php?action=browseT&forum_id=71&thread=12581&back=1&sort=lpost&z=43) thread in the German [hifi-forum.de](http://www.hifi-forum.de/).


## further readings:

* [programming the ADAU1401 with an cheap USBI-TO-EZ-ADAPTER](https://www.meddens.eu/audio/USBi.html)
* [AnalogDevices Sigma Studio documentation](https://wiki.analog.com/resources/tools-software/sigmastudio)
* [Flashing the ADAU1401 in Sigma Studio](https://suredsp.ratz-it.de/index.php?title=Basissetup_erstellen_und_hochladen) (German)
* [Using the CSR64215 with the ADAU1401](https://suredsp.ratz-it.de/index.php?title=CSRA64215) (German)
* [Using GPIOs on the ADAU1401](https://suredsp.ratz-it.de/index.php?title=GPIO_Pins_verwenden) (German)
* [Using potentiometers on the ADAU1401](https://suredsp.ratz-it.de/index.php?title=Potentiometer_verwenden) (German)
