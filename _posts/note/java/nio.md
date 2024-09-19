#### ByteBuffer
+ ByteBuffer是一个字节缓冲区，它可以在内存中存储一些字节数据，并且可以在这些数据上进行一些操作。无法扩容，但可以通过`wrap`方法将一个字节数组包装成一个ByteBuffer对象。
+ 有三个重要的属性：capacity、position、limit。
    1. capacity：缓冲区的容量，即可以存储的最大字节数。
    2. position：当前操作的位置，即下一个要操作的元素的索引。
    3. limit：缓冲区的界限，即可以操作的最大位置（limit<=capacity）。当在读取模式下，limit=position；在写入模式下，limit=capacity。
