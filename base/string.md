# Строки

### `Что такое строка`
Строки - это последовательность символов `Unicode`. В Rust строка не заканчивается `пустым` элементом, они могут содержать `пустые` элементы. Обратите внимание на символы [Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters).

### `Типы строк`
Строки бывают двух типов: 
  - `&str`
  - `String`

&str используется, если значение не должно менятся
String используется, если надо манипулировать строкой. 

### `Строковой литерал &str`
Строковой литерал имеет следующие свойства:
  - Примитивный тип
  - Неизменный
  - Строка фиксированной длины, где-то в памяти
  - Значение строки известно во время компиляции

Строковой литерал также известен как `строковой срез`.
```rust
let lang: &str = "Rust";
println!("Строковой литерал: {}", lang);
println!("Длина строкового литерала: {}", lang.len()); // у строки можно узнать длину
```

### `Строковой объект String`
Объект String имеет следующие свойства:
  - Строка кодируется как `UTF-8`
  - Структура данных, которая размещена в `куче`
  - Размер этой строки можно изменить
  - Не заканчивается на `пустой` элемент
  - Значение строки кодируется во время выполнения

```rust
let lang = String::new(); // создает пустой объект String
let s_lang = lang.to_string(); // конвертирует из объекта в тип строки

let ready_lang = String::from("Rust"); // можно создать объект из готовой строки
println!("Длина строкового объекта: {}", ready_lang.len()); // можно узнать длину
```

### `Основные методы String`
Здесь я обсуждая лишь некоторые методы String, остальные же можно найти по ссылке [String в Rust](https://doc.rust-lang.org/std/string/struct.String.html).

`capacity` - дает число байтов, выделенных на строку.
```rust
let lang = String::from("Rust");
println!("Емкость в байтах: {}", lang.capacity());
```

`contains` - позволяет узнать содержит ли строка другую строку.
```rust
let title = String::from("Программирование на Rust");
let lang = String::from("Rust");
println!("Является ли {} подстрокой {}: {}", lang, title, title.contains(&lang.to_string()));
```

`replace` - заменят все вхождения одной подстроки на другую.
```rust
let title = String::from("Программирование на Rust");
let lang = "Rust";
let next_lang = "C++";
let result = title.replace(lang, next_lang);
println!("{} теперь {}", title, result);
```

`trim` - удаляет пробелы в начале и конце строки.
```rust
let title = String::from("      Программирование на Rust      ").to_string();
let trim_string = title.trim();
println!("Необрезанная строка: {}\nОбрезанная строка: {}", title, trim_string);
```

### `Итерация строки`
У Rust есть три различных способа итерации строки:
  - split_whitespace
  - split
  - chars

`split_whitespace` -  делит строку на подстроки при появлении пробела.
```rust
let string = String::from("Программирование на Rust");
for token in string.split_whitespace() {
  println!("{}", token);
}
```

`split` - делит строку на подстроки при появлении указанного символа.
```rust
let string = String::from("Rust,C++,Java,Haskell");
for token in string.split(",") {
  println!("{}", token);
}
```

`chars` - делит строку на символы.
```rust
let string = String::from("Программирование на Rust");
for symbol in string.chars() {
  println!("{}", symbol);
}
```

### `Обновление строки`
Существующую строку можно обновить добавив к ней другой символ или строку.

Чтобы добавить к строке символ нужно использовать `push`.
```rust
let mut lang = String::from("Rus");
lang.push('t');
println!("Язык: {}", lang);
```

Строка добавляется аналогичным методом с помощью `push_str`.
```rust
let mut course = String::from("Программирование на");
course.push_str(" Rust");
println!("{}", course);
```

Строки можно объединить с помощью символа `+`. Правый операнд в таком случае должен быть заимствован.
```rust
let course = String::from("Rust").to_string();
let course_type = String::from(" для начинающих").to_string();
let res = course + &course_type;
println!("{}", res);
```

А если надо объединить несколько строк во время вывода можно использовать макрос `format!`.
```rust
let course = String::from("Rust").to_string();
let course_type = String::from(" для начинающих").to_string();
let res = format!("{} {}", course, course_type);
let res2 = format!("{1} {0}", course, course_type);
println!("{}", res);
println!("{}", res2);
```

### `Нарезка строки на подстроки`
Нарезка строки используется для того, чтобы из строки вытащить подстроку.
Для того, чтобы выбрать нужный нам отрезок мы выбираем начальный и конечный индекс.
```rust
let string = String::from("Программирование на Rust");
let slice = &string[5..12]; // 5 6 7 8 9 10 11
println!("{}", slice);
```

### `Функции и строки`
В функцию можно передать и `&str` и `String`, но String нельзя будет использовать сново после вызова функции, так как переданное значение перемещается в область действия данной функции. Более подробно в главе `Право на собственность`.

Передаем в функцию &str.
```rust
fn main() {
  let string: &str = "Программирование на Rust";
  display_string(string);
  println!("Строка: {}", string); // мы можем вызвать &str вновь
}

fn display_string(string: &str) {
  println!("Строки в функции: {}", string);
}
```

Передаем в фунцию String. 
```rust
fn main() {
  let string: String = String::from("Программирование на Rust");
  display_string(string);
  // мы не можем вновь вызывать String
}

fn display_string(string: String) {
  println!("Строки в функции: {}", string);
}
```