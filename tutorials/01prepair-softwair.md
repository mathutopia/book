~~~
<!-- PlutoStaticHTML.Begin -->
<!--
    # This information is used for caching.
    [PlutoStaticHTML.State]
    input_sha = "27af4bb84b17fcb7a2bff48ca499f424464f836f9ed59bc417643ec9397b2e1d"
    julia_version = "1.10.5"
-->






<pre class='language-julia'><code class='language-julia'>begin
using PlutoUI,PlutoTeachingTools
end;</code></pre>


<pre class='language-julia'><code class='language-julia'>TableOfContents(title="目录")</code></pre>



<p style="font-weight:bold; font-size: 60px;text-align:center">
		Julia数据挖掘
	</p>
<div style="text-align:center"><p style="font-weight:bold; font-size: 35px; font-variant: small-caps; margin: 0px">
			软件安装与环境准备
		</p><p style="font-size: 30px; font-variant: small-caps; margin: 0px">
			Weili Chen
		</p><p style="font-size: 20px;">
			GDUFS
		</p></div>


<div class="markdown"><h1>软件安装</h1></div>


<div class="markdown"><h2>安装REPL环境</h2><p>虽然是编译型的语言， 但Julia语言提供了一个类似R语言的控制台。 其安装过程非常简单， 只需按照如下步骤依次操作即可。</p><ol><li><p>请根据自己的电脑系统， 到<a href="https://julialang.org/downloads/"><strong>Julia官网</strong></a>下载最新版本的相应软件。下面假定是windows系统。</p></li><li><p>双击下载的exe文件，选择安装路径（或者采用默认的安装路径），其余都是默认就行。</p></li><li><p>安装成功之后，桌面上会出现Julia图标。</p></li><li><p>双击图标打开Julia控制台， 通常叫做<strong>REPL环境</strong>。REPL是“Read–Eval–Print Loop”(读取-求值-打印-循环)的缩写,是一种简单的、交互式的编程环境。</p></li></ol><p>下面是一个打开的REPL环境的图片。 图中的 <code>julia&gt;</code> 提示当前是Julia语句的输入模式， 在该模式下， 在光标处输入语句，回车之后就可以看到语句执行的结果。</p></div>


<div class="markdown"><p><a href="https://free2.yunpng.top/2024/09/03/66d7209b9e31c.png"><img alt="start.png" src="https://free2.yunpng.top/2024/09/03/66d7209b9e31c.png"/></a></p></div>


<div class="markdown"><p>REPL环境有四种模式： 第一种模式就是<strong>代码（Julian）模式</strong>，提示符是 <code>julia&gt;</code>， 这也是REPL启动的时候的默认模式。 这种模式下， 可以直接写Julia的代码。</p><p>在代码模式下， 输入右边中括号<code>]</code>,进入第二种模式—<strong>包模式</strong>，其提示符是Julia的版本号。例如：<code>(@v1.10 pkg)&gt;</code>。这种模式下， 可以使用<code>add Pkgname</code>安装需要的包（Package）。 比如，安装Pluto包(<code>add Pluto</code>) 。 可以同时安装多个包，只需要逗号分隔就好。 在包模式下， 按删除键可以退回代码模式。</p><p>在代码模式下， 输入问号<code>?</code>， 将进入<strong>帮助（help）模式</strong>， 其提示符是<code>help?&gt;</code>。在该模式下， 输入任何<code>名字</code>, 可获得该名字的帮助文档。 在帮助模式下， 按删除键可以退回代码模式。 </p><p>在代码模式下， 按分号键<code>;</code>， 可以进入<strong>shell模式</strong>。其提示符为<code>shell&gt;</code>。 命令模式可以执行一些操作系统命令。同样， 按删除键可以退回代码模式。</p></div>


<div class="markdown"><div class="admonition is-warn"><header class="admonition-header">设置包安装路径</header><div class="admonition-body"><p>不管你安装Julia的时候选择的路径是什么， 后续Julia都会将你安装的包之类的资料放到全局变量<code>DEPOT_PATH</code>指定的路径下， 你可以在REPL中输入这个变量名看看路径是什么， 通常是当前用户的家目录下的<code>.julia</code>目录（<code>~/.julia</code>）。对Windows系统而言， 这个目录通常在C盘。随着Julia的使用， 安装的包等各类资源可能会越来越多， 这个目录下的文件可能会越来越多， 为了避免C盘空间不足， 建议在安装任何第三方包之前先修改这个路径。修改的方式有很多， 推荐最省事的一种。定义一个环境变量， <code>JULIA_DEPOT_PATH</code>, 其值为你想要设置的路径， 比如设置为"D:/.julia"。这样，以后所有的包都会默认安装在D盘， 不会影响C盘的空间。</p></div></div></div>


