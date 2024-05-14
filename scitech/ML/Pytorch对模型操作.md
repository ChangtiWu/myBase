# Pytorch对模型操作

model为模型。

**查看模型结构**

model.state_dict()返回的是一个OrderDict，存储了网络结构的名字和对应的参数。

查看模型所有层名称，即访问键值：
```python
print(model.state_dict().keys)
```

通过键值访问模型参数张量：

```python
model.state_dict()['conv.0.weight']
```





> 参考资料：
>
> 1. https://www.volcengine.com/theme/5197831-R-7-1
