# using device APIs with the web - jessica claire [(twitter)](https://twitter.com/jsscclr)

Geolocation API
 - nagigator.geolocation [(mdn)](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/geolocation)
 - navigator.geolocation.getCurrentPosition [(mdn)](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation/getCurrentPosition)
 - we can't assume we have access

```js
var options = {
  enableHighAccuracy: true,
  timeout: 5000,
  maximumAge: 0
};

function success({coords}) {
  console.log('Your current position is:');
  console.log('Latitude : ' + coords.latitude);
  console.log('Longitude: ' + coords.longitude);
  console.log('More or less ' + coords.accuracy + ' meters.');
};

function error({code, message}) {
  console.warn('ERROR(' + code + '): ' + message);
};

navigator.geolocation.getCurrentPosition(success, error, options);
```

Battery Status API
 - navigator.getBattery [(mdn)](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/getBattery)
 - what affect does our code have on the Battery

```js
navigator.getBattery().then(battery => {
  battery.addEventListener('chargingchange', () => {});
  battery.addEventListener('levelchange', () => {});
  battery.addEventListener('chargingtimechange', () => {});
  battery.addEventListener('dischargingtimechange', () => {});
});
```

Ambient Light Sensor
 - device light event 0 - 1000
 - light level event dim/normal/bright
 - media queries too!
 - will change to AmbientLightSensor

Device Orientation
Device Orientation Absolute - useful for augmented reality
Device motion - acceleration
Compass needs calibration - lol!
Vibration API - in milliseconds
Media capture and streams
Network information API
