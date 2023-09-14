# 벡터 (Vec)

---

# 벡터

- Vec 구조체로 표현하는 가변 크기의 리스트
- vec! 매크로를 통해 손쉽게 생성할 수 있다.
- iter() 메소드를 통해 반복자를 생성할 수 있다.

```rust
#![allow(dead_code)]

fn main() {
    let mut float_vec = Vec::new();
    float_vec.push(1.3);
    float_vec.push(2.3);
    float_vec.push(3.4);

    let string_vec = vec![String::from("Hello"), String::from("World")];

    for word in string_vec.iter() {
        println!("{}", word);
    }
}
```
