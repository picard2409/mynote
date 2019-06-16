# python与Linux笔记
#### 1.修改Anaconda中Jupyter笔记本默认工作路径
安装完anaconda之后运行anaconda Prompt(开始菜单的Anaconda文件夹下面)
输入jupyter notebook --generate-config
打开生成的文件将 ：#c.NotebookApp.notebook_dir = '' 
改为 
c.NotebookApp.notebook_dir = 'your path' (注意取消注释)
我改成了我自己的路径 
c.NotebookApp.notebook_dir = 'E:\PY' 
Ctrl+1：注释/撤销注释
Ctrl+4/5：块注释/撤销块注释
Ctrl+L：跳转到行号
F5：运行
F11：全屏
Tab：空行前是代码缩进；在输入一个字母后，按Tab健会自动补全或者代码提示。
Shift+Tab：撤销代码缩进
ps：Tools-->Preferences-->Keyboard Shortcut  可以查看所有快捷键

``` python
import matplotlib.pyplot as plt
import numpy as np
y=np.random.standard_normal(100)
x=range(len(y))
plt.plot(x,y)
plt.show()
```
##### 创建Dog类并实例化
``` python
#创建DOg类
class Dog():
    """模拟dog"""
    def __init__(self,name,age):
        #初始化name和age
        self.name=name
        self.age=age
        
    def sit(self):
        #模拟小狗被命令时蹲下
        print(self.name.title()+"is sitting.")
    def roll_over(self):
        #模拟相扑被命令时打滚
        print(self.name.title()+"rolled over")
        
        
#类的实例化
my_dog=Dog("DaHuang",4)
print("My dog's name is "+ my_dog.name.title() + ".")
print("my dog is "+str(my_dog.age)+"years old.")
print("调用函数")
my_dog.sit()
my_dog.roll_over()
```

python与c++实现最大和的连续数组