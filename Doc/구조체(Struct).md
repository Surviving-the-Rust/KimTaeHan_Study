# 구조체 (Struct)

---

## 구조체

- 필드(Field)들의 Collection
- 메모리 상에 필드들을 어떻게 배치할 지에 대한 컴파일러의 청사진
- key : value 형태임

```rust
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```

## 메모리에 데이터 생성하기

- 코드에서 구조체를 인스턴스화 (Instantiate) 하면
프로그램은 연관된 필드 데이터들을 메모리 상에 나란히 생성한다.

```rust
#![allow(dead_code)]

#[derive(Debug)]
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}

fn main() {
		let user1 = User {
		    email: String::from("someone@example.com"),
		    username: String::from("someusername123"),
		    active: true,
		    sign_in_count: 1,
		};

    println!("{:?}", user1 );
}
```

# 필드 초기화 축약법

- 변수명과 구조체의 필드명이 같다면 다음과 같이 사용 가능

```rust
fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}
```

# 튜플 구조체

- 타입 정의만 가능하며 명명은 할 수 없는 구조체
- 아래 코드는 서로 다른 타입임

```rust
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

let black = Color(0, 0, 0);
let origin = Point(0, 0, 0);
```

# 메소드 정의

- Rectangle 위에 arda 메소드 정의
- impl 문법을 사용
- 첫번째 파라미터는 self 이다.

```rust
#[derive(Debug)]
struct Rectangle {
    length: u32,
    width: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.length * self.width
    }
}

fn main() {
    let rect1 = Rectangle { length: 50, width: 30 };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

# 연관 함수

- impl 내부에 있는 함수들을 칭함
- 첫번째 파라미터는 self 가 아니어도됨.

```rust
impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { length: size, width: size }
    }
}
```
