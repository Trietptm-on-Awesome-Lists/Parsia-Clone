---
date: 2018-04-27T23:03:22-04:00
draft: false
toc: false
comments: false
categories:
- Research
tags:
- Go-Fuzz
- Fuzzing
title: "Go-Fuzz Quickstart"
wip: false
snippet: "Steps to get fuzzing with Go-Fuzz quickly."
---

# Quickstart

1. Get Go-fuzz by `go get github.com/dvyukov/go-fuzz`.
2. Build and install `go-fuzz` and `go-fuzz-build`.
    - `cd src\github.com\dvyukov\go-fuzz\go-fuzz`
    - `go install`
    - `cd ..\go-fuzz-build`
    - `go install`
3. Get the target package and store it in `GOPATH`. I usually keep it under `src\github.com\author\project`.
4. Create a new file in the target package named `Fuzz.go`.
5. Create a function named `Fuzz` inside `Fuzz.go` with this signature `func Fuzz(data []byte) int`.
6. `Fuzz` should return `1` if input is good and `0` otherwise.
7. Create fuzzing directory, e.g. `go-fuzz-project-name`.
8. `go-fuzz-build github.com/author/project` (note forward slashes even on Windows). Copy the resulting file (`project-fuzz.zip`) to fuzzing directory.
9. Make a directory called `corpus` and store samples there.
10. `go-fuzz -bin=project-fuzz.zip -workdir=.` to begin fuzzing.

## Links

- Main repo: https://github.com/dvyukov/go-fuzz
- Example by @dgryski: https://medium.com/@dgryski/go-fuzz-github-com-arolek-ase-3c74d5a3150c
- Example by Nemanja Mijailovic: https://mijailovic.net/2017/07/29/go-fuzz/
- DNS parser, meet Go fuzzer by Filippo Valsorda: https://blog.cloudflare.com/dns-parser-meet-go-fuzzer/
    - His talk at GothamGo 2015: https://www.youtube.com/watch?v=kOZbFSM7PuI
