# egui_synapse

**Note: This project is currently in development and not yet ready for production use.**

`egui_synapse` is an experimental crate aimed at separating the business logic and layout logic of `egui`, an immediate mode GUI crate for Rust. This separation helps in organizing GUI code into distinct parts, making the codebase more modular and maintainable.

## Overview

`egui` is a powerful GUI library for Rust that provides immediate mode graphical user interface functionalities. However, as GUI code grows, it can become challenging to manage the interplay between business logic (application state and behavior) and layout logic (UI components and their rendering).

`egui_synapse` attempts to address this challenge by promoting a clear separation between these two aspects of GUI development:

- **Business Logic**: This encompasses the core application state, event handling, and business-specific behavior. With `egui_synapse`, you define your application's state and behavior in a clear and decoupled manner from UI concerns.

- **Layout Logic**: This focuses on defining UI components, their layout, and rendering. `egui_synapse` provides utilities to bind UI components directly to the application state defined in the business logic layer.

## Usage

To use `egui_synapse`:

1. **Define Business Logic**: Create your application state and behavior. This can include defining structs, enums, and functions to manage your application's state and respond to events.

2. **Define Layout Logic**: Implement UI components and their layout using `egui_synapse`. These components are bound to your application state, enabling automatic updates based on state changes.

3. **Integrate with `egui`**: `egui_synapse` leverages `egui` for rendering and event handling. You can seamlessly integrate `egui_synapse` components with `egui` widgets and APIs.

## Example

```rust
use egui::Ui;
use egui_synapse::{State, synapse_widget};

// Define application state
struct Counter {
    count: i32,
}

impl Counter {
    fn increment(&mut self) {
        self.count += 1;
    }
}

// Define UI component
fn ui_counter(ui: &mut Ui, state: &mut Counter) {
    ui.label(format!("Count: {}", state.count));

    if ui.button("Increment").clicked() {
        state.increment();
    }
}

fn main() {
    let mut counter_state = State::new(Counter { count: 0 });

    egui::run(|ui| {
        synapse_widget(ui, &mut counter_state, ui_counter);
    });
}
```
In this example, Counter represents the business logic state with a count value. The ui_counter function defines the layout logic for rendering the counter UI. The synapse_widget function binds the UI component to the state, allowing automatic updates.

## License
egui_synapse is licensed under the Apache License, Version 2.0. See the LICENSE file for more details.

## Contribution
Contributions to egui_synapse are welcome! Feel free to open issues for suggestions or bug reports, and submit pull requests with improvements.

