# Robotgo

<!--<img align="right" src="https://raw.githubusercontent.com/go-vgo/robotgo/master/logo.jpg">-->
<!--[![Build Status](https://travis-ci.org/go-vgo/robotgo.svg)](https://travis-ci.org/go-vgo/robotgo)
[![codecov](https://codecov.io/gh/go-vgo/robotgo/branch/master/graph/badge.svg)](https://codecov.io/gh/go-vgo/robotgo)-->
<!--<a href="https://circleci.com/gh/go-vgo/robotgo/tree/dev"><img src="https://img.shields.io/circleci/project/go-vgo/robotgo/dev.svg" alt="Build Status"></a>-->
[![Build Status](https://github.com/go-vgo/robotgo/workflows/Go/badge.svg)](https://github.com/go-vgo/robotgo/commits/master)
[![CircleCI Status](https://circleci.com/gh/go-vgo/robotgo.svg?style=shield)](https://circleci.com/gh/go-vgo/robotgo)
[![Build Status](https://travis-ci.org/go-vgo/robotgo.svg)](https://travis-ci.org/go-vgo/robotgo)
![Appveyor](https://ci.appveyor.com/api/projects/status/github/go-vgo/robotgo?branch=master&svg=true)
[![Go Report Card](https://goreportcard.com/badge/github.com/go-vgo/robotgo)](https://goreportcard.com/report/github.com/go-vgo/robotgo)
[![GoDoc](https://godoc.org/github.com/go-vgo/robotgo?status.svg)](https://godoc.org/github.com/go-vgo/robotgo)
[![GitHub release](https://img.shields.io/github/release/go-vgo/robotgo.svg)](https://github.com/go-vgo/robotgo/releases/latest)
[![Join the chat at https://gitter.im/go-vgo/robotgo](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/go-vgo/robotgo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
<!-- [![Release](https://github-release-version.herokuapp.com/github/go-vgo/robotgo/release.svg?style=flat)](https://github.com/go-vgo/robotgo/releases/latest) -->
<!-- <a href="https://github.com/go-vgo/robotgo/releases"><img src="https://img.shields.io/badge/%20version%20-%206.0.0%20-blue.svg?style=flat-square" alt="Releases"></a> -->

> Golang Desktop Automation. Control the mouse, keyboard, bitmap and image, read the screen, process, Window Handle and global event listener.

RobotGo supports Mac, Windows, and Linux(X11); and robotgo supports arm64 and x86-amd64.

[Chinese Simplified](https://github.com/go-vgo/robotgo/blob/master/README_zh.md)

## Contents
- [Docs](#docs)
- [Binding](#binding)
- [Requirements](#requirements)
- [Installation](#installation)
- [Update](#update)
- [Examples](#examples)
- [Cross-Compiling](#crosscompiling)
- [Authors](#authors)
- [Plans](#plans)
- [Donate](#donate)
- [Contributors](#contributors)
- [License](#license)

## Docs
  - [GoDoc](https://godoc.org/github.com/go-vgo/robotgo) <br>
  
  - [API Docs](https://github.com/go-vgo/robotgo/blob/master/docs/doc.md)  (Deprecated, no updated)
  - [Chinese Docs](https://github.com/go-vgo/robotgo/blob/master/docs/doc_zh.md) (Deprecated, no updated)

## Binding:
[ADB](https://github.com/vcaesar/adb), packaging android adb API.

[Robotn](https://github.com/vcaesar/robotn), binding JavaScript and other, support more language.

## Requirements:

Now, Please make sure `Golang, GCC` is installed correctly before installing RobotGo.

### ALL:
```
Golang

GCC
```

#### For Mac OS X:

Xcode Command Line Tools (And Privacy setting: [#277](https://github.com/go-vgo/robotgo/issues/277) )

```
xcode-select --install
```

#### For Windows:

[MinGW-w64](https://sourceforge.net/projects/mingw-w64/files) (Use recommended) 

```
Or the other GCC (But you should compile the "libpng" with yourself. 
Or you can removed the bitmap.go. 

In the plans, the bitmap.go will moves to the bitmap dir, but break the API. )
```

#### For everything else:

```
GCC, libpng

X11 with the XTest extension (also known as the Xtst library)

Event:

xcb, xkb, libxkbcommon
```

##### Ubuntu:

```yml
# gcc
sudo apt install gcc libc6-dev

sudo apt install libx11-dev xorg-dev libxtst-dev libpng++-dev

sudo apt install xcb libxcb-xkb-dev x11-xkb-utils libx11-xcb-dev libxkbcommon-x11-dev libxkbcommon-dev

sudo apt install xsel xclip
```

##### Fedora:

```yml
sudo dnf install libxkbcommon-devel libXtst-devel libxkbcommon-x11-devel xorg-x11-xkb-utils-devel

sudo dnf install libpng-devel

sudo dnf install xsel xclip
```

## Installation:

With Go module support (Go 1.11+), just import:

```go
import "github.com/go-vgo/robotgo"
```

Otherwise, to install the robotgo package, run the command:

```
go get github.com/go-vgo/robotgo
```

png.h: No such file or directory? Please see [issues/47](https://github.com/go-vgo/robotgo/issues/47).

## Update:
```
go get -u github.com/go-vgo/robotgo
```

Note go1.10.x C file compilation cache problem, [golang #24355](https://github.com/golang/go/issues/24355).
`go mod vendor` problem, [golang #26366](https://github.com/golang/go/issues/26366).


## [Examples:](https://github.com/go-vgo/robotgo/blob/master/examples)

#### [Mouse](https://github.com/go-vgo/robotgo/blob/master/examples/mouse/main.go)

```Go
package main

import (
  "github.com/go-vgo/robotgo"
)

func main() {
  // robotgo.ScrollMouse(10, "up")
  robotgo.Scroll(0, -10)
  robotgo.Scroll(100, 0)

  robotgo.MilliSleep(100)
  robotgo.ScrollSmooth(-10, 6)
  // robotgo.ScrollRelative(10, -100)

  robotgo.MouseSleep = 100
  robotgo.Move(10, 20)
  robotgo.MoveRelative(0, -10)
  robotgo.Drag(10, 10)

  robotgo.Click("wheelRight")
  robotgo.Click("left", true)
  robotgo.MoveSmooth(100, 200, 1.0, 10.0)

  robotgo.Toggle("left")
  robotgo.Toggle("left", "up")
}
```

#### [Keyboard](https://github.com/go-vgo/robotgo/blob/master/examples/key/main.go)

```Go
package main

import (
  "fmt"

  "github.com/go-vgo/robotgo"
)

func main() {
  robotgo.TypeStr("Hello World")
  robotgo.TypeStr("だんしゃり", 1.0)
  // robotgo.TypeStr("テストする")

  robotgo.TypeStr("Hi galaxy. こんにちは世界.")
  robotgo.Sleep(1)

  // ustr := uint32(robotgo.CharCodeAt("Test", 0))
  // robotgo.UnicodeType(ustr)

  robotgo.KeySleep = 100
  robotgo.KeyTap("enter")
  // robotgo.TypeStr("en")
  robotgo.KeyTap("i", "alt", "command")

  arr := []string{"alt", "command"}
  robotgo.KeyTap("i", arr)

  robotgo.MilliSleep(100)
  robotgo.KeyToggle("a")
  robotgo.KeyToggle("a", "up")

  robotgo.WriteAll("Test")
  text, err := robotgo.ReadAll()
  if err == nil {
    fmt.Println(text)
  }
}
```

#### [Screen](https://github.com/go-vgo/robotgo/blob/master/examples/screen/main.go)

```Go
package main

import (
  "fmt"

  "github.com/go-vgo/robotgo"
  "github.com/vcaesar/imgo"
)

func main() {
  x, y := robotgo.GetMousePos()
  fmt.Println("pos: ", x, y)

  color := robotgo.GetPixelColor(100, 200)
  fmt.Println("color---- ", color)

  sx, sy := robotgo.GetScreenSize()
  fmt.Println("get screen size: ", sx, sy)

  bit := robotgo.CaptureScreen(10, 10, 30, 30)
  defer robotgo.FreeBitmap(bit)
  robotgo.SaveBitmap(bit, "test_1.png")

  img := robotgo.ToImage(bit)
  imgo.Save("test.png", img)
}
```

#### [Bitmap](https://github.com/go-vgo/robotgo/blob/master/examples/bitmap/main.go)

```Go
package main

import (
  "fmt"

  "github.com/go-vgo/robotgo"
)

func main() {
  bitmap := robotgo.CaptureScreen(10, 20, 30, 40)
  // use `defer robotgo.FreeBitmap(bit)` to free the bitmap
  defer robotgo.FreeBitmap(bitmap)

  fmt.Println("bitmap...", bitmap)
  img := robotgo.ToImage(bitmap)
  robotgo.SavePng(img, "test_1.png")

  bit2 := robotgo.ToCBitmap(robotgo.ImgToBitmap(img))
  fx, fy := robotgo.FindBitmap(bit2)
  fmt.Println("FindBitmap------ ", fx, fy)
  robotgo.Move(fx, fy)

  arr := robotgo.FindAllBitmap(bit2)
  fmt.Println("Find all bitmap: ", arr)
  robotgo.SaveBitmap(bitmap, "test.png")

  fx, fy = robotgo.FindBitmap(bitmap)
  fmt.Println("FindBitmap------ ", fx, fy)

  robotgo.SaveBitmap(bitmap, "test.png")
}
```

#### [OpenCV](https://github.com/vcaesar/gcv)

```Go
package main

import (
  "fmt"
  "math/rand"

  "github.com/go-vgo/robotgo"
  "github.com/vcaesar/gcv"
)

func main() {
  opencv()
}

func opencv() {
  name := "test.png"
  name1 := "test_001.png"
  robotgo.SaveCapture(name1, 10, 10, 30, 30)
  robotgo.SaveCapture(name)

  fmt.Print("gcv find image: ")
  fmt.Println(gcv.FindImgFile(name1, name))
  fmt.Println(gcv.FindAllImgFile(name1, name))

  bit := robotgo.OpenBitmap(name1)
  defer robotgo.FindBitmap(bit)
  fmt.Print("find bitmap: ")
  fmt.Println(robotgo.FindBitmap(bit))

  // bit0 := robotgo.CaptureScreen()
  // img := robotgo.ToImage(bit0)
  // bit1 := robotgo.CaptureScreen(10, 10, 30, 30)
  // img1 := robotgo.ToImage(bit1)
  // defer robotgo.FreeBitmapArr(bit0, bit1)
  img := robotgo.CaptureImg()
  img1 := robotgo.CaptureImg(10, 10, 30, 30)

  fmt.Print("gcv find image: ")
  fmt.Println(gcv.FindImg(img1, img))
  fmt.Println()

  res := gcv.FindAllImg(img1, img)
  fmt.Println(res[0].TopLeft.Y, res[0].Rects.TopLeft.X, res)
  x, y := res[0].TopLeft.X, res[0].TopLeft.Y
  robotgo.Move(x, y-rand.Intn(5))
  robotgo.MilliSleep(100)
  robotgo.Click()

  res = gcv.FindAll(img1, img) // use find template and sift
  fmt.Println("find all: ", res)
  res1 := gcv.Find(img1, img)
  fmt.Println("find: ", res1)

  img2, _, _ := robotgo.DecodeImg("test_001.png")
  x, y = gcv.FindX(img2, img)
  fmt.Println(x, y)
}
```

#### [Event](https://github.com/go-vgo/robotgo/blob/master/examples/gohook/main.go)

```Go
package main

import (
  "fmt"

  "github.com/go-vgo/robotgo"
  hook "github.com/robotn/gohook"
)

func main() {
  add()
  low()
  event()
}

func add() {
  fmt.Println("--- Please press ctrl + shift + q to stop hook ---")
  robotgo.EventHook(hook.KeyDown, []string{"q", "ctrl", "shift"}, func(e hook.Event) {
    fmt.Println("ctrl-shift-q")
    robotgo.EventEnd()
  })

  fmt.Println("--- Please press w---")
  robotgo.EventHook(hook.KeyDown, []string{"w"}, func(e hook.Event) {
    fmt.Println("w")
  })

  s := robotgo.EventStart()
  <-robotgo.EventProcess(s)
}

func low() {
	evChan := hook.Start()
	defer hook.End()

	for ev := range evChan {
		fmt.Println("hook: ", ev)
	}
}

func event() {
  ok := robotgo.AddEvents("q", "ctrl", "shift")
  if ok {
    fmt.Println("add events...")
  }

  keve := robotgo.AddEvent("k")
  if keve {
    fmt.Println("you press... ", "k")
  }

  mleft := robotgo.AddEvent("mleft")
  if mleft {
    fmt.Println("you press... ", "mouse left button")
  }
}
```

#### [Window](https://github.com/go-vgo/robotgo/blob/master/examples/window/main.go)

```Go
package main

import (
  "fmt"

  "github.com/go-vgo/robotgo"
)

func main() {
  fpid, err := robotgo.FindIds("Google")
  if err == nil {
    fmt.Println("pids... ", fpid)

    if len(fpid) > 0 {
      robotgo.ActivePID(fpid[0])

      robotgo.Kill(fpid[0])
    }
  }

  robotgo.ActiveName("chrome")

  isExist, err := robotgo.PidExists(100)
  if err == nil && isExist {
    fmt.Println("pid exists is", isExist)

    robotgo.Kill(100)
  }

  abool := robotgo.ShowAlert("test", "robotgo")
  if abool {
 	  fmt.Println("ok@@@ ", "ok")
  }

  title := robotgo.GetTitle()
  fmt.Println("title@@@ ", title)
}
```

## CrossCompiling

##### Windows64 to windows32
```Go
SET CGO_ENABLED=1
SET GOARCH=386
go build main.go
```

#### Other to windows

Install Requirements (Ubuntu):
```bash
sudo apt install gcc-multilib
sudo apt install gcc-mingw-w64
# fix err: zlib.h: No such file or directory
sudo apt install libz-mingw-w64-dev
```

Build the binary:
```Go
GOOS=windows GOARCH=amd64 CGO_ENABLED=1 CC=x86_64-w64-mingw32-gcc CXX=x86_64-w64-mingw32-g++ go build -x ./
```

```
// CC=mingw-w64\x86_64-7.2.0-win32-seh-rt_v5-rev1\mingw64\bin\gcc.exe
// CXX=mingw-w64\x86_64-7.2.0-win32-seh-rt_v5-rev1\mingw64\bin\g++.exe
```

Some discussions and questions, please see [issues/228](https://github.com/go-vgo/robotgo/issues/228), [issues/143](https://github.com/go-vgo/robotgo/issues/143).

## Authors
* [The author is vz](https://github.com/vcaesar)
* [Maintainers](https://github.com/orgs/go-vgo/people)
* [Contributors](https://github.com/go-vgo/robotgo/graphs/contributors)

## Plans
- Update Find an image on screen, read pixels from an image
- Update Window Handle
- Try support Android, maybe support IOS

## Contributors

- See [contributors page](https://github.com/go-vgo/robotgo/graphs/contributors) for full list of contributors.
- See [Contribution Guidelines](https://github.com/go-vgo/robotgo/blob/master/CONTRIBUTING.md).

## License

Robotgo is primarily distributed under the terms of "both the MIT license and the Apache License (Version 2.0)", with portions covered by various BSD-like licenses.

See [LICENSE-APACHE](http://www.apache.org/licenses/LICENSE-2.0), [LICENSE-MIT](https://github.com/go-vgo/robotgo/blob/master/LICENSE).
