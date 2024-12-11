# triton-client-rs

A Rust gRPC client library for [NVIDIA Triton](https://developer.nvidia.com/nvidia-triton-inference-server).

This library provides the necessary setup to generate a Triton client from NVIDIA's Protocol Buffers definitions.

```rust
use triton_client::client::Client;
use triton_client::inference::RepositoryIndexRequest;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let client = Client::new("http://localhost:8001/", None).await?;
    let models = client
        .repository_index(RepositoryIndexRequest {
            repository_name: "".into(),
            ready: false,
        })
        .await?;
    for model in models.models {
        println!("Name: {}", model.name);
        println!("Version: {:?}", model.version);
        println!("State: {:?}", model.state);
        println!("---------------");
    }

    Ok(())
}
```
