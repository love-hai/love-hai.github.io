## 协程
1. 协程是一种轻量级的线程，可以在任何地方挂起和恢复,可以在一个线程中结束，另一个线程中恢复
2. 协程是 Kotlin 的一个库，不是语言的一部分， 需要依赖库 `kotlinx-coroutines-core`



### 挂起函数
1. 挂起函数是一个可以暂停执行并在稍后恢复的函数
2. 挂起函数可以在不阻塞线程的情况下执行长时间运行的操作
3. 比如在进行网络请求或者访问数据库时，可以使用挂起函数。有了返回结果后，再恢复执行。
4. 例子：
    ``` kotlin
    suspend fun doSomethingUsefulOne(): Int {
        delay(1000L) // 假设这里是一个耗时操作
        return 13
    }

    suspend fun doSomethingUsefulTwo(): Int {
        delay(1000L) // 假设这里是一个耗时操作
        return 29
    }

    fun main() = runBlocking {
        val time = measureTimeMillis {
            val one = doSomethingUsefulOne()
            val two = doSomethingUsefulTwo()
            println("The answer is ${one + two}")
        }
        println("Completed in $time ms")
    }
    ```
### 协程构建器
#### runBlocking
1. `runBlocking` 是一个用来启动顶层主协程或者测试的构建器
2. 他会阻塞当前线程，直到所有内部协程执行完毕
#### coroutineScope
1. `coroutineScope` 是一个挂起函数，会挂起当前协程，直到所有内部协程执行完毕。
2. `coroutineScope` 不会阻塞当前线程。
3. `coroutineScope`会执行完所有内部协程后，才会执行作用域外的代码。
4. 例子： 它会先执行完 t1() 内部所有的协程，再执行 t2()函数
    ``` kotlin
    fun main() = runBlocking {
        t1()
        t2()
    }
    suspend fun t1() = coroutineScope {
        launch {
            delay(2000)
            println("world 1")
        }
        println("hello 1")
    }

    suspend fun t2() = coroutineScope {
        launch {
            delay(1000)
            println("world 2")
        }
        println("hello 2")
    }
    ```

### An explicit job
1. `launch` 函数返回一个 `Job` 对象，可以用来控制协程的生命周期
2. 例子：
    ``` kotlin
    fun main() = runBlocking {
        val job = launch {
            delay(1000)
            println("World!")
        }
        println("Hello,")
        job.join() // 等待直到子协程执行完毕
        println("end")
    }
    ```
#### 取消和超时
1. `job.cancel()` 取消一个协程
2. `job.cancelAndJoin()` 取消一个协程，并等待协程执行完毕, 会抛出 `CancellationException`
3. isActive 判断协程是否处于活动状态。
4. 在被取消的协成中挂起函数会抛出 `CancellationException` 异常，可以使用withContext函数处理异常