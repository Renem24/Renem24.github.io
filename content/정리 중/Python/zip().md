---

---

## `zip(*batch)` 과 `zip(*[batch])` 의 차이

### `zip(*batch)`

```
batch = [('tensor1', 'label1'), ('tensor2', 'label2'), ('tensor3', 'label3')]
result = zip(*batch)  
# 여기서 *batch는 ('tensor1', 'label1'), ('tensor2', 'label2'), ('tensor3', 'label3')로 unpack 됩니다.
print(list(result))  # [('tensor1', 'tensor2', 'tensor3'), ('label1', 'label2', 'label3')]
```


### `zip(*[batch])`

```
batch = [('tensor1', 'label1'), ('tensor2', 'label2'), ('tensor3', 'label3')]
result = zip(*[batch])  
# 여기서 *[batch]는 [('tensor1', 'label1'), ('tensor2', 'label2'), ('tensor3', 'label3')]를 unpack 합니다.
print(list(result))  # [(('tensor1', 'label1'), ('tensor2', 'label2'), ('tensor3', 'label3'))]
```
