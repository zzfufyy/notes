#### 【vs-python】vs-python开发环境

-------------------------

*   安装python环境

    下载installer，不要选择自动添加至Path添加。

    系统 Path 变量如下： python +  pip

    `c:/Python38;c:/Python38/Scripts`

* 配置python在vscode debug中

  ![config1](C:\Users\10244687\Desktop\zyw\笔记-Typora\【素材】笔记图片源\vs-python_config1.JPG)
  
   打开以后  *launch.json*
  
  ```json
  {
      // Use IntelliSense to learn about possible attributes.
      // Hover to view descriptions of existing attributes.
      // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
      "version": "0.2.0",
      "configurations": [
          {
              "name": "Python: 当前文件",
              "type": "python",
              "request": "launch",
              "pythonPath": "C:\\Python38\\python.exe",
              "program": "${file}",
              "console": "integratedTerminal"
          }
      ]
  }
  ```
  
  

