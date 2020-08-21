# Tracery

This is a direct update/refresh of the original crate published by Paul Woolcock. Other than removing the nom parser and replacing it with a pest parser, there are no major changes made to this version of the crate. Additional changes/roadmap to come.

## A Text-Expansion Library for Rust

Tracery was originally a javascript library written by [galaxykate](https://github.com/galaxykate), and is available at <https://github.com/galaxykate/tracery>.
It accepts a set of rules, and produces a single string according to specific syntax in the rule set.

If a string in the rule set contains a word surrounded by `#` symbols, it will be used to select a piece of text from the rule named by the word between the `#` symbols.

Here are some examples:

```rust
let source = r#"{
    "origin": [ "The #adjective# #color# #animal# jumps over the #adjective# #animal#" ],
    "adjective": [ "quick", "lazy", "slow", "tired", "drunk", "awake", "frantic" ],
    "color": [ "blue", "red", "yellow", "green", "purple", "orange", "pink", "brown", "black", "white" ],
    "animal": [ "dog", "fox", "cow", "horse", "chicken", "pig", "bird", "fish" ]
}"#;

for _ in 0..3 {
    println!("{}", tracery::flatten(source));
}

// The quick brown fox jumps over the lazy dog
// The slow red chicken jumps over the orange bird
// The drunk purple bird jumps over the green horse
```

(You can run this exact example by running `cargo run --example readme`. If you want to try out some of your own, try piping a JSON grammar to it like this: `echo '<json here>' | cargo run --example main -- -`)