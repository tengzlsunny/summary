## react-native 学习

#### react-native环境构建
    [点击前往react-native环境构建](https://reactnative.cn/docs/getting-started.html)
*****

#### react-native bug
1. 端口号8081被占用  
  `修改端口号：react-native start --port 9999`  
  `修改模拟器地址： ip+9999，例如：192.165.1.1:9999`

2. adb版本不一致：adb server version (31) doesn’t match this client (36); killing…   
    `复制sdk里面的adb.exe改名nox_adb.exe,将nox/bin里的nox_adb.ex替换`  

3. git上拉去react native,react-native start 运行报错  
   `cd android`  
   `gradlew clean`  

4. no connect devices(没有链接设备)  
    `adb devices(这个命令是查看是否连接设备)`   
    `adb conncet 127.0.0.1:62001(手动连接设备)`

5. INSTALL_PARSE_FAILED_INCONSISTENT_CERTIFICATES(模拟器上已经安装了此APP)  
    `卸载重装即可`

6. unable to resolve module 'ACCESSIBILITYINFO' （react-native版本问题）  
    `切换版本 react-native@0.55.4  react-native-cli@1.2.0`

7. plugin 0 specified in xxx （babel-preset-react-native的包文件错误）  
    `npm install --save -dev babel-preset-react-native@2.1.0`


   
    