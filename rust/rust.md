
# Rust

## 자료

[utilForever님 OnBoarding Plan](https://github.com/utilForever/onboarding-for-beginners#materials)<br>
[The Book](https://doc.rust-lang.org/book/)<br>
[Easy Rust in Korean](https://youtube.com/playlist?list=PLfllocyHVgsSJf1zO6k6o3SX2mbZjAqYE)

## 1. 설치 및 셋팅

### 1.1. 설치

wsl 사용자
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```


설치시 PATH 설정 `source $HOME/.cargo/env`


실행해서 설정되었는지 확인 `rustc --version`
[참고](https://www.rust-lang.org/tools/install)


### 1.2. Hello World!

1. Rust 소스코드 파일 확장자는 `.rs`

1. Rust 컴파일러 명령어는 `rustc`

1. println!은 함수가 아닌 Rust 매크로. `!`가 매크로라는 뜻이라고 함

```rust
fn main() {
    println!("Hello, world!");
}
```

```
$ rustc main.rs
$ ./main
Hello, world!
```

### 1.3. Cargo

Cargo is Rust’s build system and package manager.
CMake와 이것저것 합쳐진 것 같다.


> Rust 유저들을 `Rustaceans`라고 부른다.


설치확인
```
cargo --version
```

프로젝트 만들기
```sh
cargo new hello_cargo
cd hello_cargo
```

> 기본은 .gitignore 파일과 함께 생성됨<br>
> 기존 git repo안에서 `cargo new`실행 시 git 파일은 생성되지 않음<br>
> `cargo new --vcs=git`을 사용하면 위의 내용 무시하고 git 파일 생성 가능


[TOML](https://toml.io/en/) 파일이 생성됨.
프로젝트의 정보, 프로젝트 의존성(crates) 담고있음


Cargo.toml
```toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

[dependencies]
```
Rust에서 코드 패키지를 `crate`라고 부름.

Cargo는 프로젝트의 `src` 폴더 안에서 소스파일을 찾을 것임.
프로젝트 최상위 폴더에는 README파일, 라이선스, configuration 파일 등만 포함

#### 빌드
빌드
```sh
$ cargo build
   Compiling hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

실행 파일의 위치
```sh
$ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
Hello, world!
```

실행
```sh
$ cargo run
    Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
     Running `target/debug/hello_cargo`
Hello, world!
```

check: 컴파일되는지 확인하지만 실행파일 생성하지 않음
```sh
$ cargo check
   Checking hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

#### Cargo 명령어 정리

1. `cargo new` 새로운 프로젝트 생성
1. `cargo build` 컴파일
1. `cargo run` 실행
1. `cargo check` 빠른 컴파일 여부 체크

## 2. Guessing Game 프로그래밍 해보기

`let`, `match`, methods, associated functions, external crates 쓰는 법 등을 배움

src/main.rs
```rust
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}
```

> 주석은 `//` 이용 가능. `/* */`, `///` 등 이용가능

`std::io`: `io` library from the standard library, known as `std`

`let`: 새로운 variable 생성

`mut`: Mutability를 위함. 변수를 mutable(변화 가능) 하게 만들기 위해 필요함. 기본은 immutable(불변값)

`String::new()` String 타입의 `new`라는 associated function 사용하여 인스턴스 생성.


## 3. Common Programming Concepts


### 3.1. 변수와 가변성
`let x`: 새로운 immutable 변수 x 생성<br>
`let mut y': 새로운 mutable 변수 y생성<br>
`const Z`: 새로운 상수 Z 생성<br>

#### Shadowing: immutable 변수를 `let` 키워드를 이용해서 같은 변수 이름으로 다시 다른 데이터 넣어줌. 

차이점
1. 기존 데이터는 사라짐.
1. 다른 데이터 타입의 데이터 할당 가능


> mutable 변수에 `let` 키워드로 shadowing 시도하면 컴파일 에러.


### 3.2. 데이터 타입

`let guess: u32 = 42` 처럼 `u32` 부분에 타입을 지정 가능


1. 스칼라 타입: 정수, 부동소수점, 불리안, 문자
1. 컴파운드 타입: 튜플, 배열

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);  // tuple 선언 및 초기화

    let five_hundred = x.0; // tuple의 원소에 접근

    let a: [i32; 5] = [1, 2, 3, 4, 5];  // array 선언 및 초기화

    let first = a[0];   // array 원소에 접근
}
```

### 3.3. 함수

Rust 코드의 함수와 변수명은 `snake case`를 컨벤션으로 사용.<br>
알파벳 소문자와 언더바(_)만을 사용


#### 3.3.1. 매개변수
```rust
fn main() {
    print_labeled_measurement(5, 'h');
}

fn print_labeled_measurement(value: i32, unit_label: char) {    // 매개변수 타입 선언
    println!("The measurement is: {} {}", value, unit_label);
}
```

#### 3.3.2. 문장과 표현 (Statements and Expressions)
함수의 Body 부분은 statements로 이루어져 있는데, 각 statement는 expression으로 끝날 수도 있다. <br>
1. Statements are instructions that perform some action and **do not return** a value. 
1. Expressions evaluate to a resulting value.

예시.
```rust
fn main() {
    let y = 6;              // good
    let x = (let y = 6);    // error
}
```
`let y = 6;`은 statement다. 함수 정의도 statement다. 따라서 return value가 없다. <br>
그래서 두 번째 문장에서 에러가 난다. `let y = 6`은 value가 아니기 때문. C언어에서는 `x = y = 6;`과 같은 대입이 가능했지만 Rust에서는 불가능하다.

Expression은 어떤 value로 평가된다(만들어진다). `5 + 6`이 `11`의 값으로 평가되듯이 어떤 값을 나타낸다. <br>
Expression은 statement를 구성하는 한 부분이 될 수 있다. `let y = 6`에서 `6`은 expression이다. 함수를 호출하는 것, 매크로를 호출하는 것, `{ }`를 통해 생긴 새로운 scope block도 expression이다.

예시.
```rust
fn main() {
    let y = {
        let x = 3;
        x + 1
    };

    println!("The value of y is: {}", y);
}
```
새로운 블록:
```
{
    let x = 3;
    x + 1
}
```
이 블록은 하나의 expression이고, `4`의 value를 나타낸다. <br>
`x + 1`의 끝에 `;`이 안붙어있는데, expression은 세미콜론으로 끝나지 않는다. 세미콜론을 붙이면 statement가 된다. 그렇기 때문에 세미콜론을 붙이면 값을 반환하지 않으니 구분하자.


### 3.4. 주석


### 3.5. 제어문



## 4. 소유권 이해하기

Rust의 가장 특별한 점.
Rust가 가비지 콜렉터(Garbage Collector)없이 메모리 안정성을 보장하는 방법.


기존 언어들: 직접 관리 vs. 가비지 콜렉션
| 분류 | 가비지 콜렉션 | 가비지 콜렉션 |
| :---: | :---: | :---: |
|  | 런타임에 계속해서 돌아가는 GC | 프로그래머가 직접 할당, 해제 |


러스트는 컴파일 타임에 소유권을 체크하여 메모리 할당을 자동으로 해제해줌!


### 소유권 규칙
1. 러스트의 각각 값은 해당 값의 오너(Owner)라 불리는 변수 가짐
1. 한번에 딱 하나의 오너만 존재.
1. 오너가 스코프(scope) 밖으로 벗어날 때, 값은 버려짐(dropped)


