# Go Persian Calendar

[![godoc](https://img.shields.io/badge/godoc-reference-blue.svg)](https://godoc.org/github.com/yaa110/go-persian-calendar) [![Build Status](https://travis-ci.org/yaa110/go-persian-calendar.svg)](https://travis-ci.org/yaa110/go-persian-calendar) [![goreportcard](https://img.shields.io/badge/go%20report-A%2B-brightgreen.svg)](http://goreportcard.com/report/yaa110/go-persian-calendar) [![License](http://img.shields.io/:license-mit-blue.svg)](https://github.com/yaa110/go-persian-calendar/blob/master/LICENSE)

**Go Persian Calendar** provides functionality for conversion among Persian (Solar Hijri) and Gregorian calendars. A Julian calendar is used as an interface for all conversions. The package name is `ptime` and it is compatible with the package [time](https://golang.org/pkg/time). All months are available with both Iranian and Dari Persian names. This source code is licensed under MIT license that can be found in the LICENSE file.

## Installation

```bash
go get github.com/alirezarabie/go-persian-calendar-f
```

## Getting started

1- Import the package `ptime`. Most of the time you need to import `time` and `fmt` packages, too.

```go
import (
    ptime "github.com/alirezarabie/go-persian-calendar-f"
    "time"
    "fmt"
)
```

2- Convert Gregorian calendar to Persian calendar.

```go
// Create a new instance of time.Time
var t time.Time = time.Date(2016, time.January, 1, 12, 1, 1, 0, ptime.Iran())

// Get a new instance of ptime.Time using time.Time
pt := ptime.New(t)

// Get the date in Persian calendar
fmt.Println(pt.Date()) // output: 1394 دی 11
```

3- Convert Persian calendar to Gregorian calendar.

```go
// Create a new instance of ptime.Time
var pt ptime.Time = ptime.Date(1394, ptime.Mehr, 2, 12, 59, 59, 0, ptime.Iran())

// Get a new instance of time.Time
t := pt.Time()

// Get the date in Gregorian calendar
fmt.Println(t.Date()) // output: 2015 September 24
```

4- Get the current time.

```go
// Get a new instance of ptime.Time representing the current time
pt := ptime.Now()

// Get year, month, day
fmt.Println(pt.Date()) // output: 1394 بهمن 11
fmt.Println(pt.Year(), pt.Month(), pt.Day()) // output: 1394 بهمن 11

// Get hour, minute, second
fmt.Println(pt.Clock()) // output: 21 54 30
fmt.Println(pt.Hour(), pt.Minute(), pt.Second()) // output: 21 54 30

// Get Unix timestamp (the number of seconds since January 1, 1970 UTC)
fmt.Println(pt.Unix()) // output: 1454277270

// Get yesterday, today and tomorrow
fmt.Println(pt.Yesterday().Weekday()) // output: شنبه
fmt.Println(pt.Weekday()) // output: یک‌شنبه
fmt.Println(pt.Tomorrow().Weekday()) // output: دوشنبه

// Get First and last day of week
fmt.Println(pt.FirstWeekDay().Date()) // output: 1394 بهمن 10
fmt.Println(pt.LastWeekday().Date()) // output: 1394 بهمن 16

// Get First and last day of month
fmt.Println(pt.FirstMonthDay().Weekday()) // output: پنج‌شنبه
fmt.Println(pt.LastMonthDay().Weekday()) // output: جمعه

// Get First and last day of year
fmt.Println(pt.FirstYearDay().Weekday()) // output: شنبه
fmt.Println(pt.LastYearDay().Weekday()) // output: شنبه

// Get the week of month
fmt.Println(pt.MonthWeek()) // output: 3

// Get the week of year
fmt.Println(pt.YearWeek()) // output: 46

// Get the number of remaining weeks of the year
fmt.Println(pt.RYearWeek()) // output: 6
```

5- Format the time.

```go
// Get a new instance of ptime.Time using Unix timestamp
pt := ptime.Unix(1454277270, 0)

fmt.Println(pt.Format("yyyy/MM/dd E hh:mm:ss a")) // output: 1394/11/11 یک‌شنبه 09:54:30 ب.ظ

// yyyy, yyy, y     year (e.g. 1394)
// yy               2-digits representation of year (e.g. 94)
// MMM              the Persian name of month (e.g. فروردین)
// MMI              the Dari name of month (e.g. حمل)
// MM               2-digits representation of month (e.g. 01)
// M                month (e.g. 1)
// rw               remaining weeks of year
// w                week of year
// W                week of month
// RD               remaining days of year
// D                day of year
// rd               remaining days of month
// dd               2-digits representation of day (e.g. 01)
// d                day (e.g. 1)
// E                the Persian name of weekday (e.g. شنبه)
// e                the Persian short name of weekday (e.g. ش)
// A                the Persian name of 12-Hour marker (e.g. قبل از ظهر)
// a                the Persian short name of 12-Hour marker (e.g. ق.ظ)
// HH               2-digits representation of hour [00-23]
// H                hour [0-23]
// kk               2-digits representation of hour [01-24]
// k                hour [1-24]
// hh               2-digits representation of hour [01-12]
// h                hour [1-12]
// KK               2-digits representation of hour [00-11]
// K                hour [0-11]
// mm               2-digits representation of minute [00-59]
// m                minute [0-59]
// ss               2-digits representation of seconds [00-59]
// s                seconds [0-59]
// ns               nanoseconds
// S                3-digits representation of milliseconds (e.g. 001)
// z                the name of location
// Z                zone offset (e.g. +03:30)
```

6- Format the time using [standard format](https://golang.org/src/time/format.go).

```go
pt := ptime.Date(1394, 7, 2, 14, 7, 8, 0, Iran())

fmt.Println(pt.TimeFormat("2 Jan 2006")) // output: 2 مهر 1394

// 2006        four digit year (e.g. 1399)
// 06          two digit year (e.g. 99)
// 01          two digit month (e.g. 01)
// 1           one digit month (e.g. 1)
// Jan         month name (e.g. آذر)
// January     month name (e.g. آذر)
// 02          two digit day (e.g. 07)
// 2           one digit day (e.g. 7)
// _2          right justified two character day (e.g.  7)
// Mon         weekday (e.g. شنبه)
// Monday      weekday (e.g. شنبه)
// 03          two digit 12 hour format (e.g. 03)
// 3           one digit 12 hour format (e.g. 3)
// 15          two digit 24 hour format (e.g. 15)
// 04          two digit minute (e.g. 03)
// 4           one digit minute (e.g. 03)
// 05          two digit minute (e.g. 09)
// 5           one digit minute (e.g. 9)
// .000        millisecond (e.g. .120)
// .000000     microsecond (e.g. .123400)
// .000000000  nanosecond (e.g. .123456000)
// .999        trailing zeros removed millisecond (e.g. .12)
// .999999     trailing zeros removed microsecond (e.g. .1234)
// .999999999  trailing zeros removed nanosecond (e.g. .123456)
// PM          full 12-Hour marker (e.g. قبل از ظهر)
// pm          short 12-Hour marker (e.g. ق.ظ)
// MST         the name of location
// -0700       zone offset (e.g. +0330)
// -07         zone offset (e.g. +03)
// -07:00      zone offset (e.g. +03:30)
// Z0700       zone offset (e.g. +0330)
// Z07:00      zone offset (e.g. +03:30)
```

## Changelog

### v1.0.0

- Remove `loc *time.Location` argument from `ptime.Unix()`, `ptime.SetUnix()` and `ptime.Now()`

### v0.6.0

- Support standard time format

### v0.5.0

- Add `BeginningOfWeek`, `BeginningOfMonth` and `BeginningOfYear` methods.
- Format UTC timezone by `Z` instead of `+00:00`

### v0.4.1

- Refactor code

### v0.4.0

- Change module import name

### v0.3.1

- Use Go modules

### v0.3

- `ptime.Iran` and `ptime.Afghanistan` changed to `ptime.Iran()` and `ptime.Afghanistan()`, respectively.

## Documentation

Use [GoDoc documentation](https://godoc.org/github.com/yaa110/go-persian-calendar) for more information about methods and functionality available for `ptime.Time`, `ptime.Month`, `ptime.Weekday` and `ptime.AmPm`.
