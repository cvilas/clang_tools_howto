# clang_tools_example

Shows how to integrate clang format and clang tidy with your CMake project

* Install clang clang tools

```
sudo apt-get install clang-tidy clang-format clang
```

* Formatting rules are in `.clang-format` file at the top level directly

* Clang-tidy rules are specified in `Configure linter` section in top level CMakeLists.txt (This could be moved to a separate file)

* Add the line `add_clang_format(<cmake_target_name>)` to automatically format sources to rules from .clang-format

* During build, you should see linter messages due to code not compliant with clang-tidy rules 
