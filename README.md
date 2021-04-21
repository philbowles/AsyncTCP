# AsyncTCP 

## Async TCP Library for ESP32 Arduino

This is a fully asynchronous TCP library much like the original, apart form the fact that it works properly.

## What's fixed

95% of the API is the same as ESPAsyncTCP (the ESP8266 version) apart from one minor problem: This lib does not pass through the TCP PSH flag, which means you can never receive more than N buffers' worth of data (where N is implementation-dependent) because you cannot tell which is the last packet in a multi-packet > buffer size set of data. Clue: It's the one with the PSH flag set. See the problem?

So, PSH flag collected on TCP recv, saved and made available to new API call (same as ESPAsyncTCP)

```cpp
bool isRecvPush(); // is the PSH flag set, i.e. is this the last packet?
```