# 열거형 (enum)

---

# 열거형

- enum 키워드를 통해 몇 가지 태그된 원소의 값을 갖는 새로운 자료형을 생성할 수 있다.
- match 와 함께 사용하면 품질 좋은 코드를 만들 수 있다.

```rust
#![allow(dead_code)]

enum Species {
    Crab,
    Octopus,
    Fish,
    Clam,
}

struct SeaCreature {
    species: Species,
}
    name: String

fn main() {
    let ferris = SeaCreature {
        species: Species::Crab,
        name: String:: from("Ferris"),
    };

    match ferris.species {
        Species::Crab => println!("{} is Crab", ferris.name),
        Species::Octopus => println!("{} is Octopus", ferris.name),
        Species::Fish => println!("{} is Fish", ferris.name),
        Species::Clam => println!("{} is Clam", ferris.name),
    }
}
```

# 열거형 정의하기

- IP 주소를 예시로 V4,V6 식으로 정의 가능

```rust
enum IpAddrKind {
    V4,
    V6,
}
```

# 열거형 값

- 다음과 같이 인스턴스 생성 가능

```rust
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```

```rust
enum IpAddrKind {
    V4,
    V6,
}

struct IpAddr {
    kind: IpAddrKind,
    address: String,
}

let home = IpAddr {
    kind: IpAddrKind::V4,
    address: String::from("127.0.0.1"),
};

let loopback = IpAddr {
    kind: IpAddrKind::V6,
    address: String::from("::1"),
};
```

- 각 variant 에도 값을 부여할 수 있다.

```rust
enum IpAddr {
    V4(String),
    V6(String),
}

let home = IpAddr::V4(String::from("127.0.0.1"));

let loopback = IpAddr::V6(String::from("::1"));
```

# Option 열거형

- 표준 라이브러리 에서 정의된 타입
- null 값을 대체할 수 있음 (Option::None)

```rust
enum Option<T> {
    Some(T),
    None,
}
```

```rust
let some_number = Some(5);
let some_string = Some("a string");

let absent_number: Option<i32> = None;
```

- Option 끼리의 연산은 불가능

```rust
let x: i8 = 5;
let y: Option<i8> = Some(5);
let sum = x + y;  // 컴파일 에러
```

# Match

- switch case와 비슷하다

```rust
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u32 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```

# 값을 바인딩 하는 패턴

- 매치된 값들과 패턴을 바인딩 할 수 있다.
- Enum variant 롭부터 값을 추출 할 수 있는 방법이다

```rust
#[derive(Debug)] // So we can inspect the state in a minute
enum UsState {
    Alabama,
    Alaska,
    // ... etc
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}
```

```rust
fn value_in_cents(coin: Coin) -> u32 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        },
    }
}
```

# Option<T>를 이용하는 매칭

- 함수 인자로 Option를 받음

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```

# Match 의 정밀함

- 아래 코드는 None 케이스를 다루지 않아 버그를 일으킴

```rust
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        Some(i) => Some(i + 1),
    }
}
```

- 하지만 다음과 같이 에러를 잡아냄

```rust
error[E0004]: non-exhaustive patterns: `None` not covered
 -->
  |
6 |         match x {
  |               ^ pattern `None` not covered
```

# _ 변경자 (placeholder)

- match 문에서 예외처리가 가능함
- 아래 코드는 1,3,5,7 빼고 예외처리가 됨

```rust
let some_u8_value = 0u8;
match some_u8_value {
    1 => println!("one"),
    3 => println!("three"),
    5 => println!("five"),
    7 => println!("seven"),
    _ => (),
}
```

# if let 흐름 제어

- match 문법

```rust
let some_u8_value = Some(0u8);
match some_u8_value {
    Some(3) => println!("three"),
    _ => (),
}
```

- if let 문법

```rust
if let Some(3) = some_u8_value {
    println!("three");
}
```

- match 문법

```rust
let mut count = 0;
match coin {
    Coin::Quarter(state) => println!("State quarter from {:?}!", state),
    _ => count += 1,
}
```

- if let 문법

```rust
let mut count = 0;
if let Coin::Quarter(state) = coin {
    println!("State quarter from {:?}!", state);
} else {
    count += 1;
}
```
