# 忽略列表

有时你可能不想同步某个资料库里的某些文件或文件夹。
为了满足这种需求，可以在资料库的根目录下创建一个叫做seafile-ignore.txt的文件。这个特定的文件指定了Seafile不应该同步的文件和文件夹。ignore.txt文件中的每一行指定了一个模式，下面是支持的模式格式。

1. 空行不和任何文件匹配
2. 以#开头的代表注释
3. Seafile在模式中支持通配符。例如，"foo/*" 匹配 "foo/1" 和 "foo/hello"。 "foo/?" 匹配 "foo/1"但不匹配"foo/hello"。 注意通配符号*递归地匹配一个文件夹下的所有路径。例如，"foo/*.html" 匹配 "foo/a.html" 和 "foo/templates/b.html"。
4. 如果模式以/结束，它只支持一个文件夹。换句话说，foo/只匹配一个文件夹，"foo"却可以匹配它和它下面的所有路径，但是却不匹配一个普通的文件或者符号连接"foo"。
5. 如果一个模式不以/或者*结束，它就不会和一个文件夹匹配。例如，"foo"可以只匹配普通文件"foo"或者符号链接；但是"foo/" 和"foo*"却可以匹配一个文件夹以及该文件夹下的所有路径。

## 示例

```
# 一个普通文件
test-file

# 一个路径
test-dir/

# 通配符 *
test-star1/*
test-star2/*.html

# 通配符 ?
test-qu1/?.html
test-qu2/?/
```

## 注意

seafile-ignore.txt文件只用来控制在客户端这边有哪些文件被排除在外。你也可以从Seahub网页上创建一个文件来排除客户端中同步的某些文件或文件夹。在这种情况下，

* 已经创建的文件仍然会被同步到客户端。但是任何后续的修改都会被忽略。
* 如果文件在Seahub上被修改了，该文件的新版本会被同步回客户端； 如果该文件在客户端也被修改了，客户端将会生成一个冲突文件。

seafile-ignore.txt只会忽略还未被同步的那些文件。如果一个文件已经被同步完成，而你在一段时间后才把它添加到忽略列表中，那么它的那个已经存在的版本将不会被删除掉。