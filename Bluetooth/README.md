# Bluetooth

The Web Bluetooth API provides the ability to connect and interact with Bluetooth Low Energy peripherals.

## Interfaces
#### Bluetooth
Returns a Promise to a BluetoothDevice object with the specified options.
#### BluetoothAdvertisingData  
Provides advertising data about a particular Bluetooth device.
#### BluetoothCharacteristicProperties
Provides properties of a particular BluetoothRemoteGATTCharacteristic.
#### BluetoothDevice
Represents a Bluetooth device inside a particular script execution environment.
#### BluetoothRemoteGATTCharacteristic
Represents a GATT Characteristic, which is a basic data element that provides further information about a peripheral’s service.
#### BluetoothRemoteGATTDescriptor
Represents a GATT Descriptor, which provides further information about a characteristic’s value.
#### BluetoothRemoteGATTServer
Represents a GATT Server on a remote device.
#### BluetoothRemoteGATTService
Represents a service provided by a GATT server, including a device, a list of referenced services, and a list of the characteristics of this service.

## Methods
#### BluetoothDevice.watchAdvertisments() 
A Promise that resolves to undefined or is rejected with an error if advetisments can’t shown for any reason.
#### BluetoothDevice.unwatchAdvertisments() 
Stops watching for advertisments.
#### BluetoothDevice.connectGATT()  
A Promise that resolves to an instance of BluetoothGATTRemoteServer.

## Examples
#### Find a bluetooth device

```js
function run (characteristics) {
    pioSetting = characteristics[0];
    pioOutput = characteristics[1];
    console.log(pioSetting);
    console.log(pioOutput);
    var data = new Uint8Array(1);
    data[0] = 1 << 1;
    pioSetting.writeValue(data);
    setInterval(function () {
        data[0] ^= (1 << 1);
    	pioOutput.writeValue(data);
    }, 500);
    pioOutput.writeValue(data);
}

function service (service) {
    console.log(service);
    Promise.all([
    	service.getCharacteristic('229b3000-03fb-40da-98a7-b0def65c2d4b'),
    	service.getCharacteristic('229b3002-03fb-40da-98a7-b0def65c2d4b')
    ]).then(run, error);
}

function gatt (server) {
    console.log(server);
    server.getPrimaryService('229bff00-03fb-40da-98a7-b0def65c2d4b').then(service, error);
}

function found (device) {
    console.log(device);
    device.connectGATT().then(gatt, error);
}

function error (e) {
    console.log(e);
}

function find () {
	var options = {
	    filters: [{
//	        services: ['229bff00-03fb-40da-98a7-b0def65c2d4b']
	        namePrefix: 'delca'
	    }]
	};
    navigator.bluetooth.requestDevice(options).then(found, error);
}
```