# merkle-generator

Rust version of [mafintosh/merkle-tree-stream](https://github.com/mafintosh/merkle-tree-stream). Generate a merkle tree based on incoming data.

![Cargo Version](https://img.shields.io/crates/v/merkle-generator.svg)

```
merkle-generator = "0.1.2"
```

## Usage

```rust
extern crate merkle_generator;

// define how to hash incoming data
fn parent(a: &Node, b: &Node) -> Vec<u8> {
    let ref mut hash = a.hash.clone();
    hash.extend(b.hash.iter().cloned());

    digest::digest(&digest::SHA256, data.as_slice())
        .as_ref()
        .to_vec()
}

// define how to hash two merkle tree node hashes into a new parent hash
fn leaf(leaf: &Node, roots: &Vec<Node>) -> Vec<u8> {
    let data = leaf.data.clone().unwrap();
    digest::digest(&digest::SHA256, data.as_slice()).as_ref().to_vec()
}

let mut gen = Generator::new(leaf, parent);

let nodes = gen.next(b"Hello World".to_vec());
println!("{:?}", nodes);
```

## Tree Structure

See [mafintosh/flat-tree-rs](https://github.com/mafintosh/flat-tree-rs) for more information about how node/parent indexes are calculated.

## License

The MIT License
