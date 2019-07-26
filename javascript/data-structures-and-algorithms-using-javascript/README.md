# 《数据结构与算法JavaScript描述》

> 通过学习本书，巩固自己的数据结构及算法方面的能力

## 第二章 数组

数组是计算机编程世界里最常见的数据结构。任何一种编程语言都包含数组，只是形式上 略有不同罢了。数组是编程语言中的内建类型，通常效率很高，可以满足不同需求的数据存储。

由于 Array 在 JavaScript 中被当作对象，因此它有许多属性和方法可以在编程时使用。

### 1.  创建一个记录学生成绩的对象，提供一个添加成绩的方法，以及一个显示学生平均成绩的方法。

<details><summary><b>答</b></summary>
<p>

``` js
// 记录学生成绩的对象
function Student(name) {
	this.name = name;
	this.grade = {};
	this.addGrade = addGrade;
	this.averageGrade = averageGrade;
}
// 添加成绩的方法
function addGrade(subject, mark) {
	this.grade[subject] = mark;
}
// 显示学生平均成绩的方法
function averageGrade() {
	let sum = 0;
	Object.values(this.grade).forEach(sub => {
		sum += sub;
	})
	console.log('平均成绩：', sum / Object.values(this.grade).length);
}
// 测试
let Mike = new Student('Mike');
Mike.addGrade('语文', 88);
Mike.addGrade('数学', 99);
Mike.addGrade('英语', 33);
Mike.averageGrade();     // 平均成绩： 73.33333333333333
```

</p>
</details>

### 2.  将一组单词存储在一个数组中，并按正序和倒序分别显示这些单词。

<details><summary><b>答</b></summary>
<p>

``` js
let arr = ['ds', 'sg', 'ag', 'ew', 'b'];
function positiveArr() {
	console.log('正序：', arr.sort());
}
function reverseArr() {
	console.log('正序：', arr.sort().reverse());
}
// 测试
positiveArr();  // 正序： (5) ["ag", "b", "ds", "ew", "sg"]
undefined
reverseArr();  // 正序： (5) ["sg", "ew", "ds", "b", "ag"]
```

</p>
</details>

### 3.  修改本章前面出现过的 weeklyTemps 对象，使它可以使用一个二维数组来存储每月的有用数据。增加一些方法用以显示月平均数、具体某一周平均数和所有周的平均数。

原文 weeklyTemps 对象：

``` js
function weekTemps() {
	this.dataStore = [];
	this.add = add;
	this.average = average;
} 
 
function add(temp) {
	this.dataStore.push(temp);
} 
 
function average() {
	var total = 0;
	for (var i = 0; i < this.dataStore.length; ++i) {
		total += this.dataStore[i];
	}
	return total / this.dataStore.length;
} 
```

<details><summary><b>答</b></summary>
<p>

``` js
function MonthTemps() {
	this.dataStore = [];
	this.add = add;
	this.getMonthAverage = getMonthAverage;
	this.getWeekAverage = getWeekAverage;
	this.getAllWeekAverage = getAllWeekAverage;
}
// 增加
function add(week, temp) {
	if(this.dataStore[week] === undefined) {
		this.dataStore[week] = [];
	}
	this.dataStore[week].push(temp);
}
// 月平均数
function getMonthAverage() {
	var total = 0;
	var days = 0;
	for(var i = 0; i < this.dataStore.length; ++i) {
		days += this.dataStore[i].length;
		for(var j = 0; j < this.dataStore[i].length; ++j) {
			total += this.dataStore[i][j];
		}
	}
	return total / days;
}
// 某一周平均数
function getWeekAverage(week) {
	var total = 0;
	for(var i = 0; i < this.dataStore[week].length; ++i) {
		total += this.dataStore[week][i];
	}
	return total / this.dataStore[week].length;
}
// 所有周的平均数
function getAllWeekAverage() {
	var total = 0;
	for(var i = 0; i < this.dataStore.length; ++i) {
		total += this.getWeekAverage(i);
	}
	return total / this.dataStore.length;
}

// 测试
let thisMonth = new MonthTemps();
for(var i = 0;i < 4; ++i){
	for(var j = 0; j < 7; ++j) {
		thisMonth.add(i, Math.floor(Math.random() * 100 + 1));
	}
}
thisMonth.getMonthAverage();   // 58.75
thisMonth.getWeekAverage(2);   // 60.714285714285715
thisMonth.getAllWeekAverage();   // 58.75
```

</p>
</details>

### 4.  创建这样一个对象，它将字母存储在一个数组中，并且用一个方法可以将字母连在一起，显示成一个单词。

<details><summary><b>答</b></summary>
<p>

``` js
function Letters() {
	this.letterList = ['a', 'd', 'b', 's', 'h'];
	this.joinLetter = joinLetter;
}
function joinLetter(separator) {
	let _separator = ',', str = '';
	if(separator) {
		_separator = separator;
	}
	for(var i = 0; i < this.letterList.length; ++i) {
		str += this.letterList[i] + (i < this.letterList.length - 1 ? _separator : '');
	}
	return str;
}

// 测试
let newLetters = new Letters();
newLetters.joinLetter('/');  // 'a/d/b/s/h'
newLetters.joinLetter();  // 'a,d,b,s,h'
```

</p>
</details>