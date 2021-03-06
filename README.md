# Android-translator

> 该项目使用 Python 语言进行编写，用来根据指定的 strings.xml 文件自动生成用于多语言翻译的 Excel 表格，
> 以便提供给专门人员进行多语言翻译。在翻译之后可以根据 Excel 的内容自动生成各个语言对应的 strings.xm l文件。
> 最新加入的功能，使用指令对生成的 Excel 中的字符串直接进行翻译。

## 1、项目结构

![demo](resources/pic_demo1.png)

```
\----
    \----xml_reader.py     从XML中读取字符串资源 
    \----xml_writer.py     将翻译的结果写入到XML文件中
    \----excel_reader.py   从Excel中读取翻译的结果
    \----excel_writer.py   将XML中解析出的内容写入到Excel文件中
    \----translator.py     封装的翻译帮助模块
    \----run.py            命令行窗口、校验等
```

## 2、目前的功能

![demo2](resources/pic_demo2.png)

- 从XML中读取字符串资源，写入到 Excel 表格中；
- 将翻译的结果从 Excel 中读取并创建可用的xml字符资源文件；
- 获取所有语言当前的翻译状态；
- 记录程序中的日志到文件当中；
- 使用三方Api直接对 Excel 进行翻译

## 3、用法

### 3.1 使用程序

你可以直接使用打包的exe文件：[run.exe](run.exe)，或者自己打包 exe 。打包之前需要先用Python安装`pyinstaller`：

    pip install pyinstaller 

然后在当前目录下面执行指令来完成打包。生成的 exe 文件将放置到`dist`目录下面。

    pyinstaller -F run.py
	
执行程序的时候需要将`strings.xml`文件放置在与run.exe同级的目录中，然后双击run.exe执行即可。
	
### 3.2 自动翻译
	
如果需要使用三方的 api 对文档的内容进行翻译，
你需要先到[百度翻译平台](http://api.fanyi.baidu.com/api/trans/product/index)注册称为开发者。
获取到`APP ID`和密钥之后将它们写入到`config.json`文件中。
`config.json`文件也要放置在与run.exe同一级的目录中。

百度翻译支持38种语言，你可以在`config.json`文件的`mappings`中进行配置。
这里的映射是用来将values文件夹的后缀名映射成为百度支持的语言参数用的，
比如中文繁体的`strings.xml`在Android中要放在`values-zh-rTW`目录下面，
而在百度支持的语言中使用`cht`表示繁体，所以你就要加入映射`"zh-rTW":"cht"`。

百度翻译支持的语言及其名称可以到[语言列表](http://api.fanyi.baidu.com/api/trans/product/apidoc#languageList)中查找。

### 3.3 开发

如果要在该项目的基础之上继续进行开发，需要安装的环境：

    pip install xlwt
    pip install xlrd
    pip install xlutils
    pip install pyinstaller 

## 4、TODO

- [ ] 丰富指令：一键式生成所有语言的翻译
- [ ] 丰富指令：根据传入的参数选择指定的语言用于生成翻译后的字符串资源

