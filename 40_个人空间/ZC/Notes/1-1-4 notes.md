# Cmake 的入门

### 基础流程
1. **编写 CMakeLists.txt**：在项目根目录创建该文件。
2. **构建步骤**：
   ```bash
   mkdir build && cd build
   cmake ..
   make
   ```

### 核心指令
- `cmake_minimum_required(VERSION 3.10)`：指定最低版本要求。
- `project(MyProject)`：定义项目名称。
- `add_executable(main main.cpp)`：将源文件编译为可执行程序。
- `add_library(mylib STATIC lib.cpp)`：创建静态库或动态库（SHARED）。
- `target_link_libraries(main mylib)`：将库链接到目标程序。

# Cpp 语法的学习
### 迭代器（Iterators）
迭代器提供了一种统一的方法来访问容器（如 `vector`, `list`, `map`）中的元素，其行为类似于指针。

- **获取迭代器**：`auto it = vec.begin();`（指向首元素），`vec.end();`（指向末尾元素的下一个位置）。
- **迭代器种类**：
  - **输入/输出迭代器**：最基本的读写。
  - **前向迭代器 (Forward)**：支持 `it++`。
  - **双向迭代器 (Bidirectional)**：支持 `it++` 和 `it--`（如 `std::list`, `std::set`）。
  - **随机访问迭代器 (Random Access)**：支持 `it + n`, `it[n]`, `<` 等比较（如 `std::vector`, `std::deque`）。

# Cpp 的 filesystem 库
引入头文件 `<filesystem>`，使用命名空间 `namespace fs = std::filesystem;`。

### 常用接口整理表

| 接口名称 | 功能描述 | 示例 |
| :--- | :--- | :--- |
| **路径与查询** | | |
| `fs::path` | 路径类，支持路径拼接 (`/`) 和格式转换 | `fs::path p("src/main.cpp");` |
| `fs::exists()` | 检查文件或目录是否存在 | `if (fs::exists(p)) { ... }` |
| `fs::is_directory()` | 判断路径是否为文件夹 | `fs::is_directory(p);` |
| `fs::current_path()` | 获取或设置当前工作目录 | `auto cp = fs::current_path();` |
| **目录遍历** | | |
| `fs::directory_iterator` | 遍历当前目录下的文件（不含子目录） | `for (auto& entry : fs::directory_iterator(p))` |
| `fs::recursive_directory_iterator` | 递归遍历所有子目录 | `for (auto& entry : fs::recursive_directory_iterator(p))` |
| **Path 对象成员接口** | *(p 为 fs::path 对象)* | |
| `p.filename()` | 返回文件名（带后缀） | `"main.cpp"` |
| `p.extension()` | 返回文件后缀名 | `".cpp"` |
| `p.stem()` | 返回主文件名（无后缀） | `"main"` |
| `p.parent_path()` | 返回父目录路径 | `"/home/user/src"` |
| `p.is_absolute()` | 是否为绝对路径 | `true / false` |
| `p.replace_extension()`| 修改后缀名 | `p.replace_extension(".h");` |
| `p1 / p2` | **路径拼接运算符**（自动处理分隔符）| `fs::path full = p1 / "subdir" / "file.txt";` |
| **Entry 对象接口** | *(entry 为遍历得到的对象)* | |
| `entry.path()` | 获取当前项的完整路径 | `std::cout << entry.path();` |
| `entry.is_regular_file()` | 是否为常规文件 | `if (entry.is_regular_file())` |
| `entry.is_directory()` | 是否为目录 | `if (entry.is_directory())` |
| `entry.file_size()` | 获取文件大小（字节） | `auto size = entry.file_size();` |
| `entry.last_write_time()` | 获取最后修改时间 | `auto time = entry.last_write_time();` |
| **文件操作** | | |
| `fs::create_directories()`| 递归创建多级目录 | `fs::create_directories("a/b/c");` |
| `fs::copy()` | 复制文件或目录 | `fs::copy("old.txt", "new.txt");` |
| `fs::remove_all()` | 递归删除目录及其所有内容 | `fs::remove_all("dir_name");` |
