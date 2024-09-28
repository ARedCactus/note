# ~/.bashrc 环境变量
## C
### C_INCLUDE_PATH
- **仅对预处理C有效**
```
export C_INCLUDE_PATH=/usr/local/include:$C_INCLUDE_PATH
```
## C++
### CPLUS_INCLUDE_PATH 
- **仅对预处理C++有效，而`CPATH`对所有语言均有效**
```
export CPLUS_INCLUDE_PATH=/usr/local/include:$CPLUS_INCLUDE_PATH
```
### LIBRARY_PATH 
- **程序编译期间查找动态链接库时指定查找共享库的路径**
```
export LIBRARY_PATH=/usr/local/lib:$LIBRARY_PATH
```
### LD_LIBRARY_PATH 
- **程序加载运行期间查找找动态链接库时指定除了系统默认路径之外的其他路径**
```
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
```