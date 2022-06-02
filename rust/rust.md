
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
