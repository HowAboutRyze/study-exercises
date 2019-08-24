# 《数据结构与算法JavaScript描述》

> 通过学习本书，巩固自己的数据结构及算法方面的能力

# 第二章 数组

数组是计算机编程世界里最常见的数据结构。任何一种编程语言都包含数组，只是形式上 略有不同罢了。数组是编程语言中的内建类型，通常效率很高，可以满足不同需求的数据存储。

由于 Array 在 JavaScript 中被当作对象，因此它有许多属性和方法可以在编程时使用。

## 练习:

### 1.  创建一个记录学生成绩的对象，提供一个添加成绩的方法，以及一个显示学生平均成绩的方法。

<details><summary><b>my answer</b></summary>
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

<details><summary><b>my answer</b></summary>
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

<details><summary><b>my answer</b></summary>
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

<details><summary><b>my answer</b></summary>
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

# 第三章 列表

在日常生活中，人们经常使用列表：待办事项列表、购物清单、十佳榜单、最后十名榜单 等。计算机程序也在使用列表，尤其是列表中保存的元素不是太多时。当不需要在一个很 长的序列中查找元素，或者对其进行排序时，列表显得尤为有用。反之，如果数据结构非 常复杂，列表的作用就没有那么大了。

## 列表的抽象数据类型定义

列表是一组有序的数据。每个列表中的数据项称为元素。在 JavaScript 中，列表中的元素可以是任意数据类型。列表中可以保存多少元素并没有事先限定，实际使用时元素的数量受到程序内存的限制。
不包含任何元素的列表称为空列表。列表中包含元素的个数称为列表的 length。在内部实现上，用一个变量 listSize 保存列表中元素的个数。可以在列表末尾 append 一个元素，也可以在一个给定元素后或列表的起始位置 insert 一个元素。使用 remove 方法从列表中 删除元素，使用 clear 方法清空列表中所有的元素。
还可以使用 toString() 方法显示列表中所有的元素，使用 getElement() 方法显示当前元素。列表拥有描述元素位置的属性。列表有前有后（分别对应 front 和 end）。使用 next() 方法可以从当前元素移动到下一个元素，使用 prev() 方法可以移动到当前元素的前一个元素。还可以使用 moveTo(n) 方法直接移动到指定位置，这里的 n 表示要移动到第 n 个位置。currPos 属性表示列表中的当前位置。

## 实现列表类

``` js
function List() {
   this.listSize = 0;
   this.pos = 0;
   this.dataStore = [];
   this.clear = clear;
   this.find = find;
   this.toString = toString;
   this.insert = insert;
   this.append = append;
   this.remove = remove;
   this.front = front;
   this.end = end;
   this.prev = prev;
   this.next = next;
   this.length = length;
   this.currPos = currPos;
   this.moveTo = moveTo;
   this.getElement = getElement;
   this.contains = contains;
}
// 给列表添加元素
function append(element) {
   this.dataStore[this.listSize++] = element;
}
// 在列表中查找某一元素
function find(element) {
   for (var i = 0; i < this.dataStore.length; ++i) {
      if (this.dataStore[i] == element) {
         return i;
      }
   }
   return -1;
}
// 从列表中删除元素
function remove(element) {
   var foundAt = this.find(element);
   if (foundAt > -1) {
      this.dataStore.splice(foundAt,1);
      --this.listSize;
      return true;
   }
   return false;
}
// 列表中有多少个元素
function length() {
    return this.listSize;
}
// 显示列表中的元素
function toString() {
    return this.dataStore;
}
// 向列表中插入一个元素
function insert(element, after) {
    let insertPos = this.find(after);
    if (insertPos > -1) {
        this.dataStore.splice(insertPos + 1, 0, element);
        this.listSize++;
        return true;
    }
    return false;
}
// 清空列表中所有的元素
function clear() {
    delete this.dataStore;
    this.dataStore.length = 0;
    this.listSize = this.pos = 0;
}
// 判断给定值是否在列表中
function contains(element) {
    for (let i = 0; i < this.dataStore.length; i++) {
        if (this.dataStore[i] === element) {
            return true;
        }
    }
    return false;
}
// 移动到列表中的第一个元素
function front() {
    this.pos = 0;
}
// 移动到列表中的最后一个元素
function end() {
    this.pos = this.listSize - 1;
}
// 向前移动一个单位
function prev() {
    --this.pos;
}
// 向后移动一个单位
function next() {
    if (this.pos < this.listSize) {
        ++this.pos;
    }
}
// 显示当前位置
function currPos() {
    return this.pos;
}
// 移动到指定位置
function moveTo(position) {
    this.pos = position;
}
// 获取当前元素
function getElement() {
    return this.dataStore[this.pos];
}
```

## 练习

### 1.  增加一个向列表中插入元素的方法，该方法只在待插元素大于列表中的所有元素时才执行插入操作。这里的大于有多重含义，对于数字，它是指数值上的大小；对于字母，它是指在字母表中出现的先后顺序。

