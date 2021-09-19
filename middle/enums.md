# Перечисления

### `Что такое перечисление`
Перечимление - это настраиваемый тип данных, которые состоит из вариантов. Его цель перечислеть все возможные значения и выбрать одно из этого списка.

### `Объявление перечисления`
Перечимление объявляется через ключевое значение `enum`. А затем в теле перечисляются значения.
```rust
enum KnightMoves {
  Horizontal,
  Vertical,
}
```

### `Иницилизация перечисления`
Перечисление иницилизируется с использованием имени и указании выбора через `::`.
```rust
// Чтобы enum можно было вывести с помощью {:?}
#[derive(Debug)]
enum KnightMoves {
  Horizontal,
  Vertical,
}

fn main() {
  let horizontal_move = KnightMove::Horizontal;
  let vertical_move = KnightMove::Vertical;
  println!("Движение 1: {:?}", horizontal_move);
  println!("Движение 2: {:?}", vertical_move);
}
```

### `Перечисление с типом данных`
Можно использовать разные типы данных для элементов перечисления.
```rust
#[derive(Debug)]
enum KnightMoves {
  Horizontal (String),
  Vertical (String),
}

fn main() {
  let horizontal_move = KnightMove::Horizontal(String::from("Влево"));
  let vertical_move = KnightMove::Vertical(String::from("Вниз"));
  println!("Движение 1: {:?}", horizontal_move);
  println!("Движение 2: {:?}", vertical_move);
}
```

### `Методы перечислений`
Методы у перечислений работают также как и у структур.
```rust
#[derive(Debug)]
enum TrafficSignal {
  Red,
  Green,
  Yellow,
}

impl TrafficSignal {
  fn is_stop(&self) -> bool {
    match self {
      TrafficSignal::Red => return true;
      _ => return false;
    }
  }
}

fn main() {
  let action = TrafficSignal::Red;
  println!("Какое значение сигнала: {:?}", action);
  println!("Должны ли мы остановиться", action.is_stop());
}
```

### `Перечисления и структуры`
Перечисления можно использовать как элементы структуры.
```rust
enum KnightMove {
  Horizontal,
  Vertical,
}

struct Player {
  color: String,
  knight: KnightMove,
}
```
### `Вариант и перечисление`
Вариант или `Option` - это встроенное перечисление в стандартной библиотеки Rust. Имеется два вариант `Some` и `None`. Используется в том случае, если ожидается, что значения может не существовать.
```rust
// Возвращает либо что-то, либо None
fn learn_lang(lang: &str) -> Option<bool> {
  if lang == "Rust" {
    return Some(true);
  } else {
    return None;
  }
}
```

### `Результат и перечисление`
Результат или `Result` - это встроенное перечисление в стандартной библиотеке Rust. Имеется два варианта `Ok` и `Err`. Ok выполняется если все в порядке, а Err если была найдена ошибка во время выполнения.
```rust
fn file_found(i: bool) -> Result<i32, bool> {
  if i {
    return Ok(200);
  } else {
    return Err(false);
  }
}
```