You are welcome to install the software using PowerShell
-
欢迎您使用 PowerShell 安装软件
-

```
  . The main function
    1. If the installation package does not exist locally, activate the download function;
    2. When using the download function, it automatically judges the system type, automatically selects in order, and so on;
    3. Automatically select drive letter:
        3.1    The drive letter can be specified, and the current system drive will be excluded after setting automatic.
               If no available disk is found, return to the current system disk;
        3.2    The minimum required remaining free space can be set, the default is 1GB;
 
    4. Search file name supports fuzzy search, wildcard *;
    5. Queue, add to the queue after running the installer, and wait for the end;
    6. Search sequentially according to the preset structure:
       * Original download address: https://fengyi.tel/Instl.Packer.Latest.exe
         + Fuzzy file name: Instl.Packer*
           - Condition 1: System language: en-US, search condition: Instl.Packer*en-US*
           - Condition 2: Search for fuzzy file name: Instl.Packer*
           - Condition 3: Search the website to download the original file name: Instl.Packer.Latest

    7. Dynamic function: add pre-run and post-run processing, go to Function OpenApp {} to change the module;
    8. Support decompression package processing, etc.
```

```
  . 主要功能
    1. 本地不存在安装包，激活下载功能；
    2. 使用下载功能时，自动判断系统类型，自动按顺序选择，依次类推；
    3. 自动选择盘符：
        3.1    可指定盘符，设置自动后将排除当前系统盘，
               搜索不到可用盘时，回退到当前系统盘；
        3.2    可设置最低要求剩余可用空间，默认 1GB；

    4. 搜索文件名支持模糊查找，通配符 *；
    5. 队列，运行安装程序后添加到队列，等待结束；
    6. 依次按预先设置的结构搜索：
       * 原始下载地址：https://fengyi.tel/Instl.Packer.Latest.exe
         + 模糊文件名：Instl.Packer*
           - 条件 1：系统语言：en-US，搜索条件：Instl.Packer*en-US*
           - 条件 2：搜索模糊文件名：Instl.Packer*
           - 条件 3：搜索网站下载原始文件名：Instl.Packer.Latest

    7. 动态功能：已添加运行前，运行后处理，前往 Function OpenApp {} 处更改该模块；
    8. 支持解压包处理等。
```


# Package configuration tutorial
```
{
	"GUID":      "3d617284-f5ed-4656-b5f9-cc75e5452128",    # Unique identifier; for automatic selection, please add to "DefaultSelect"
	"Name":      "Intel Wireless Wi-Fi Drivers",            # Package name
	"Action":    "Install",                                 # Action: Install - Install; NoInst - Download without installing; Unzip - Download and only extract; To - Install to directory
	"Manner":    "Queue",                                   # Execution method: Wait - Wait for completion; Fast - Run directly; Queue = Queue
	"DLetter":   "Auto",                                    # When set to automatic, the current system drive will be excluded; if no available drive is found, the default setting will be the current system drive; specify drive letter [A:]-[Z:]; specify path: \\192.168.1.1
	"Structure": "Yi\\Installation package\\Drive",         # Directory structure
	"Unpwd":     "",                                        # Archive extraction password
	"Url": {                                                # Download link
		"arm64": "",                                          
		"x64":   "",                                          
		"x86":   "https://downloadmirror.intel.com/871633/WiFi-24.10.0-Driver64-Win10-Win11.exe"
	},
	"FindFile":  "WiFi*",                                   # File name fuzzy search (*)
	"param":     "-s -norestart",                           # Execution parameters
	"PS": [                                                 # Run PowerShell function
		"Set_WiFi -SSID 'Yi' -PSK 'P@ssw0rd'"                 # After installing the WiFi driver, run the `Set_Wifi` function, adding the WiFi connection name and WiFi password.
	],
	"Command": []                                           # After execution, run the program by its name, for example, run calc or notepad.
}
```

# 软件包配置教程
```
{
	"GUID":      "3d617284-f5ed-4656-b5f9-cc75e5452128",    # 唯一识别码，自动选择请添加到 "DefaultSelect" 里
	"Name":      "Intel Wireless Wi-Fi Drivers",            # 软件包名称
	"Action":    "Install",                                 # 动作：Install - 安装；NoInst - 下载后不安装；Unzip - 下载后仅解压；To - 安装到目录
	"Manner":    "Queue",                                   # 运行方式：Wait - 等待完成；Fast - 直接运行；Queue = 队列
	"DLetter":   "Auto",                                    # 设置自动后将排除当前系统盘，搜索不到可用盘时，默认设置为当前系统盘；指定盘符 [A:]-[Z:]；指定路径：\\192.168.1.1
	"Structure": "Yi\\Installation package\\Drive",         # 目录结构
	"Unpwd":     "",                                        # 压缩包解压密码
	"Url": {                                                # 下载连接
		"arm64": "",                                          
		"x64":   "",                                          
		"x86":   "https://downloadmirror.intel.com/871633/WiFi-24.10.0-Driver64-Win10-Win11.exe"
	},
	"FindFile":  "WiFi*",                                   # 文件名模糊查找 (*)
	"param":     "-s -norestart",                           # 运行参数
	"PS": [                                                 # 运行 PowerShell 函数
		"Set_WiFi -SSID 'Yi' -PSK 'P@ssw0rd'"                 # 安装完 WiFi 驱动后，运行函数里的 Set_Wifi，添加连接 WIFI 连接名称 和 WIFI 密码
	],
	"Command": []                                           # 运行完成后运行程序名，例如运行 calc，notepad
}
```
