## settings.json
### ~/.config/Code/User/settings.json
```
{
  "cmake.configureOnOpen": false,
  "editor.minimap.enabled": false,
  "editor.mouseWheelZoom": true,
  "editor.renderControlCharacters": true,
  "editor.rulers": [100],
  "editor.tabSize": 2,
  "files.associations": {
    "*.repos": "yaml",
    "*.world": "xml",
    "*.xacro": "xml"
  },
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "terminal.integrated.scrollback": 1000000,
  "workbench.iconTheme": "vscode-icons",
  "workbench.editor.pinnedTabSizing": "compact",
  "ros.distro": "foxy",
  "colcon.provideTasks": true
}
```


## c_cpp_properties.json
### ~/robot_ws/.vscode/c_cpp_properties.json
```
{
  "configurations": [
    {
      "name": "Linux",
      "includePath": [
        "${default}",
        "${workspaceFolder}/**",
        "/opt/ros/foxy/include/**"
      ],
      "defines": [],
      "compilerPath": "/usr/bin/g++",
      "cStandard": "c99",
      "cppStandard": "c++14",
      "intelliSenseMode": "linux-gcc-x64"
    }
  ],
  "version": 4
}
``` 

## tasks.json
### ~/robot_ws/.vscode/tasks.json
```
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "colcon: build",
      "type": "shell",
      "command": "colcon build --cmake-args '-DCMAKE_BUILD_TYPE=Debug'",
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    },
    {
      "label": "colcon: test",
      "type": "shell",
      "command": "colcon test && colcon test-result"
    },
    {
      "label": "colcon: clean",
      "type": "shell",
      "command": "rm -rf build install log"

    }
  ]
}
```

## launch.json
### ~/robot_ws/.vscode/launch.json

```
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug-rclpy(debugpy)",
      "type": "python",
      "request": "launch",
      "program": "${file}",
      "console": "integratedTerminal"
    },
    {
      "name": "Debug-rclcpp(gbd)",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/install/${input:package}/lib/${input:package}/${input:node}",
      "args": [],
      "preLaunchTask": "colcon: build",
      "stopAtEntry": true,
      "cwd": "${workspaceFolder}",
      "externalConsole": false,
      "MIMode": "gdb",
      "setupCommands": [
        {
          "description": "Enable pretty-printing for gdb",
          "text": "-enable-pretty-printing",
          "ignoreFailures": true
        }
      ]
    }
  ],
  "inputs": [
    {
      "id": "package",
      "type": "promptString",
      "description": "package name",
      "default": "topic_service_action_rclcpp_example"
    },
    {
      "id": "node",
      "type": "promptString",
      "description": "node name",
      "default": "argument"
    }
  ]
}
```