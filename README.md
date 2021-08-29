# Zerologr

[![Go Reference](https://pkg.go.dev/badge/github.com/hn8/zerologr.svg)](https://pkg.go.dev/github.com/hn8/zerologr)
![test](https://github.com/hn8/zerologr/workflows/test/badge.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/hn8/zerologr)](https://goreportcard.com/report/github.com/hn8/zerologr)

A [logr](https://github.com/go-logr/logr) LogSink implementation using [Zerolog](https://github.com/rs/zerolog).

## Usage

```go
import (
    "os"

    "github.com/go-logr/logr"
    "github.com/hn8/zerologr"
    "github.com/rs/zerolog"
)

func main() {
    zerologr.NameFieldName = "logger"
    zerologr.NameSeparator = "/"

    zl := zerolog.New(os.Stderr)
    var log logr.Logger = zerologr.New(&zl)

    log.Info("Logr in action!", "the answer", 42)
}
```

## Implementation Details

For the most part, concepts in Zerolog correspond directly with those in logr.

Levels in logr correspond to custom debug levels in Zerolog. Any given level
in logr is represents by `zerologLevel = 1 - logrLevel`.

For example `V(2)` is equivalent to Zerolog's `TraceLevel`, while `V(1)` is
equivalent to Zerolog's `DebugLevel`.
