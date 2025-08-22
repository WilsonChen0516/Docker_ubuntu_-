# Docker_ubuntu_-
學習筆記 用於紀錄docker的使用方式


## 基本概念
Docker：把程式、依賴、環境打包成「容器」，到哪台機器都長一樣。  
映像（image）：容器的模板；  
容器（container）：從映像跑出來的實例。  
掛載（mount/volume）：把你主機資料夾映射到容器內，檔案不會跟著容器消失。  
# DL with docker
GPU in Docker：需要 NVIDIA 驅動 + NVIDIA Container Toolkit；容器裡用 --gpus all。  
## 1.準備 GPU 執行環境
1. 檢查主機 NVIDIA 驅動  
```bash
nvidia-smi
```
2. 安裝 NVIDIA Container Toolkit（讓容器能用 GPU）
```bash
# 官方套件庫
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | \
sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -fsSL https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt-get update
sudo apt-get install -y nvidia-container-toolkit
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

