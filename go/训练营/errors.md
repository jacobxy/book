# errors

errors.New() 返回的是指针 

errors.New("A") != errors.New("A")

# errorgroup
[errgroup](https://github.com/golang/sync/blob/036812b2e83c0ddf193dd5a34e034151da389d09/errgroup/errgroup.go)

```go
type Group struct {
	cancel func()

	wg sync.WaitGroup

	errOnce sync.Once
	err     error
}
```

## 预定义的错误信息
例：io.EOF

无法携带上下文
扩大包级别的表面积

## 自定义类型
```go
type MyError struct {
	Msg string
	File string 
	Line int	
}

func (e *MyError)Error() string{
	return fmt.Sprintf("%s:%d:%s", e.File, e.Line,e.Msg)
}
```

## 不透明的错误类型
```go
type temporary interface {
	Temporary() bool
}

func IsTemporary(err error)bool {
	te,ok := err.(tempporary)
	return ok && te.Temporary()
}
```

## Wrap errors

[errors]
```go
	
	//%w 表达需要wrapError
	err1 := fmt.Errorf("XXXXXX %v : %w",name,err)

	//判断是否是同一血脉的error
	errors.Is(err1,err)

	//判断是否可以转换为同一血脉的error
	var err2 error
	errors.As(err1, &err2)

	type wrapError struct {
		msg string
		err error
	}

	func (w wrapEror)UnWrap() error {return w.err}

```

[pkg/errors](https://github.com/pkg/errors)

```go
	errors.WithMessage
	errors.withStack

	//会记录堆栈信息
	errors.Wrap(err,"open failed")

	fmt.Println("%+v",err)

	errors.Cause()获取root error
```
包含了堆栈信息,所以推荐只用 pkg/errors.Wrap 来包装，errors.Is 来判断


