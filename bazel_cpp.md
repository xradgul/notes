# Bazel for C++ projects

Bazel is great, but it is painful to use for C++ projects. There are two key issues:

1. Lack of IDE/LSP support

Most IDEs/LSPs (e.g. Vim/YouCompleteMe) depend on `compile_commands.json` to provide dev tooling such as autocomplete and error highlighting for C++ projects. Bazel lacks native support for generating `compile_commands.json`, which is trivial in cmake. There are some [abandoned](https://github.com/grailbio/bazel-compilation-database)/[half-baked](https://github.com/hedronvision/bazel-compile-commands-extractor) open source projects on GitHub but they are clunky to use and are not dependable. 
   
2. Lack of automatic build cleaner

It's painful to keep build rules up-to-date in BUILD files manually every time you include a new header file in a class. This process could have been automated, but it's not.
