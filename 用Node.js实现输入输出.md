### 用Node.js实现输入输出

#### 输入单行的情况

```
// 输入单行的情况
var readline = require('readline'); // 引入readline接口，读取输入行
var rl = readline.createInterface({ // 创建输入输出接口
	input: process.stdin,
	output: process.stdout
});
rl.on('line', function(line) { // 监听控制台输入
	var data = line.trim(); // 获取控制台输入
	// 逻辑处理
	// ......
	console.log(data); // 输出结果
});
```

#### 输入k行的情况

```
// 输入k行的情况，比如k=2时
var readline = require('readline');
var rl = readline.createInterface({
	input: process.stdin,
	output: process.stdout
});

var k = 2;
var row = []; // 用于存储每行的输入

rl.on('line', function(line) {
	row.push(line.trim());
	if (row.length === k) { // 当输入的行数为k时，开始逻辑处理
		// 逻辑处理
		// ......
		console.log(row);
		row.length = 0; // 状态重置（如果没有这句代码，就只能实现输入一次的结果）
	}
});
```

#### 第一行输入一个数字N，接下来输入N行的情况

```
var readline = require('readline');
var rl = readline.createInterface({
	input: process.stdin,
	output: process.stdout
});

var row = []; // 用于存储每行的输入

rl.on('line', function(line) {
	row.push(line.trim());
	var N = parseInt(row[0]);
	if (row.length === N + 1) {
		// 逻辑处理
		// ......
		console.log(row);
	}
});
```

上面这样书写只能实现输入一次的结果,下面的写法就可以实现多次输入的情况。

```
var readline = require('readline');
var rl = readline.createInterface({
	input: process.stdin,
	output: process.stdout
});

var k = 0; // 先给行数置0，表示还没开始读取
var row = []; // 用来存储每行的输入

rl.on('line', function(line) {
	if (k === 0) {
		k = parseInt(line.trim()); // 读取第一行，得到接下来的行数
	} else {
		row.push(line.trim()); // 将每行输入的数据存入row数组中
		if (k === row.length) { // 当输入的行数等于设定的k值时，开始逻辑处理
			// 逻辑处理
			// ......
			console.log(row);
			// 状态重置
			row.length = 0;
			k = 0;
		}
	}
});
```
