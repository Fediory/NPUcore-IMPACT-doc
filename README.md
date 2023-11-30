# NPUcore-Book

这是西北工业大学NPUcore教材的 $\LaTeX$ 版本仓库，用于内部编写教材。

基于开源库：

* [NWPUMetaphysicsOffice/Yet-Another-LaTeX-Template-for-NPU-Thesis: 西北工业大学硕博学位论文模版 | Yet Another Thesis Template for Northwestern Polytechnical University (github.com)](https://github.com/NWPUMetaphysicsOffice/Yet-Another-LaTeX-Template-for-NPU-Thesis)
* [polossk/LaTeX-Template-For-NPU-Thesis: 西北工业大学本科毕业设计论文模版 | Thesis Template for Northwestern Polytechnical University (github.com)](https://github.com/polossk/LaTeX-Template-For-NPU-Thesis)

## 使用说明

1. 克隆这个项目到本地
2. 安装不低于2021版本的TexLive，参考[TexLive 2021 安装指南 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/362275032)，如果是windows系统并且使用vscode做编写，可以参考使用本README最后的vscode settings分享。
3. 在chapters目录下找到自己负责的章节文件，章节文件名加上路径格式为“chapters/01/01.tex”，对应代表第一章第一节。
4. 编写过程中需要插入图片，存放在figures目录下。图片命名格式为“01-01-figurename.png”，对应代表第一章第一节所用到的图片。
5. 推荐另行创建自己的仓库用于组内共享编写，版本迭代较为稳定之后推到此仓库中。

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
* **常用latex语法汇总**

  * 加粗：`\textbf{文本}`
  * 插入图片（参考chapters\03\03.tex）

  ```latex
  \begin{figure}[htb]
    \centering
    \includegraphics[width=\textwidth]{figures/03-03-syscall和SBI区别.png}
    \caption{
        syscall和SBI区别
    }
    \label{fig:syscall和SBI区别}
  \end{figure}
  ```

  使用 `\autoref{fig:syscall和SBI区别}`引用图片。
  不明白的参数上网查询相关资料学习。

  * 插入代码（参考chapters\03\01.tex）

  ```latex
  \begin{lstlisting}[language={Rust}, label={code:forktest},
    caption={forktest.rs}]
  pub fn main() -> i32 {
      0
  }
  \end{lstlisting}
  ```

  * 行内代码

  ```latex
  \lstinline`行内代码`
  ```
* **latex报错解决**

  * 报错 `Missing $ inserted`
    可能的原因：文中出现下划线 `"_"`，被latex识别为特殊字符。
    解决方法：在下划线 `"_"`前加上斜杠 `"\"`，即改为 `"\_"`。
    注意：在label标签中的下划线前不需要添加斜杠，否则编译不通过，举例如下：
    ```latex
    \begin{lstlisting}[language={Rust}, label={code:map_one}, caption={map\_one}]
    ```
* **vscode settings分享**

仅仅适用于windows系统，并且需要修改 `path/to`的内容为自己电脑上的程序路径。

```json
{
    // ======================== LaTeX 设置 BEGIN  ========================
    // bibtex 格式
    "latex-workshop.bibtex-format.tab": "tab",

    // 自动编译，全部关闭，当且仅当你认为有需要的时候才会去做编译
    "latex-workshop.latex.autoBuild.run": "never",
    "latex-workshop.latex.autoBuild.cleanAndRetry.enabled": false,

    // 设置 latex-workshop 的 PDF　预览程序，external　指的是外部程序
    "latex-workshop.view.pdf.viewer": "external",
    "latex-workshop.view.pdf.ref.viewer": "external",
    "latex-workshop.view.pdf.external.viewer.command": "path/to/SumatraPDF.exe",
    "latex-workshop.view.pdf.external.viewer.args": [
        "%PDF%"
    ],

    // 配置正向、反向搜索：.tex -> .pdf
    "latex-workshop.view.pdf.external.synctex.command": "path/to/SumatraPDF.exe",
    "latex-workshop.view.pdf.external.synctex.args": [
        // 正向搜索
        "-forward-search",
        "%TEX%",
        "%LINE%",
        "-reuse-instance",
        // 反向搜索
        "-inverse-search",
        "\"path/to/Microsoft VS Code/Code.exe\" \"path/to/Microsoft VS Code/resources/app/out/cli.js\" -gr %f:%l",
        "%PDF%"
    ],

    // 这是一些独立的编译选项，可以作为工具被编译方案调用
    "latex-workshop.latex.tools": [
        {
            // Windows 原生安装 TeX Live 2021 的编译选项
            "name": "Windows XeLaTeX",
            "command": "xelatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOCFILE%"
            ]
        },
        {
            // Windows Biber 编译
            "name": "Windows Biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            // Windows Biber 编译
            "name": "删除中间文件",
            "command": "del",
            "args": [
                "/s",
                "/f",
                "*.log",
                "*.aux",
                "*.nlo",
                "*.gz",
                "*.thm",
                "*.toc",
                "*.lof",
                "*.lot",
                "*.bbl",
                "*.blg"
            ]
        }
    ],

    // 这是一些编译方案，会出现在 GUI 菜单里
    "latex-workshop.latex.recipes": [
        {
            // 1.1 Windows 编译简单的小文档，这个选项不太常用，因为绝大多数文章都需要有参考文献索引
            "name": "Windows XeLaTeX 简单编译",
            "tools": [
                "删除中间文件",
                "Windows XeLaTeX",
                "Windows XeLaTeX",
                "删除中间文件"
            ]
        },
        {
            // 1.2 Windows 编译带有索引的论文，需要进行四次编译；-> 符号只是一种标记而已，没有程序上的意义
            "name": "Windows xe->bib->xe->xe 复杂编译",
            "tools": [
                "Windows XeLaTeX",
                "Windows Biber",
                "Windows XeLaTeX",
                "Windows XeLaTeX"
            ]
        }
    ],

    // 清空中间文件
    "latex-workshop.latex.clean.fileTypes": [
        "*.aux",
        "*.bbl",
        "*.blg",
        "*.idx",
        "*.ind",
        "*.lof",
        "*.lot",
        "*.out",
        "*.toc",
        "*.acn",
        "*.acr",
        "*.alg",
        "*.glg",
        "*.glo",
        "*.gls",
        "*.ist",
        "*.fls",
        "*.log",
        "*.fdb_latexmk",
        "*.bcf",
        "*.run.xml",
        "*.synctex.gz"
    ]
    // ======================== LaTeX 设置 END ========================
}
```
