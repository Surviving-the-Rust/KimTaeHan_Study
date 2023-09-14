# Generic 자료형

---

# Generic 자료형

- struct 나 enum을 부분적으로 정의해, 컴파일러가 컴파일 타임에 코드 사용을 기반으로
완전히 정의된 버전을 만들 수 있게 해준다.

```rust
#![allow(dead_code)]

struct BagOfHolding<T> {
    item : T,
}

fn main() {
    let i32_bag = BagOfHolding::<i32> { item : 42 };
    let bool_bag = BagOfHolding::<bool> { item : true };
    let float_bag = BagOfHolding { item : 3.14 };
    let bag_in_bag = BagOfHolding {
        item: BagOfHolding { item: "boom!" },
    };

    println!("{} {} {} {}",i32_bag.item, bool_bag.item, float_bag.item, bag_in_bag.item.item);
}
```

# Option

- null 을 쓰지 않고도 Nullable 한 값을 표현할 수 있는 내장된 Generic 열거체

```rust
enum Option<T> {
		None,
		Some(T),
}
```

```rust
#![allow(dead_code)]

struct BagOfHolding<T> {
    item : Option<T>,
}

fn main() {
    let i32_bag = BagOfHolding::<i32> { item : None };

    if i32_bag.item.is_none() {
        println!("Nothing!")
    }
    else {
        println!("Found Something!")
    }

    let i32_bag = BagOfHolding::<i32> { item: Some(42)};

    if i32_bag.item.is_some() {
        println!("Found Something!")
    }
    else {
        println!("Nothing!")
    }

    match i32_bag.item {
        Some(v) => println!("Found {}!", v),
        None => println!("Nothing"),
    }
}
```

# Result

- 실패할 가능성이 있는 값을 리턴할 수 있도록 해주는 내장된 Generic 열거체

```rust
enum Result<T, E> {
		Ok(T),
		Err(E),
}
```

```rust
#![allow(dead_code)]

fn do_something_that_might_fall(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    }
    else {
        Err(String::from("Not Match!"))
    }
}

fn main() {
    let result = do_something_that_might_fall(12);
    
    match result {
        Ok(v) => println!("Found {}", v),
        Err(e) => println!("Error: {}", e),
    }
}
```

## Result?

- Result 와 함께 쓸 수 있는 연산자

```rust
do_something_that_might_fail()?

match do_something_that_might_fail() {
		Ok(v) => v,
		Err(e) => return Err(e),
}
```

```rust
#![allow(dead_code)]

fn do_something_that_might_fall(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    }
    else {
        Err(String::from("Not Match!"))
    }
}

fn main() -> Result<(), String> {
    let v = do_something_that_might_fall(42)?;
    println!("Found {}", v);
    Ok(())
}
```

# 추한 옵션/결과 처리

- unwrap 이라는 함수를 사용해 빠르고 더러운 방식으로 값을 가져올 수 있다.
    - Option/Result 내부의 값을 꺼내오고
    - enum이 None/Err인 경우에는 panic!

```rust
#![allow(dead_code)]

fn do_something_that_might_fall(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    }
    else {
        Err(String::from("Not Match!"))
    }
}

fn main() -> Result<(), String> {
    let v = do_something_that_might_fall(42).unwrap();
    println!("Found {}", v);

    let v = do_something_that_might_fall(1).unwrap();
    println!("Found {}", v);

    Ok(())
}
```
