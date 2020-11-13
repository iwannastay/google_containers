# Readme

## Environment

python version=3.6.9

```
conda create -n rf_demo python=3.6.9
conda activate rf_demo
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -r requirements.txt
```

Run

```
python main.py
```

## 实现方案

在NCSCC代码的env_wrappers.py中嵌入SaveImg类，用于保存图像到本地。
