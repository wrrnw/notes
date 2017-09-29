##Linux目录结构及文件基本操作
####**1. FHS标准**
 Linux目录结构遵循FHS(_Filesystem Hierarchy Standard_)  
 FHS定义了两层规范
  1. **/** 下面的各个目录该放什么文件数据, 如 **/etc** 应该放置设置文件， **/bin /sbin** 应该放置可执行文件.
  2. 针对 **/usr /var** 这两个目录的子目录来定义, 如 **/var/log** 放置系统登录文件, **/usr/share 放置共享数据**.
