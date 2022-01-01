# Lumi Router

This firmware is a replacement for the original firmware for the __Zigbee__ chip JN5169 on __Xiaomi DGNWG05LM__ and __Aqara ZHWG11LM__ gateways which allows to use the gateway as a router (repeater-like) in any Zigbee network instead of the stock coordinator firmware for the propriate Xiaomi MiHome Network.

---

This instruction assumes that an alternative __OpenWRT__ firmware is already installed on the gateway. If you have not done this, use the following instruction [https://openlumi.github.io](https://openlumi.github.io)

### Firmware

1. Connect to device via SSH.
2. Issue the following commands in the command line.

```shell
wget https://github.com/igo-r/Lumi-Router-JN5169/releases/latest/download/LumiRouter_20210320.bin -O /tmp/LumiRouter.bin 
jnflash /tmp/LumiRouter.bin
```

### Pairing

Issue the following command in the command line.

```shell
jntool erase_pdm
```

After this the device will automatically join.

### Restart

Issue the following command in the command line.

```shell
jntool soft_reset
```

## Building

1. Downlaod and unpack ba2 toolchain, e.g. from https://github.com/openlumi/BA2-toolchain/releases/download/20201219/ba-toolchain-20201219.tar.bz2
2. Donwload and unpack NXP SDK (JN-SW-4170) from nxp.com. If you use linux, you can use patched version that fixed compiling issues from https://github.com/devbis/JN-SW-4170/archive/refs/heads/master.zip
3. Configure project with proviing paths to SDK and toolchain:

```
cmake -B build -DTOOLCHAIN_PREFIX=/full/path/to/toolchain -DSDK_PREFIX=/full/path/to/sdk
```

4. Build project

```
cmake --build build --target LumiRouter.bin -j$(nproc)
```

5. Get compiled firmware in build/src/LumiRouter.bin
