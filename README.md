# NPUcore-Book

这是西北工业大学NPUcore教材的 $\LaTeX$ 版本仓库，用于内部编写教材。

基于开源库：

* [NWPUMetaphysicsOffice/Yet-Another-LaTeX-Template-for-NPU-Thesis: 西北工业大学硕博学位论文模版 | Yet Another Thesis Template for Northwestern Polytechnical University (github.com)](https://github.com/NWPUMetaphysicsOffice/Yet-Another-LaTeX-Template-for-NPU-Thesis)
* [polossk/LaTeX-Template-For-NPU-Thesis: 西北工业大学本科毕业设计论文模版 | Thesis Template for Northwestern Polytechnical University (github.com)](https://github.com/polossk/LaTeX-Template-For-NPU-Thesis)

## 使用说明

1. 克隆这个项目到本地
2. 安装不低于2021版本的TexLive，参考[TexLive 2021 安装指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/362275032)

## 常见问题 Q&A

* **Q：我是 Linux/macOS 用户，字体是否兼容？**
  * 本模板使用的是 **Windows** 系统的自带字体（宋体、黑体、楷体、仿宋、Times New Roman、Consolas），Windows 环境下目前能保证字体的指向正确。
  * 本模板目前兼容 Linux 与 macOS 用户。请在编译的时候添加 `-shell-escape` 选项，以保证模板正确识别操作系统。
  * Linux 用户请检查自己的字体库中是否有上述字体，推荐从 Windows 系统上拷贝一整套字体（宋黑楷仿宋）以方便后续使用。
  * macOS 用户使用系统自带的宋、黑、楷、仿宋字体（华文字体系列），对应的字体名分别是：STSongti-SC-Regular、STHeiti、STKaiti、STFangSong。
* **Q：我没有等宽字体（默认 Consolas），应该怎么办？**
  * 非 Windows 操作系统的用户（包括 macOS 与 Linux 用户）需要安装 Consolas 字体后使用，字体文件可于仓库[Fonts-For-NPU-Thesis-Template](https://github.com/NWPUMetaphysicsOffice/Fonts-For-NPU-Thesis-Template) 下载
* **Q：这个编译报错了 balabala，怎么解决？**
  * 建议善用搜索引擎或 ChatGPT，搜索排查许久尚不能解决，询问助教。
* **Q：编译时卡顿了，怎么解决？**
  * 对于 Windows 电脑，如果在编译过程中遇到卡在字体缓冲问题，请先关闭当前进程，并用管理员模式打开命令提示符（或终端），键入 `fc-cache -f -v` 强制刷新字体缓存即可
* **Q：LaTeX 怎么调整公式大小/公式换行/怎么加粗？**
  * 抱歉，**恕不解答任何 LaTeX 使用问题**，请自行上网搜索或查阅相关书籍。
* **Q：请问默认的 `makefile` 提供了那些功能？**
  * 本模板提供了简单的 `makefile` 文件来控制编译流程，可以编译 `dtx` 文件从而得到模板类 `cls` 文件，也可以编译大论文文档 `yanputhesis-sample.tex`。
  * 所有基本流程为关闭当前已打开的输出 pdf 文件并删除，清理缓存文件，编译 tex 文档并打开。
  * 默认选项 `make` 或者 `make main` 负责编译编译 `dtx` 文件从而得到模板类 `yanputhesis.cls` 文件和样例文件 `yanputhesis-sample.tex`。
  * 提供选项 `make sample` 负责生成不含参考文献的样例文档 `yanputhesis-sample.pdf`
  * 提供选项 `make samplebib` 负责生成含有参考文献的样例文档 `yanputhesis-sample.pdf`
  * 同时提供了 `open[sample]`, `close`, `clean`, `wipe[sample]` 四组快捷指令，其效果如下：
    * `open[sample]`：使用 Acrobat 打开输出的 pdf 文件；
    * `close`：终止 Acrobat 进程从而关闭输出的 pdf 文件（会误伤其他以打开的文件）；
    * `clean`：删除 `*.aux` 和其他缓存文件；
    * `wipe[sample]`：删除输出的 pdf 文件；
  * 对于 Linux 玩家而言，可参考上述功能，并在此 `makefile` 基础上稍作修改即可使用。

## 其他注意事项

* **格式符说明**
  * 字体大小（size）的控制命令统一前缀为 `s`
  * 字体格式（font）的控制命令统一前缀为 `f`
