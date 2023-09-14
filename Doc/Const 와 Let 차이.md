# const 와 let 차이

---

# const 와 let 차이

- const 의 값은 컴파일 타임에 결정됨
- let 의 값은 런타임 에 결정됨
- const 는 타입 명시가 필요
- const 는 global 선언 가능

```rust
let a = 1;
let a = a*a; // OK

const b: u32 = 3;
const b: u32 = b*b; //ERROR
```

```rust
let version = "0.1.1";	// ERROR
const VERSION: &'static str = "0.1.1";	// OK

fn main() {
	
}
```
