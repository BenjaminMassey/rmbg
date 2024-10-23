# RMBG Crate

This crate provides an easy-to-use interface for removing backgrounds from images, leveraging a machine learning model.
It's designed to integrate seamlessly into Rust projects requiring background removal capabilities.

Rust docs: https://docs.rs/rmbg/latest/rmbg/struct.Rmbg.html
Crates.io: https://crates.io/crates/rmbg

## Features

- Load and apply a machine learning model to remove backgrounds from images.
- Maintains original image dimensions, replacing the background with transparency.
- Preprocess and postprocess images to conform to model requirements.

## Getting Started

### Prerequisites

Before using the `rmbg` crate, you need to download the required `model.onnx` file. This model is a crucial component as
it powers the background removal process. You can download it from the following URL:

[https://huggingface.co/briaai/RMBG-1.4/blob/main/onnx/model.onnx](https://huggingface.co/briaai/RMBG-1.4/blob/main/onnx/model.onnx)

Place the downloaded `model.onnx` file in a known directory within your project.

### Installation

Either use `cargo add rmbg` from the terminal, or add `rmbg` to your `Cargo.toml` file:

```toml
[dependencies]
rmbg = "0.1.1"
```

### Usage

To use the `rmbg` crate in your project, first, initialize an instance of the `Rmbg` struct with the path to
the `model.onnx` file. Then, call the `remove_background` method with an image to process.

Here's a simple example:

```rust
use rmbg::Rmbg;

fn main() {
    // Load the model
    let rmbg = Rmbg::new("path/to/model.onnx").unwrap();

    // Load an image
    let original_img = image::open("path/to/image.png").unwrap();

    // Remove the background
    let img_without_bg = rmbg.remove_background(&original_img).unwrap();

    // Save or further process `img_without_bg` as needed
    let _ = img_without_bg.save("path/for/result.png");
}
```

A note that this is reliant on the [`image` crate](https://crates.io/crates/image), so make sure to `cargo add image`.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

### Model License

The model.onnx file used by this crate is subject to its own license terms. The model is released under the
bria-rmbg-1.4 license, which is a Creative Commons license for non-commercial use only. Commercial use of the model
requires a commercial agreement with BRIA.

Please ensure you comply with the model's license terms when using it in your projects.
