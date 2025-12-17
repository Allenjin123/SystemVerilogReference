## Interface

``` verilog 
interface ctl_to_data_if;
    // Signal declarations (the actual wires)
    logic        valid;
    logic [7:0]  data;
    logic        ready;

    // Modports define "views" of the interface from different perspectives
    modport ctl_mp (output valid, data, input ready);
    modport data_mp (input valid, data, output ready);

endinterface
```

**The Signals**
```
┌─────────────────────────────┐
│     ctl_to_data_if          │
├─────────────────────────────┤
│  valid  (1 bit)             │
│  data   (8 bits)            │
│  ready  (1 bit)             │
└─────────────────────────────┘
```

**Modports: Different Perspectives**

`modport` defines which signals are inputs vs outputs for each side of the interface:
```
       Controller                              Data Unit
    ┌─────────────┐                         ┌─────────────┐
    │             │   valid (output→input)  │             │
    │   uses      │ ─────────────────────►  │   uses      │
    │   ctl_mp    │   data  (output→input)  │   data_mp   │
    │             │ ─────────────────────►  │             │
    │             │   ready (input←output)  │             │
    │             │ ◄─────────────────────  │             │
    └─────────────┘                         └─────────────┘
