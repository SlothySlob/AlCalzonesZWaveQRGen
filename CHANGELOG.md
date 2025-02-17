# CHANGE LOG

## 2025-02-17 DT:00.11.002E.1 fix
Apprently Z-Wave Alliance is saying that the TLV block for Supported protocols must have a **Length** value of 3. On a quick check of the code, the level function was replaced with uint8 function, as the returned value is the required value.

```javascript
if (info.supportedProtocols !== void 0) {
  const supportedProtocols = encodeTLV(
    ProvisioningInformationType.SupportedProtocols,
    false,
  //level(encodeBitMask(info.supportedProtocols, void 0, Protocols.ZWave))
    uint8(encodeBitMask(info.supportedProtocols, void 0, Protocols.ZWave))
  );
  partsAfterChecksum.push(supportedProtocols);
}
```

Another change was in the **index.html**. Specifically for Generic device type and Specific device type. Since both combine into the Device type values, the values for each should be only 0-255 or 0-FF.