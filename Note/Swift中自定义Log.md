title: Swift中自定义Log
date: 2016-06-12 20:00:00
tags:
---

用于输出的常用函数

|函数名|含义|
|:----|-----:|
|#function|获取当前输出所在的文件路径|
|#line|获取当前输出所在的行号|
|#file|获取当前输出的文件名|

所以利用上面的内容，我们可以定义以下函数做为输出：

~~~
func CRLog<T>(content: T, fileName:String = #file, methodName: String = #function, lineNumber: Int = #line){
    let tempFileName = (#file as NSString).pathComponents.last! as NSString
    tempFileName
    print(tempFileName.stringByDeletingPathExtension + "." + methodName + "___" + "\(lineNumber)")
}
~~~
其中后面几个值有默认值，当不输入时，则会自动获得相应内容打印.

如果我们有需求，当在DEBUG模式下，就打印输出，在release模式下就不打印，那么我们需要改写我们的代码如下：

~~~
func CRLog<T>(content: T, fileName:String = #file, methodName: String = #function, lineNumber: Int = #line){
        #if DEBUG
            let tempFileName = (#file as NSString).pathComponents.last! as NSString
            tempFileName
            print(tempFileName.stringByDeletingPathExtension + "." + methodName + "___" + "\(lineNumber)")
        #endif
        
    }
~~~

其中DEBUG可为任意内容，由于Swift中没有像OC中自身定义了DEBUG宏，所以此处的DEBUG可以为任意值，你可以写成你的名字等等,写完后，我们需要去配置一下这个值,于是我们需要来到:
工程目录->Targets->Build Settings->Swift Compiler -> Custom Flags -> Other Swift Flags -> Debug，然后在里面填写 __-D DEBUG __,此处的DEBUG就是你上面定义的值，与代码中的那个值保持一致就可以了，至此，你可以切换成DEBUG模式和Release模式各自尝试一下输出效果。


