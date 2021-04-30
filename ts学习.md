# 基础类型



## 布尔值

```tsx
	let isDone: boolean = false
```



## 字符串

```tsx
let name: string = "bob";
name = "smith"

let name: string = `Gene`;
let age: number = 37;
let sentence: string = `Hello,my name is ${name}.

I'll be ${ age +1} years old next month.`
```



## 数组

```typescript
let list: number[] = [1,2,3];

let list: Array<number> = [1,2,3];
```



## 数字

```typescript
let decLiteral: number = 6;
```



## 元祖Tuple

```typescript
//Declare a tuple type
let x: [string, number];
x=['hello',10]
```

当访问一个已知索引的元素，会得到正确的类型

当访问一个越界的元素，会使用联合类型替代 （string | number）类型



## 枚举类型

> `enum`类型是对JavaScript标准数据类型的一个补充

```typescript
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

默认情况下，从`0` 开始为元素编号。你也可以手动的指定成员的数值。例如，我们将上面的例子改成从`1` 开始编号;

```typescript
enum Color {Red = 1, Green, Blue}
let c： Color = Color.Green;
```

或者，全部都采用手动赋值:

```typescript
enum Color {Red = 1,Green = 2,Blue = 4}
let c: Color = Color.Green;

enum Color {Red =1,Green ,Blue}
let colorName: string = Color[2];

alert(colorName);//显示'Green'因为上面代码里它的值是2
```



## 任意值

```typescript
let notSure: any = 4;
notSure = "maybe a string instead"
notSure = false;
notSure.ifItExists();
//Object类型变量只允许赋值任意，却不能调用上面的方法
let list: any[] = [1, true, "free"];
list[1] = 100;
```



## 空值

表示没有任何类型

```typescript
function warnUser(): void {
    alert("This is my warning message");
}
//void类型变量只能赋值 undefined 和 null
let unusable: void = undefined;
```



## Null 和 Undefined

```typescript
let u: undefined = undefined;
let n: null = null;
//默认情况下 null 和 undefined是所有类型的子类 --strictNullChecks标记下只能赋值给void和自己
```



## Never

`never` 类型表示的是那些永不存在的值的类型。例如：`never`类型是那些总会抛出异常或根本不会有返回值的函数表达式或箭头函数表达式的返回值类型;变量也可能是`never`类型，当它们被永不为真的类型保护所约束时。

```typescript
//返回never的函数必须存在无法到达的终点
function error(message: string): never {
    throw new Error(message);
}

//推断的返回值类型为never
function fail() {
    return error("something failed");
}

//返回never的函数必须存在无法到达的终点
function infiniteLoop(): never {
    while (true){
        
    }
}

```



## 类型断言

```typescript
let someValue: any = "this is a string";

//<>语法
let strLength: number = (<string>someValue).length;

//as 语法 在TypeScript里使用JSX时，只有as语法断言是被允许的
let strLength: number = (someValue as string).length
```

# 变量声明

## var声明

## let声明

### 块作用域

```typescript
function f(input: boolean) {
    let a = 100;
    
    if (input) {
        //still okay to reference 'a'
        let b = a+1;
        return b;
    }
    
    // Error: 'b' doesn't exist here
    return b;
}

//illegal to user 'a' before it's declared;
a++;
let a;

//我们可以在拥有块级作用域变量被声明前获取它。只是我们不能在变量声明前去调用那个函数。
function foo(){
    //okay to capture 'a'
    return a;
}
//不能在'a' 被声明前调用foo，运行时应该抛出错误
foo();
let a;
```



### 重定义及屏蔽

```typescript
//var 不在乎你声明多少次；你只会得到一个
function f(x) {
    var x;
    var x;
    
    if(true) {
        var x;
    }
}

let x = 10;
let x = 20; // error,不能在1个作用域多次声明'x'

//并不是要求2个均是块级作用域的声明TypeScript才会给出一个错误的警告
function f(x) {
    let x = 100;//error: interfers with paramter declaration
}

function g() {
    let x = 100;
    var x = 100; //error: can't have both declarations of 'x'
}

//并不是说块级作用域变量不能用函数作用域变量来声明。块级作用域变量需要在明显不同的块里声明
function f(condition, x) {
    if (condition) {
        let x = 100;
        return x;
    }

    return x;
}

f(false, 0); // returns 0
f(true, 0);  // returns 100
```



### 块级作用域变量的获取

```typescript
for (let i = 0; i<10; i++) {
    setTimeout(function() {console.log(i);},100 * i);
}
```



## `const`声明

与`let`声明类似，被赋值后不能再改变。

```typescript
const numLivesForCat = 9;
const kitty = {
    name: "Aurora",
    numLives: numLivesForCat,
}

// Error
kitty = {
    name: "Danielle",
    numLives: numLivesForCat
};

// all "okay"
kitty.name = "Rory";
kitty.name = "Kitty";
kitty.name = "Cat";
kitty.numLives--;
```



## 解构

### 解构数组

```typescript
let input = [1,2];
let [first, second] = input;
console.log(first); //outputs 1
console.log(second); //outputs 2

//swap variables
[first, second] = [second, first]

//作用于函数参数
function f([first, second]: [number, number]){
    console.log(first);
    console.log(second);
}
f(input);

//使用 ...语法创建剩余变量
let [first, ...rest] = [1,2,3,4];
console.log(first); //outputs 1
console.log(rest); //outputs[2,3,4]

//你可以忽略尾随元素
let [first] = [1,2,3,4];
console.log(first); //outputs 1

let [, second, , fourth] = [1,2,3,4];
```



### 对象解构

```typescript
let o = {
    a: "foo",
    b: 12,
    c:"bar"
};
let {a,b} = o;

({a, b} = {a: "baz", b:101});

let { a, ...passthrough} = o;
let total = passthrough.b + passthrough.c.length;
```



### 属性重命名

```typescript
let { a: newName1, b: new Name2} = o;
let {a, b}: {a: string, b: number} = o;
```



### 默认值

> 默认值可以让你在属性为`undeifined`时使用缺省值:

```typescript
function keepWholeObject(wholeObject: { a: string, b?: number}){
    let { a, b = 1001 } = wholeObject;
}
```



现在即使`b`为undefined, `keepWholeObject` 函数的变量 `wholeobject` 的属性 `a` 和`b` 都会有值

### 函数声明

```typescript
type C = { a: string, b?: number}
function f({ a, b }: C): void {
    //...
}

function f({ a, b } = { a: "", b: 0}): void {
    //...
}
f(); //ok,default to { a: "", b: 0}
```



## 展开

``` typescript
//这会令bothPlus的值为[0, 1, 2, 3, 4, 5]。 展开操作创建了first和second的一份浅拷贝。 它们不会被展开操作所改变。
let first = [1, 2];
let second = [3, 4];
let bothPlus = [0, ...first, ...second, 5];
//search的值为{ food: "rich", price: "$$", ambiance: "noisy" }。 对象的展开比数组的展开要复杂的多。 像数组展开一样，它是从左至右进行处理，但结果仍为对象。 这就意味着出现在展开对象后面的属性会覆盖前面的属性。 因此，如果我们修改上面的例子，在结尾处进行展开的话：
let defaults = { food: "spicy", price: "$$", ambiance: "noisy" };
let search = { ...defaults, food: "rich" };

//对象展开还有其它一些意想不到的限制。 首先，它仅包含对象 自身的可枚举属性。 大体上是说当你展开一个对象实例时，你会丢失其方法：
class C {
  p = 12;
  m() {
  }
}
let c = new C();
let clone = { ...c };
clone.p; // ok
clone.m(); // error!
```

