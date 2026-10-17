# PS5 A53 Code Execution PoC

Proof of concept for code execution on the PS5's a53.
Can be used to disable/defeat the Hypervisor till 5.00 (unimplemented).

Currently relies on DECI5S / sdbgp Protocol for read/write on a53 but can be done also from x86 (credits: flat_z).

**DON'T BRICK YOUR CONSOLE BY WRITING TO SOMEWHERE YOU DON'T KNOW ABOUT!**

## What it does

1. Initializes DECI5S communication with the A53 via `/dev/mp4/dump`
2. Discovers the real physical addresses of firmware code via L3 page table walk
3. Patches a version string in `.data` and an instruction in `.text`
4. Triggers the patched function via DECI5S GET_CONF command
5. Displays `"pwned by cragson - 33"` instead of the firmware version string
6. Restores everything to original state

## Requirements

- PS5 FW 01.00 - 11.40 ( 11.60+ Patched )
- Kernel read/write exploit (provides `kernel_read4/8`, `kernel_write4/8`, etc.)
- PS5 Payload SDK (`PS5_PAYLOAD_SDK` environment variable)

## Building

```bash
export PS5_PAYLOAD_SDK=/path/to/ps5-payload-sdk
make
```
## Credits

- astrelsky (mp4rw)
- Specter (byepervisor)
- John Toernblom (sdk)
- me, myself and I

