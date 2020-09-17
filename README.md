# Haveacry/flux-adsbstation
Kubernetes manifests to setup a ADS-B collection station. Assumes use of a USB SDR for capturing ADS-B/Mode S broadcasts.

Submits ADS-B data to the following services:
* FlightAware
* FlightRadar24
* RadarBox

## Prerequisites

You must blacklist the SDR modules on the host so the container may claim the USB device

To do this, create a file `/etc/modprobe.d/blacklist-rtl2832.conf` containing the following:

```shell
# Blacklist RTL2832 so container can use the device

blacklist rtl2832
blacklist dvb_usb_rtl28xxu
blacklist rtl2832_sdr
```

Once this is done it is recommended to reboot the host device to ensure modules aren't loaded (or you may unplug the SDR and unload the modules, then plug it back in).

## Configuration

The following configuration maps are required for the containers to operate correctly
