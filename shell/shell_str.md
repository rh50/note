
## 变量子串，截取：
    ${param}: 返回变量$param的内容
    ${#param}: 返回变量$param的长度
    ${param:offset}: 从变量$param的offset开始提取子串到结尾处
    ${param:offset:length}: 从变量$param的offset开始提取长度为length的子串
    ${#param:-word}: 如果变量为空或未赋值，那么返回备用的word
    ${#param:=word}: 如果变量为空或为负值，返回备用的word并将param设置为word
