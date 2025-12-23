## 创建虚拟环境
```bash
# 创建虚拟环境
conda create -n env_name python=x.x -y

# 激活环境
conda activate env_name

# 退出环境
conda deactivate env_name
```

## 安装torch
[去这里]([Previous PyTorch Versions](https://pytorch.org/get-started/previous-versions/)) 

```bash
# pip临时指定镜像源
pip install [包名] -i [镜像源URL]
```

镜像源URL：
- 清华源： https://pypi.tuna.tsinghua.edu.cn/simple 
- 阿里源： https://mirrors.aliyun.com/pypi/simple/

