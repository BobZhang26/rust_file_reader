# Rust project: file reader and debugging 
```
use std::fs::File;
use std::io::{BufRead, BufReader};
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();
    print!("My file path is: {:?}", args[0]);

    let file: Result<File, std::io::Error> = File::open("non_existent_file.txt");
    let file: File = match file {
        Ok(file) => file,
        Err(error) => {
            match error.kind() {
                std::io::ErrorKind::NotFound => {
                    panic!("File not found: {}", error)
                }
                _ => {
                    panic!("Error opening file: {}", error)
                }
            }
        }
    };
    
    let reader: BufReader<File> = BufReader::new(file);
    for line in reader.lines() {
        match line {
            Ok(line) => println!("{}", line),
            Err(error) => {
                panic!("Error reading line: {}", error)
            }
        }
    }
}

```
## Concepts Covered:
- Introduction to Rust: Students will be introduced to the provided source code and its basic structure, serving as a starting point for the lab.
- Variable assignment and immutability: Students will explore how variables are assigned and how immutability is enforced in Rust.
- Basics of control flow: Students will understand how control flow structures like match expressions and loops are used to handle errors and process file contents.
- Function Basics: Students will examine the main function and its purpose, as well as how to structure and organize code in Rust programs.
- Error handling: Students will learn how to handle different error cases when opening and reading files, using the match expression to provide helpful error messages.
- File processing: Students will modify the code to read the specified file line by line and print its contents to the console.

By completing this lab, you will gain practical experience in Rust by extending an existing file reader application. You will develop skills in file I/O, error handling, and some basic code organization, utilizing the concepts introduced in the lessons for this week.
