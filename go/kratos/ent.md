# ENT

## 工具
```go
go get entgo.io/ent/cmd/ent
```

## 魔改工具

[包名](entgo.io/ent/entc)

## 步骤
```go
//创建ent/schema下默认文件User.go,School.go
ent init User School ...

//修改User.go等，添加字段，依赖等等

//根据./ent/schema下的文件自动生成调用函数文件
go generate ./ent
```
<image  src="./ent.png">

## templates
```shell
ent generate --template <dir-path> --template glob="xxxx/*.tmpl" ./ent/schema
```

## description
```shell
ent describe ./ent/schema
```
## Field类型
[链接](https://entgo.io/docs/schema-fields/#built-in-validators)
```go
func (User)Fields()[]ent.Field {
    return []ent.Field{
        field.Int("age").Positive(),
        field.Float("rank").Optional(),
        field.Bool("active").Default(false),
        field.String("name").Unique(),
        field.Time("created_at").Default(time.Now),
        field.JSON("url", &url.URL{}).Optional(),
        field.JSON("strings",[]string{}).Optional(),
        field.Enum("state").Values("on","off").Optional(),
        field.UUID("uuid",uuid.UUID{}).Default(uuid.New),
    }
}
```

## Edges  外键
通常用来描述数个Entity之间的从属关系
```go
func (User) Edges() []ent.Edge{
    return []ent.Edge{
        edge.To("pets".Pet.Type)
    }
}

func (Pet)Edges() []ent.Edge{
    return []ent.Edge{
        edge.From("owner",User.Type).Ref("pets").Unique(),
    }
}

//Unique 决定成员 是否是 数组

func (User)Fields() ent.Field {
    return []ent.Field {
        edge.To("friends",User.Type),
    }
}
type User struct{
    Friends []User
}

```
## Indexes 索引

```go
func (User) Indexes() []ent.Index{
    return []ent.Index{
        index.Fields("field1","field2"),
        index.Fields("first_name","last_name").Unique(),
    }
}

```

## Mixin 处理公共Field

```go
type TimeMixin struct {
    mixin.Schema
}

//Immutable 表示只赋值一次
func (TimeMixin)Fields() []ent.Field {
    return []ent.Field{
        field.Time("created_at").Immutable().Default(time.Now),
        field.Time("updated_at").Default(time.Now).UpdateDefault(time.Now),
    }
}

```

## Annotations 注释
