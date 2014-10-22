#Go OpenCV binding

## Why fork?
Original project (https://code.google.com/p/go-opencv) looks abandoned. Therefore, I decide to fork it and host it on Github, so that others can help to maintain this package.

## Install

### Linux & Mac OS X

Install Go and OpenCV, you might want to install both of them via `apt-get` or `homebrew`.

```
go get github.com/lazywei/go-opencv
cd ${GoOpenCVRoot}/samples && go run hellocv.go
```

### Windows

- Install Go and MinGw
- install OpenCV-2.4.x to MinGW dir
  - `libopencv*.dll` --> `${MinGWRoot}\bin`
  - `libopencv*.lib` --> `${MinGWRoot}\lib`
  - `include\opencv` --> `${MinGWRoot}\include\opencv`
  - `include\opencv2` --> `${MinGWRoot}\include\opencv2`

```
go get code.google.com/p/go-opencv/trunk/opencv
cd ${GoOpenCVRoot}/trunk/samples && go run hellocv.go
```

## Example

### Resizing

```go
package main

import opencv "github.com/lidaohang/go-opencv/opencv"

func main() {
	filename := "bert.jpg"
	srcImg := opencv.LoadImage(filename)
	if srcImg == nil {
		panic("Loading Image failed")
		return nil
	}
	defer srcImg.Release()
	
	destImg := opencv.Resize(srcImg, 400, 300, 2)
	destImg.Release()
	img := opencv.EncodeImage(".jpg", unsafe.Pointer(destImg), 80)
	return img.GetData()
}
```

### Webcam

Yet another cool example is created by @saratovsource which demos how to use webcam:

```
cd samples
go run webcam.go
```

### More

You can find more samples at: https://github.com/lazywei/go-opencv/tree/master/samples

## How to contribute

- Fork this repo
- Clone the main repo, and add your fork as a remote

```
git clone https://github.com/lazywei/go-opencv.git
cd go-opencv
git remote rename origin upstream
git remote add origin https://github.com/your_github_account/go-opencv.git
```

- Create new feature branch

```
git checkout -b your-feature-branch
```

- Commit your change and push it to your repo 

```
git commit -m 'new feature'
git push origin your-feature-branch
```

- Open a pull request!

## TODOs
- More details doc
- Implement more bindings
