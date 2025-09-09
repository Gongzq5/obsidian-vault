## Attention

抽象了 3 个向量，分别称为 $q, k, v$，这里借鉴了数据库的概念。
如何形象的理解呢，

* $q$：表示一个查询，编码了“当前这个 token 更关注哪些信息”
* $k$：表示一个关键字，编码了“当前这个 token 可以提供哪些信息”
* $v$：表示一个含义，编码了“当前这个 token 自己拥有哪些信息”

这样，对于每个词，就可以使用自己的 $q$，去和前边每个词的 $k$ 去匹配，就可以查到自己更关注哪个 token：谁可以给我更关心的信息，谁对我更重要？然后去每个 token 的 $v$ 里，根据不同 token 的重要性，将他们的 $v$ 加权求和，得到自己当前关心的表示。

最终抽象得到的公式就是

$$
h = softmax(\frac{QK^T}{\sqrt{d}}) V
$$

输入维度是多少呢？`(batch_size, seq_len, d_model)`

Check this:
* https://docs.google.com/document/d/105Cw-oZsxSc-lc8LnepI1FlC5h87Fdhrwd899mRGuYo/edit?tab=t.0