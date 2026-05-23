# 定义编译器（默认g++，可替换为arm-linux-gcc等交叉编译器）
CXX = g++

# 源文件（如果有多个.cpp文件，用空格分隔，如：SRC = example.cpp test.cpp）
SRC = example.cpp

# 头文件搜索路径（-I参数，多个路径用空格分隔）
INCLUDES = -I./include/ \
           -I./include/opencv_4.2.0/include/

# 库文件搜索路径（-L参数，多个路径用空格分隔）
LIBS_PATH = -L./lib/

# 链接的库文件（-l参数，按原命令顺序排列，无需修改）
LIBS = -ljsoncpp \
       -lopencv_core \
       -lopencv_highgui \
       -lopencv_imgcodecs \
       -lopencv_imgproc \
       -lopencv_videoio \
       -lperception \
	   -ldevice_manager \
       -ltracker_full

# 编译选项（-Wall显示警告，-O2优化，可根据需求添加-std=c++11等）
CXXFLAGS = -Wall -O2 $(INCLUDES)

# 链接选项（组合库路径和库文件）
LDFLAGS = $(LIBS_PATH) $(LIBS)

# 默认目标：如果直接执行make（不带参数），生成默认文件名example
all: example
	@echo "编译完成！可执行文件：./example"

# 核心规则：匹配任意自定义目标（比如app、tracker等），生成对应可执行文件
%: $(SRC)
	$(CXX) $(CXXFLAGS) $^ -o $@ $(LDFLAGS)
	@echo "编译完成！可执行文件：./$@"

# 清理目标：删除所有生成的可执行文件和中间.o文件
clean:
	rm -rf *.o
	# 只删除当前目录下的"非源文件、非目录"的可执行文件（避免误删其他文件）
	find . -maxdepth 1 -type f -executable ! -name "*.cpp" ! -name "*.h" ! -name "Makefile" -delete
	@echo "清理完成！已删除所有可执行文件和中间文件"

# 重编译目标：先清理再编译（需指定文件名，如make rebuild app）
rebuild: clean
	$(MAKE) $(filter-out $@, $(MAKECMDGOALS))

# 伪目标声明（避免目录中存在同名文件导致Makefile失效）
.PHONY: all clean rebuild

# 忽略rebuild后的参数（让make rebuild app能正常执行）
%: PHONY