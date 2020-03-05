# About This Repository

This repository is the source code of our manual.

## Building

You need to install `gitbook-cli` first. Install `yarn`

https://classic.yarnpkg.com/en/docs/install#debian-stable

Install `gitbook-cli` using `yarn`

```
yarn global add gitbook-cli
```

When you build this for the first time, you need to install plugins.

```
gitbook install
```

Then run

```
gitbook build . docs
```

If you want to preview, run the command below. The local website is http://localhost:4000.

```
gitbook serve
```

## License

The manual is distributed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.

## Repository Structure

The body is placed under the `content` folder, and the chapters are placed in the corresponding chapter folder, starting with `ch` and followed by two-digit numbers.

Each section and subsection is placed in the chapter folder. The pictures and other content used in the text are placed in the `assets` folder in the corresponding chapter folder.
