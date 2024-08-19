
# Bluetooth Battery Level Reader

This project demonstrates how to use the Web Bluetooth API to connect to Bluetooth devices and read their battery level using JavaScript. The provided code allows a user to scan for nearby Bluetooth devices, connect to one, and retrieve the battery percentage.

## Before we start


This document assumes you have some basic knowledge of how Bluetooth Low Energy (BLE) and the  [Generic Attribute Profile](https://developer.chrome.com/docs/capabilities/bluetooth/GATT)  work.

Even though the  [Web Bluetooth API specification](https://webbluetoothcg.github.io/web-bluetooth/)  is not finalized yet, the spec authors are actively looking for enthusiastic developers to try out this API and give  [feedback on the spec](https://github.com/WebBluetoothCG/web-bluetooth/issues)  and  [feedback on the implementation](https://bugs.chromium.org/p/chromium/issues/entry?components=Blink%3EBluetooth).

A subset of the Web Bluetooth API is available in ChromeOS, Chrome for Android 6.0, Mac (Chrome 56) and Windows 10 (Chrome 70). This means you should be able to  [request](https://developer.chrome.com/docs/capabilities/bluetooth#request)  and  [connect to](https://developer.chrome.com/docs/capabilities/bluetooth#connect)  nearby Bluetooth Low Energy devices,  [read](https://developer.chrome.com/docs/capabilities/bluetooth#read)/[write](https://developer.chrome.com/docs/capabilities/bluetooth#write)  Bluetooth characteristics,  [receive GATT Notifications](https://developer.chrome.com/docs/capabilities/bluetooth#notifications), know when a  [Bluetooth device gets disconnected](https://developer.chrome.com/docs/capabilities/bluetooth#disconnect), and even  [read and write to Bluetooth descriptors](https://developer.chrome.com/docs/capabilities/bluetooth#descriptors). See MDN's  [Browser compatibility](https://developer.mozilla.org/docs/Web/API/Web_Bluetooth_API#Browser_compatibility)  table for more information.

### Step - 1
Go to Chrome Search bar then paste
```
about://flags
```

### Step - 2
Then again search
```
experimental-web-platform-features
```
by default is `Disable` make it `Enable`
![CLI](https://github.com/asimar007/Cross-Region-Migration-of-AWS-EBS-Volumes/blob/main/Screenshot/Bluetooth.png?raw=true)

### Step - 3
Open Chrome Developer Tool `console` tab

[Mac    `option+command+i`]

Then Paste the Code 


## Additional Resources

For more information on using the Web Bluetooth API, refer to the [Web Bluetooth API Documentation](https://developer.chrome.com/docs/capabilities/bluetooth).
## Code

```javascript
navigator.bluetooth.requestDevice({ acceptAllDevices: true, optionalServices: ['battery_service'] })
  .then(device => device.gatt.connect())
  .then(server => {
    // Getting Battery Service…
    return server.getPrimaryService('battery_service');
  })
  .then(service => {
    // Getting Battery Level Characteristic…
    return service.getCharacteristic('battery_level');
  })
  .then(characteristic => {
    // Reading Battery Level…
    return characteristic.readValue();
  })
  .then(value => {
    console.log(`Battery percentage is ${value.getUint8(0)}`);
  })
  .catch(error => { 
    console.error(error); 
  });
