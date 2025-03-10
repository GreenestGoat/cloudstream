# CloudStream

[![NPM](https://img.shields.io/npm/v/cloudstream?color=red)](https://www.npmjs.com/package/cloudstream)
[![MIT License](https://img.shields.io/github/license/GreenestGoat/cloudstream.svg?color=blue)](https://github.com/GreenestGoat/cloudstream/blob/next/LICENSE)

Svelte component for Cloudflare Stream

[Demo](https://svelte.dev/playground/77a3baaf835249d0be3eefc08a4b40ae?version=5.22.6)

## Installation

```shell
# npm
npm install cloudstream
```

```shell
# pnpm
pnpm install cloudstream
```

```shell
# yarn
yarn add cloudstream
```

## Usage

```svelte
<script>
  import { CloudStream } from "cloudstream";
</script>

<CloudStream
  videoid="6b9e68b07dfee8cc2d116e4c51d6a957"
  customer="f33zs165nr7gyfy4"
  params={{
    loop: false,
    muted: true
  }}
/>
```

## Development

```shell
git clone https://github.com/GreenestGoat/cloudstream.git
cd cloudstream
npm install
npm run dev -- --open
```

## License

Licensed under the [MIT license](https://github.com/GreenestGoat/cloudstream/blob/main/LICENSE.md).

## Contributors

Contributions are welcome! Please feel free to submit a Pull Request.

<a href="https://github.com/GreenestGoat/cloudstream/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=GreenestGoat/cloudstream" />
</a>