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

