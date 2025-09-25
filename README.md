### 1. clone the template

```bash
git clone https://github.com/yourusername/cpp-project-template.git my-new-project
cd my-new-project
```

clean git history:

```bash
rm -rf .git
git init
git add .
git commit -m "initial commit for my-new-project"
```

---

### 2. install vcpkg (if not already installed)

```bash
git clone https://github.com/microsoft/vcpkg.git C:/vcpkg
cd C:/vcpkg
.\bootstrap-vcpkg.bat
```

make sure `C:/vcpkg` is in your system `PATH`.

---

### 3. install libraries

for example:

```bash
C:/vcpkg/vcpkg install fmt:x64-windows
C:/vcpkg/vcpkg install asio:x64-windows
C:/vcpkg/vcpkg install crow:x64-windows
```

check installed libraries:

```bash
C:/vcpkg/vcpkg list
```

---

### 4. configure the project

```bash
cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows
```

* `build/` will contain the cmake-generated project files
* open `build/` in visual studio or use:

```bash
cmake --build build --config Release
```

---

### 5. adding libraries to the project

1. install via vcpkg (step 3)
2. in `CMakeLists.txt` add:

```cmake
find_package(fmt CONFIG REQUIRED)
target_link_libraries(main1 PRIVATE fmt::fmt)
```

3. re-run cmake (step 4)

---

### 6. optional third-party directories

* if `thirdParty/profilerLib` or `thirdParty/safeSave` exist, they will be automatically added and linked
* if missing, cmake will skip them

---

### 7. adding source files

* place `.cpp` files in `src/`
* place headers in `include/`
* `CMakeLists.txt` automatically includes all `src/*.cpp` files

---

### 8. resource path

* `RESOURCES_PATH` is automatically defined as:

```
${CMAKE_CURRENT_SOURCE_DIR}/resources
```

* use this in your code to load assets relative to the project root

---

### 9. cleaning / rebuilding

```bash
rm -r build
cmake -B build -S . -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake -DVCPKG_TARGET_TRIPLET=x64-windows
cmake --build build --config Release
```

---

this template is intended as a starting point for new c++ projects with minimal setup overhead.
simply clone, add libraries, and start coding.
