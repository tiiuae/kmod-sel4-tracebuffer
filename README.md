# kmod-sel4-tracebuffer

seL4 tracebuffer access and control linux kernel module.

## Configure

You need to provide following information in device tree file:

```
reserved-memory {
  sel4_tracebuffer {
    compatible = "sel4_tracebuffer";
    reg = <{address} {size}>;
  }
}
```

During the boot time you should be able to see that module has been loaded at proper address and with proper size:

```
[   13.785765] sel4_tracebuffer_parse_dt: map phaddr:0x8800000 to vaddr: 0xffffffc012400000
[   13.794167] sel4_tracebuffer_probe: probed sel4 trace buffer 0x200000@0x8800000
```

Following debufs structure will appear:

```
# ls /sys/kernel/debug/sel4_tracebuffer/     
trace      trace_on   tracedata
```

## Usage

`trace`     (RO)  - file give line by line access to internal seL4 tracebuffer in human readable format  
`trace_on`  (RW)  - file controls seL4 logging: write 1/start/enable to start 0/stop/disable to stop logging  
`tracedata` (RO)  - file give entry by entry access to internal seL4 tracebuffer in binary format  
