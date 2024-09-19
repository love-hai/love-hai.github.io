# 任务


| 任务                            | 是否完成 |
| --------------------------------- | ---------- |
| shopee商品查询时，sku个数也要查 |          |

6、判断erp，浏览器的版本是否符合要求
5、上新生命周期的筛选项，有勾选的全部都取消
7、浏览器重新创建页面时，菜单不重新创建(暂时不做，先登记到gitee)
shopee店铺下载折扣明细同步报错产品同步未执行完成(暂时不做)
1、TemuHistoryDeleteConsumer修改
2、模板空间授权bug
temu浏览器选择店铺进行操作(做完第7点和我碰一下)
4、erp显示通知时，如果没有就不显示dialog
3、删除过期45天以上的存储空间及图片信息

# 已完成的任务


| 任务                                                      | 时间       |
| ----------------------------------------------------------- | ------------ |
| 判断erp，浏览器的版本是否符合要求                         | 2023.11.04 |
| 上新生命周期的筛选项，有勾选的全部都取消                  | 2023.11.04 |
| 浏览器重新创建页面时，菜单不重新创建                      | 2023.11.04 |
| TemuHistoryDeleteConsumer修改                             | 2023.11.02 |
| 浏览器的订阅通知不要每次都弹出来                          | 2023.11.02 |
| 版本管理里面的lalang浏览器类型改成浏览器                  | 2023.11.02 |
| 找到最新的浏览器版本使用版本号来找                        | 2023.11.02 |
| 浏览器的通知时间显示修改                                  | 2023.11.01 |
| 没选文件不要报发生异常,错误信息要说明是没有选择文件导致的 | 2023.11.01 |
| 浏览器更新后删除历史残留版本                              | 2023.11.01 |

# 业务问题

## 如何解决了用户的问题该如何回答

@userName 具体问题，问题原因

## 问题

temu浏览器在使用的时候不要将temu.zip当文件夹使用


| 条件(指定订阅人为空)                       | 外部人是否有权限 |
| -------------------------------------------- | ------------------ |
| NoteEventSubject Json字符串为空            | yes              |
| eventSubject的第一个元素的subject值isEmpty | yes              |

# shopee店铺上下架分表

## 店铺导入数据测试

### 店铺


| 数据名         | old  | new |
| ---------------- | ------ | ----- |
| 上架产品表     | 131  |     |
| 下架产品表     | 1620 |     |
| 上架sku表 上架 | 1885 |     |
| 上架sku表 下架 | 6    |     |
| 上架sku表 删除 | 6    |     |
| 下架sku表 上架 | 4    |     |
| 下架sku表 下架 | 4208 |     |
| 下架sku表 删除 | 4178 |     |

## 新增的api


| Method | 方法名             | 注释               | url                               | Controller         | service |
| -------- | -------------------- | -------------------- | ----------------------------------- | -------------------- | --------- |
| Post   | getShopProductList | shopee店铺商品查询 | /shopee-discount/get-product-list | DiscountController | base    |
|        |                    |                    |                                   |                    |         |

## warnings

* 店铺查询时，sku的上下架状态未作为查询条件
* batchAddProductPriceOffline批量插入的时候，mycat会根据插入的店铺编码字段，自己选择数据库吗。
* 下架的需要这些功能吗
* 是否促销是产品和sku都要符合吗。
* 点击商品促销只有一个跳转页面吗

### 表格的菜单功能

# 系统升级通知

## 新增的api

/notice/recieve/get-version-upgrade-notice NoticeRecieveController get getVersionUpgradeNotice 获取版本升级通知

/monitor/subscribe/delete-by-acId  NoticeSubscribeController  delete  deleteVersionUpgradeSubscribe  notice

/monitor/subscribe/add-version-upgrade-Subscribe NoticeSubscribeController get addVersionUpgradeSubscribe  notice

## 操作

添加三个主题
