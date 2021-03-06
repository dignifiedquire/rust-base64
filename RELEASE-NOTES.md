# Next

- Minimum rust version 1.27.2

# 0.10.0

- Remove line wrapping. Line wrapping was never a great conceptual fit in this library, and other features (streaming encoding, etc) either couldn't support it or could support only special cases of it with a great increase in complexity. Line wrapping has been pulled out into a [line-wrap](https://crates.io/crates/line-wrap) crate, so it's still available if you need it.
  - `Base64Display` creation no longer uses a `Result` because it can't fail, which means its helper methods for common
  configs that `unwrap()` for you are no longer needed
- Add a streaming encoder `Write` impl to transparently base64 as you write.
- Remove the remaining `unsafe` code.
- Remove whitespace stripping to simplify `no_std` support. No out of the box configs use it, and it's trivial to do yourself if needed: `filter(|b| !b" \n\t\r\x0b\x0c".contains(b)`.
- Detect invalid trailing symbols when decoding and return an error rather than silently ignoring them.

# 0.9.3

- Update safemem

# 0.9.2

- Derive `Clone` for `DecodeError`.

# 0.9.1

- Add support for `crypt(3)`'s base64 variant.

# 0.9.0

- `decode_config_slice` function for no-allocation decoding, analogous to `encode_config_slice`
- Decode performance optimization

# 0.8.0

- `encode_config_slice` function for no-allocation encoding

# 0.7.0

- `STANDARD_NO_PAD` config
- `Base64Display` heap-free wrapper for use in format strings, etc

# 0.6.0

- Decode performance improvements
- Use `unsafe` in fewer places
- Added fuzzers

# 0.5.2

- Avoid usize overflow when calculating length
- Better line wrapping performance

# 0.5.1

- Temporarily disable line wrapping
- Add Apache 2.0 license

# 0.5.0

- MIME support, including configurable line endings and line wrapping
- Removed `decode_ws`
- Renamed `Base64Error` to `DecodeError`

# 0.4.1

- Allow decoding a `AsRef<[u8]>` instead of just a `&str`

# 0.4.0

- Configurable padding
- Encode performance improvements

# 0.3.0

- Added encode/decode functions that do not allocate their own storage
- Decode performance improvements
- Extraneous padding bytes are no longer ignored. Now, an error will be returned.
