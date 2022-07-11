# `systemview-target`

<!-- cargo-rdme start -->

RTOS tracing trait implementation for SEGGER SystemView.

SEGGER SystemView can be used for non-commercial project for free and is 
available [`here`](https://www.segger.com/products/development-tools/systemview/).

## Features

- `callbacks-os`: Check if RTOS supports tracing callbacks from SystemView.
- `callbacks-os-time`: Check if RTOS supports timestamp callback from SystemView.
- `callbacks-app`: Check if your application supports callback from SystemView.
- `log`: Activates global `log` over RTT.
- `cortex-m`: Enables Arm Cortex-M support.

## Usage

If you are using an RTOS which supports [`rtos-trace`](https://docs.rs/rtos-trace/)
add the following dependencies:

```toml
# Cargo.toml
[dependencies]
rtos-trace = "0.1"
systemview-target = { version = "0.1", features = ["log", "callbacks-app", "callbacks-os", "callbacks-os-time", "cortex-m"] }
log = { version = "0.4", features = ["max_level_trace", "release_max_level_warn"] }
```

and add to your code
```ìgnore
// for tracing
use systemview_target::SystemView;
rtos_trace::global_trace!{SystemView}

static LOGGER: systemview_target::SystemView = systemview_target::SystemView::new();

fn main() -> ! {
    LOGGER.init();
    // for logs
    log::set_logger(&LOGGER).ok();
    log::set_max_level(log::LevelFilter::Trace);
    /*..*/
}
```

<!-- cargo-rdme end -->
