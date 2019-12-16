<center> ES6 学习笔记 </center>
###  let 关键字的语法与规范  
指定编码   <meta charset = "utf - 8">

**let**    声明的变量不能重复声明     不存在变量提升   俗称 零时性死区

**let**     的块级作用域    可以代替 闭包的一些功能   **for    if     while    else** 等代码块产生块级作用域     循环里 用着很舒服

**const**    声明常量    常量的值 一旦声明 就不能修改   **const** 声明的 常量也具有(块级作用域   局部作用域   全局作用域)

**window**   顶层对象    **ES6** 中去掉了顶层对象的概念   
为了向下兼容  在全局作用域中使用 **var**  声明的变量和直接声明的函数任然是顶层对象的属性和方法. 而使用 **let** 和 **const** 声明的变量不再输入顶层对象

### 数组的解构赋值
` let  [ a , b , c] = [ 100 ,200 ,300 ]`
复杂数组的模式匹配
` let  [  a , [ [ b ], [ c , d ] ] ] = [ 100, [ [ 200],[ 300 ,400 ] ] ]`
变量 可以有默认值   
保证等号两边的数组模式是一样
如果不能正确解构   有的变量可能会自动赋个值 undefined

### 对象的解构赋值
` let  { aa   ,   bb  }  =  { aa: '1111' , bb:'2222'  }`
` let  {  one:a   ,   two:b  }   =   { one:'nihao' ,  two:'gun'  }

对象解构   复杂的形式
```
let   obj =  {
				p:  [
						'hello',
						{ y: 'world'  }
				]
}
let  { p:  [x ,  { y:y } ]  }  =  obj 
			console.log( x   ,  y  );
```
#### 特殊对象的解构
一切皆对象     字符串可以被看做是由字符串组成的数组
```
let   [ a  ,   b  ,  c  ,  d ,  e  , f  ]  =   '  hellow'
```
字符串当成  对象
```
let   { length:len}   =  'world'
console.log (len)   // 输出是5   因为 world 这个字符串 长度是 5

```
### 变量的解构赋值
交换两个变量的值
提取 **json** 中数据
设置函数的默认值
ES6模块

```
let   a   =  100;
let   b   =  200;
// 交换值
[ a  ,   b  ]    =  [   b   ,   a   ]
console.log(  a   ,    b  );      //  输出值已近被互换了

// 提取   josn  中的数据
let   jsonData  =  {
				id:42,
				name:'OK',
				data:[ 666 ,777 ]
};
let  {  id   ,  name  ,  data  }  =  jsonData;
console.log ( id ,  name , data );

// 函数中的默认值
```
### for   of  语法结构的用法
可以遍历那些数据类型

1. Array**       字符串      类数组对象         **arguments     Map     Set**
2. for   of**   与 其他遍历方式做个比较
3.    for      of**    可以遍历的类型比    **for    in**   更多
4.  for       of**     直接遍历出值     **for    in**    遍历处来的是   **key** 
5.  forEach**  方式  可以遍历更多的类型     可以使用   **break**   和  **continue**  等结束语句
6. Iterator**    遍历器     是 ES6  定义的一个接口
7.  Array**   实现了  **Interator** 的接口
8.   遍历器接口的数据类型都可以用于      **for    of**  

```
<script>
	//  遍历数组
		let  arr  =  [  'aaa'  ,'bb' ,'cc' ];
				for ( let  var   of   arr) {
							console.log(var);
				}
	// 遍历字符串
	for ( let  var    of    'abcdef') {
					console.log( var )
	}
	</script>
```
### 字符串新曾的特性
模板字符串    定义比较长   复杂字符串   如  html  代码
模板字符串中写    `  需要转义
模板字符串中  插入变量    ${ 变量名}
模板字符串中   插入函数的调用    ${  函数名() }

```
<script>
//  定义变量
let  username  =  "小强";
// 模块字符串   ``   
// 函数
function   fn( ){
			return   "hello   world";
}
let  html = `
		<div>
				<div>
						<p>${ username }</p>
						<p>${ fn() }> </p>
				</div>
		</div>
		`;
consol.log(html);
</script>
```
**repeat**  方法
把字符串      重复输出

```
let   str  =   "hellow";
// 重复输出  3次  hellow
console.log(str.repeat(3) );
// 重复输出  10 次  a
console.log('a'.repeat(10) );
```

**字符串补全长度的方法**   **padStart( )     padEnd( )**

