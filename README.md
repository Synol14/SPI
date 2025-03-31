## ***/!\ This a fork to add prescaler managment in SPISettings class for Teensy 4.x /!\\***

- Solution source : [forum.pjrc.com](https://forum.pjrc.com/index.php?threads/achieving-slow-10-khz-spi-clock-on-teensy-4-1-using-lpspi-tcr-prescale.73363/)
- Code added :
```C++
	//above is the existing constructor
	//below is the modified one
	SPISettings(uint32_t clockIn, uint8_t bitOrderIn, uint8_t dataModeIn, uint8_t prescale) : _clock(clockIn) {
		init_AlwaysInline(bitOrderIn, dataModeIn);
		uint32_t tprsc = (prescale & 7);
		tprsc <<= 27;
		tcr &= 0xC7FFFFFF; //clear bits 29-27
		tcr |= tprsc; //load bits 29-27
	}
```

# SPI Library for Teensy

http://www.pjrc.com/teensy/td_libs_SPI.html

![](http://www.pjrc.com/teensy/td_libs_SPI_1.jpg)

