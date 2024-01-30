# FarFrame 🦀

## A Simple [Farcaster Frame](https://warpcast.notion.site/Farcaster-Frames-4bd47fe97dc74a42a48d3a234636d8c5) Server

![Demo](./demo.png)

```Rust
#[tokio::main]
async fn main() {
    let app = Router::new()
    .route("/", get( Html(
        "
        <!DOCTYPE html>
        <html lang=\"en\">
        <head>
        <meta charset=\"UTF-8\" />
        <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\" />
        <title>FarFrame</title>
        <meta property=\"og:title\" content=\"FarFrame\" />
        <meta property=\"og:image\" content=\"https://farframe-rs.fly.dev/public/initial.png\" />
        <meta property=\"fc:frame\" content=\"vNext\" />
        <meta property=\"fc:frame:image\" content=\"https://farframe-rs.fly.dev/public/initial.png\" />
        <meta property=\"fc:frame:button:1\" content=\"Roll\" />
        <meta property=\"fc:frame:post_url\" content=\"https://farframe-rs.fly.dev/api/frame\" />
        </head>
        <body>
        <h1>FarFrame</h1>
        </body>
        </html>
        "
    )))
    .route("/api/frame", post(Html("
    <!DOCTYPE html>
    <html lang=\"en\">
    <head>
    <meta property=\"fc:frame\" content=\"vNext\" />
    <meta property=\"fc:frame:image\" content=\"https://farframe-rs.fly.dev/public/roll.png\" />
    <meta property=\"fc:frame:post_url\" content=\"https://farframe-rs.fly.dev/api/frame\" />
    </head>
    </html>
    ")))
    .nest_service("/public", ServeDir::new("public"));

    let listener = tokio::net::TcpListener::bind("0.0.0.0:3000").await.unwrap();
    axum::serve(listener, app).await.unwrap();
}
```

## Inspirations

- [gskril](https://github.com/gskril)'s [farcast-frame](https://github.com/gskril/farcaster-frame)
- [Zizzamia](https://github.com/Zizzamia)'s [a-frame-in-100-lines](https://github.com/Zizzamia/a-frame-in-100-lines)
