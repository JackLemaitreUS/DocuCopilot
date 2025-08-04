// 🦀 Rust Cookbook: All-in-One Code Frame



// 📘 Variables and Mutability

let x = 5;

let mut y = 10;

y += 1;



// 🧮 Data Types

let a: i32 = 42;

let b: f64 = 3.14;

let c: bool = true;

let d: char = '🦀';



// 🧪 Functions

fn add(a: i32, b: i32) -> i32 {

&nbsp;   a + b

}



// 🔁 Control Flow

let number = 7;

if number < 10 {

&nbsp;   println!("Small number");

} else {

&nbsp;   println!("Big number");

}



for i in 0..5 {

&nbsp;   println!("i = {}", i);

}



// 📦 Ownership and Borrowing

fn takes\_ownership(s: String) {

&nbsp;   println!("{}", s);

}



fn makes\_copy(x: i32) {

&nbsp;   println!("{}", x);

}



fn main() {

&nbsp;   let s = String::from("hello");

&nbsp;   takes\_ownership(s);



&nbsp;   let x = 5;

&nbsp;   makes\_copy(x);

}



// 📚 References and Borrowing

fn calculate\_length(s: \&String) -> usize {

&nbsp;   s.len()

}



fn main() {

&nbsp;   let s1 = String::from("hello");

&nbsp;   let len = calculate\_length(\&s1);

&nbsp;   println!("Length is {}", len);

}



// 🧱 Structs and Enums

struct Point {

&nbsp;   x: i32,

&nbsp;   y: i32,

}



enum Direction {

&nbsp;   North,

&nbsp;   South,

&nbsp;   East,

&nbsp;   West,

}



// 🧠 Traits and Generics

trait Speak {

&nbsp;   fn speak(\&self);

}



struct Dog;



impl Speak for Dog {

&nbsp;   fn speak(\&self) {

&nbsp;       println!("Woof!");

&nbsp;   }

}



fn print<T: std::fmt::Debug>(item: T) {

&nbsp;   println!("{:?}", item);

}



// 🧰 Error Handling

fn divide(a: f64, b: f64) -> Result<f64, String> {

&nbsp;   if b == 0.0 {

&nbsp;       Err(String::from("Cannot divide by zero"))

&nbsp;   } else {

&nbsp;       Ok(a / b)

&nbsp;   }

}



// 📚 Modules

mod greetings {

&nbsp;   pub fn hello() {

&nbsp;       println!("Hello!");

&nbsp;   }

}



fn main() {

&nbsp;   greetings::hello();

}



// 📦 Crates and Cargo (Cargo.toml)

// \[dependencies]

// serde = "1.0"

// reqwest = "0.11"



// 🧵 Concurrency

use std::thread;



fn main() {

&nbsp;   let handle = thread::spawn(|| {

&nbsp;       println!("Hello from a thread!");

&nbsp;   });



&nbsp;   handle.join().unwrap();

}



// 🧪 Testing

\#\[cfg(test)]

mod tests {

&nbsp;   #\[test]

&nbsp;   fn it\_works() {

&nbsp;       assert\_eq!(2 + 2, 4);

&nbsp;   }

}



// 🧬 Lifetimes

fn longest<'a>(x: \&'a str, y: \&'a str) -> \&'a str {

&nbsp;   if x.len() > y.len() { x } else { y }

}



// 🧱 Macros

macro\_rules! say\_hello {

&nbsp;   () => {

&nbsp;       println!("Hello!");

&nbsp;   };

}



fn main() {

&nbsp;   say\_hello!();

}



// 📂 File I/O

use std::fs::File;

use std::io::{self, Read};



fn main() -> io::Result<()> {

&nbsp;   let mut file = File::open("hello.txt")?;

&nbsp;   let mut contents = String::new();

&nbsp;   file.read\_to\_string(\&mut contents)?;

&nbsp;   println!("{}", contents);

&nbsp;   Ok(())

}



// 🌐 HTTP Request (with reqwest)

use reqwest;



\#\[tokio::main]

async fn main() -> Result<(), reqwest::Error> {

&nbsp;   let body = reqwest::get("https://www.rust-lang.org")

&nbsp;       .await?

&nbsp;       .text()

&nbsp;       .await?;

&nbsp;   println!("{}", body);

&nbsp;   Ok(())

}



// ⏳ Async/Await

use tokio::time::{sleep, Duration};



\#\[tokio::main]

async fn main() {

&nbsp;   println!("Waiting...");

&nbsp;   sleep(Duration::from\_secs(2)).await;

&nbsp;   println!("Done!");

}



// 📚 Arrays

let arr = \[1, 2, 3, 4, 5];

println!("First element: {}", arr\[0]);

println!("Length: {}", arr.len());



for val in arr.iter() {

&nbsp;   println!("{}", val);

}



// 📌 Slices

let slice = \&arr\[1..3]; // \[2, 3]

println!("{:?}", slice);



// 📌 References

let x = 42;

let r = \&x;

println!("Reference points to: {}", r);



// 🧨 Raw Pointers (unsafe)

let a = \[1, 2, 3];

let ptr = a.as\_ptr(); // \*const i32

unsafe {

&nbsp;   println!("First element via raw pointer: {}", \*ptr);

}



// 🧠 Smart Pointers

use std::rc::Rc;



let a = Rc::new(5);

let b = Rc::clone(\&a);

println!("a = {}, b = {}", a, b);



