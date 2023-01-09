
# 运行系统命令

## os.execute("cmd") 可以执行命令，但是返回的是系统状态码，默认输出
```lua
os.execute("cp a b")
```

## io.popen("") 也可以执行命令，但是返回一个文件
```lua
local t = io.popen('svn help')
local a = t:read("*all")
```