<div class="markdown"><div class="admonition is-warn"><header class="admonition-header">增加一个注册中心</header><div class="admonition-body"><p>在设置完<code>JULIA_DEPOT_PATH</code>之后， 请增加一个包注册中心。 这个注册中心是为了方便后面使用自己编写的包而设置的。 实现很简单， 在代码模式下， 输入如下语句即可。</p><pre><code class="language-julia">import Pkg
Pkg.Registry.add(RegistrySpec(url = "https://gitee.com/mathutopia/dplusreg.git"))</code></pre></div><pre><code class="language-julia">import Pkg
Pkg.Registry.add(RegistrySpec(url = "https://gitee.com/mathutopia/dplusreg.git"))</code></pre></div></div>


<div class="markdown"><h2>安装Pluto包</h2><p>Pluto是一个基于Julia的科学计算环境， 类似Jupyte notebook， 但存在一些设计上的显著差异。 本教程关于Julia的操作都在Pluto中完成。 下面介绍如何安装Pluto环境， 具体可以参考下面的视频。</p><p>Pluto是一个Julia的包（package）， 其安装只需要</p><ol><li><p>在REPL环境中， 将REPL切换到包安装模式（在Julia模式下，输入<strong>英文状态</strong>的右中括号 ]。）</p></li><li><p>在包模式下（提示符： <code>(@v1.9) pkg&gt;</code>, 不同版本会稍有不同），执行<code>add Pluto</code>就可以了（你的安装信息可能跟视频中的不同， 视频中是因为已经安装了）。</p></li><li><p>安装完成之后， 通过输入删除符号（Backspace）切换到Julia语句模式下， 通过执行</p></li></ol><pre><code class="language-julia">using Pluto
Pluto.run()</code></pre><p>两条语句即可启动Pluto环境。默认情况下，Pluto会打开一个网页。</p></div>


<div class="markdown"><p>下面的动图显示了我的电脑从启动Julia到安装pluto， 启动pluto的整个过程。</p></div>


<div class="markdown"><p><a href="https://free2.yunpng.top/2024/09/03/66d725372503d.gif"><img alt="pluto.gif" src="https://free2.yunpng.top/2024/09/03/66d725372503d.gif"/></a></p></div>


<div class="markdown"><p>整个过程结束后的界面应该是下面的图片的样子。 注意这个网址， http://localhost:1235/?secret=auGzZKwc, 如果系统没有自动打开浏览器的话，你可以将该网址复制进你喜欢的浏览器，接下来就可以用Pluto写代码了。Pluto启动，每次的网址都会不同。</p><p><a href="https://free2.yunpng.top/2024/09/03/66d72614ba33a.png"><img alt="pluto-started.png" src="https://free2.yunpng.top/2024/09/03/66d72614ba33a.png"/></a></p></div>


<div class="markdown"><div class="admonition is-warn"><header class="admonition-header">安装常用的包</header><div class="admonition-body"><p>虽然我们大部分时候使用Pluto, 不需要自己安装包。不过， 包一些包安装在本地， 可以方便在REPL中使用Julia。 以下几个包， 课程常用可以安装。 在代码模式下， 进入包模式， 安装即可。</p><pre><code class="language-julia">] add Plots # 用于绘图
] add Tidier # 用于数据处理与分析
] add Clustering # 用于聚类分析
] add MLJ # 用于分类计算
] add RuleMiner # 关联规则挖掘
] add OutlierDetection # 异常检测  
] add StatisticalMeasures # 评估模型，
] add DataFrame # 用于表格数据分析</code></pre></div><pre><code class="language-julia">] add Plots # 用于绘图
] add Tidier # 用于数据处理与分析
] add Clustering # 用于聚类分析
] add MLJ # 用于分类计算
] add RuleMiner # 关联规则挖掘
] add OutlierDetection # 异常检测  
] add StatisticalMeasures # 评估模型，
] add DataFrame # 用于表格数据分析</code></pre></div></div>


<div class="markdown"><h1>Pluto使用</h1></div>


<div class="markdown"><h2>Pluto的主界面</h2></div>


