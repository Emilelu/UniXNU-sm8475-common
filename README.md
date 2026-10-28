# UniXNU SM8475 common

Shared Qualcomm SM8475 (Snapdragon 8+ Gen 1) support for UniXNU device
repositories: the CPU topology, the GICv3 window and the platform switches that
every board on this SoC needs.

A device repository selects this source through `board.toml`:

```toml
[board]
soc = "SM8475"
soc_source = "sm8475"
```

and pins it in `feeds.toml`:

```toml
[[source]]
name = "sm8475"
kind = "soc"
git = "https://github.com/Emilelu/UniXNU-sm8475-common"
commit = "<40-character commit>"
```

## Layout

| Path | Contents |
| --- | --- |
| `soc.toml` | SoC identity, source reference, component selection |
| `configs/sm8475.config` | platform switches shared by every board |
| `dts/sm8475.dtsi` | CPUs, PSCI conduit, GICv3 distributor and redistributor |
| `patches/xnu/series` | XNU patches that belong to the SoC layer |

Board files include `sm8475.dtsi` and add memory, peripherals and the Apple
identity; the device repository owns those.

## Values

The register and interrupt facts match the SM8475 board that already runs this
kernel:

| Resource | Address |
| --- | --- |
| APSS window | `0x17000000`, 32 MiB |
| GIC distributor | `0x17100000`, 64 KiB |
| GIC redistributors | `0x17180000`, 2 MiB, 256 KiB stride |
| Arch timer | 19.2 MHz |
| PSCI conduit | `smc` |
