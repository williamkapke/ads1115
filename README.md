# ADS1115
A Node.js library for an ADS1115 analog to digital converter

Theses are [super inexpensive on amazon](https://amzn.to/2pLbWML)!

The joystick is: [here](https://amzn.to/2LKvvgP)<br>
The display is: [here](https://amzn.to/2pEUCZz)<br>
&nbsp; --> Also checkout my node module for it!: [here](https://npmjs.com/package/ssd1327)<br>
<br>
![tfmini-plus](ads1115.gif)

```js
const ADS1115 = require('ads1115')
const map = (value) => Math.floor((value - MIN) * 127 / (MAX - MIN));

const i2c = require('i2c-bus')
i2c.openPromisified(1).then(async (bus) => {
  const ads1115 = await ADS1115(bus)
  // ads1115.gain = 1

  for (let i = 0; i < 1000; i++) {
    let value = await ads1115.measure('0+GND')
    console.log(value)
  }
})
```

## Install
https://npmjs.com/package/ads1115

    npm install ads1115 i2c-bus


#### *i2c-bus not included in dependencies
To prevent multiple  instances of [i2c-bus](https://npmjs.com/package/i2c-bus)
being installed in your project- it is NOT included as a dependency. You just
need to install it separately.

This also allows you to swap in a different bus, such as an [i2cdriver](https://npmjs.com/package/i2cdriver) if desired.

## API

### ads1115.gain
Gets or sets the gain. You can use a `Number` or `String`.

Valid values:<br>
`2/3` = +/- 6.144V (default)<br>
`1`   = +/- 4.096V<br>
`2`   = +/- 2.048V<br>
`4`   = +/- 1.024V<br>
`8`   = +/- 0.512V<br>
`16`  = +/- 0.256V<br>

### ads1115.measure(mux)
Requests a single measurement.

Valid values for `mux` parameter:<br>
`'0+1'` = Differential measurement between A0 & A1<br>
`'0+3'` = Differential measurement between A0 & A3<br>
`'1+3'` = Differential measurement between A1 & A3<br>
`'2+3'` = Differential measurement between A2 & A3<br>
`'0+GND'` = Single-ended measurement on A0<br>
`'1+GND'` = Single-ended measurement on A1<br>
`'2+GND'` = Single-ended measurement on A2<br>
`'3+GND'` = Single-ended measurement on A3<br>

# License
MIT