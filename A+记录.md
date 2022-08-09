### 1、数组扁平化后去重

#### 数组扁平化

- 二维数组时，可以简单使用flat()方法

let arr=[1,2,[3,4],[3,4]].flat();

如果是多维数组，则flat()将达不到效果，

此时需要给flat()传一个参数， var newArray=arr.flat([depth]),

参数：depth，可选，指定要提取嵌套数组的结构深度，默认值为1.

let arr=[1,2,[3,4,[3,4]]].flat(Infinity);

- 迭代实现（ES6扩展运算符···）

```javascript
const arr = [1,2,[3,4,5,[6,7],8],9,10,[11,[12,13]]];
const flatten = (arr) => {
    while(arr.some(item=>Array.isArray(item))){
        arr=[].concat(...arr);
    }
    return arr;
}
 
console.log(flatten(arr)); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
```

- 普通递归实现

```javascript
const arr = [1,2,[3,4,5,[6,7],8],9,10,[11,[12,13]]];
 
const flatten = (arr) => {
  let result = [];
  arr.forEach((item, i, arr) => {
    if (Array.isArray(item)) {
      result = result.concat(flatten(item));
    } else {
      result.push(arr[i])
    }
  })
  return result;
};
 
console.log(flatten(arr));
```

- 高级递归（reduce方法）

```javascript
const flatten = (array) => array.reduce((acc,cur)=>
    (Array.isArray(cur)?[...acc,...flatten(cur)]:[...acc,cur]),[])
```

- [].concat.apply

```
const arr = [1,2,[3,4,5,[6,7],8],9,10,[11,[12,13]]];
 
const flatten = (arr) => {
  while (arr.some(item => Array.isArray(item))){
    arr = [].concat.apply([], arr);
  }
  return arr;
}
 
console.log(flatten(arr));
```

#### 数组去重

- 定义一个新数组，逐一和原数组元素对比，不同则存放在新数组中

```javascript
function change(arr){
			let newArr=[];
			for(let i=0;i<arr.length;i++){
				let repeat=false;
				for(let j=0;j<newArr.length;j++){
					if(arr[i]==newArr[j]){
						repeat=true;
						break;
					}
				}
				if(!repeat) newArr.push(arr[i]);
			}
			return newArr
		}
```

- 先将原数组排序，再与相邻的进行比较，如果不同则存入新数组

```javascript
function change(arr3){
			arr.sort()
			let newArr=[]
			for(let i=0;i<arr.length;i++){
				if(arr[i]!=arr[i-1]){
					newArr.push(arr[i])
				}
			}
			return newArr
		}
```

- 利用对象属性存在的特性，如果没有该属性则存入新数组

```js
function change(arr){
			let obj={}
			let newArr=[]
			for(let i=0;i<arr.length;i++){
				if(!obj[arr[i]]){
					obj[arr[i]]=1
					newArr.push(arr[i])
				}
			}
			return newArr.sort()
		}
```

- 利用数组的indexOf下标来查询

```js
function change(arr){
			let newArr=[]
			for(let i=0;i<arr.length;i++){
				if(newArr.indexOf(arr[i])==-1){
					newArr.push(arr[i])
				}
			}
			return newArr
		}
```

- 利用数组原型对象上的includes方法

```js
function change(arr){
			let newArr=[]
			for(let i=0;i<arr.length;i++){
				if(!newArr.includes(arr[i])){
					newArr.push(arr[i])
				}
			}
			return newArr
		}
```

- 利用数组原型对象上的filter和includes方法

```js
function change(arr){
			let newArr=[]
			newArr=arr.filter((item)=>{
				return newArr.includes(item)?'':newArr.push(item)
			})
			return newArr
		}
```

- 利用数组原型对象上的forEach和includes方法

```js
function change(arr){
			let newArr=[];
			arr.forEach(item=>{
				return newArr.includes(item)?'':newArr.push(item)
			})
			return newArr
		}
```

- 利用数组原型对象上的splice方法

```js
function change(arr){
			let i,j,len=arr.length;
			for(i=0;i<len;i++){
				for(j=i+1;j<len;j++){
					if(arr[i]==arr[j]){
						arr.splice(j,1);
						len--;
						j--
					}
				}
			}
			return arr;
		}
```

- 利用数组原型对象上的lastIndexOf方法

```js
function change(arr){
			let res=[];
			for(let i=0;i<arr.length;i++){
				res.lastIndexOf(arr[i])!==-1?'':res.push(arr[i])
			}
			return res;
		}
```

- 利用ES6的Set方法

```js
arr1=Array.from(new Set(arr))
```

### 2、将JS对象转换成树形结构

```js
// 转换前：
source = [{
            id: 1,
            pid: 0,
            name: 'body'
          }, {
            id: 2,
            pid: 1,
            name: 'title'
          }, {
            id: 3,
            pid: 2,
            name: 'div'
          }]
// 转换为: 
tree = [{
          id: 1,
          pid: 0,
          name: 'body',
          children: [{
            id: 2,
            pid: 1,
            name: 'title',
            children: [{
              id: 3,
              pid: 1,
              name: 'div'
            }]
          }
        }]
 
function jsonToTree(data) {
  // 初始化结果数组，并判断输入数据的格式
  let result = []
  if(!Array.isArray(data)) {
    return result
  }
  // 使用map，将当前对象的id与当前对象对应存储起来
  let map = {};
  data.forEach(item => {
    map[item.id] = item;
  });
  // 
  data.forEach(item => {
    let parent = map[item.pid];
    if(parent) {
      (parent.children || (parent.children = [])).push(item);
    } else {
      result.push(item);
    }
  });
  return result;
}
```

### 3、统计字符串各个字符的个数

```js
 let str='dalgjajgagagj';
    let map={};
    for(let i=0;i<str.length;i++){
      if(map[str[i]]){
        map[str[i]]++;
      }else{
        map[str[i]]=1;
      }
    }
    console.log(map );
```

