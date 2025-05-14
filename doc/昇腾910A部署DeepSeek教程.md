## （1）.更新驱动和固件

### 1.查看固件和驱动的地址
```bash
cat /etc/ascend_install.info
```

```bash
UserName=HwHiAiUser
UserGroup=HwHiAiUser
Driver_Install_Type=full
Driver_Install_Path_Param=/usr/local/Ascend
Driver_Install_For_All=yes
Driver_Install_Mode=normal
Firmware_Install_Type=full
Firmware_Install_Path_Param=/usr/local/Ascend
```
### 1.卸载驱动
```bash
bash /usr/local/Ascend/driver/script/uninstall.sh --force
```
##### 有下面这条信息就卸载成功了
```bash
[INFO]Driver package uninstalled successfully! Reboot needed for uninstallation to take effect!
```
### 2.卸载固件
```bash
bash /usr/local/Ascend/firmware//script/uninstall.sh
```

```bash
[Firmware] [2025-03-31 09:49:12] [INFO]base version is 7.1.0.3.220.
[Firmware] [2025-03-31 09:49:12] [INFO]Firmware package uninstalled successfully! Uninstallation takes effect immediately.
```
### 3.安装驱动
[固件驱动下载地址](https://www.hiascend.com/hardware/firmware-drivers/community?product=4&model=10&cann=8.0.0.beta1&driver=1.0.22.5.alpha)
![[https://github.com/longllovers/Deploying-DeepSeek-on-Ascend-910A/blob/main/img/img1.png]]
#### 先下载，后切换为root权限，放到任意目录下面
```bash
chmod +x Ascend-hdk-910-npu-driver_24.1.0_linux-aarch64.run 
./Ascend-hdk-910-npu-driver_24.1.0_linux-aarch64.run --full --install-for-all
```

```bash
Verifying archive integrity...  100%   SHA256 checksums are OK. All good.
Uncompressing ASCEND DRIVER RUN PACKAGE  100%
[Driver] [2025-03-31 09:50:07] [INFO]Start time: 2025-03-31 09:50:07
[Driver] [2025-03-31 09:50:07] [INFO]LogFile: /var/log/ascend_seclog/ascend_install.log
[Driver] [2025-03-31 09:50:07] [INFO]OperationLogFile: /var/log/ascend_seclog/operation.log
[Driver] [2025-03-31 09:50:07] [WARNING]Do not power off or restart the system during the installation/upgrade
[Driver] [2025-03-31 09:50:08] [INFO]set username and usergroup, HwHiAiUser:HwHiAiUser
[Driver] [2025-03-31 09:50:09] [INFO]driver install type: DKMS
[Driver] [2025-03-31 09:50:09] [INFO]upgradePercentage:10%
[Driver] [2025-03-31 09:50:15] [INFO]upgradePercentage:30%
[Driver] [2025-03-31 09:50:16] [INFO]upgradePercentage:40%
[Driver] [2025-03-31 09:50:33] [INFO]upgradePercentage:90%
[Driver] [2025-03-31 09:51:36] [INFO]upgradePercentage:100%
[Driver] [2025-03-31 09:51:36] [INFO]Driver package installed successfully! Reboot needed for installation/upgrade to take effect!
[Driver] [2025-03-31 09:51:36] [INFO]End time: 2025-03-31 09:51:36
```
### 4.安装固件
```bash
chmod +x Ascend-hdk-910-npu-firmware_7.5.0.2.220.run 
./Ascend-hdk-910-npu-firmware_7.5.0.2.220.run --full
```

```bash
Verifying archive integrity...  100%   SHA256 checksums are OK. All good.
Uncompressing ASCEND-HDK-910-NPU FIRMWARE RUN PACKAGE  100%
[Firmware] [2025-03-31 09:52:40] [INFO]Start time: 2025-03-31 09:52:40
[Firmware] [2025-03-31 09:52:40] [INFO]LogFile: /var/log/ascend_seclog/ascend_install.log
[Firmware] [2025-03-31 09:52:40] [INFO]OperationLogFile: /var/log/ascend_seclog/operation.log
[Firmware] [2025-03-31 09:52:41] [WARNING]Do not power off or restart the system during the installation/upgrade
[Firmware] [2025-03-31 09:52:47] [INFO]upgradePercentage: 4%
[Firmware] [2025-03-31 09:52:57] [INFO]upgradePercentage: 51%
[Firmware] [2025-03-31 09:53:09] [INFO]upgradePercentage: 86%
[Firmware] [2025-03-31 09:53:19] [INFO]upgradePercentage: 86%
[Firmware] [2025-03-31 09:53:29] [INFO]upgradePercentage: 86%
[Firmware] [2025-03-31 09:53:32] [INFO]upgradePercentage: 100%
[Firmware] [2025-03-31 09:53:32] [INFO]The firmware of [8] chips are successfully upgraded.
[Firmware] [2025-03-31 09:53:32] [INFO]Firmware package installed successfully! Reboot now or after driver installation for the installation/upgrade to take effect.
[Firmware] [2025-03-31 09:53:32] [INFO]End time: 2025-03-31 09:53:32
```

## (2)重启和查看版本
### 1.重启
```bash
reboot
```
### 2.查看驱动版本
```bash
npu-smi info
```

```bash
+------------------------------------------------------------------------------------------------+
| npu-smi 24.1.0                   Version: 24.1.0                                               |
+---------------------------+---------------+----------------------------------------------------+
| NPU   Name                | Health        | Power(W)    Temp(C)           Hugepages-Usage(page)|
| Chip                      | Bus-Id        | AICore(%)   Memory-Usage(MB)  HBM-Usage(MB)        |
+===========================+===============+====================================================+
| 0     910B                | OK            | 65.7        38                0    / 0             |
| 0                         | 0000:C1:00.0  | 0           2382 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 1     910B                | OK            | 62.3        33                0    / 0             |
| 0                         | 0000:81:00.0  | 0           2378 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 2     910B                | OK            | 64.9        34                0    / 0             |
| 0                         | 0000:41:00.0  | 0           2382 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 3     910B                | OK            | 62.9        40                0    / 0             |
| 0                         | 0000:01:00.0  | 0           2384 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 4     910B                | OK            | 67.1        38                0    / 0             |
| 0                         | 0000:C2:00.0  | 0           2385 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 5     910B                | OK            | 63.5        33                0    / 0             |
| 0                         | 0000:82:00.0  | 0           2355 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 6     910B                | OK            | 64.2        33                0    / 0             |
| 0                         | 0000:42:00.0  | 0           2384 / 15038      0    / 32768         |
+===========================+===============+====================================================+
| 7     910B                | OK            | 63.0        37                0    / 0             |
| 0                         | 0000:02:00.0  | 0           2355 / 15038      0    / 32768         |
+===========================+===============+====================================================+
+---------------------------+---------------+----------------------------------------------------+
| NPU     Chip              | Process id    | Process name             | Process memory(MB)      |
+===========================+===============+====================================================+
| No running processes found in NPU 0                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 1                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 2                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 3                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 4                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 5                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 6                                                            |
+===========================+===============+====================================================+
| No running processes found in NPU 7                                                            |
+===========================+===============+====================================================+
```
### 3.查看固件版本
```bash
/usr/local/Ascend/driver/tools/upgrade-tool --device_index -1 --component -1 --version
```

```bash
Get component version(7.5.0.2.220) succeed for deviceId(0), componentType(0).
        {"device_id":0, "component":nve, "version":7.5.0.2.220}
```
### 4.运行和启动容器

```bash
docker run -itd --privileged --name=deepseek --net=host --shm-size=500g --device=/dev/davinci0 --device=/dev/davinci1 --device=/dev/davinci2 --device=/dev/davinci3 --device=/dev/davinci4 --device=/dev/davinci5 --device=/dev/davinci6 --device=/dev/davinci7 --device=/dev/davinci_manager --device=/dev/devmm_svm --device=/dev/hisi_hdc -v /usr/local/Ascend/driver:/usr/local/Ascend/driver -v /usr/local/Ascend/add-ons/:/usr/local/Ascend/add-ons/ -v /usr/local/sbin/:/usr/local/sbin/ -v /var/log/npu/slog/:/var/log/npu/slog -v /var/log/npu/profiling/:/var/log/npu/profiling -v /var/log/npu/dump/:/var/log/npu/dump -v /var/log/npu/:/usr/slog -v /home/202502yf/deepseek/DeepSeek-R1-Distill-Qwen-32B/weights:/weights/DeepSeek-R1-Distill-Qwen-32B/weights deepseek:32b bash
```

```bash
docker exec -it deepseek /bin/bash
```
### 6.服务化拉起

#### 1.修改权重权限
```bash
chmod 750 ./weights && chmod 740 ./weights/config.json 
```

#### 2.修改配置文件
```bash
vim /usr/local/Ascend/mindie/latest/mindie-service/conf/config.json
```

#### 3.修改启动配置文件 
```bash 
vim /usr/local/Ascend/mindie/latest/mindie-service/conf/config.json 

```
##### 简单配置如下
```bash
"npuDeviceIds" : [[0,1,2,3]]
"worldSize" : 4,
"httpsEnabled" : false
```
#### 4.拉取服务
```bash
cd /usr/local/Ascend/mindie/latest/mindie-service/bin && ./mindieservice_daemon
```

### 7.推理测试
```shell 
curl 127.0.0.1:1025/generate -d '{
"prompt": "介绍深度求索这个公司?",
"max_tokens": 8192,
"stream": false,
"do_sample":true,
"repetition_penalty": 1.00,
"temperature": 0.01,
"top_p": 0.001,
"top_k": 1,
"model": "(模型名称)" 
}'
```

### 附录环境加载(非必须)
#### 1. 环境加载
```bash
# 1. 加载各类环境配置脚本
source /usr/local/Ascend/nna/atb/set_env.sh
source /usr/local/Ascend/mindie/latest/mindie-service/set_env.sh
source /usr/local/Ascend/ascend-toolkit/set_env.sh
source /usr/local/Ascend/atb-models/set_env.sh
source /usr/local/Ascend/mindie/latest/mindie-llm/set_env.sh
source /usr/local/Ascend/mindie/latest/mindie-service/set_env.sh
source /usr/local/Ascend/mindie/set_env.sh

# 2. 设置 Python 环境变量（确保自定义包可导入）
export PYTHONPATH=/usr/local/lib/python3.11/site-packages:$PYTHONPATH
export PYTHONPATH=/usr/local/lib64/python3.11/site-packages:$PYTHONPATH

# 3. 设置共享库路径（LD_LIBRARY_PATH）
export LD_LIBRARY_PATH=/usr/lib64:$LD_LIBRARY_PATH

# 4. MindIE 日志和权限设置（控制台输出日志和写文件日志）
export MINDIE_LOG_TO_STDOUT=1
export MINDIE_CHECK_INPUTFILES_PREMISSION=0
export MINDIE_LLM_PYTHON_LOG_TO_STDOUT=1
export MINDIE_LLM_PYTHON_LOG_TO_FILE=1

# 设置日志等级为 ERROR（屏蔽 INFO 和 WARNING 等）
export ASDOPS_LOG_LEVEL=ERROR

```

#### 2. 查看日志
```shell 
grep -rn "ERROR" ~/ascend/log
grep -rn "ERROR" ~/mindie/log

```

### 3. 卡的虚拟化恢复
#### 查看是否有虚拟化
```shell 
ls /dev/*davinci*  
```
**若为0-7，则无虚拟化，不然则是有虚拟化，则有必要看下面的教程**
##### 查看卡虚拟化id
```shell 
npu-smi info -t info-vnpu -i 1 -c 0  
```

| 参数             | 说明                                         |
| -------------- | ------------------------------------------ |
| `npu-smi info` | 华为提供的 NPU 监控命令工具，类似于 NVIDIA 的 `nvidia-smi` |
| `-t info-vnpu` | 指定查询信息类型为 `vNPU`（虚拟 NPU）信息                 |
| `-i 1`         | 指定 NPU 设备 ID，这里是第 1 个 NPU（通常从 0 开始编号）      |
| `-c 0`         | 指定 NPU 上的第 0 个 `vNPU`（逻辑分区或上下文）            |

##### 取消虚拟化
```shell 
npu-smi set -t destroy-vnpu -i 3 -c 0 -v 150
```

| 参数                | 含义                                         |
| ----------------- | ------------------------------------------ |
| `npu-smi`         | 昇腾 NPU 资源监控和管理工具（类似 NVIDIA 的 `nvidia-smi`） |
| `set`             | 设置命令，表示要对某种状态进行更改                          |
| `-t destroy-vnpu` | 表示销毁虚拟 NPU（vNPU），释放资源                      |
| `-i 3`            | 指定第 3 号 NPU 卡（NPU ID = 3）                  |
| `-c 0`            | 指定卡上第 0 个逻辑通道/物理核（context/channel 0）       |
| `-v 150`          | 指定 **vNPU ID 为 150**，表示销毁该 vNPU 实例         |

#### 简单的测试
```shell 
bash run.sh pa_fp16 performance [[256,256]] 4 qwen /weights/DeepSeek-R1-Distill-Qwen-32B/weights 8
```


