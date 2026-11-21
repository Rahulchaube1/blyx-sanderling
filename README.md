<img src="assets/logo.png" width="112" height="112" alt="A silver-white sanderling runs on short dark legs.">

# Sanderling

Choose a cache serving mode from stored age, local elapsed time and grace policy. This Blyx workflow framework is part of the networking and cache control collection.

Starting freshness at zero on every cache hop can keep stale content alive. Carry the stored age forward before applying grace. [IETF RFC 9111, freshness](https://www.rfc-editor.org/rfc/rfc9111.html#section-4.2)

## Editor extension

Install **RahulChaube.blyx-sanderling** to run the worked example and use the framework’s function completions in a Blyx file. Open an empty `.blyx` file, enter `blyx-sanderling-demo`, then choose **Blyx: Run File**. [Editor downloads](https://www.blyx-lang.space/packages/sanderling#editor) · [Download the extension](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-sanderling-0.1.0.vsix) · [Starter with framework source](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-sanderling-starter-0.1.0.zip)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-sanderling.git
cd blyx-sanderling
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-sanderling) · [Package page](https://www.blyx-lang.space/packages/sanderling) · [Handbook](https://doc.blyx-lang.space/guide/sanderling)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-sanderling.git vendor/sanderling
```

```blyx
use vendor::sanderling::sanderling;

fn main() {
    let age_at_store = 8.0;
    let stored = 100.0;
    let now = 105.0;
    let lifetime = 10.0;
    let grace = 6.0;
    let mandatory = 0.0;
    let result = sanderling_lookup(age_at_store, stored, now, lifetime, grace, mandatory);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
13
3
```

## API

`sanderling_lookup(age_at_store, stored, now, lifetime, grace, mandatory)`

Returns [mode, current age, ticks until mode changes]. Mode 0 serves fresh, 1 serves under explicit stale grace, and 2 requires validation. The host parses and enforces other cache directives. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| age_at_store | A nonnegative finite number |
| stored | A nonnegative finite number |
| now | A nonnegative finite number |
| lifetime | A nonnegative finite number |
| grace | A nonnegative finite number |
| mandatory | A nonnegative exact integer |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- 8 100 105 10 6 0
```

## Libraries

- [FreshClock](https://github.com/Rahulchaube1/blyx-freshclock/tree/v0.1.0) — Advance an already calculated HTTP cache age on a monotonic clock.
- [StaleWindow](https://github.com/Rahulchaube1/blyx-stalewindow/tree/v0.1.0) — Classify a cache entry under an explicit stale-serving policy.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-sanderling/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The [artwork notice](assets/NOTICE.txt) records credits for earlier editions.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
