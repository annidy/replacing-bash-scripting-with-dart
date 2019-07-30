## 读写文件

以行形式读文件
```
final lines = File('./bin/main.dart').readAsLinesSync();
lines.forEach((l) {
    print(l);
});
```

写文件
```
File('file.txt').writeAsStringSync("hello world");
```

## 命令行接口
stdin读数据

```
  final readline = stdin.readLineSync();
  print(readline);
```

命令行参数

```
main(List<String> args) {
}
```

环境变量

```
Map<String, String> envVars = Platform.environment;
print(envVars['PATH']);
```

## 文件系统

遍历路径
```
var dir = Directory('.');

dir.list(recursive: true).listen((FileSystemEntity onData) {
    print(onData.path);
});
```


拷贝文件
```
final f1 = File('./file.txt');
f1.copy('./file2.txt');
```

创建目录
```
Directory('./tmp').create();
```

## 正则表达式

```
'Never odd or even'.contains('odd');
```

更多RegExp的使用参考 
https://dart.dev/guides/libraries/library-tour#strings-and-regular-expressions


## 运行程序

```
Process.run('ls', ['-l']).then((ProcessResult results) {
    print(results.stdout);
});  
```

错误码可以通过 ProcessResult.exitCode 获取。

程序运行可能会很久，Stream形式读取结果更快
```
  final process = await Process.start('ls', ['-l']);
  var lineStream =
      process.stdout.transform(Utf8Decoder()).transform(LineSplitter());
  await for (var line in lineStream) {
    print(line);
  }

  await process.stderr.drain();
  print('exit code: ${await process.exitCode}');
```


## 杂项

获取时间

```
var now = new DateTime.now();
print(now);
```
