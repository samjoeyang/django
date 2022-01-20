# Python环境

## 安装Python3

```
sudo apt-get install -y python3
```

## 安装pip

```
sudo apt-get install -y python3-pip
```

### pip 检查更新

```
pip3 install --upgrade pip3
```

## 安装虚拟环境工具

```
pip3 install virtualenv
```

## 虚拟环境的操作

```
#创建虚拟环境
virtualenv venv

#进入虚拟环境 
source venv/bin/activate

# 查看环境
which python 
python -V 
pip -V 
echo $PATH 

# pip升级一下
pip install --upgrade pip 

#退出虚拟环境
deactivate  
```
