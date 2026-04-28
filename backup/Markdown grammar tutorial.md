# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

（“#”后需要空一格）

#这是一个标签


# 文字样式
## 加粗：
**obisidian**    分别 在 需要加粗文字前后添加两个星号      or     选中文字然后Ctrl+B

## 倾斜：
*obisidian*     分别 在 需要加粗文字前后添加单个星号      or     选中文字然后Ctrl+I

## 高亮：
==obisidian==     分别 在 需要加粗文字前后添加两个等号

## 下划线：
<u>obisidian</u>    用u标签包住文字

## 删除线：
~~obisidian~~      分别 在 需要加粗文字前后添加两个波浪号 

## 超链接：
王力宏[《我们的歌》](【【1080P】王力宏2021福利秀《我们的歌》】 https://www.bilibili.com/video/BV1zV411e7id/?share_source=copy_web&vd_source=b4602159fb04925f1f56ddcad61dc50f)                                                             选中文字然后Ctrl+K并附上链接

| 样式         | 语法          | 快捷键    | 示例              |
| ---------- | ----------- | ------ | --------------- |
| **加粗**     | `**文字**`    | Ctrl+B | **Obsidian**    |
| *倾斜*       | `*文字*`      | Ctrl+I | *Obsidian*      |
| ==高亮==     | `==文字==`    | -      | ==Obsidian==    |
| <u>下划线</u> | `<u>文字</u>` | -      | <u>Obsidian</u> |
| ~~删除线~~    | `~~文字~~`    | -      | ~~Obsidian~~    |


# 有序列表
1. first
2. second
3. third
## ==序号和文字直接一定要有space==


# 无序列表
- ajskldj
	- asjioduqw
- dqoiwrufn
- aoieurg
## ==减号“-”和文字直接一定要有space==

# 任务列表
- [x] 未完成任务1
- [ ] 未完成任务2

## ==减号“-”加中括号“[ ]”且三个符号中间一定要有space==


### **以上三种列表都可以使用==Tab==实现缩进，以及==Shift＋Tab==取消缩进**


# 引用
> quote
> This is a quote. 
> You just need to add  symbol '>' at every line to achieve your quote. 


# Callout 引用
> [!danger]  Dangerous behavior !

> [!attention] 

> [!tip] 

> [!note] 

> [!abstract] 

> [!example] 

> [!question] 


# 链接

# 跳转链接
两个左中括号

[[Welcome]]

[[Welcome]]|[[create a link]]

## 嵌入链接
在跳转链接前加感叹号即可
![[Welcome]]


# 其他样式

## 脚注 [^1]    

[^1]: 是的
**方括号加^符号**


## 分割线

这是普通内容

 ---


##### 最好要在普通内容后==再空一行==，否则识别为标题


## 代码块

```
n=eval(input())  
a=1  
b=1  
c=1  
print(a)  
print(b)  
for i in range(1,n):  
    c = a + b  
    a = b  
    b = c  
    print(c)
```

使用符号键盘左上Esc下方的按键连续三次，位置分别在代码块的上下


---

###  Markdown 表格创建技巧

#### 1. **基础结构**
```markdown
| 表头1   | 表头2   |
|---------|---------|
| 内容A   | 内容B   |
```
- 第一行定义表头
- 第二行用 `|---|` 分隔表头和内容
- 从第三行开始写实际内容

#### 2. **对齐控制**
```markdown
| 左对齐      | 居中对齐    | 右对齐      |
|:------------|:-----------:|------------:|
| 文本        | 文本        | 文本        |
```
- `:---` 左对齐
- `:---:` 居中对齐
- `---:` 右对齐

#### 3. **内容排版技巧**
- **特殊字符处理**：
  ```markdown
  | 显示 \| 符号 | 使用 `\|` 转义 |
  ```
- **多行内容**：
  ```markdown
  | 单元格1 | <div style="width:100px">单元格2<br>第二行内容</div> |
  ```
- **嵌入样式**：
  ```markdown
  | 样式 | 示例 |
  |------|------|
  | 颜色 | <span style="color:red">红色文字</span> |
  ```



# Ctrl＋E 切换编辑和阅读模式

 ---
 


# 颜色编辑 （类似CSS）

```markdown
<span style="color:red">红色文字</span>
<span style="color:#00FFFF">绿色文字</span>
<span style="background-color:yellow; color:black">黄底黑字</span>
<span style='background-color:#000000;color:#FFFFFF'>我是红色</span>
```

### **以下为效果：**

<span style="color:red">红色文字</span>
<span style="color:#00FFFF">绿色文字</span>
<span style="background-color:yellow; color:black">黄底黑字</span>
<span style='background-color:#000000;color:#FFFFFF'>我是红色</span>