```
// 字符串自动补全的方法
let    str  =  "hellow";
console.log( str );
console.log( str.padStart(10) )
console.log( str.padStart(10," * ")  )   // 以星号 补全   
```
**字符串包含验证**
includes(  )       startsWith(  )        endsWith(  )

 ```
let   str  =  " hellow   world";
console.log ( str . indexOf( 'w ') );
console.log ( str.includes ( 'a' ) );
// 判断字符串开头
console.log( str .startsWith ( 'hellow' ) );
// 判断字符串以什么结尾
console.log( str .endsWith( 'world' ) );
 ```
###  函数的 新增特性
函数参数的默认值  
**reset** 参数       得到一个纯数组
**箭头函数**   
          简化函数的声明 
          参数超过1个加 (  )
          函数体 超过1行   加 {  }   自己写 return 
箭头函数的作用  
				简化回调函数的写法
				箭头函数中的 this  是函数声明时所在的对象  
				函数参数的尾逗号( ES2017新增的)
```
let  fn = val => val;   
//等同于    let  fn  = function( val ) {  return  val;  }   
// 实现两个数的和
let  sun = ( num1 , num2 )  =>  num1+num2;
console.log( sum( 1,5 ) );    // 输出两数的和

```
### 数组的新增扩展
1. 扩展运算符  ( ... )       定义 扩展运算符相当于  rest 参数的 逆运算   把数组转为用逗号分割的参数列表 
```
//rest   参数
function  fn  (...args ){
		console.log(args);   // 接收到了所以传进来的参数 转换成数组了 
}
			fn(1,4,7);
			
// 定义函数
function  demo( x , y  , z) {
		console.log( x +  y  +  z );
}
demo (10 , 20 ,30 );
// 定义一个函数
let  arglist   =   [ 1, 2, 3 ];
demo(...arglist );      //  这里前面加上三个点 转换成了  demo( 1  ,2 , 3 )
```
#### 应用
复制数组    (克隆数组)
合并数组
与解构赋值一起使用
作用于 字符串
```
let  a  =  [ 10 ,20 ,30 ];
// 复制a 数组  赋值给b    这里赋值其实是把 a 的地址赋给 b  两个地址都指向一段数据  
 let  b  =  a;

console.log(a );
console.log(b );
b[ 1 ] = '小明';
console.log ( a );

// 复制 数组
let arr1  =  [ 100 , 220 ,330  ];
let arr2  =  [ ...arr1  ];     // 这样复制的数组  也叫克隆  给的是数据 不是地址

// 合并数组
let   a  =  [ '第一个数组' , '你大爷'];
let   b  =  [ '第二个数组' ,'他大爷 ' ] ;
let   c   =  [ 100,200 ];
// ES5 中的 合并
let  newarr   =  a.concat ( b , c );
console.log ( newarr );   //  三个数组被合并在一起了

//  ES6  扩展运算符
let    newlist   =   [ ...a ,  ...b ,  ...c  ];
console.log ( newlist );

//  扩展运算符与 解构赋值一起使用
let  [ a ,b, ...args ] = [1 ,  2 ,  3 , 4 , 5  , 6];
console.log( a );   //  输出 1
console.log( b );   // 输出  2
		console.log( args );   // 输出的是一个数组   3  4  5  6  
		
// 扩展运算符   作用于字符串
let  args  =  [ ...  'hellow' ];     //  [ 'h' , 'e', 'l' , 'l' ,'o' ,'w' ]
console.log( args );    //  这里把字符串转为了 由逗号隔开的参数列表
// 扩展运算符  作用于所以实现了  Iterator (迭代器接口)  的数据类型
```
### Array 构造函数的新增方法
**Array . from ( )** 可以把  类数组对象和实现了迭代器接口的数据类型 转换成真正的对象
**Array . of ( )**   将一组值 转换为  数组 (创建数组)

### 数组新增特效    - 数组对象方法
**find ( )** 返回数组中第一个满足条件的元素   参数是回调函数
**findIndex (  )**  获取数组中第一个满足条件的索引   参数都是回调函数
**entries( )**      遍历数组中的  key  和 value         for  ....of
**keys( )**     遍历数组中 所有的  索引值 key     for ...of
**values( )**     chrome  中未能实战
**includes ( )**   表示数组中 是否包含某个指定的值  返回布尔值

