# VSCode 编译调试环境配置文件
`.vscode`  文件夹里包含三个文件：`c_cpp_properties.json`、`launch.json`、`tasks.json`



`c_cpp_properties.json` ：编译器配置文件

```json
{
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "C:\\mingw64\\bin\\g++.exe",
            "cStandard": "c11",
            "cppStandard": "c++14",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}
```



`tasks.json`：编译命令配置文件

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++.exe 生成活动文件",  // 编译任务的名称，跟 launch.json 最后的 preLaunchTask 的值对应
			"command": "C:\\mingw64\\bin\\g++.exe",  // 编译器的路径，须跟你自己的安装路径相符
			"args": [  // 编译器执行时的参数，跟手动编译时输入的内容基本一致，主要是多了 -g 参数，以加入调试信息
				"-fdiagnostics-color=always",
				"-g",
				"${file}",  // 编译该文件
				//"${fileDirname}\\sqtree.cpp",  // 编译特定文件 sqtree.cpp
				//"${fileDirname}\\*.cpp", 	   // 编译文件夹下所有 .cpp 文件
				"-o",
				"${fileDirname}\\${fileBasenameNoExtension}.exe"
			],
			"options": {
				"cwd": "${fileDirname}"
                //"cwd": "C:\\mingw64\\bin"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"detail": "编译器: C:\\mingw64\\bin\\g++.exe"
		}
	]
}
```



`launch.json`：调试器配置文件

```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "g++.exe - 生成和调试活动文件",  // 该调试任务的名字，启动调试时会在待选列表中显示
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,  // 控制是否在入口处暂停，默认false不暂停，改为true暂停
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false, // 控制是否启动外部控制台（独立的黑框）运行程序，默认 false 表示在集成终端中运行
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\mingw64\\bin\\gdb.exe",  // 调试器路径，必须与你自己的安装路径相符
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "C/C++: g++.exe 生成活动文件"  // 调试前的预执行任务，这里的值是tasks.json文件中对应的编译任务，也就是调试前需要先编译
        }
    ]
}
```

