#### 【vs-java】vs-java开发环境

------------------------------

* 配置

  插件  Java Extension Pack

  ![java插件](..\【素材】笔记图片源\vs-java开发环境.png)

  配置launch.json 

  ```json
  {
              "type": "java",
              "name": "Java: CurrentFile",
              "cwd":"${workspaceFolder}",
              "stopOnEntry": false,
              "request": "launch",
              "mainClass": "${file}",
              "console": "internalConsole"
  }
  ```

  配置settings.json

  ```json
   // java CONFIG
      "java.semanticHighlighting.enabled": true,
      "java.errors.incompleteClasspath.severity": "ignore",
      "java.configuration.checkProjectSettingsExclusions": false,
      "java.home": "D:\\env_programming\\env_java\\1.8"
  ```

  