#### updateByExampleSelective和updateByExample

`updateByExampleSelectiveupdateByExample` 函数：

* 这个函数用于按照指定的条件 `example` 更新记录。
* 它会根据 `record` 参数中非空的字段值来执行更新，即只会更新 `record` 中那些非空字段的值，而会忽略 `record` 中的空字段。
* 如果您想部分更新记录，而不是全部字段更新，可以使用这个函数。

`updateByExample` 函数：

* 这个函数也用于按照指定的条件 `example` 更新记录。
* 与 `updateByExampleSelective` 不同，它会更新 `record` 参数中的所有字段，不管这些字段是否为空。
* 如果您希望更新记录的所有字段，包括那些为空的字段，可以使用这个函数。

总结起来，区别在于选择性更新字段的范围。`updateByExampleSelective` 只更新 `record` 中非空字段的值，而 `updateByExample` 更新 `record` 中的所有字段的值，包括空字段。


## selectByExampleSelective使用方法

```
TemuCrawlBatch.Column[] selectiveColumns = {TemuCrawlBatch.Column.batchId};
List<TemuCrawlBatch> result = temuCrawlBatchMapper.selectByExampleSelective(example,selectiveColumns);
```