```
let   arrs = [ '小 ' ,  '大'  ,   100 ,  'mi'  ];
//keys()     遍历数组中 所有的  索引值
for ( let  k  of  arrs . keys( )  ) {
				console.log( k );
}
// entrirs ( )   遍历数组中的额key  和 value 
for( let  [ key , val ] of  arrs . entries ( ) ) {
				console.log( key , val );
}

```
### 对象的新增特性
属性的简洁表示
```
let  username  =  "didi";
let  userage  =  100;
// ES5 写法
let  userInfo  =  {
			username = username, 
			userage  =  userage
};
//  ES6  新写法
let  userInfo  = {
			username,
			userage,
			
			// ES5  
			fn:function ( ){
					console.log( 'fn' );
			} ,
			// ES6   方法的简写
			demo( ){
					console.log( 'demo' );
			}
}
console.log ( userInfo )
```
###  Object.is (  )
用于比较  类似于  === 
0  和 -0   使用 Object .is ( )  判断不相等
NaN   和   NaN 使用Object . is ( )  判断 相等
` console.log ( Object .is ( 10,100 ) );`
 Object . assign ( )  合并对象
 Object  . keys ( )   取对象中的属性名  以数组形式返回
 Object . values( )   取对象中的   属性 以数组形式返回
 Object . entries( )    遍历对象中的 属性和方法

 ### 新增 Set   和 Map 类型数据解构
 + 定义 
类似于数组, 但是其成员是唯一的
实现了 Interator  接口
set  结构只有值  没有索引
```
let  mysey  = new set([10,20,30,10,30]);
			myset.add('myset');
			myset.delete(20);
```
Set  的构造函数  可以接受一个数组
可以接受所有实现了 Interator 接口的数据解构
+ 属性: set 数据解构的属性     size
+ 方法     add ( )  向 set 中添加一个会员  
 delete ( value ) 删除某个成员  要有成员的值
has ( value ) 检查数组中是否存在某个值    结果返回 布尔值
 clear ( )      清除所以成员

Set  数据解构的遍历
foreach  (  )
keys (  )   等同于   values (  )
values (  )
entries (  )

### WeakSet  
+ 定义
与 Set 类型 相似  成员唯一   成员必须是对象
WeakSet  中的对象都是弱引用   
不能遍历     也没有   size  属性
没有实现  Interator 接口
```
let  ws  = new WeakSet( [ string,{ } ] );
ws.add ( window );
ws.delete ( string );
```
+ 方法
add ( )
delete (  )
has (  )

###  Map
+ 定义
Map  跟对象类似    键值对组成集合  键的类型可以是任何类型
+ 构造函数
构造函数的 参数可以是数组   数组是二维数组   元素数组两个元素   key  value
+ 属性
size   得到他的长度
+ 方法
get ( key )  取值
set ( key )    添加 
set  ( key, value )    修改/添加
has ( key )  判断是否存在
clear (  )  清空所以
```
let  m  = Map ( [ ["name","ooo" ],["age","zzzz" ],["diid","oppo" ] ] );
//  取值
console.log( m.get( 'name' ) );
cons哦了.log( m.size )
// 添加
m.set ( true , "出出出" );
// 判断  键是否存在
console.log ( m.has ( true ) );
// 清空所以
m.clear ( );
```
###  weakmap
+ 定义
键必须是对象   键所执行的对象是弱引用
不可遍历  没有实现 Interator  接口
+方法
get ( key )  取值
set ( key )    添加 
has ( key )  判断是否存在
delete(  ) 删除
```
let  wm  =  new  WeakMap (  );
// 添加
wm.set ( { },"hellow");
wm.set (window, 'world );
```
###  Promise  基础
+ js 中的异步操作
ajax  请求
浏览器事件
定时器
+ 回调函数

```
setTime( function (  ){

},1000 );

ele.addEventListener ( "click" , function ( ) {

} )

xhr.addEventListener ( "readystatechange"  , function ( ) {

} )
```
###  回调地狱    
回调函数嵌套回调函数   影响代码的可读性
+ Promise 
解决回调地狱
向同步操作那样去执行异步的操作
+ Promise  的构造函数
构造函数必须接受一个函数作为参数  函数可以接口参数
+ Promise   的原理
一个promise  实例  ( 对象 )   代表一个异步操作
promise   通过状态去 管理  异步操作
+ 状态
pendding     ( 进行中 )
fufilled    ( 已完成 )       什么时候是已完成状态    resolve (  ) 函数执行之后
rejected  ( 已失败 )      reject (  )  函数执行的时候 就变成失败状态了

