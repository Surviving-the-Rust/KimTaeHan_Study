# Struct Debug 오류 해결

---

- 출력은 {:?} 권장

```rust
println!("{:?}", ferris);
```

- struct 상단에 #[derive(Debug)] 재기

```rust
#[derive(Debug)]
struct SeaCreature {
    animal_type: String,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}
```

- #![allow(dead_code)] 를 통해 waring 제거

```rust
#![allow(dead_code)]
```
