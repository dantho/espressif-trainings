# HTTPS CLIENT

You will now make changes to your http client files so that it also works for encrypted connections.

`intro/http-client/examples/http_client.rs` contains the solution. You can run it with the following command:
(It won't build unless you have completed the first step of the exercise.)

```
cargo run --example https_client
```

Create a custom client configuration to use an `http::client::EspHttpClientConfiguration` which enables the use of these certificates and uses default values for everything else:

```rust
let mut client = EspHttpClient::new(&EspHttpClientConfiguration {
        use_global_ca_store: true,
        crt_bundle_attach: Some(esp_idf_sys::esp_crt_bundle_attach),

        ..Default::default()
    }
```

✅ Initialize your HTTP client with this new configuration and verify HTTPS works by downloading from a `https` resource e.g. `https://espressif.com/`. the download will show as raw html in the terminal output.

## Troubleshooting (repeated from previous section)

- `missing WiFi name/password`: ensure that you've configured `cfg.toml` according to `cfg.toml.example` - a common problem is that package name and config section name don't match.

```toml
# Cargo.toml
#...
[package]
name = "http-client"
#...

# cfg.toml
[http-client]
wifi_ssid = "..."
wifi_psk = "..."
```
