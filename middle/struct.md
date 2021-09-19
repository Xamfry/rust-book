# Структуры

### `Что такое структура`
Структуры помогают создавать пользовательские типы данных. Структуры состоят из связанных элементов, которые могут иметь разные типы.

### `Создание структуры`
Чтобы создать структуру объявляется ключевое слово `struct`, за которым следует имя структуры, а затем тело.
Тело состоит из элементов, которые определяется как элемент_структуры:тип_элемента.

Структуры должны именоваться в `PascalCase`, что означает что первая буква каждого слова должна быть с большой буквы.
```rust
struct Course {
  code: i32,
  name: String,
  level: String,
}
```

### `Иницилизация структуры`
Объявление структуры определяет только схему для настраиваемого типа данных, но объект в памяти не создается.
Это делается при создании экземпляра переменной данного типа. При иницилизации мы указывает не тип данных, а само значение.
```rust
let my_course = Course { // Иницилизация и запись в память происходит лишь на этом этапе
  code: 130,
  name: String::from("Rust"),
  level: String::from("middle"),
};
```

### `Элементы структуры`
Чтобы получить элемент структуры мы должны обратиться к структуре и через точку указать нужный нам элемент.
```rust
println!("{}", my_course.code);
```

Однако, если мы хотим изменить какой-либо элемент, мы должны явно указать, что структура изменяема.
```rust
let mut mut_course = Course {
  code: 130,
  name: String::from("Rust"),
  level: String::from("middle"),
};

mut_course.code = 566;
```

### `Функции и структуры`
Функция работает со структурами точно также, как и с любым другим типом данных.
```rust

fn main() {
   //initialize
  let course1 = Course  {
    name:String::from("Rust"),
    level:String::from("beginner"),
    code:130
  };
 
  let course2 = Course  {
    name:String::from("Java"),
    level:String::from("beginner"),
    code:130
  };

  let choose_course = return_course_info(course1, course2);
}

fn return_course_info(c1: Course, c2: Course) -> Course {
  if c1.name == "Rust" {
    return c1;
  } else {
    return c2;
  }
}
```

### `Методы структур`
Что такое метод? `Метод` - это пользовательская функция, но которые специально объявляются в контексте структуры.

В метод надо передавать аргумент `&self`, который будет ссылаться на структуру. А реализация методов происходит внутри `impl` структуры.
```rust
struct Course {
  code: i32,
  name: String,
  level: String,
}

impl Course {
  fn name_code(&self) -> String {
    return format!("{} {}", self.name, self.code);
  }
}

fn main() {
  let course1 = Course {
    name:String::from("Java"),
    level:String::from("beginner"),
    code:130
  };
  println!("{}", course1.name_code()); // метод вызывается как элемент структуры
}
```

### `Статические методы структур`
`Статические` методы - это методы, которые можно вызвать без создания экземпляра структуры. Им не нужно передавать `&self`, статический и не статический метод могут иметь одно и то же название. Вызывается через `::`.
```rust
struct Course {
  code: i32,
  name: String,
  level: String,
}

impl Course {

  fn my_static_method(n: String, l: String, c: i32) -> Course {
    return Course {
      name: n,
      level: l,
      code: c,
    };
  }

  fn display(&self) {
    println!("name: {}, code: {} of type: {}", self.name, self.code, self.level);
  }
}

fn main() {
  let c1 = Course::my_static_method("Rust".to_string(), "Beginner".to_string(), 132);
  c1.display();
}
```

### `Кортежные структуры`
`Кортежная структура` - это тип данных, который является гибридом структуры и кортежа. У элементов кортежной структуры нет имен, есть только типы данных.

Обращаться к элементам кортежной структуры можно по индексам.
```rust
struct FruitQuantity(String, i32);

fn main() {
  let r1 = FruitQuantity("апельсинов".to_string(), 12);
  println!("У меня есть {} {}", r1.1, r1.0);
}
```