<div class="markdown"><p>Pluto的主界面是一个网页，上面有几个信息是常用。首先， 如果要创建新的notebook， 可以使用网页上的菜单， 点击 <strong>Create a new notebook"</strong> 即可。 请忽略图片中显示的几个文件名。</p><p><a href="https://free2.yunpng.top/2024/09/03/66d7274624ac1.png"><img alt="create-notebook.png" src="https://free2.yunpng.top/2024/09/03/66d7274624ac1.png"/></a></p></div>


<div class="markdown"><p>如果你是想打开一个已经存在的notebook，那么可以在<strong>Open a notebook</strong>部分输入要打开的notebook的地址——可以是网址，或一个本地文件路径。</p><p><a href="https://free2.yunpng.top/2024/09/03/66d727489a931.png"><img alt="open-notebook.png" src="https://free2.yunpng.top/2024/09/03/66d727489a931.png"/></a></p></div>


<div class="markdown"><p>当你的鼠标放进这个路径输入框时， 下面会有提示可选择的文件。 默认是Pluto启动的时候的工作路径。你可以在Julia中输入<code>pwd()</code>看到你的工作路径。为了方便起见， 建议先设置好工作路径后，再启动Pluto。 你可以使用<code>cd</code>函数设置工作路径。</p><pre><code class="language-julia"> cd(dir::AbstractString=homedir())</code></pre><p>`</p></div>


<div class="markdown"><p>除此以外， 在Pluto的主界面上还有很多漂亮的notebook样本。你可以点击任何一个去学习。 下面显示了我当前的Pluto版本包含的示例notebook。</p></div>


<div class="markdown"><p><a href="https://free2.yunpng.top/2024/09/03/66d72af432c58.png"><img alt="featured-notebook.png" src="https://free2.yunpng.top/2024/09/03/66d72af432c58.png"/></a></p></div>


<div class="markdown"><p>点击第一个notebook之后， 我们首先看到一个静态的网页， 网页的右上角有一个<strong>Edit or run this notebook</strong>,按钮， 只要点击，就可以启动这个notebook了。否则你看到的就只是一个静态的网页。</p><p><a href="https://free2.yunpng.top/2024/09/03/66d72cbf25a81.gif"><img alt="open-feat-notebook.gif" src="https://free2.yunpng.top/2024/09/03/66d72cbf25a81.gif"/></a></p></div>


<div class="markdown"><p><a href="https://free2.yunpng.top/2024/09/03/66d72d8392cd1.png"><img alt="edit-or-run.png" src="https://free2.yunpng.top/2024/09/03/66d72d8392cd1.png"/></a></p></div>


<div class="markdown"><p>当我们新建一个notebook之后， 我们看到是一个几乎空白的网页， 不过网页中有4个地方有特别的含义。下面分别介绍一下。</p><p>如下图所示： </p><ul><li><p>标记为1的地方是一个Pluto的logo， 点击这个logo会回到Pluto的主界面。</p></li><li><p>标记为2的地方对应的是notebook的文件名，仔细看你会发现一个Save notebook的提示。这里可以输入文件名去保存文件，如果你没有输入文件名， 它默认会有一个，只是你不知道它是什么样子。你最好将文件命名好，并保存到你要保存的位置。 </p></li><li><p>标记3对应的符号是一个导出符号， 点击之后可以看到一些导出选项， 你可以导出为pdf，html等格式。</p></li><li><p>标记4是notebook的cell， 这里可以写如Julia代码，就像你在REPL中写代码一样。不过， 跟Jupyter写代码时不同， Pluto中每一个cell<strong>只能写一条语句</strong>.如果你确实要写多条语句， 请用<code>begin...end</code>构建复合语句。如下面的代码所示。</p></li></ul><pre><code class="language-julia">begin
statement1
statement2
...
end</code></pre></div>


<div class="markdown"><p><a href="https://free2.yunpng.top/2024/09/03/66d72f7f700fe.png"><img alt="cell.png" src="https://free2.yunpng.top/2024/09/03/66d72f7f700fe.png"/></a></p></div>


<div class="markdown"><p>当你把鼠标放到cell上时， 你会看到cell的左边会出现一个显示和隐藏代码的按钮。有时候， 我们希望隐藏我们的代码， 只显示代码运行的结果。这时候， 可以关闭对应的cell。</p><p><a href="https://free2.yunpng.top/2024/09/03/66d732759811b.png"><img alt="cell-open.png" src="https://free2.yunpng.top/2024/09/03/66d732759811b.png"/></a></p></div>


<div class="markdown"><h2>Pluto的使用</h2><p>由于Pluto是本教程的关键计算环境， 下面的视频简要介绍了一下Pluto的使用。 更多使用的方法， 可以参考Pluto提供的官方notebook。</p></div>


<div class="markdown"><p>关于Pluto， 需要了解以下内容：</p><ul><li><p>如何打开和保存Pluto文件</p></li><li><p>Pluto文件，本质上还是可直接运行的jl文件</p></li><li><p>Pluto文件中， 每一个cell只能有一条julia语句。如果要写多条语句， 需要用<code>begin...end</code>包裹起来。相当于构建复合语句。</p></li><li><p>如果想在cell中写文本，可以按照makdwon格式去写，然后将文本用三引号包裹（相当于Julia中的字符串)，再在前面加一个<code>md</code>即可。这是Julia中的一种特殊字符串， Julia会按照<code>markdwon</code>语法解析字符串，并最终形成html文本显示出来。 如果觉得这么写比较麻烦， 可以使用快捷键<code>Ctrl + M</code>， 它会自动给一个cell加上<code>md</code>关键字和字符串标识。</p></li></ul><pre><code class="language-julia">md'''
...你的文本...
'''</code></pre><p>当然， 你也可以直接写html字符串。只需要在字符串的前面加上<code>html</code>标识即可。</p><ul><li><p>Pluto文件中， 每一个变量名只能定义一次（这是一个跟写Jupyer Notebook 有显著差异的地方）。</p></li></ul></div>


<div class="markdown"><h1>关于环境</h1><p>环境（Environment）在编程和软件开发中是一个重要的概念，特别是在使用包管理和版本控制系统的语言中，如Julia。以下是关于环境的一些基础知识：</p><h3>什么是环境？</h3><p>环境是一个包含特定版本软件包（pakckages）、依赖项（dependencies）和配置的隔离空间。在Julia中，环境通常指的是一组相互兼容的包和它们的确切版本，这些包和版本被记录在<code>Project.toml</code>和<code>Manifest.toml</code>文件中。在启动Julia后， 进入package模式， 前面的提示符<code>(@v1.10 pkg)&gt;</code>显示的就是当前的环境， 你对包所做的所有操作， 影响的都是这个环境。 这个环境是Julia的默认环境， 如果你一直使用这个默认环境， 随着包安装也来越多， 可能包之间会存在冲突。 所以， 安全情况下， 我们会为每一个项目创建一个环境。 所以， 你只要看到<code>Project.toml</code>和<code>Manifest.toml</code>文件， 就表明这个目录有一个环境。<code>Project.toml</code>中记录了这个环境中安装的所有包。（你通过 add 增加的包会记录在这个文件中）</p><h3>如何创建环境？</h3><p>在Julia中，可以使用包管理器Pkg来创建和管理环境。以下是创建环境的步骤：</p><ol><li><p><strong>创建新环境</strong>：通过<code>Pkg.activate</code>命令激活一个新的环境。例如，<code>Pkg.activate("MyProject")</code>(或者<code>] activate MyProject</code>)会在当前目录下创建一个新的环境。 <code>] activate .</code>是将当前工作路径设置为一个Project。 如果只是<code>] activate</code>， 表明激活的是全局环境。</p></li><li><p><strong>添加包</strong>：使用<code>Pkg.add</code>命令向环境中添加包。例如，<code>Pkg.add("Example")</code>会将Example包添加到当前激活的环境中，并更新<code>Project.toml</code>和<code>Manifest.toml</code>文件。</p></li></ol></div>


<div class="markdown"><h3>使用别人的环境</h3><p>如果你拿到别的一个环境， 也就是Project.toml和Manifest.toml文件。 你可以将这两个文件放置在某个文件夹下， 然后直接激活这个环境，就可以复现别人的代码了。 </p><p>不过， 有时候， 你可能只有Project.toml一个文件， 也就是拿到别的项目依赖了哪些包， 而不知道这些包之间的依赖关系（Manifest.toml文件给出）， 这时候， 你可以在包模式下输入<code>instantiate</code>或者代码模式下<code>] instantiate</code></p></div>
<div class='manifest-versions'>
<p>Built with Julia 1.10.5 and</p>
PlutoTeachingTools 0.2.15<br>
PlutoUI 0.7.60
</div>

<!-- PlutoStaticHTML.End -->
~~~