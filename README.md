# A simple example showing how to use the nRF52840's external flash for mcuboot with sysbuild and WITHOUT partition manager

```
west build -b nrf52840dk/nrf52840 --sysbuild -p -- -DEXTRA_CONF_FILE=overlay-bt.con
```

Critical changes were made in "sysbuild.conf" and the sysbuild folder

To demonstrate DFU, run the following mcumgr commands:

```
$ sudo ./mcumgr conn add zephyr type=ble connstring=peer_name="Zephyr"
```

```
$ sudo ./mcumgr -c zephyr image upload -n 1 <SAMPLE_DIR>/build/smp_svr/zephyr/zephyr.signed.bin
```

Next, get the hash of the new image that has been uploaded:

```
sudo ./mcumgr -c zephyr image list
```

Then confirm the image and reset

```
$ sudo ./mcumgr -c zephyr image confirm <SLOT1_HASH>
```

```
$ sudo ./mcumgr -c zephyr reset
```
