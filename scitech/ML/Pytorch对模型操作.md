# Pytorch对模型操作

## 查看遍历模型

### 查看网络模型结构

    import torchvision
    from torch import nn
    
    resnet = torchvision.models.resnet101(pretrained=True)


（1）查看网络结构可直接打印

    print(resnet)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic4.zhimg.com%2Fv2-8dd9aeed7657feb9814df07d5fdf1f97_b.jpeg)

（2）使用children 和 named\_children遍历

    for m in resnet.children():
        print(m)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic3.zhimg.com%2Fv2-18b6c660b621490badffc3aa61db4d5e_b.jpeg)

    for name, m in resnet.named_children():
        print(name, " >>> ", m)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic3.zhimg.com%2Fv2-c52fc556f1526c0a92c7437ce99a8d0e_b.jpeg)

（3）使用modules和named\_modules

    for m in resnet.modules():
        print(m)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic3.zhimg.com%2Fv2-6936536666ccf2f68921a44a340e1d66_b.jpeg)

    for name, m in resnet.named_modules():
        print(name, " >>> ", m)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic2.zhimg.com%2Fv2-fcba8236cd4ea4f447d4a30b257fabdd_b.jpeg)

注意：named-children 和 named-modules 的区别 children 和 modules同理

    import torch
    import torch.nn as nn
     
    class TestModule(nn.Module):
        def __init__(self):
            super(TestModule,self).__init__()
            self.layer1 = nn.Sequential(
                nn.Conv2d(16,32,3,1),
                nn.ReLU(inplace=True)
            )
            self.layer2 = nn.Sequential(
                nn.Linear(32,10)
            )
     
        def forward(self,x):
            x = self.layer1(x)
            x = self.layer2(x)
     
    model = TestModule()
     
    for name, module in model.named_children():
        print('children module:', name)
     
    for name, module in model.named_modules():
        print('modules:', name)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic4.zhimg.com%2Fv2-0fc3b1edfef20f85d76df02da68400fb_b.jpeg)

请注意第三行modules后面没有参数，是因为这里返回的是layer1和layer2的整体，不要遗漏。

观察一下模型输出：

    for name, module in model.named_children():
        print('children module:', name, module)
    
    print('\n')
     
    for name, module in model.named_modules():
        print('modules:', name, module)


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic4.zhimg.com%2Fv2-672346bec742019334c33f3d37988dd7_b.jpeg)

用list举例就是：

    a = [1, 2, [3], [4, 5]]
    
    children返回：
    1, 2, [3], [4, 5]
    
    modules返回：
    [1, 2, [3], [4, 5]], 1, 2, [3], 3, [4, 5], 4, 5

### 查看遍历网络模型参数

    import torchvision
    from torch import nn
    
    resnet = torchvision.models.resnet101(pretrained=True)


（1）仅仅查看每一层的参数

这里使用了.size()查看参数的尺寸，方便显示，想查看参数值，可以将.size()去掉

    for p in Resnet.parameters():
        print(p.size())


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic1.zhimg.com%2Fv2-bccad618c565721644b33586a1afe6bc_b.jpeg)

（2）查看每一层的参数名和参数

    for name, par in resnet.named_parameters():
        print(name, "   ", par.size())


![](Pytorch对模型操作.assets/filtersno_upscale()imageUrl=https%3A%2F%2Fpic2.zhimg.com%2Fv2-fd1da66ae62ac196f80bf7e1c5b3b25d_b.jpeg)



## 判断每一层的类型

用isinstance判断。

```python
for layer in model.children(): # traverse every layer of model
            if isinstance(layer, nn.Conv2d): # if layer is a conv
                print("the layer is a conv")  
            elif isinstance(layer, nn.Linear): # if layer is a fc
                print("the layer is a fc")
            else:
                print("the layer is not a conv neither a fc")
```





> 参考资料：
>
> 1. https://zhuanlan.zhihu.com/p/428838496
> 2. https://aisaka.cloud/%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD/pytorch%E8%8E%B7%E5%8F%96%E4%B8%AD%E9%97%B4%E5%B1%82%E5%8F%82%E6%95%B0%E3%80%81%E8%BE%93%E5%87%BA%E4%B8%8E%E5%8F%AF%E8%A7%86%E5%8C%96/
