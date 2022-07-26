# hades-logger

A logging library for ios, with support for printing logs to console, and saving to file summaries. Provides in-app log viewing and log sharing functions.

## Features

- Easier to filter log in both cosole at bottom of `Xcode` and `Console.app`
- Easier to shre logs for writing logs into files

## How to use?

Initialize the log module.

```swift
  let label = "xyz.123.qqq"
  let handler = HadesLogger.hadesHandler(label: label)
  log = Logger(label: label, handler)
  log.logLevel = .debug
  LoggingSystem.bootstrapInternal() { _ in handler }
```

You can print your logs with these methods (`log.debug()`, `log.info()`...). It's useful to print logs with `category` of metadata when you want to debug code via logs. You can filter logs with `category` to focus logs you want.

![filter xcode](./docs/images/filter_xcode.jpg)

![filter console](./docs/images/image-20220730224659248.png)

```swift
log.debug("hugo", metadata: ["category": "hugo"])
log.debug("mask", metadata: ["category": "mask"])
log.debug("default")
```

### Share logs

You can send the zip file to others later if the zip is successful.

```swift
let url = try fileLogHandler.zipLogs()
```

![zip logs](docs/images/image-20220730230255924.png)

For iOS side, you can share logs through `UIActivityViewController`, e.g.

```swift
guard let url = try? hadesLogger.zipLogs() else {
    return
}
var filesToShare = [Any]()
filesToShare.append(url)
let activityViewController = UIActivityViewController(
    activityItems: filesToShare,
    applicationActivities: nil
)
```

<img src="docs/images/image-20220731005753835.png" alt="share logs at iOS device" style="zoom: 25%;" />

## Class Diagram

![class diagram](./docs/01.class_diagram.png) 
