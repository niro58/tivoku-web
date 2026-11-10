# Tivoku

The source of the Tivoku website (tivoku.com), a small set of free tools that work inside your browser. Your files are never sent to a server: the image and video work is done on your own computer, in the page.

## The tools

- **Image Resizer** – resize up to 100 images at once (up to 25 MB each). Set a fixed size, choose how it is cut (crop to the longest side, crop to the shortest side, or downscale), and save as PNG, JPEG or WebP. Download the results one by one or as a single ZIP.
- **Video Converter** – convert a video (up to 100 MB) to MP4, WebM, MKV, MOV, AVI, FLV, WMV, OGV or 3GP, or pull out the sound as MP3, AAC, FLAC, WAV, OGG, M4A and a few other audio formats. Up to 10 files at a time.
- **Website Blocker page** – a landing page for my Chrome extension that blocks distracting sites, with its screenshots. The extension is a separate project; only the page is here.

## Why nothing is uploaded

The image tool draws the resized picture on a browser canvas. The video tool uses FFmpeg compiled to WebAssembly, which runs in the page. The site's own code makes no upload requests. One thing to know: the first time you convert a video, the browser downloads the FFmpeg engine (the conversion code, a sizeable file) from the unpkg CDN. Your video is not part of that.

## Run it yourself

You need Node 22 and pnpm.

```
pnpm install
pnpm dev
```

Then open the address Vite prints. The dev server sends the two security headers (`Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy`) that the video converter needs. If you host a build elsewhere, your server must send them too, or the video tool will not start.

Other commands:

| Command | What it does |
| --- | --- |
| `pnpm build` | Production build (Node server, run with `node build`) |
| `pnpm check` | Type check |
| `pnpm lint` | Prettier and ESLint |
| `pnpm test` | Unit tests (there is only a placeholder test so far) |

The `Dockerfile` and the `.k8s` folder are how I deploy it to my own cluster. You do not need them.

The site sets `PUBLIC_MODE=prod` in production, which redirects visitors to the `www.` address. It also loads Google Analytics, after the visitor accepts a consent banner.

## Built with

SvelteKit with Svelte 5, TypeScript, Tailwind CSS, shadcn-svelte components, FFmpeg.wasm, JSZip.

## Status

The image resizer, video converter and blocker page are built. A **video trimmer** is started but not finished: its screens are in `src/routes/video-trimmer`, but it is switched off and not linked from the site. The project is a one-person hobby; there are almost no tests.