<details><summary><b>my answer</b></summary>
<p>

``` js
List.prototype.insertMax = function(element) {
	let isNum = !isNaN(element);
	for (let i = 0; i < this.dataStore.length; i++) {
		if(isNum && !isNaN(this.dataStore[i]) && element <= this.dataStore[i]) {
			return false;
		}
		if(!isNum && isNaN(this.dataStore[i]) && this.dataStore[i].charCodeAt() && element.charCodeAt() <= this.dataStore[i].charCodeAt()) {
			return false;
		}
	}
	this.append(element);
	return true;
}

let testList = new List();
testList.append(`h`);
testList.append(`j`);
testList.append(`d`);
testList.append(3);
testList.append(5);
testList.insertMax(6);  // true
testList.insertMax(3);  // false
testList.insertMax('s'); // true
testList.insertMax('a');  // false
testList.dataStore;  // ["h", "j", "d", 3, 5, 6, "s"]
```

</p>
</details>

### 2.  增加一个向列表中插入元素的方法，该方法只在待插元素小于列表中的所有元素时才执 行插入操作。

<details><summary><b>my answer</b></summary>
<p>

``` js
List.prototype.insertMin = function(element) {
	let isNum = !isNaN(element);
	for (let i = 0; i < this.dataStore.length; i++) {
		if(isNum && !isNaN(this.dataStore[i]) && element >= this.dataStore[i]) {
			return false;
		}
		if(!isNum && isNaN(this.dataStore[i]) && this.dataStore[i].charCodeAt() && element.charCodeAt() >= this.dataStore[i].charCodeAt()) {
			return false;
		}
	}
	this.append(element);
	return true;
}

let testList = new List();
testList.append(`h`);
testList.append(`j`);
testList.append(`d`);
testList.append(3);
testList.append(5);
testList.insertMin(6);  // false
testList.insertMin(3);  // false
testList.insertMin(2);  // true
testList.insertMin('s'); // false
testList.insertMin('a');  // true
testList.dataStore;  // ["h", "j", "d", 3, 5, 2, "a"]
```

</p>
</details>

### 3.  创建 Person 类，该类用于保存人的姓名和性别信息。创建一个至少包含 10 个 Person 对象的列表。写一个函数显示列表中所有拥有相同性别的人。

<details><summary><b>my answer</b></summary>
<p>

``` js
function Person() {
	this.dataStore = [];
	this.append = append;
	this.showSameSex = showSameSex;
}
function append(name, sex) {
	const people = { name, sex };
	this.dataStore.push(people);
}
function showSameSex(sex) {
	const sameSex = [];
	const len = this.dataStore.length;
	for(let i = 0; i < len; i++) {
		if(this.dataStore[i].sex === sex) {
			sameSex.push(this.dataStore[i].name);
		}
	}
	return sameSex;
}

let per = new Person();
per.append('李一','男');
per.append('李二','女');
per.append('李三','男');
per.append('李四','男');
per.append('李五','女');
per.append('李六','男');
per.append('李七','男');
per.append('李八','男');
per.append('李九','女');
per.append('李十','女');
per.showSameSex('男');  // ["李一", "李三", "李四", "李六", "李七", "李八"]
per.showSameSex('女');  // ["李二", "李五", "李九", "李十"]
```

</p>
</details>

### 4.  修改本章的影碟租赁程序，当一部影片检出后，将其加入一个已租影片列表。每当有客户检出一部影片，都显示该列表中的内容。

<details><summary><b>my answer</b></summary>
<p>

``` js
function Customer(name, movie) {
	this.name = name;
	this.movie = movie;
}
function checkOut(name, movie, filmList, customerList, rentedList) {
	if(filmList.contains(movie)) {
		let c = new Customer(name, movie);
		customerList.append(c);
		filmList.remove(movie);
		rentedList.append(movie);
		console.log('已租：', rentedList.dataStore);
	} else {
		console.log(movie + 'is not available');
	}
}
const movies = ['大鱼海棠', '大圣归来', '哪吒之魔童降世', '烈火英雄', '流浪地球', '扫毒', '追龙'];
let movieList = new List();
let customers = new List();
let rentedList = new List();
for(let i = 0; i < movies.length; ++i) {
	movieList.append(movies[i]);
}
checkOut('李四', '大圣归来', movieList, customers, rentedList);  // 已租： ["大圣归来"]
```

</p>
</details>

### 5.  为影碟租赁程序创建一个 check-in() 函数，当客户归还一部影片时，将该影片从已租列表中删除，同时添加到现有影片列表中。

<details><summary><b>my answer</b></summary>
<p>

``` js
function checkIn(movie, filmList, rentedList) {
	if(rentedList.contains(movie)) {
		filmList.append(movie);
		rentedList.remove(movie);
		console.log('已还：', movie,'，已租列表：', rentedList.dataStore);
	} else {
		console.log(movie + 'is not rented');
	}
}
checkIn('大圣归来', movieList, rentedList);  // 已还： 大圣归来 ，已租列表： []
```

</p>
</details>
