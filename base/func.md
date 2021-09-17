# Функции

### `Что такое функция`
`Функция` - это блок кода, который можно использовать повторно. Каждая функция используется для выполнения определенных задач.

Функции делятся на функцию `main` и `пользовательские` функции.

### `Как определить функцию`
Функцию можно определить через ключевое слово `fn`. 
У любой функции должно быть название.
```rust
fn main() {
  println!("Main функция");
}

fn my_func() {
  println!("Пользовательская функция");
}
``` 

### `Вызов функции`
Чтобы вызвать функцию достаточно указать ее наименование, за которым следуют `()` скобки.
```rust
fn main() {
  println!("Main функция");
  my_func();
}

fn my_func() {
  println!("Пользовательская функция");
}
```

### `Функции с параметрами`
В функции можно передавать данные в виде параметров.
`Параметры` - это переменные или значения, которые входят в определение функции.

Чтобы в функцию можно было передать параметры, нужно описать аргументы функции.
`Аргументы` - это переменные или значения, которые заменят параметры при вызове функции.
То есть в функции мы `описываем` аргументы, а `принимает` она параметры.
```rust
fn main() {
  println!("Main функция");
  my_func(5, 6); // Здесь 5 и 6 являются параметрами
}

fn my_func(a: i32, b: i32) { // Здесь a и b являются аргументами
  println!("Пользовательская функция");
  println!("{}", a + b);
}
```

В качестве параметров можно передавать переменные и значение, либо ссылки на них.

### `Передача аргументов по значению`
Когда мы передаем аргумент по значению. Значение может быть изменено только внутри самой функции.
```rust
fn square(mut n:i32){
  n = n * n;
  println!("The value of n inside function : {}", n); // 16
}

fn main() {
  let n = 4;
  println!("Значение до вызова функции : {}", n); // 4
  println!("Вызываем функцию");
  square(n);
  println!("\nЗначение после вызова функции : {}", n); // 4
}
```

### `Передача аргументов по ссылке`
Если мы хотим, чтобы после изменения аргумента в функции, она изменилась и вне функции, то мы должны передать аргумент не по значению, а по ссылке.
```rust
fn square(&mut n:i32){
  *n = *n * *n;
  println!("The value of n inside function : {}", n); // 16
}

fn main() {
  let mut n = 4;
  println!("Значение до вызова функции : {}", n); // 4
  println!("Вызываем функцию");
  square(&mut n);
  println!("\nЗначение после вызова функции : {}", n); // 16
}
```

### `Возвращаем значение из функции`
Функции могут возвращать некоторое значение, используя ключевое слово `return`.
Также в определении функции должно быть определно какой тип вернется из функции.
```rust
fn square(n:i32)->i32{ // мы указали, что функция должна вернуть число
  println!("Значение n: {}", n);
  let m = n * n;
   m // Ключевое слово return писать необязательно, как и ставить ; в последний строчке функции
}  
fn main() {
  let n = 4;
  println!("Значение n: {}", n);
  println!("Вызов функции");
  println!("\nРезультат : {}",square(n));
}
```

### `Возвращаем несколько значений из функции`
Функция может вернуть несколько значений похожим образом. Результатом будет кортеж.
```rust
fn main() {
    let length = 4;
    let width = 3;
    println!("Длина прямоугольника:{}", length);
    println!("Ширина прямоугольника:{}", width);
    let (area, perimeter) = calculate_area_perimeter(length, width);
    println!("Площадь: {}, Периметр: {}", area, perimeter);
}

fn calculate_area_perimeter(x: i32, y: i32) -> (i32, i32) { // указывает типы с помощью кортежа
    let area = x * y;
    let perimeter = 2 * (x + y);
    (area, perimeter) // возвращаем значение также с помощью кортежа
}
```

### `Принимаем множество в качестве аргумента`
Чтобы передать множества в функцию или вернуть множества из функции, действия почти не отличаются.
```rust
fn main() {
   let arr = [1, 2, 3, 4, 5];
   modify_my_array(arr);
   println!("Изначальный массив : {:?}", arr);
   println!("Массив после вызова функции : {:?}", modify_my_array(arr));
}
fn modify_my_array(mut arr:[i32;5])->[i32;5]{
   arr[2] = 8;
   arr[3] = 9;
   arr
}

// можно также и с помощью ссылочного аргумента
fn modify_my_array_ref(mut arr:&mut[i32;5]) {
   arr[2] = 8;
   arr[3] = 9;
}
```