# Step 0
The command

```bash
cmake -B build
```

did not work and gave me the error

```
CMake Error at CMakeLists.txt:3 (project):

Running


'nmake' '-?'


failed with:


no such file or directory



CMake Error: CMAKE_C_COMPILER not set, after EnableLanguage

CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage

-- Configuring incomplete, errors occurred!
```

The reason behind this error is that `cmake` tried to use the default generator, `nmake`, but it wasn't installed on my shell. So I used the `G` flag to specify the generator that was installed - in this case `MinGW Makefiles`

```bash
cmake -B build -G "MinGW Makefiles"
```

To avoid this problem in the future, I added the following code to `~/.bashrc`

```bash
export CMAKE_GENERATOR="MinGW Makefiles"
```

Now I can run the following to build files
```bash
cmake -B build
```

Then run the command to create the executable 
```bash
cmake --build build
```
