#学习笔记
#Tic-Tac-Toe 实现
	总结：
		
	（1）二维数组和一维数组的复制：
		 JSON.parse(JSON.stringify(pattern));//二维数组或者一维数组的复制方法
		 Object.create(pattern);//二维数组转一维数据的复制方法
	（2）递归
		递归调用的过程
		递归终止的条件
#处理异步有以下方式：
##promise
    A.三种状态
        (1)pending: 初始状态，不是成功或失败状态。
        (2)fulfilled: 意味着操作成功完成。
        (3)rejected: 意味着操作失败。
    B.promise的创建：Promise新建后就会立即执行
        var promise = new Promise(function(resolve, reject) {
            // 异步处理
            // 处理结束后、调用resolve 或 reject
        });
    C.promise的自带方法：
        (1)Promise.prototype.then  两种状态的回调
        (2)Promise.prototype.catch
        (3)Promise.all 
			（3.1）Promise.all 方法用于将多个 Promise 实例，包装成一个新的 Promise 实例
	            var p = Promise.all([p1,p2,p3]);
     D.Promise.resolve 方法，Promise.reject 方法
		
##async await
	A.async
		(1)async 函数返回一个 Promise 对象，可以使用 then 方法添加回调函数
			async function f() {
			  return 'hello'
			}
			
			console.log(f());      // promise对象
			f().then(result => {
			  console.log(result); // hello
			})
		(2)async 函数内部抛出错误，会导致返回的 Promise 对象变为 reject 状态。抛出的错误对象会被 catch 方法回调函数接收到。
			async function f() {
			  throw new Error('出错了')
			}
			
			f().then(result => {
			  console.log(result); 
			}).catch(err => {
			  console.log(err); // Uncaught (in promise) Error: 出错了
			})
	B.await
		(1)await 命令后面是一个 Promise 对象，返回该对象的结果。如果不是 Promise 对象，就直接返回对应的值。另外，await 命令只能用在 async 函数之中，如果用在普通函数，就会报错
			async function f() {
			  // 等同于
			  // return 123;
			  return await 123;
			}
			
			f().then(v => console.log(v))
			// 123
		(2)await 命令后面的 Promise 对象如果变为 reject 状态，则 reject 的参数会被 catch 方法的回调函数接收到。等同于async函数返回的 Promise 对象被reject。
			async function f() {
			  await Promise.reject('出错了');
			}
			
			f()
			.then(v => console.log(v))
			.catch(e => console.log(e))
			// 出错了
		(3)任何一个await语句后面的 Promise 对象变为reject状态，那么整个async函数都会中断执行。
			async function f() {
			  await Promise.reject('出错了');
			  await Promise.resolve('hello world'); // 不会执行
			}
		(4)await 命令后面的 Promise对象，运行结果可能是 rejected ，所以最好把 await 命令放在 try...catch 代码块中。
			async function myFunction() {
			  try {
			    await test();
			  } catch (err) {
			    console.log(err);
			  }
			}
			
			// 另一种写法
			async function myFunction() {
			  await test().catch(function (err) {
			    console.log(err);
			  });

##callback(setTimeout)

