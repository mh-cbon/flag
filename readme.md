# flag

[![Build Status](https://travis-ci.org/posener/flag.svg?branch=master)](https://travis-ci.org/posener/flag)
[![codecov](https://codecov.io/gh/posener/flag/branch/master/graph/badge.svg)](https://codecov.io/gh/posener/flag)
[![GoDoc](https://godoc.org/github.com/posener/flag?status.svg)](http://godoc.org/github.com/posener/flag)
[![Go Report Card](https://goreportcard.com/badge/github.com/posener/flag)](https://goreportcard.com/report/github.com/posener/flag)

Experimental

Flag library that provides bash completion out of the box, 
it is also fully compatible with standard library flag package.

## Features

* file completion flag
* directory completion flag
* bool flag (that does not complete)
* set flag
* custom completions

## Usage

```diff
import (
-	"flag"
+	"github.com/posener/flag"
)

var (
-	file = flag.String("file", "", "file value")
+	file = flag.File("file", "*.md", "", "file value")
-	dir  = flag.String("dir", "", "dir value")
+	dir  = flag.Dir("dir", "*", "", "dir value")
	b    = flag.Bool("bool", false, "bool value")
	s    = flag.String("any", "", "string value")
)

func main() {
+	if flag.Complete() {  // runs bash completion if necessary
+		return  // return from main without executing the rest of the command
+	}
+	flag.AddCompleteFlags(nil, "complete", "uncomplete")  // add flags for (un)installing bash completion
	flag.Parse()
+	if flag.ParseInstallFlags() {  // parse bash completion installation flags
+		return  // return from main if the bash completion was installed
+	}
    ...
}
```

## Example

Here is an [example](./example/example.go)
