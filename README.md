# Go master 또는 아무개 branch 컴파일
작업 중에 다른 버전의 `Golang`을 임시로 돌려야 할 경우.
윈도우 파워셸 기준

## 1. Gotip 사용 - master만 컴파일
```sh
# 귀찮으니까 현재폴더/bin을 gotip 실행파일 저장경로로 잡아준다
$env:gobin=$(get-location).Path+"/bin"
go get golang.org/dl/gotip
# GOBIN을 비워주지 않으니까 에러가 막 뜬다.
ri env:gobin

$env:goroot_bootstrap=$env:goroot

.\bin\gotip.exe download

# Path, GOROOT 수정. GOBIN등은 알아서...
$env:goroot=$env:userprofile+"/sdk/gotip"
$env:path=$env:userprofile+"/sdk/gotip/bin"

# Go version 체크까지 하면 끝
go version

# 컴파일 결과물 삭제 - 중간 부산물 삭제는 알아서 ^-^
ri $env:userprofile"/sdk" -Force -Recurse
```

## 2. 직접 컴파일
```sh
git clone https://github.com/golang/go.git

ri env:gobin

# 원하는 branch로 체크아웃 - master는 생략해도 됨
cd go
git checkout master

cd go/src

$env:goroot_bootstrap=$env:goroot

make.bat
# 또는 all.bat

# 환경설정은 알아서 ^-^
# Gotip의 경우와 마찬가지로 path, goroot만 잡아주면 되고
# Gopath, Gocache 등은 어차피 기존 것을 그대로 쓰면 된다.

# 컴파일 결과물 및 부산물 삭제는 알아서 ^-^
```

참고:
* https://golang.org/doc/install/source
* https://godoc.org/golang.org/dl/gotip

끝.