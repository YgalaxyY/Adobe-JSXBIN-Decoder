# JSXBIN to JSX converter

A C# adaptation of [autoboosh's JSXBIN-to-JSX converter](https://github.com/codecopy/jsxbin-to-jsx-converter). The converter reads encoded Adobe ExtendScript and reconstructs readable JSX. Most of the converter implementation and its tests come from the upstream project.

## Source and build

- [Solution](jsxbin_to_jsx.sln) — open in Visual Studio on Windows with the relevant .NET Framework targeting pack.
- [Converter source](jsxbin_to_jsx) and [tests](jsxbin_to_jsx.Tests).
- [Contribution notes](CONTRIBUTING.md).

The tool's output and format compatibility depend on the input. This repository includes an adaptation of the source, with upstream credit and the original [MIT license](LICENSE).
