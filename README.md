### rust demo

### hello_rust
执行下面的语句，可以看到rust编译输出的"Hello，rust!"

1. `cargo new hello_rust` 
- 新建一个hello_rust项目
2. `cd hello_rust`
- 进入项目文件
3. `cargo build` 
- 编译生成项目
- `cargo build`之前要安装MSVC生成工具
  - [链接:https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/](https://visualstudio.microsoft.com/zh-hans/visual-cpp-build-tools/)
  - 需要安装的内容：![MSVC](./MSVC.PNG)
  - 参考内容：[链接：https://blog.csdn.net/coolsoloist/article/details/106425656](https://blog.csdn.net/coolsoloist/article/details/106425656)
4. `./target/debug/hello_rust.exe`
- 运行编译后的可执行文件
> 注：可以使用`cargo run`直接编译运行项目(等同第3、4步)
5. `cargo build --release`
- 发布最终项目

### guessing_name
猜测1-100的随机数字是多少

1. `cargo new guessing_name`
- 新建一个guessing_name项目
2. `cd guessing_name`
- 进入项目文件
3. 在项目的`Cargo.toml`文件中的`[dependencies]`一栏下添加`rand = "0.7.0"`
- 添加随机数的库名
4. 编辑`.src/main.rs`文件如下
```
use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    println!("Guess the number!");
    
    let secret_number = rand::thread_rng().gen_range(1,101);
        
    loop {
 
      println!("Please input your guess.");
 
      let mut guess = String::new();
      
      io::stdin()
          .read_line(&mut guess)
          .expect("Failed to read line");
      
      let guess: u32 = match guess.trim().parse() {
          Ok(num) => num,
          Err(_) => continue,
      };
      
      println!("You guessed: {}",guess);
      
      match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => {
          println!("You win!");
          break;
        }
      }
    
    }
}
```
5. `cargo run`编译运行项目
