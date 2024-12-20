+++
weight = 1
sort_by = "weight"
template = "index.html"
insert_anchor_links = "right"
+++

<a href="javascript:request_admin()" style="cursor:default; "><img id="logo" class="hide_on_small" src="logo.png" alt="Ferris holding a cheat sheet."></img></a>
<pagetitle>Rust 语言速查表</pagetitle>
<subtitle><span id="subtitle" onclick="advance_subtitle()">{{ date() }}</span></subtitle>


<blockquote class="legend">

<symbol-legend class="short">

包含可点击链接到
**The Book** {{ book(page="") }},
**Rust by Example** {{ ex(page="") }},
**Std Docs** {{ std(page="std") }},
**Nomicon** {{ nom(page="") }},
**Reference** {{ ref(page="") }}.

</symbol-legend>

<symbol-legend class="long">

<twocolumn>
<column>

**可点击的符号** <br>
<br> <legend-symbol> {{ book(page="") }} </legend-symbol> **The Book**.
<br> <legend-symbol> {{ ex(page="") }} </legend-symbol> **通过例子学Rust**.
<br> <legend-symbol> {{ std(page="std") }} </legend-symbol>  **标准库 (API)**。
<br> <legend-symbol> {{ nom(page="") }} </legend-symbol> **Nomicon**.
<br> <legend-symbol> {{ ref(page="") }} </legend-symbol> **Reference**.
<br> <legend-symbol> {{ rfc(page="") }} </legend-symbol> 官方 **RFC** 文档。
<br> <legend-symbol> {{ link(url="https://cheats.rs") }} </legend-symbol> The **internet**.
<br> <legend-symbol> {{ above(target="#") }} </legend-symbol> 本页中，**上方**。
<br> <legend-symbol> {{ below(target="#") }} </legend-symbol> 本页中，**下方**。

</column>
<column>

**其他符号** <br>
<br> <legend-symbol> {{ deprecated() }}   </legend-symbol>大多数**已弃用**。
<br> <legend-symbol> {{ edition(ed="'18") }} </legend-symbol>需要**最低版本**要求。
<br> <legend-symbol> {{ experimental() }} </legend-symbol>需要 **Rust nightly**（或不完整）。
<br> <legend-symbol> {{ bad() }}   </legend-symbol>有意的**错误示例**或**陷阱**。
<br> <legend-symbol> {{ esoteric() }}   </legend-symbol>略为**深奥**，很少使用或进阶内容。
<br> <legend-symbol> {{ hot() }}   </legend-symbol>具有**极大实用性**的内容。
<br> <legend-symbol> {{ expands_to() }} </legend-symbol>父级项目**扩展为** &hellip;
<br> <legend-symbol> {{ opinionated() }} </legend-symbol>**有个人见解**。
<br> <legend-symbol> {{ todo() }} </legend-symbol>缺少**合适链接**或说明。

</column>
</twocolumn>
</symbol-legend>

<div style="text-align: right; height: 1px;">
    <span class="expander" style="font-size: 10px; position: relative; top: -20px;">
        <a href="javascript:toggle_legend();">➕</a>
    </span>
</div>

</blockquote>


<noprint>
<page-controls>
    <!-- <a id="" href="" style="float: left; margin-left:5px;">X-Ray Mode 👓</a> -->
    <a id="toggle_ligatures" href="javascript:toggle_ligatures()">字体连字 (<code>..=, =></code>)</a>
    <!-- <a id="expand_everything" class="hide_on_small" href="javascript:toggle_expand_all()">展开所有内容？</a> -->
    <a href="javascript:toggle_night_mode()">夜间模式 &#x1f4a1;</a>
    <a class="admin" href="javascript:toggle_xray()">X-Ray 📈</a>
</page-controls>

<div class="xray-help">
X-Ray 可视化已启用。这些显示每个部分的汇总反馈。目前该功能还在试验阶段。已知的问题包括： 
<ul>
<li>某些收到大量反馈的部分未显示（例如，“Hello Rust”）</li>
<li>未考虑部分内容的发布时间长短（某些部分已存在数年，另一些则仅存在几个月）</li>
<li>未考虑反馈激增（例如某人重复按下同一按钮三次），也未考虑“最新反馈”（例如某人先投赞成票后又投反对票）。</li>
</ul>
The feedback format is (<span style="color:green;">positive</span>, <span style="color:red;">negative</span>, textual), equivalent to use of the feedback buttons.
</div>

</noprint>

<noprint>
<toc><column>

**语言结构**
* [数据结构](#data-structures)
* [引用 & 指针](#references-pointers)
* [函数 & 行为](#functions-behavior)
* [控制流](#control-flow)
* [代码组织](#organizing-code)
* [类型别名和强制类型转换](#type-aliases-and-casts)
* [宏 & 属性](#macros-attributes)
* [模式匹配](#pattern-matching)
* [泛型 & 约束](#generics-constraints)
* [高阶条目](#higher-ranked-items){{ esoteric() }}
* [字符串 & 字符](#strings-chars)
* [文档](#documentation)
* [杂项](#miscellaneous)

**幕后原理**
* [抽象机](#the-abstract-machine)
* [语言糖](#language-sugar)
* [内存 & 生命周期](#memory-lifetimes)


**内存布局**
* [基本类型](#basic-types)
* [自定义类型](#custom-types)
* [引用 & 指针](#references-pointers-ui)
* [闭包](#closures-data)
* [标准库类型](#standard-library-types)

**杂项**
* [链接 & 服务](#links-services)
* [打印 & PDF](#printing-pdf)

</column>

<column>

**标准库**
* [One-Liners](#one-liners)
* [线程安全](#thread-safety)
* [迭代器](#iterators)
* [数值转换](#number-conversions)
* [字符串转换](#string-conversions)
* [字符串输出](#string-output)


**工具**
* [项目结构](#project-anatomy)
* [Cargo](#cargo)
* [交叉编译](#cross-compilation)
* [工具指令](#tooling-directives)


**类型操作**
* [类型, 特性, 泛型](#types-traits-generics)
* [外部类型和特性](#foreign-types-and-traits)
* [类型转换](#type-conversions)


**编码指南**
* [符合Rust规范的写法](#idiomatic-rust)
* [性能优化建议](#performance-tips)
* [Async-Await 101](#async-await-101)
* [API中的闭包](#closures-in-apis)
* [不安全, 无效, 未定义](#unsafe-unsound-undefined)
* [对抗性代码](#adversarial-code){{ esoteric() }}
* [API稳定性](#api-stability)


</column>
</toc>
</noprint>

<noprint>

## 你好，Rust!

如果你是 Rust 新手，或者想尝试下列内容：


<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-1" name="tab-hello" checked/>
<label for="tab-hello-1"><b>Hello World</b></label>
<panel><div>
<div id="hellostatic">

```rust
fn main() {
    println!("Hello, world!");
}
```


</div>
<div id="helloplay"></div>
<div id="helloinfo">Service provided by <a href="https://play.rust-lang.org/" target="_blank" rel="noopener">play.rust-lang.org <sup>🔗</sup></a></div>
<div id="helloctrl"><a href="javascript:show_playground(true);">▶️ Edit & Run</a></div>
</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-3" name="tab-hello">
<label for="tab-hello-3"><b>优点</b></label>
<panel><div>

**Rust 的显著优点**

- 编译后的代码具有与 C / C++ [类似的性能](https://benchmarksgame-team.pages.debian.net/benchmarksgame/box-plot-summary-charts.html)，出色的[内存和能效管理](https://docente.ifsc.edu.br/mello/livros/java/paperSLE.pdf)
- 可以[避免 C / C++ 中 70% 以上的安全问题](https://www.chromium.org/Home/chromium-security/memory-safety)，并减少大多数内存问题
- 强类型系统防止[数据竞争](https://doc.rust-lang.org/nomicon/races.html)，带来了['无畏并发'](https://blog.rust-lang.org/2015/04/10/Fearless-Concurrency.html)等优势
- 无缝的 C 语言互操作性，并[支持基于 LLVM 的多种平台](https://doc.rust-lang.org/rustc/platform-support.html)。
- 连续 <strike>4</strike> <strike>5</strike> <strike>6</strike> <strike>7</strike> 8 年被评为[“最受喜爱或最受敬仰的语言”](https://survey.stackoverflow.co/2023/#section-admired-and-desired-programming-scripting-and-markup-languages)🤷‍♀️。
- 现代工具链：`cargo`（构建 _简洁高效_）、`clippy`（700+ 代码质量检查）、`rustup`（轻松的工具链管理）。

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-4" name="tab-hello">
<label for="tab-hello-4"><b>缺点</b></label>
<panel><div>

**Rust 的潜在不足**

- 学习曲线陡峭；<sup>1</sup> 编译器会强制执行内存规则，这些在其他地方可能只作为“最佳实践”。
- 在某些领域缺少 Rust 原生的库，目标平台（特别是嵌入式）缺少功能，IDE 特性也有限。<sup>1</sup>
- 编译时间比其他语言“类似”代码稍长。<sup>1</sup>
- 不小心使用`不安全`代码（unsafe）的库可能会暗中破坏安全保障。
- ~~Rust 尚无正式的语言规范~~，{{ link(url="https://spec.ferrocene.dev/") }}~~在某些领域（例如航空、医疗）可能影响法律使用~~ {{ link(url="https://ferrous-systems.com/ferrocene/") }}
- Rust 基金会可能对使用其知识产权的 _'Rust'_ 项目施加限制（例如禁止名称、强制执行政策）. {{ link(url="https://devclass.com/2023/04/11/dont-call-it-rust-community-complains-about-draft-trademark-policy-restricting-use-of-word-marks/") }}{{ link(url="https://web.archive.org/web/20230413161930/https://old.reddit.com/r/rust/comments/12e7tdb/rust_trademark_policy_feedback_form/") }}<sup>2</sup>


<sup>1</sup> 详细参见[Rust Survey](https://blog.rust-lang.org/2020/04/17/Rust-survey-2019.html#why-not-use-rust). <br>
<sup>2</sup> 避免使用商标（例如名称、URL、标志），这可能已经足够。

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-5" name="tab-hello">
<label for="tab-hello-5"><b>安装</b></label>
<panel><div>

**下载**
- 从 [**rustup.rs**](https://rustup.rs/) 获取安装程序（强烈推荐）{{ hot() }}


**IDEs**
- [**Rust Rover**](https://www.jetbrains.com/rust/) (非商业用途免费)
- [Visual Studio Code](https://code.visualstudio.com/) 配合 [**rust-analyzer**](https://rust-analyzer.github.io/) (免费)


</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-hello-6" name="tab-hello">
<label for="tab-hello-6"><b>第一步</b></label>
<panel><div>

<!-- Note - Please ONLY submit PRs linking to high-quality, "permanent" sites
            dedicated to learning Rust that work in a browser, are moderately
            condensed, and have a public Git repo and issue tracker.
            Also, this section should be very short <=3 entries, so it should only list
            "the best of their kind".
             -->

**模块化入门资源**
- [**Tour of Rust**](https://tourofrust.com/TOC_en.html) - 代码和解释并排呈现的互动学习资源。
- [**Rust in Easy English**](https://dhghomon.github.io/easy_rust/Chapter_3.html) - 60 多个概念，简易英语，例子丰富。

此外，还可以查看通常的学习资源：{{ book(page="") }} {{ ex(page="") }} {{ std(page="std") }}


> **个人见解** {{ opinionated() }} &mdash; 如果从未见过或使用过任何 Rust 代码，建议先访问以上链接之一，否则下一章可能显得较难理解。

</div></panel></tab>

</tabs>
</noprint>


### Data Structures

使用关键字定义的数据类型和内存位置。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `struct S {}` | 定义一个 **结构体** {{ book(page="ch05-00-structs.html") }} {{ ex(page="custom_types/structs.html") }} {{ std(page="std/keyword.struct.html") }} {{ ref(page="expressions/struct-expr.html") }} 具有命名字段。|
| {{ tab() }} `struct S { x: T }` | 定义一个带有命名字段 `x` 类型为 `T` 的结构体。|
| {{ tab() }} `struct S` &#8203;`(T);` | 定义一个包含编号字段 `.0` 类型为 `T` 的“元组”结构体。|
| {{ tab() }} `struct S;` | 定义 **零大小** {{ nom(page="exotic-sizes.html#zero-sized-types-zsts")}} 的单位结构体。占用空间为零，编译器会优化掉。|
| `enum E {}` | 定义一个**枚举**, {{ book(page="ch06-01-defining-an-enum.html") }} {{ ex(page="custom_types/enum.html#enums") }} {{ ref(page="items/enumerations.html") }} _例如_ [代数数据类型](https://en.wikipedia.org/wiki/Algebraic_data_type), [标签联合](https://en.wikipedia.org/wiki/Tagged_union). |
| {{ tab() }}  `enum E { A, B`&#8203;`(), C {} }` | 定义枚举的变体，可以是单元类型 `A`，元组类型 `B` &#8203;`()`，或结构体类型 `C{}`。|
| {{ tab() }}  `enum E { A = 1 }` | 带有显式 **判别值** 的枚举，{{ ref(page="items/enumerations.html#custom-discriminant-values-for-fieldless-enumerations") }} 例如用于 FFI. |
| {{ tab() }}  `enum E {}` | 没有变体的枚举是 **不可实例化的**，{{ ref(page="glossary.html#uninhabited") }} 不能创建，_类似于_ 'never' {{ below(target="#miscellaneous") }} {{ esoteric() }} |
| `union U {}` | 不安全的类似 C 的 **联合体**  {{ ref(page="items/unions.html") }} 用于与 FFI 兼容。{{ esoteric() }} |
| `static X: T = T();`  | **全局变量** {{ book(page="ch19-01-unsafe-rust.html#accessing-or-modifying-a-mutable-static-variable") }} {{ ex(page="custom_types/constants.html#constants") }} {{ ref(page="items/static-items.html#static-items") }}  具有 `'static` 生命周期，唯一 {{ bad() }}{{ note( note="1") }} 的内存位置。|
| `const X: T = T();`  | 定义 **常量**，{{ book(page="ch03-01-variables-and-mutability.html#constants") }} {{ ex(page="custom_types/constants.html") }} {{ ref(page="items/constant-items.html") }} 在使用时会复制到临时变量中。|
| `let x: T;`  | 在栈上分配 `T` 字节{{ note( note="2") }} 绑定为 `x`。只能赋值一次，不可变。|
| `let mut x: T;`  | 类似于 `let`，但允许 **可变性** {{ book(page="ch03-01-variables-and-mutability.html") }} {{ ex(page="variable_bindings/mut.html") }} 并允许可变借用。{{ note( note="3") }} |
| {{ tab() }} `x = y;` | 将 `y` 移动到 `x`，如果 `T` 不是 **`Copy`**，{{ std(page="std/marker/trait.Copy.html") }} 则 `y` 失效，否则复制 `y`。|

</fixed-2-column>

<footnotes>

<sup>1</sup> 在 _库_ 中，您可能会偷偷地获得多个 `X` 实例，具体取决于您的 crate 是如何导入的。{{ link(url="https://doc.rust-lang.org/cargo/reference/resolver.html#version-incompatibility-hazards") }} <br>
<sup>2</sup> **绑定变量** {{ book(page="ch03-01-variables-and-mutability.html") }} {{ ex(page="variable_bindings.html") }} {{ ref(page="variables.html") }} 对于同步代码，绑定变量位于栈上。在 `async {}` 中，它们成为异步状态机的一部分，可能位于堆上。<br>
<sup>3</sup> 从技术上讲，_可变_ 和 _不可变_ 是误称。不可变绑定或共享引用仍然可能包含 Cell {{ std(page="std/cell/index.html") }}，从而实现 _内部可变性_。

</footnotes>


{{ tablesep() }}

创建和访问数据结构；以及一些更为 _符号化_ 的类型。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `S { x: y }` | 创建 `struct S {}` 或 `use` 过的 `enum E::S {}`，将字段 `x` 设置为 `y`。 |
| `S { x }` | 同样，但使用本地变量 `x` 来作为字段 `x` 的值。 |
| `S { ..s }` | 使用 `s` 填充剩余的字段，尤其适用于 `Default::default()`。{{ std(page="std/default/trait.Default.html") }} |
| `S { 0: x }` | 类似于下面的 `S` &#8203;`(x)`，但使用结构体语法设置字段 `.0`。  |
| `S`&#8203; `(x)` | 创建 `struct S` &#8203;`(T)` 或 `use` 过的 `enum E::S`&#8203; `() `，并将字段 `.0` 设置为 `x`。 |
| `S` | 如果 `S` 是单元结构体 `struct S;` 或 `use` 过的 `enum E::S`，则创建 `S` 的值。 |
| `E::C { x: y }` | 创建枚举变体 `C`。其他方法同样适用。 |
| `()` | 空元组，既是字面量也是类型，亦称为 **单元**。{{ std(page="std/primitive.unit.html") }} |
| `(x)` | 括起来的表达式。 |
| `(x,)` | 单元素 **元组** 表达式。{{ ex(page="primitives/tuples.html") }} {{ std(page="std/primitive.tuple.html") }} {{ ref(page="expressions/tuple-expr.html") }} |
| `(S,)` | 单元素元组类型。 |
| `[S]` | 未指定长度的数组类型，即 **切片**。{{ ex(page="primitives/array.html") }} {{ std(page="std/primitive.slice.html") }} {{ ref(page="types/slice.html") }} 无法驻留在栈上。{{ note( note="*") }} |
| `[S; n]` | 长度为 `n` 的 **数组类型**，其元素类型为 `S`。{{ ex(page="primitives/array.html") }} {{ std(page="std/primitive.array.html") }} {{ ref(page="types/array.html") }} |
| `[x; n]` | **数组实例** {{ ref(page="expressions/array-expr.html") }}（表达式），包含 `n` 个 `x` 的副本。 |
| `[x, y]` | 包含给定元素 `x` 和 `y` 的数组实例。 |
| `x[0]` | 集合索引，这里使用 `usize`。通过 [**Index**](https://doc.rust-lang.org/std/ops/trait.Index.html)，[**IndexMut**](https://doc.rust-lang.org/std/ops/trait.IndexMut.html) 实现。 |
| {{ tab() }} `x[..]` | 使用范围（这里是 _完整范围_）的相同方式，也可以使用 `x[a..b]`、`x[a..=b]`，等等，见下文。  |
| `a..b` | **右开区间** {{ std(page="std/ops/struct.Range.html") }} {{ ref(page="expressions/range-expr.html") }} 创建，例如 `1..3` 表示 `1, 2`。  |
| `..b` | 没有起点的右开 **区间到** {{ std(page="std/ops/struct.RangeTo.html") }}。  |
| `..=b` | 没有起点的 **包含区间到** {{ std(page="std/ops/struct.RangeToInclusive.html") }}。  |
| `a..=b` | **包含区间**，{{ std(page="std/ops/struct.RangeInclusive.html") }} `1..=3` 表示 `1, 2, 3`。 |
| `a..` | 没有终点的 **区间从** {{ std(page="std/ops/struct.RangeFrom.html") }}。  |
| `..` | **完整区间**，{{ std(page="std/ops/struct.RangeFull.html") }} 通常表示 _整个集合_。   |
| `s.x` | 命名 **字段访问**，{{ ref(page="expressions/field-expr.html") }} 如果 `x` 不是 `S` 类型的一部分，可能会尝试 [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html)。 |
| `s.0` | 数字字段访问，适用于元组类型 `S` &#8203;`(T)`。 |

</fixed-2-column>

<footnotes>

<sup>*</sup> 目前，{{ rfc( page ="1909-unsized-rvalues.html") }}，等待 [跟踪问题](https://github.com/rust-lang/rust/issues/48055) 的完成。

</footnotes>


### References & Pointers

授予对非所有内存的访问权限。另请参阅泛型 & 约束部分。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `&S` | 共享 **引用** {{ book(page="ch04-02-references-and-borrowing.html") }} {{ std(page="std/primitive.reference.html") }} {{ nom(page="references.html")}} {{ ref(page="types.html#pointer-types")}}（类型；用于保存 _任意_ `&s` 的空间）。 |
| {{ tab() }} `&[S]` | 特殊的切片引用，包含（`地址`，`数量`）。 |
| {{ tab() }} `&str` | 特殊的字符串切片引用，包含（`地址`，`字节长度`）。 |
| {{ tab() }} `&mut S` | 排他性引用，允许可变性（也包括 `&mut [S]`，`&mut dyn S`，等等）。 |
| {{ tab() }} `&dyn T` | 特殊的 **特征对象** {{ book(page="ch17-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types") }} 引用，包含（`地址`，`虚函数表`）。 |
| `&s` | 共享 **借用** {{ book(page="ch04-02-references-and-borrowing.html") }} {{ ex(page="scope/borrow.html") }} {{ std(page="std/borrow/trait.Borrow.html") }}（例如，_这个_ `s` 的地址、长度、虚函数表等，如 `0x1234`）。 |
| {{ tab() }} `&mut s` | 允许 **可变性** 的排他性借用。{{ ex(page="scope/borrow/mut.html") }} |
| `*const S` | 不可变 **原始指针类型** {{ book(page="ch19-01-unsafe-rust.html#dereferencing-a-raw-pointer") }} {{ std(page="std/primitive.pointer.html") }} {{ ref(page="types.html#raw-pointers-const-and-mut") }}，没有内存安全性。 |
| {{ tab() }} `*mut S` | 可变的原始指针类型，没有内存安全性。 |
| {{ tab() }} `&raw const s` | 创建原始指针，而不通过引用；_参考_ `ptr:addr_of!()` {{ std(page="std/ptr/macro.addr_of.html") }} {{ esoteric() }}  |
| {{ tab() }} `&raw mut s` | 相同，但可变。{{ experimental() }} 适用于未对齐、打包的字段。{{ esoteric() }} |
| `ref s` | **通过引用绑定**，{{ ex(page="scope/borrow/ref.html") }} 使绑定为引用类型。{{ deprecated() }}|
| {{ tab() }} `let ref r = s;` | 等价于 `let r = &s`。 |
| {{ tab() }} `let S { ref mut x } = s;` | 可变引用绑定（`let x = &mut s.x`），简写解构 {{ below( target = "#pattern-matching") }} 版本。 |
| `*r` | **解引用** {{ book(page="ch15-02-deref.html") }} {{ std(page="std/ops/trait.Deref.html") }} {{ nom(page="vec-deref.html") }} 引用 `r` 以访问其指向的内容。 |
| {{ tab() }} `*r = s;` | 如果 `r` 是可变引用，将 `s` 移动或复制到目标内存。 |
| {{ tab() }} `s = *r;` | 如果 `r` 引用的是 `Copy` 类型，则将 `s` 设为 `r` 引用内容的副本。 |
| {{ tab() }} `s = *r;` | 如果 `*r` 不是 `Copy`，将不起作用 {{ bad() }}，因为这会移动并留下空值。 |
| {{ tab() }} `s = *my_box;` | **`Box`** 的特殊情况 {{ link(url="https://web.archive.org/web/20230130111147/https://old.reddit.com/r/rust/comments/b4so6i/what_is_exactly/ej8xwg8/") }} 可以移出内容，而不是 `Copy`。{{ std(page="std/boxed/index.html") }} |
| `'a`  | **生命周期参数**，{{ book(page="ch10-00-generics.html") }} {{ ex(page="scope/lifetime.html")}} {{ nom(page="lifetimes.html") }} {{ ref(page="items/generics.html#type-and-lifetime-parameters")}} 在静态分析中表示流程的持续时间。<sup>1</sup> |
| {{ tab() }}  `&'a S`  | 只接受某个 `s` 的地址；地址存在 `'a` 或更长时间。 |
| {{ tab() }}  `&'a mut S`  | 相同，但允许修改地址内容。 |
| {{ tab() }}  `struct S<'a> {}`  | 表明此 `S` 将包含生命周期为 `'a` 的地址。`S` 的创建者决定 `'a`。 |
| {{ tab() }} `trait T<'a> {}` | 表明任何实现了 `T` 的 `S` 可能包含地址。 |
| {{ tab() }}  `fn f<'a>(t: &'a T)`  | 表明此函数处理某个地址，调用者决定 `'a`。 |
| `'static`  | 特殊生命周期，持续整个程序执行时间。 |

</fixed-2-column>

<footnotes>

<sup>1</sup> 如果这还不太明白，可以粗略地将 Rust 的生命周期理解为“打印在纸上的一些代码行，您可以在页面左边的边缘用黄色荧光笔连续标记的那几行”。<br>

</footnotes>



###  Functions & Behavior

定义代码单元及其抽象。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `trait T {}`  | 定义一个 **trait**；{{ book(page="ch10-02-traits.html") }} {{ ex(page="trait.html") }} {{ ref(page="items/traits.html") }} 类型可以遵循的通用行为。 |
| `trait T : R {}` | `T` 是 **超 trait** 的子 trait {{ book(page="ch19-03-advanced-traits.html#using-supertraits-to-require-one-traits-functionality-within-another-trait") }} {{ ex(page="trait/supertraits.html") }} {{ ref(page="items/traits.html#supertraits") }} `R`。任何 `S` 必须先实现 `R` 才能实现 `T`。 |
| `impl S {}`  | **实现** {{ ref(page="items/implementations.html") }} 类型 `S` 的功能，例如方法。 |
| `impl T for S {}`  | 为类型 `S` 实现 trait `T`；指定 `S` 如何具体表现为 `T`。 |
| `impl !T for S {}` | 禁用自动派生的 **自动 trait**。{{ nom(page="send-and-sync.html") }} {{ ref(page="special-types-and-traits.html#auto-traits") }} {{ experimental() }} {{ esoteric() }} |
| `fn f() {}`  | 定义一个 **函数**；{{ book(page="ch03-03-how-functions-work.html") }} {{ ex(page="fn.html") }} {{ ref(page="items/functions.html") }} 或如果在 `impl` 内则为关联函数。 |
| {{ tab() }} `fn f() -> S {}`  | 相同，返回一个类型为 `S` 的值。 |
| {{ tab() }} `fn f(&self) {}`  | 定义一个 **方法**，{{ book(page="ch05-03-method-syntax.html") }} {{ ex(page="fn/methods.html") }} {{ ref(page="items/associated-items.html#methods") }} 例如在 `impl S {}` 内。 |
| `struct S` &#8203;`(T);` | 更神秘地说，也 {{ above(target="#data-structures") }} 定义了 `fn S(x: T) -> S` **构造函数**。{{ rfc(page="1506-adt-kinds.html#tuple-structs") }} {{ esoteric() }} |
| `const fn f() {}`  | 常量 `fn` 可在编译时使用，例如 `const X: u32 = f(Y)`。{{ ref(page="const_eval.html#const-functions") }} {{ edition(ed="'18") }}|
| {{ tab() }} `const { x }`  | 用在函数内，确保 `{ x }` 在编译期间求值。{{ ref(page="expressions/block-expr.html#const-blocks") }} |
| `async fn f() {}`  | **异步** {{ ref(page="items/functions.html#async-functions") }} {{ edition(ed="'18") }} 函数转换，{{ below(target="#async-await-101") }} 使 `f` 返回一个 `impl` **`Future`**。{{ std(page="std/future/trait.Future.html") }} |
| {{ tab() }} `async fn f() -> S {}`  | 相同，但使 `f` 返回一个 `impl Future<Output=S>`。 |
| {{ tab() }} `async { x }`  | 用在函数内，使 `{ x }` 成为 `impl Future<Output=X>`。{{ ref(page="expressions/block-expr.html#async-blocks") }} |
| {{ tab() }} `async move { x }`  | 将捕获的变量移动到 future 中，_参考_ move 闭包。{{ ref(page="expressions/block-expr.html#capture-modes") }} {{ below(target="#functions-behavior") }} |
| `fn() -> S`  | **函数引用**，<sup>1</sup> {{ book(page="ch19-05-advanced-functions-and-closures.html#function-pointers") }} {{ std(page="std/primitive.fn.html") }} {{ ref(page="types.html#function-pointer-types") }} 内存中保存可调用的地址。 |
| `Fn() -> S`  | **可调用 Trait** {{ book(page="ch19-05-advanced-functions-and-closures.html#returning-closures") }} {{ std(page="std/ops/trait.Fn.html") }}（也包括 `FnMut`，`FnOnce`），由闭包、函数实现等。 |
| <code>&vert;&vert; {}</code> | 一个 **闭包** {{ book(page="ch13-01-closures.html") }} {{ ex(page="fn/closures.html") }} {{ ref(page="expressions/closure-expr.html")}}，借用其 **捕获的变量**，{{ below(target="#closures-data") }} {{ ref(page="types/closure.html#capture-modes") }}（例如一个本地变量）。 |
| {{ tab() }} <code>&vert;x&vert; {}</code> | 接受一个名为 `x` 的参数的闭包，主体是一个块表达式。 |
| {{ tab() }} <code>&vert;x&vert; x + x</code> | 相同，但没有块表达式；只能包含一个表达式。 |
| {{ tab() }} <code>move &vert;x&vert; x + y </code> | **移动闭包** {{ ref(page="types/closure.html#capture-modes")}} 获取所有权；即 `y` 被转移到闭包中。 |
| {{ tab() }} <code> return &vert;&vert; true </code> | 闭包有时看起来像逻辑或（这里：返回一个闭包）。 |
| `unsafe` | 如果您喜欢调试段错误；**不安全代码**。{{ below(target="#unsafe-unsound-undefined") }} {{ book(page="ch19-01-unsafe-rust.html#unsafe-superpowers") }} {{ ex(page="unsafe.html#unsafe-operations") }} {{ nom(page="meet-safe-and-unsafe.html") }} {{ ref(page="unsafe-blocks.html#unsafe-blocks") }} |
| {{ tab() }} `unsafe fn f() {}` | 意味着“_调用可能导致未定义行为，{{ below(target="#unsafe-unsound-undefined") }} **您必须检查** 要求_”。 |
| {{ tab() }} `unsafe trait T {}` | 意味着“_不小心实现 `T` 可能导致未定义行为_；**实现者必须检查**”。 |
| {{ tab() }} `unsafe { f(); }` | 向编译器保证“_**我已经检查了** 要求，相信我_”。 |
| {{ tab() }} `unsafe impl T for S {}` | 保证“_`S` 在 `T` 方面表现良好_”；人们可以在 `S` 上安全地使用 `T`。 |
| {{ tab() }} `unsafe extern "abi" {}` | 从 Rust 2024 开始，`extern "abi" {}` 块 {{ below(target="#organizing-code")}} 必须是 `unsafe`。 |
| {{ tab() }} {{ tab() }} `pub safe fn f();`  | 在 `unsafe extern "abi" {}` 中，标记 `f` 实际上是安全的。{{ rfc(page="3484-unsafe-extern-blocks.html") }} |

</fixed-2-column>

<footnotes>

<sup>1</sup> 大多数文档称它们为函数 **指针**，但函数 **引用** 可能更合适{{ link(url="https://users.rust-lang.org/t/why-are-function-pointers-special-no-null/87990/16") }}，因为它们不能是 `null`，且必须指向有效目标。

</footnotes>

### Control Flow

控制函数内的执行。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `while x {}`  | **循环**，{{ ref(page="expressions/loop-expr.html#predicate-loops") }} 当表达式 `x` 为真时运行。 |
| `loop {}`  | **无限循环** {{ ref(page="expressions/loop-expr.html#infinite-loops") }} 直到 `break`。可以通过 `break x` 生成一个值。 |
| `for x in collection {}` | 语法糖，用于遍历 **迭代器**。{{ book(page="ch13-02-iterators.html") }} {{ std(page="std/iter/index.html") }} {{ ref(page="expressions/loop-expr.html#iterator-loops") }} |
| <less-important> {{ tab() }} {{ expands_to()}} `collection.into_iter()` </less-important> | <less-important>有效地将任何 **`IntoIterator`** {{ std(page="std/iter/trait.IntoIterator.html") }} 类型首先转换为合适的迭代器。</less-important> |
| <less-important> {{ tab() }} {{ expands_to()}} `iterator.next()` </less-important> | <less-important>对于合适的 **`Iterator`** {{ std(page="std/iter/trait.Iterator.html") }} 然后 `x = next()` 直到耗尽（首次 `None`）。</less-important> |
| `if x {} else {}`  | **条件分支** {{ ref(page="expressions/if-expr.html") }} 如果表达式为真。 |
| `'label: {}` | **块标签**，{{ rfc(page="2046-label-break-value.html" )}} 可以与 `break` 一起使用以退出此块。{{ edition(ed="1.65+")}} |
| `'label: loop {}` | 类似的 **循环标签**，{{ ex(page="flow_control/loop/nested.html") }} {{ ref(page="expressions/loop-expr.html#loop-labels")}} 在嵌套循环中对流控制很有用。 |
| `break`  | **中断表达式** {{ ref(page="expressions/loop-expr.html#break-expressions") }} 用于退出标记的块或循环。 |
| {{ tab() }} `break 'label x`  | 跳出名为 `'label` 的块或循环，并将 `x` 作为其值。 |
| {{ tab() }} `break 'label`  | 相同，但不生成任何值。 |
| {{ tab() }} `break x`  | 将 `x` 作为最内层循环的值（仅在实际的 `loop` 中）。 |
| `continue `  | **继续表达式** {{ ref(page="expressions/loop-expr.html#continue-expressions") }} 进入此循环的下一次迭代。 |
| `continue 'label`  | 相同，但不是这个循环，而是标记为 'label 的外层循环。 |
| `x?` | 如果 `x` 是 [Err](https://doc.rust-lang.org/std/result/enum.Result.html#variant.Err) 或 [None](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None)，则 **返回并传播**。{{ book(page="ch09-02-recoverable-errors-with-result.html#propagating-errors") }} {{ ex(page="error/result/enter_question_mark.html") }} {{ std(page="std/result/index.html#the-question-mark-operator-") }} {{ ref(page="expressions/operator-expr.html#the-question-mark-operator")}} |
| `x.await` | 语法糖用于 **获取 future，轮询，yield**。{{ ref(page="expressions/await-expr.html#await-expressions") }} {{ edition(ed="'18") }} 只能在 `async` 中使用。 |
| <less-important> {{ tab() }} {{ expands_to()}} `x.into_future()` </less-important> | <less-important>有效地将任何 **`IntoFuture`** {{ std(page="std/future/trait.IntoFuture.html") }} 类型首先转换为合适的 future。</less-important> |
| <less-important> {{ tab() }} {{ expands_to()}} `future.poll()` </less-important> | <less-important>对于合适的 **`Future`** {{ std(page="std/future/trait.Future.html") }} 然后 `poll()` 并在 **`Poll::Pending`** 时 yield 流。{{ std(page="std/task/enum.Poll.html") }}</less-important> |
| `return x`  | **提前返回** {{ ref(page="expressions/return-expr.html" ) }} 结束函数。更惯用的做法是以表达式结束。 |
| {{ tab() }} `{ return }`  | 在普通 `{}` 块内 `return` 退出周围的函数。 |
| {{ tab() }} <code>&vert;&vert; { return }</code>  | 在闭包中 `return` 只退出该闭包，即闭包是 _s. fn._。 |
| {{ tab() }} `async { return }`  | 在 `async` 中，`return` **只能** {{ ref(page="expressions/block-expr.html#control-flow-operators") }} {{ bad() }} 退出该 `{}`，即 `async {}` 是 _s. fn._。 |
| `f()` | 调用可调用的 `f`（例如函数、闭包、函数指针、`Fn` 等）。 |
| `x.f()` | 调用成员函数，要求 `f` 以 `self`，`&self` 等作为第一个参数。 |
| {{ tab() }} `X::f(x)` | 等同于 `x.f()`。除非 `impl Copy for X {}`，否则 `f` 只能被调用一次。 |
| {{ tab() }} `X::f(&x)` | 等同于 `x.f()`。 |
| {{ tab() }} `X::f(&mut x)` | 等同于 `x.f()`。 |
| {{ tab() }} `S::f(&x)` | 如果 `X` [解引用](https://doc.rust-lang.org/std/ops/trait.Deref.html) 到 `S`，即 `x.f()` 查找 `S` 的方法，则与 `x.f()` 相同。 |
| {{ tab() }} `T::f(&x)` | 如果 `X impl T`，即 `x.f()` 在作用域内查找 `T` 的方法，则与 `x.f()` 相同。 |
| `X::f()` | 调用关联函数，例如 `X::new()`。 |
| {{ tab() }} `<X as T>::f()` | 调用为 `X` 实现的 trait 方法 `T::f()`。 |

</fixed-2-column>



### Organizing Code

将项目划分为更小的单元并最小化依赖性。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `mod m {}`  | 定义一个 **模块**，{{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }} {{ ex(page="mod.html#modules") }} {{ ref(page="items/modules.html#modules") }} 从 `{}` 内部获取定义。{{ below(target="#project-anatomy") }} |
| `mod m;`  | 定义一个模块，从 `m.rs` 或 `m/mod.rs` 中获取定义。{{ below(target="#project-anatomy") }}|
| `a::b` | 命名空间 **路径** {{ ex(page="mod/use.html") }} {{ ref(page="paths.html")}} 到 `a` 中的元素 `b`（`mod`，`enum` 等）。 |
| {{ tab() }} `::b` | 在 **crate 根** {{ edition(ed="'15") }} {{ ref(page="glossary.html#crate")}} 或 **外部预导入** 中查找 `b`；{{ edition(ed="'18") }} {{ ref(page="names/preludes.html#extern-prelude")}} **全局路径**。{{ ref(page="paths.html#path-qualifiers")}} {{ deprecated() }}  |
| {{ tab() }} `crate::b` | 在 crate 根中查找 `b`。{{ edition(ed="'18") }} |
| {{ tab() }} `self::b`  | 在当前模块中查找 `b`。 |
| {{ tab() }} `super::b`  | 在父模块中查找 `b`。 |
| `use a::b;`  | **使用** {{ ex(page="mod/use.html#the-use-declaration") }} {{ ref(page="items/use-declarations.html") }} `b` 直接在此作用域中使用，无需再使用 `a`。 |
| `use a::{b, c};` | 同样，但将 `b` 和 `c` 引入作用域。 |
| `use a::b as x;`  | 将 `b` 引入作用域，但命名为 `x`，如 `use std::error::Error as E`。 |
| `use a::b as _;`  | 将 `b` 匿名引入作用域，适用于具有冲突名称的特征。 |
| `use a::*;`  | 将 `a` 中的所有内容引入，仅当 `a` 是某种 **预导入** 时推荐使用。{{ std(page="std/prelude/index.html#other-preludes")}} {{ link(url="https://stackoverflow.com/questions/36384840/what-is-the-prelude") }} |
| `pub use a::b;`  | 将 `a::b` 引入作用域并从此处重新导出。 |
| `pub T`  | “如果父路径是公共的，则为公共的” **可见性** {{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }} {{ ref(page="visibility-and-privacy.html")}} 适用于 `T`。  |
| {{ tab() }} `pub(crate) T` | 至多在当前 crate 中可见<sup>1</sup>。  |
| {{ tab() }} `pub(super) T`  | 至多在父模块中可见<sup>1</sup>。  |
| {{ tab() }} `pub(self) T`  | 至多在当前模块中可见（默认值，与没有 `pub` 相同）<sup>1</sup>。  |
| {{ tab() }} `pub(in a::b) T`  | 至多在祖先 `a::b` 中可见<sup>1</sup>。  |
| `extern crate a;` | 声明对外部 **crate** 的依赖；{{ book(page="ch02-00-guessing-game-tutorial.html#using-a-crate-to-get-more-functionality") }} {{ ref(page="items/extern-crates.html#extern-crate-declarations") }} {{ deprecated() }} 在 {{ edition(ed="'18") }} 中只需 `use a::b`。  |
| `extern "C" {}`  | _声明_ 外部依赖和 ABI（例如 `"C"`），用于 **FFI**。{{ book(page="ch19-01-unsafe-rust.html#using-extern-functions-to-call-external-code") }} {{ ex(page="std_misc/ffi.html#foreign-function-interface") }} {{ nom(page="ffi.html#calling-foreign-functions") }} {{ ref(page="items/external-blocks.html#external-blocks") }} |
| `extern "C" fn f() {}`  | _定义_ 要导出到 FFI 的具有 ABI（例如 `"C"`）的函数。 |

</fixed-2-column>

<footnotes>

<sup>1</sup> 子模块中的项目始终可以访问任何项目，无论是否为 `pub`。

</footnotes>


### Type Aliases and Casts

类型的简写名称以及将一种类型转换为另一种类型的方法。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `type T = S;`  | 创建一个 **类型别名**，{{ book(page="ch19-04-advanced-types.html#creating-type-synonyms-with-type-aliases") }} {{ ref(page="items/type-aliases.html#type-aliases") }} 即 `S` 的另一个名称。 |
| `Self`  | **实现类型**的类型别名，{{ ref(page="types.html#self-types") }} 例如 `fn new() -> Self`。 |
| `self`  | **方法主体** {{ book(page="ch05-03-method-syntax.html#method-syntax") }} {{ ref(page="items/associated-items.html#methods") }} 在 `fn f(self) {}` 中，例如类似于 `fn f(self: Self) {}`。 |
|  {{ tab() }}  `&self`  | 相同，但引用 self，等同于 `f(self: &Self)`。 |
|  {{ tab() }}  `&mut self`  | 相同，但可变引用 self，等同于 `f(self: &mut Self)`。 |
|  {{ tab() }}  `self: Box<Self>`  | [**任意 self 类型**](https://github.com/withoutboats/rfcs/blob/arbitray-receivers/text/0000-century-of-the-self-type.md)，为智能指针添加方法（例如 `my_box.f_of_self()`）。 |
| `<S as T>`  | **消除歧义** {{ book(page="ch19-03-advanced-traits.html#fully-qualified-syntax-for-disambiguation-calling-methods-with-the-same-name") }} {{ ref(page="expressions/call-expr.html#disambiguating-function-calls") }} 类型 `S` 作为 trait `T`，例如 `<S as T>::f()`。 |
| `a::b as c`  | 在符号的 `use` 中，将 `S` 导入为 `R`，例如 `use a::S as R`。 |
| `x as u32`  | 基本类型 **转换**，{{ ex(page="types/cast.html#casting") }} {{ ref(page="expressions/operator-expr.html#type-cast-expressions") }} 可能会截断且有点令人意外。<sup>1</sup> {{ nom(page="casts.html") }} |

</fixed-2-column>

<footnotes>

<sup>1</sup> 请参阅下面的 [**类型转换**](#type-conversions)，了解在类型之间进行转换的所有方式。

</footnotes>



### Macros & Attributes

在实际编译之前扩展的代码生成结构。

<fixed-2-column>

| 示例 |  解释 |
|---------|---------|
| `m!()` |  **宏** {{ book(page="ch19-06-macros.html") }} {{std(page="std/index.html#macros")}} {{ ref(page="macros.html") }} 调用，也可以是 `m!{}`，`m![]`（取决于宏的类型）。 |
| `#[attr]`  | 外部 **属性**，{{ex(page="attribute.html")}} {{ref(page="attributes.html")}} 注释接下来的项目。 |
| `#![attr]` | 内部属性，注释 _上层_ 的包围项。 |

</fixed-2-column>

{{ tablesep() }}

<fixed-2-column class="color-header special_example">

| 宏内部 <sup>1</sup> |  解释 |
|---------|---------|
| `$x:ty`  | 宏捕获，`:ty` **片段说明符** {{ ref(page="macros-by-example.html#metavariables") }} <sup>,2</sup> 声明 `$x` 可以是什么。 |
| `$x` |  宏替换，例如，使用上面捕获的 `$x:ty`。 |
| `$(x),*` | 宏 **重复** {{ ref(page="macros-by-example.html#repetitions") }} _零次或多次_。|
| {{ tab() }} `$(x),+` | 相同，但 _一次或多次_。 |
| {{ tab() }} `$(x)?` | 相同，但 _零次或一次_（分隔符不适用）。 |
| {{ tab() }} `$(x)<<+` | 实际上，除了 `,` 以外的分隔符也可以接受。这里是：`<<`。 |

</fixed-2-column>

<footnotes>

<sup>1</sup> 适用于 **'示例宏'**。{{ ref(page="macros-by-example.html") }} <br>
<sup>2</sup> 请参阅下面的 [**工具指令**](#tooling-directives) 以获取所有片段说明符。

</footnotes>



### Pattern Matching

在 `match` 或 `let` 表达式中或函数参数中的构造。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `match m {}` | 发起 **模式匹配**，{{ book(page="ch06-02-match.html") }} {{ ex(page="flow_control/match.html") }} {{ ref(page="expressions/match-expr.html") }} 然后使用匹配分支，参考下表。 |
| `let S(x) = get();`  | 值得注意的是，`let` 也可以 **解构** {{ ex(page="flow_control/match/destructuring.html") }}，类似于下表。 |
|  {{ tab() }} `let S { x } = s;` | 只有 `x` 会绑定到值 `s.x`。 |
|  {{ tab() }} `let (_, b, _) = abc;` | 只有 `b` 会绑定到值 `abc.1`。 |
|  {{ tab() }} `let (a, ..) = abc;` | 忽略“其余部分”也是可行的。 |
|  {{ tab() }} `let (.., a, b) = (1, 2);` | 特定绑定优先于“其余部分”，这里 `a` 是 `1`，`b` 是 `2`。 |
|  {{ tab() }} `let s @ S { x } = get();`  | 绑定 `s` 到 `S`，同时 `x` 绑定到 `s.x`，**模式绑定**，{{ book(page="ch18-03-pattern-syntax.html#-bindings") }} {{ ex(page="flow_control/match/binding.html#binding") }} {{ ref(page="patterns.html#identifier-patterns") }} 参考下文 {{ esoteric() }} |
|  {{ tab() }} `let w @ t @ f = get();`  | 将 `get()` 结果的 3 份副本分别存储在 `w`，`t`，`f` 中。{{ esoteric() }} |
|  {{ tab() }} <code>let (&vert;x&vert; x) = get();</code> | 病态或模式，{{ below(target="#pattern-matching")}} **不是** 闭包。{{ bad() }} 相当于 `let x = get();` {{ esoteric() }}  |
| `let Ok(x) = f();` | 如果模式可以 **被驳斥**，则 **不会** 工作 {{ bad() }}，{{ ref(page="expressions/if-expr.html#if-let-expressions") }} 使用 `let else` 或 `if let` 替代。 |
| `let Ok(x) = f();` | 但如果没有其他可实例化的模式，例如 `f` 返回 `Result<T, !>`，则可以工作 {{ edition(ed="1.82+") }} |
| `let Ok(x) = f() else {};`  | 尝试赋值 {{ rfc(page="3137-let-else.html") }}，如果不是则 `else {}` 必须 `break`，`return`，`panic!`，等等 {{ edition(ed="1.65+")}} {{ hot() }} |
| `if let Ok(x) = f() {}`  | 如果模式可以被赋值（例如，`enum` 变体），则进行分支，语法糖。 <sup>*</sup>|
| `while let Ok(x) = f() {}`  | 等价；这里不断调用 `f()`，只要模式可以被赋值就运行 `{}`。 |
| `fn f(S { x }: S)`  | 函数参数也可以像 `let` 一样工作，这里 `x` 绑定到 `f(s)` 的 `s.x`。 {{ esoteric() }} |

</fixed-2-column>

<footnotes>

<sup>*</sup> 语法糖转换为 `match get() { Some(x) => {}, _ => () }`。

</footnotes>

{{ tablesep() }}

`match` 表达式中的模式匹配分支。这些分支的左侧也可以出现在 `let` 表达式中。

<fixed-2-column class="color-header special_example">

| 匹配分支内 | 解释 |
|---------|-------------|
|  `E::A => {}` | 匹配枚举变体 `A`，参考 **模式匹配**。{{ book(page="ch06-02-match.html") }} {{ ex(page="flow_control/match.html") }} {{ ref(page="expressions/match-expr.html") }} |
|  `E::B ( .. ) => {}` | 匹配枚举元组变体 `B`，忽略任何索引。 |
|  `E::C { .. } => {}` | 匹配枚举结构变体 `C`，忽略任何字段。 |
|  `S { x: 0, y: 1 } => {}` | 匹配具有特定值的结构体（仅 `s` 的 `s.x` 为 `0`，`s.y` 为 `1`）。 |
|  `S { x: a, y: b } => {}` | 匹配具有 _任意_ {{ bad() }} 值的结构体，并将 `s.x` 绑定到 `a`，`s.y` 绑定到 `b`。 |
|  {{ tab() }} `S { x, y } => {}` | 相同，但简写形式，将 `s.x` 和 `s.y` 分别绑定为 `x` 和 `y`。 |
|  `S { .. } => {}` | 匹配具有任意值的结构体。 |
|  `D => {}` | 匹配枚举变体 `E::D`，如果 `D` 在 `use` 中。 |
|  `D => {}` | 匹配任何东西，绑定 `D`；可能是 `E::D` 的假朋友 {{ bad() }}，如果 `D` 不在 `use` 中。 |
|  `_ => {}` | 正确的通配符，匹配任何东西 / “所有其他”。 |
| <code>0 &vert; 1 => {}</code> | 模式替代，**或模式**。{{ rfc( page ="2535-or-patterns.html") }}|
| {{ tab() }}  <code>E::A &vert; E::Z => {}</code> | 相同，但用于枚举变体。 |
| {{ tab() }}  <code>E::C {x} &vert; E::D {x} => {}</code> | 相同，但如果所有变体都有 `x`，则绑定 `x`。 |
| {{ tab() }}  <code>Some(A &vert; B) => {}</code> | 相同，也可以匹配深层嵌套的替代项。 |
| {{ tab() }}  <code>&vert;x&vert; x => {}</code> | **病态或模式**，{{ above(target="#pattern-matching")}}{{bad()}} 前面的 <code>&vert;</code> 被忽略，实际上是 <code>x &vert; x</code>，因此是 <code>x</code>。 {{esoteric()}}
|  `(a, 0) => {}` | 匹配元组，第一个元素为 `a`，第二个元素为 `0`。 |
|  `[a, 0] => {}` | **切片模式**，{{ ref(page="patterns.html#slice-patterns") }} {{ link(url="https://doc.rust-lang.org/edition-guide/rust-2018/slice-patterns.html") }} 匹配数组，第一个元素为 `a`，第二个元素为 `0`。 |
|  {{ tab() }} `[1, ..] => {}` | 匹配以 `1` 开头的数组，其余为任意值；**子切片模式**。{{ ref(page="patterns.html#rest-patterns") }} {{ rfc(page="2359-subslice-pattern-syntax.html") }} |
|  {{ tab() }} `[1, .., 5] => {}` | 匹配以 `1` 开头、以 `5` 结尾的数组。 |
|  {{ tab() }} `[1, x @ .., 5] => {}` | 相同，但也将 `x` 绑定到表示中间部分的切片（参考模式绑定）。 |
|  {{ tab() }} `[a, x @ .., b] => {}` | 相同，但匹配任意第一个和最后一个，分别绑定为 `a`，`b`。 |
|  `1 .. 3 => {}` | **范围模式**，{{ book(page="ch18-03-pattern-syntax.html#matching-ranges-of-values-with-") }} {{ ref(page="patterns.html#range-patterns") }} 这里匹配 `1` 和 `2`；部分不稳定。{{ experimental() }} |
|  {{ tab() }} `1 ..= 3 => {}` | 包含范围模式，匹配 `1`，`2` 和 `3`。 |
|  {{ tab() }} `1 .. => {}` | 开放范围模式，匹配 `1` 和任何更大的数。 |
| `x @ 1..=5 => {}` | 将匹配绑定到 `x`；**模式绑定**，{{ book(page="ch18-03-pattern-syntax.html#-bindings") }} {{ ex(page="flow_control/match/binding.html#binding") }} {{ ref(page="patterns.html#identifier-patterns") }} 这里 `x` 会是 `1` &hellip; `5`。 |
| {{ tab() }} `Err(x @ Error {..}) => {}` | 嵌套使用也是可行的，这里 `x` 绑定到 `Error`，尤其适用于下面的 `if`。 |
| `S { x } if x > 10 => {}`  | 模式 **匹配守卫**，{{ book(page="ch18-03-pattern-syntax.html#extra-conditionals-with-match-guards")}} {{ ex(page="flow_control/match/guard.html#guards")}} {{ ref(page="expressions/match-expr.html#match-guards") }} 条件也必须为真才能匹配。 |

</fixed-2-column>

### Generics & Constraints

泛型结合类型构造器、特征和函数，为用户提供更多的灵活性。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `struct S<T> …`  | 一个带有类型参数的 **泛型** {{ book(page="ch10-01-syntax.html") }} {{ ex(page="generics.html") }} 类型（`T` 在这里是占位符）。 |
| `S<T> where T: R`  | **特征约束**，{{ book(page="ch10-02-traits.html#using-trait-bounds-to-conditionally-implement-methods") }} {{ ex(page="generics/bounds.html") }} {{ ref(page="trait-bounds.html#trait-and-lifetime-bounds" ) }} 限制允许的 `T`，保证 `T` 具有特征 `R`。 |
| {{ tab() }} `where T: R, P: S`  | **独立的特征约束**，这里一个用于 `T`，一个用于（未显示）`P`。|
| {{ tab() }} `where T: R, S`  | 编译错误，{{ bad() }} 你可能需要下面的复合约束 `R + S`。 |
| {{ tab() }} `where T: R + S`  | **复合特征约束**，{{ book(page="ch10-02-traits.html#specifying-multiple-trait-bounds-with-the--syntax") }} {{ ex(page="generics/multi_bounds.html") }} `T` 必须满足 `R` 和 `S`。 |
| {{ tab() }} `where T: R + 'a`  | 相同，但加上了生命周期。`T` 必须满足 `R`，如果 `T` 有生命周期，必须比 `'a` 活得更久。 |
| {{ tab() }} `where T: ?Sized` | 选择退出预定义的特征约束，这里是 `Sized`。{{ todo() }} |
| {{ tab() }} `where T: 'a` | 类型的 **生命周期约束**；{{ ex(page="scope/lifetime/lifetime_bounds.html") }} 如果 T 有引用，它们必须比 `'a` 活得更久。  |
| {{ tab() }} `where T: 'static` | 相同；这并 **不** 意味着值 `t` **将** {{ bad() }} 活到 `'static`，只是说它可以。 |
| {{ tab() }} `where 'b: 'a` | 生命周期 `'b` 必须至少比 `'a` 活得更久（即 **超出** `'a` 的约束）。 |
| {{ tab() }} `where u8: R<T>`  | 还可以对其他类型进行条件语句。{{ esoteric() }} |
| `S<T: R>`  | 简写的约束，几乎与上面相同，书写更简短。 |
| `S<const N: usize>` | **泛型常量约束**；{{ ref(page="items/generics.html#const-generics") }} `S` 类型的使用者可以提供常量值 `N`。 |
| {{ tab() }} `S<10>` | 在使用时，可以将常量约束提供为基本值。 |
| {{ tab() }} `S<{5+5}>` | 表达式必须放在花括号中。 |
| `S<T = R>` | **默认参数**；{{ book(page="ch19-03-advanced-traits.html#default-generic-type-parameters-and-operator-overloading") }} 使 `S` 更易于使用，但保持灵活性。 |
| {{ tab() }} `S<const N: u8 = 0>` | 常量的默认参数，例如在 `f(x: S) {}` 中参数 `N` 为 `0`。 |
| {{ tab() }} `S<T = u8>` | 类型的默认参数，例如在 `f(x: S) {}` 中参数 `T` 为 `u8`。 |
| `S<'_>` | 推断的 **匿名生命周期**；请求编译器在明显的情况下 **'自动推断'**。  |
| `S<_>` | 推断的 **匿名类型**，例如，`let x: Vec<_> = iter.collect()`。 |
| `S::<T>` | **Turbofish** {{ std(page="std/iter/trait.Iterator.html#method.collect")}} 调用站点类型消除歧义，例如 `f::<u32>()`。 |
| `trait T<X> {}`  | 一个泛型 `X` 的特征。可以有多个 `impl T for S`（每个 `X` 一个）。 |
| `trait T { type X; }`  | 定义 **关联类型** {{ book(page="ch19-03-advanced-traits.html#specifying-placeholder-types-in-trait-definitions-with-associated-types") }} {{ ref(page="items/associated-items.html#associated-types") }} {{ rfc(page="0195-associated-items.html") }} `X`。只能有一个 `impl T for S`。 |
| `trait T { type X<G>; }`  | 定义 **泛型关联类型**（GAT），{{ rfc(page="1598-generic_associated_types.html") }} `X` 可以是泛型 `Vec<>`。 |
| `trait T { type X<'a>; }`  | 定义一个泛型关联类型（GAT）具有生命周期。 |
| {{ tab() }} `type X = R;`  | 在 `impl T for S { type X = R; }` 中设置关联类型。 |
| {{ tab() }} `type X<G> = R<G>;`  | GAT 的相同形式，例如 `impl T for S { type X<G> = Vec<G>; }`。 |
| `impl<T> S<T> {}`  | 为 `S<T>` 实现任何 `T` 的方法 **_泛型化_**，{{ ref(page="items/implementations.html#generic-implementations") }} 这里 `T` 是类型参数。 |
| `impl S<T> {}`  | 为 `S<T>` 实现方法 **_固有地_**，{{ ref(page="items/implementations.html#inherent-implementations") }} 这里 `T` 是特定类型，例如 `u8`。  |
| `fn f() -> impl T`  | **存在类型**，{{ book(page="ch10-02-traits.html#returning-types-that-implement-traits") }} 返回一个对调用者未知的 `S`，其 `impl T`。 |
| {{ tab() }} `-> impl T + 'a`  | 表示隐藏类型至少与 `'a` 一样长。{{ rfc(page="3498-lifetime-capture-rules-2024.html#capturing-lifetimes") }}  |
| {{ tab() }} `-> impl T + use<'a>`  | 表示隐藏类型捕获了生命周期 `'a`，**使用约束**。{{ link(url="https://blog.rust-lang.org/2024/09/05/impl-trait-capture-rules.html") }} {{ todo() }}|
| {{ tab() }} `-> impl T + use<'a, R>`  | 也表示隐藏类型可能已从 `R` 中捕获生命周期。 |
| `fn f(x: &impl T)`  | 通过“**impl 特征**”进行特征约束，{{ book(page="ch10-02-traits.html#trait-bound-syntax") }} 类似于下面的 `fn f<S: T>(x: &S)`。 |
| `fn f(x: &dyn T)`  | 通过 **动态派发** 调用 `f`，{{ book(page="ch17-02-trait-objects.html#using-trait-objects-that-allow-for-values-of-different-types") }} {{ ref(page="types.html#trait-objects") }} `f` 不会为 `x` 实例化。 |
| `fn f<X: T>(x: X)`  | 函数对 `X` 泛型化，`f` 将为每个 `X` 实例化（'[单态化](https://en.wikipedia.org/wiki/Monomorphization)'）。 |
| `fn f() where Self: R;`  | 在 `trait T {}` 中，使 `f` 只能在已知类型也 `impl R` 时访问。  |
| {{ tab() }} `fn f() where Self: Sized;`  | 使用 `Sized` 可以选择退出特征对象 vtable，从而启用 `dyn T`。 |
| {{ tab() }} `fn f() where Self: R {}`  | 其他 `R` 在默认方法中有用（非默认方法需要被实现）。 |
</fixed-2-column>



### Higher-Ranked Items {{ esoteric() }} {#higher-ranked-items}

**实际类型和特征，通常抽象化生命周期。**

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `for<'a>` | **高阶生命周期界定符**的标记。{{ nom(page="hrtb.html")}} {{ ref(page="trait-bounds.html#higher-ranked-trait-bounds")}} {{ esoteric() }} |
| {{ tab() }} `trait T: for<'a> R<'a> {}` | 任何实现了 `T` 的类型 `S` 也必须满足 `R` 对任何生命周期的约束。 |
| `fn(&'a u8)` | 函数指针类型，持有一个能用 **特定** 生命周期 `'a` 调用的函数。 |
| `for<'a> fn(&'a u8)` | **高阶类型**<sup>1</sup> {{ link(url="https://github.com/rust-lang/rust/issues/56105") }}，持有可以用 **任意** 生命周期调用的函数。是上述类型的子类型。{{ below(target="#type-conversions") }} |
| {{ tab() }} `fn(&'_ u8)` | 相同；自动扩展为类型 `for<'a> fn(&'a u8)`。 |
| {{ tab() }} `fn(&u8)` | 相同；自动扩展为类型 `for<'a> fn(&'a u8)`。 |
| `dyn for<'a> Fn(&'a u8)` | 高阶（特征对象）类型，工作方式类似于上面的 `fn`。 |
| {{ tab() }} `dyn Fn(&'_ u8)` | 相同；自动扩展为类型 `dyn for<'a> Fn(&'a u8)`。 |
| {{ tab() }} `dyn Fn(&u8)` | 相同；自动扩展为类型 `dyn for<'a> Fn(&'a u8)`。 |

<footnotes>

<sup>1</sup> 是的，`for<>` 是类型的一部分，这就是为什么你在下面编写 `impl T for for<'a> fn(&'a u8)` 时需要它。

</footnotes>

</fixed-2-column>

<div class="color-header special_example">
{{ tablesep() }}

| 实现特征 | 解释 |
|---------|-------------|
| `impl<'a> T for fn(&'a u8) {}` | 针对函数指针的实现，调用接受 **特定** 生命周期 `'a` 时，实现特征 `T`。|
| `impl T for for<'a> fn(&'a u8) {}` | 针对函数指针的实现，调用接受 **任意** 生命周期时，实现特征 `T`。 |
| {{ tab() }} `impl T for fn(&u8) {}` | 相同，简写形式。 |

</div>


### Strings & Chars

Rust 有几种方法可以创建文本值。

<fixed-2-column>

| 示例 | 解释 |
|--------|-------------|
| `"..."` | **字符串字面量**，{{ ref(page="tokens.html#string-literals")}}<sup>, 1</sup> 一个 UTF-8 `&'static str`，{{ std(page="std/primitive.str.html") }} 支持以下转义：  |
| {{ tab() }} `"\n\r\t\0\\"` | **常见转义** {{ ref(page="tokens.html#ascii-escapes") }}，例如，`"\n"` 变为 _换行符_。 |
| {{ tab() }} `"\x36"` | **ASCII 转义** {{ ref(page="tokens.html#ascii-escapes") }}，范围最多到 `7f`，例如，`"\x36"` 会变成 `6`。 |
| {{ tab() }} `"\u{7fff}"` | **Unicode 转义** {{ ref(page="tokens.html#unicode-escapes") }} 最多 6 位数字，例如，`"\u{7fff}"` 会变成 `翿`。 |
| `r"..."` | **原始字符串字面量**。{{ ref(page="tokens.html#raw-string-literals")}}<sup>, 1</sup> UTF-8，但不会解释上述任何转义字符。 |
| `r#"..."#` | 原始字符串字面量，UTF-8，但也可以包含 `"`。`#` 的数量可以变化。|
| `c"..."` | **C 字符串字面量**，{{ ref(page="tokens.html#c-string-literals")}} 一个以 NUL 结尾的 `&'static CStr`，{{ std(page="std/ffi/struct.CStr.html") }} 用于 FFI。{{ edition(ed="1.77+")}}  |
| `cr"..."`, `cr#"..."#` | 原始 C 字符串字面量，类似于上面的组合。|
| `b"..."` | **字节字符串字面量**；{{ ref(page="tokens.html#byte-and-byte-string-literals")}}<sup>, 1</sup> 构造 ASCII-only 的 `&'static [u8; N]`。 |
| `br"..."`, `br#"..."#` | 原始字节字符串字面量，类似于上面的组合。|
| `b'x'` | ASCII **字节字面量**，{{ ref(page="tokens.html#byte-literals")}} 一个单一的 `u8` 字节。  |
| `'🦀'` | **字符字面量**，{{ ref(page="tokens.html#character-and-string-literals")}} 固定 4 字节的 Unicode '**char**'。{{ std(page="std/primitive.char.html") }} |

<footnotes>

<sup>1</sup> 支持多行。需要注意的是 `Debug`{{ below(target="#string-output") }}（例如，`dbg!(x)` 和 `println!("{x:?}")`）可能会将它们渲染为 `\n`，而 `Display`{{ below(target="#string-output") }}（例如，`println!("{x}")`）会正确地显示它们。

</footnotes>

</fixed-2-column>



### Documentation

调试器讨厌他。避免错误的这个奇怪的小技巧。

<fixed-2-column>

| 示例 | 解释 |
|--------|-------------|
| `///` | 外部行 **文档注释**<sup>1</sup> {{ book(page="ch14-02-publishing-to-crates-io.html#making-useful-documentation-comments") }} {{ ex(page="meta/doc.html#documentation") }} {{ ref(page="comments.html#doc-comments")}}，用于类型、特征、函数等。 |
| `//!` | 内部行文档注释，通常用于文件顶部。 |
| `//` | 行注释，用于记录代码流或内部实现。 |
| `/* … */` | 块注释。<sup>2</sup> {{ deprecated() }} |
| `/** … */` | 外部块文档注释。<sup>2</sup> {{ deprecated() }} |
| `/*! … */` | 内部块文档注释。<sup>2</sup> {{ deprecated() }} |

</fixed-2-column>

<footnotes>

<sup>1</sup> [工具指令](#tooling-directives) 概述了你可以在文档注释中做些什么。<br>
<sup>2</sup> 通常不推荐使用，因其用户体验差。如果可能，请使用具有 IDE 支持的等效行注释。

</footnotes>



### Miscellaneous

这些符号没有适合的其他类别，但仍然值得了解。

<fixed-2-column>

| 示例 | 解释 |
|---------|-------------|
| `!` | 永远为空的 **never 类型**。{{ book(page="ch19-04-advanced-types.html#the-never-type-that-never-returns") }} {{ ex(page="fn/diverging.html#diverging-functions") }} {{ std(page="std/primitive.never.html") }} {{ ref(page="types.html#never-type") }} |
| {{ tab() }} `fn f() -> ! {}` | 永不返回的函数；与任何类型兼容，例如 `let x: u8 = f();` |
| {{ tab() }} `fn f() -> Result<(), !> {}` | 必须返回 `Result` 的函数，但表示它不可能返回 `Err`。{{ experimental() }} |
| {{ tab() }} `fn f(x: !) {}` | 存在的函数，但永远无法被调用。不是很有用。{{ esoteric() }} {{ experimental() }} |
| `_` | 未命名的 **通配符** {{ ref(page="patterns.html#wildcard-pattern")}} 变量绑定，例如 <code>&vert;x, _&vert; {}</code>。|
| {{ tab() }} `let _ = x;`  | 未命名的赋值是无操作，不会 **移动** {{ bad() }} `x` 或保持作用域！ |
| {{ tab() }} `_ = x;`  | 你可以将 **任何内容** 赋值给 `_` 而不使用 `let`，例如 `_ = ignore_rval();` {{ hot() }} |
| `_x` | 变量绑定不会发出 **未使用变量** 警告。 |
| `1_234_567` | 数字分隔符，用于视觉清晰度。 |
| `1_u8` | **数字字面量**的类型说明符 {{ ex(page="types/literals.html#literals") }} {{ ref(page="tokens.html#number-literals") }}（也可以是 `i8`，`u16` 等）。 |
| `0xBEEF`, `0o777`, `0b1001`  | 十六进制（`0x`）、八进制（`0o`）和二进制（`0b`）整数字面量。 |
| `r#foo` | 一个 **原始标识符** {{ book(page="appendix-01-keywords.html#raw-identifiers") }} {{ ex(page="compatibility/raw_identifiers.html#raw-identifiers") }} 用于版本兼容性。{{ esoteric() }} |
| `x;` | **语句** {{ ref(page="statements.html")}} 终止符，对比 **表达式** {{ ex(page="expression.html") }} {{ ref(page="expressions.html")}} |

</fixed-2-column>




### Common Operators

Rust 支持大多数你所期望的运算符（`+`，`*`，`%`，`=`，`==`，&hellip;），包括 **重载**。{{ std(page="std/ops/index.html")}} 由于它们在 Rust 中的行为与其他语言没有太大区别，因此在这里不详细列出。


---

<magic>

# Behind the Scenes

神秘的知识，可能对你的思维造成不可估量的影响，非常推荐。

## The Abstract Machine

与 `C` 和 `C++` 类似，Rust 基于一种 _抽象机器_。


<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-abstract-machine-1" name="tab-group-abstract-machine" checked>
<label for="tab-abstract-machine-1"><b>概述</b></label>
<panel><div>


<div style="text-align: center;">

<mini-zoo class="zoo" style="text-align: center;">
    <entry>
        <machine class="bad">Rust</machine>
    </entry>
    <code style="text-align:center;">→</code>
    <entry>
        <machine class="bad">CPU</machine>
    </entry>
    <br/>
    <note>{{bad()}} 具有误导性。</note>
</mini-zoo>

<mini-zoo class="zoo" style="text-align: center; margin-left: 80px;">
    <entry>
        <machine class="good">Rust</machine>
    </entry>
    <code style="text-align:center">→</code>
    <entry style="width: 120px;">
        <machine class="good">抽象机器</machine>
    </entry>
    <code style="text-align:center">→</code>
    <entry>
        <machine class="good">CPU</machine>
    </entry>
    <br/>
    <note>正确的。</note>
</mini-zoo>

</div>

{{ tablesep() }}

除极少数例外，您永远不会“被允许推理”关于实际的 CPU。您为一个 _抽象化的_ CPU 编写代码。Rust 然后（某种程度上）理解您的意图，并将其转换为实际的 RISC-V / x86 / … 机器代码。

{{ tablesep() }}

这个 _抽象机器_
- 不是运行时，并且没有任何运行时开销，而是一种 _计算模型抽象_，
- 包含诸如内存区域（_栈_ 等）、执行语义等概念，
- _知道_ 并 _看到_ 您的 CPU 可能不关心的事情，
- 实际上是您与编译器之间的契约，
- 并且**利用以上所有内容进行优化**。


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-abstract-machine-2" name="tab-group-abstract-machine">
<label for="tab-abstract-machine-2"><b>误解</b></label>
<panel><div>

<div class="color-header abstract-machine">

在左侧是人们可能错误地认为在 Rust 直接面向 CPU 时“应该能逃脱惩罚”的操作。在右侧是如果您违反抽象机器（AM）契约，实际上会干扰的事情。

{{ tablesep() }}

| 没有 AM | 有 AM |
|---------|-------------|
| `0xffff_ffff` 可以是一个有效的 `char`。{{ bad() }} | AM 可以利用“无效”位模式来打包无关的数据。 |
| `0xff` 和 `0xff` 是相同的指针。{{ bad() }} | AM 指针可以附加“域”以进行优化。 |
| 对指针 `0xff` 的任何读/写都没问题。{{ bad() }} | AM 可能会发出缓存友好的操作，因为“无法读取”。 |
| 读取未初始化的值只会得到随机值。{{ bad() }} | AM “知道”读取是不可能的，可能会移除所有相关代码。 |
| 数据竞争只会给出随机值。{{ bad() }} | AM 可能会拆分读/写，产生“不可能的”值，参见上文。 |
| 空引用只是寄存器中的 `0x0`。{{ bad() }} | 在引用中持有 `0x0` 会召唤克苏鲁。 |

{{ tablesep() }}

> 这个表格仅用于概述 AM 的工作原理。与 C 或 C++ 不同，Rust 从不允许你做错事，除非你用 `unsafe` 强行进行操作。{{ below(target="#unsafe-unsound-undefined") }}

</div>
</div></panel></tab>


</tabs>

<!--  -->
<!-- > Practically this means: -->
<!-- > - before assuming your **CPU** will do `A` when writing `B` you need positive proof **via documentation**(!), -->
<!-- > - if you don't have that any physical behavior is _coincidental_, -->
<!-- > - violate the abtract machine's contract and the optimizer makes your CPU do something **entirely else** &mdash; **undefined behavior**.{{ below(target="#unsafe-unsound-undefined")}} -->
<!--  -->


## Language Sugar

如果某些东西“在你现在考虑后不应该起作用，但它却起作用”，可能是由于以下原因之一。

<div class="color-header language-sugar">

| 名称 | 描述 |
|--------| -----------|
| **Coercions** {{ nom(page="coercions.html") }} | 将类型“弱化”以匹配签名，例如，`&mut T` 转换为 `&T`；参考 _类型转换_ {{ below(target="#type-conversions") }} |
| **Deref** {{ nom(page="vec-deref.html") }} {{ link(url="https://stackoverflow.com/questions/28519997/what-are-rusts-exact-auto-dereferencing-rules") }} | [Deref](https://doc.rust-lang.org/std/ops/trait.Deref.html) 将 `x: T` 解引用直到 `*x`，`**x`，&hellip; 与某些目标 `S` 兼容。 |
| **Prelude** {{ std(page="std/prelude/index.html") }} | 自动导入基本项目，例如 `Option`，`drop()`，等。|
| **Reborrow** {{ link(url="https://quinedot.github.io/rust-learning/st-reborrow.html") }} | 由于 `x: &mut T` 无法被复制；而是移动新的 `&mut *x`。 |
| **Lifetime Elision** {{ book(page="ch10-03-lifetime-syntax.html#lifetime-elision") }} {{ nom(page="lifetime-elision.html#lifetime-elision") }} {{ ref(page="lifetime-elision.html#lifetime-elision") }} | 允许你编写 `f(x: &T)` 而不是 `f<'a>(x: &'a T)`，以简洁为目的。 |
| **Lifetime Extensions** {{ link(url="https://blog.m-ou.se/super-let/") }}  {{ ref(page="destructors.html#temporary-lifetime-extension") }} | 在 `let x = &tmp().f` 等类似情况下，保持临时值超出这一行。 |
| **Method Resolution** {{ ref(page="expressions/method-call-expr.html") }} | 解引用或借用 `x` 直到 `x.f()` 起作用。 |
| **Match Ergonomics** {{ rfc(page="2005-match-ergonomics.html") }} | 对 [scrutinee](https://doc.rust-lang.org/stable/reference/glossary.html#scrutinee) 进行反复解引用，并向绑定添加 `ref` 和 `ref mut`。 |
| **Rvalue Static Promotion** {{ rfc(page="1414-rvalue_static_promotion.html") }}  {{ esoteric() }} | 将常量的引用变为 `'static`，例如 `&42`，`&None`，`&mut []`。 |
| **Dual Definitions** {{ rfc(page="1506-adt-kinds.html#tuple-structs") }} {{ esoteric() }} | 定义一个（例如，`struct S(u8)`）隐式定义了另一个（例如，`fn S`）。 |
| **Drop Hidden Flow** {{ ref(page="destructors.html") }} {{ esoteric() }} | 在块结束 `{ ... }` 或 `_` 赋值时，可能会调用 `T::drop()`。{{ std(page="std/ops/trait.Drop.html") }} |
| **Drop Not Callable** {{ std(page="std/ops/trait.Drop.html") }} {{ esoteric() }} | 编译器禁止显式调用 `T::drop()`，必须使用 `mem::drop()`。{{ std(page="std/mem/fn.drop.html") }} |

</div>

{{ tablesep() }}

> **观点** {{ opinionated() }} &mdash; 这些功能让你在使用 Rust 时更加轻松，但在学习它时却是障碍。如果你想发展出真正的理解，请花一些额外的时间来探索它们。


## Memory & Lifetimes


移动、引用和生命周期的图解指南


<tabs class="lifetimes">

<!-- 新的标签页 -->
<tab>
<input type="radio" id="tab-lt-1" name="tab-lt" checked>
<label for="tab-lt-1"><b>类型与移动</b></label>
<panel>
<div>

<lifetime-section>
<lifetime-example>
    <section-header>应用程序内存</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="" style="right: 10px;">&nbsp;</label>
        </labels>
        <subtext>应用程序内存</subtext>
    </memory-row>
</lifetime-example>
<explanation>

- 应用程序内存在低级别上就是字节数组。
- 操作环境通常将其划分为以下部分：
    - **栈**（小型、低开销的内存，<sup>1</sup> 大多数 _变量_ 都在这里），
    - **堆**（大型、灵活的内存，但总是通过栈代理进行处理，如 `Box<T>`），
    - **静态**（最常用于 `&str` 中的 `str` 部分），
    - **代码**（存放函数的字节码的位置）。
- 最棘手的部分在于 **栈如何演变**，这是我们的 **重点**。

<footnotes>

<sup>1</sup> 对于固定大小的值，栈是容易管理的：_在需要的时候多占用几个字节，离开时就可以丢弃_。然而，将指针指向这些 _瞬态_ 位置构成了 _生命周期_ 存在的精髓所在，也是本章其余部分的主题。

</footnotes>

</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <section-header>变量</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(1)</value>
            <value class="t byte2" style="left: 97.5px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
        </labels>
        <subtext>变量</subtext>
        <!-- <subtext><code>let t = S(1);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let t = S(1);
```

- 保留名为 `t` 的内存位置，类型为 `S`，其中存储了值 `S(1)`。
- 如果用 `let` 声明，该位置将存在于栈上。<sup>1</sup>
- 注意术语 **_变量_** 的**语言歧义**，它可能意味着：
    1. 源文件中的位置的**名称**（“重命名该变量”），
    1. 编译后的应用程序中的**位置**，例如 `0x7`（“告诉我该变量的地址”），
    1. 所包含的**值**，例如 `S(1)`（“增加该变量”）。
- 对于编译器来说，`t` 可以意味着 `t` 的**位置**，例如这里的 `0x7`，也可以意味着 `t` 中的**值**，例如这里的 `S(1)`。

<footnotes>

<sup>1</sup> 比较上述内容，{{ above(target="#data-structures" ) }} 对于完全同步的代码是正确的，但 `async` 栈帧可能通过运行时将其放置在堆上。

</footnotes>


</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header>移动语义</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
        </labels>
        <subtext>移动</subtext>
        <!-- <subtext><code>let a = t;</code></subtext> -->
    </memory-row>
</lifetime-example>

<explanation>

```
let a = t;
```

- 这将**移动**`t`中的值到`a`的位置，或者如果`S`是`Copy`类型，则会复制它。
- 移动后，位置`t`变为**无效**，无法再读取。
  - 技术上讲，该位置的比特实际上并没有真正变为 _空_，而是 _未定义_。
  - 如果你仍然可以访问`t`（通过 `unsafe`），它们可能 _看起来_ 仍然是有效的`S`，但是任何尝试将它们作为有效的`S`使用的行为都是未定义行为。{{ below(target="#unsafe-unsound-undefined") }}
- 我们这里不会明确讨论`Copy`类型。它们在规则上稍有不同，但变化不大：
  - 它们不会被丢弃。
  - 它们不会留下“空的”变量位置。

</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <section-header>类型安全</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <failed style="left: 231.5px;"><value class="atomic byte4">M { … }</value></failed>
            <denied style="left: 141px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code></code></label>
            <label class="byte2" style="left: 170px;"><code>c</code></label>
        </labels>
        <subtext>类型安全</subtext>
        <!-- <subtext><code>let c: S = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>


```
let c: S = M::new();
```

- **变量的类型**有多个重要的用途，它：
  1. 决定了如何解释底层的比特；
  2. 只允许对这些比特进行定义明确的操作；
  3. 防止其他随机的值或比特被写入该位置。
- 在这里，赋值操作无法编译，因为`M::new()`的字节无法转换为类型`S`的形式。
- **类型之间的转换通常总是会失败**，**除非有明确的规则允许**（例如强制转换、类型转换等）。
- 这将**移动**`t`中的值到`a`的位置，或者如果`S`是`Copy`类型，则会复制它。
- 移动后，位置`t`变为**无效**，无法再读取。
  - 技术上讲，该位置的比特实际上并没有真正变为 _空_，而是 _未定义_。
  - 如果你仍然可以访问`t`（通过 `unsafe`），它们可能 _看起来_ 仍然是有效的`S`，但是任何尝试将它们作为有效的`S`使用的行为都是未定义行为。{{ below(target="#unsafe-unsound-undefined") }}
- 我们这里不会明确讨论`Copy`类型。它们在规则上稍有不同，但变化不大：
  - 它们不会被丢弃。
  - 它们不会留下“空的”变量位置。

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header>范围 & 丢弃</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <drop><value class="t byte2" style="left: 57px;">S(1)</value><droparrow style="left:37px;">▼</droparrow></drop>
            <value class="t byte2 hide" style="left: 87.5px;">C(2)</value>
            <drop><value class="t byte2" style="left: 128px;">S(2)</value><droparrow style="left:107px;">▼</droparrow></drop>
            <failed style="left: -27.5px;"><value class="t byte2" style="left: 128px;">S(3)</value></failed>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code></code></label>
            <label class="byte2" style="left: 97.5px;"><code>t</code></label>
            <!-- <label class="byte2" style="left: 136.5px;"><code>c</code></label> -->
        </labels>
        <subtext>范围 & 丢弃</subtext>
        <!-- <subtext><code>{ let a = ...; }</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
{
    let mut c = S(2);
    c = S(3);  // <- Drop called on `c` before assignment.
    let t = S(1);
    let a = t;
}   // <- Scope of `a`, `t`, `c` ends here, drop called on `a`, `c`.
```

- **一旦非空闲变量的“名称”超出（销毁）**范围，其包含的值就会被**丢弃**。
  - 经验法则：当执行到达变量名称离开其定义的 `{}` 块的点时，该变量就会被销毁。
  - 详细情况更复杂，尤其是临时变量，&hellip;
- 当给现有变量位置赋予新值时，也会调用 Drop。
- 在这种情况下，会对该值的位置调用 **`Drop::drop()`**。
  - 在上面的例子中，`drop()` 被调用在 `a` 上，`c` 上调用了两次，但不会在 `t` 上调用。
- 大多数非`Copy`类型的值大多数时候都会被丢弃；例外情况包括 `mem::forget()`，`Rc` 循环，`abort()`。

</explanation>
</lifetime-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-2" name="tab-lt">
<label for="tab-lt-2"><b>调用栈</b></label>
<panel><div>

<lifetime-section>
<lifetime-example>
    <section-header>栈帧</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
        </labels>
        <subtext>函数边界</subtext>
        <!-- <subtext><code>fn f(x: S) {}</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) { … }

let a = S(1); // <- We are here
f(a);
```

- 当**函数被调用**时，内存会在栈上为参数（以及返回值）保留空间。<sup>1</sup>
- 在调用 `f` 之前，`a` 中的值被移动到栈上“约定的位置”，并且在 `f` 执行过程中，`a` 的值会表现得像一个'局部变量' `x`。

<footnotes>

<sup>1</sup> 实际位置取决于调用约定，实际上可能根本不会在栈上，但这并不改变我们的心理模型。

</footnotes>

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 131px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
            <label class="byte2" style="left: 136px;"><code>x</code></label>
        </labels>
        <subtext>嵌套函数</subtext>
        <!-- <subtext><code>fn f(x: S) { ... f(x) ... }</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) {
    if once() { f(x) } // <- We are here (before recursion)
}

let a = S(1);
f(a);
```

- **递归调用**函数，或者调用其他函数，同样会扩展栈帧。
- 嵌套过多次调用（尤其是通过无界递归）会导致栈增长，最终导致栈溢出，从而终止应用程序。

</explanation>
</lifetime-section>


<lifetime-section>

<lifetime-example class="not-first">
    <section-header>变量的有效性</section-header>
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t" style="opacity: 0.4;"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 131px;">S(1)</value>
            <value class="atomic byte4" style="left: 190px;">M { }</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte2" style="left: 97.5px;"><code>x</code></label>
            <label class="byte2" style="left: 174px;"><code>m</code></label>
        </labels>
        <subtext>重新利用记忆</subtext>
        <!-- <subtext><code>f(x); let m = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: S) {
    if once() { f(x) }
    let m = M::new() // <- We are here (after recursion)
}

let a = S(1);
f(a);
```

- 之前用于保存某种类型的栈空间会在不同函数之间（甚至在同一个函数内）重新利用。
- 在这里，对 `f` 的递归调用产生了第二个 `x`，在递归之后，这部分栈空间部分地被 `m` 重新利用。

> 关键点在于，之前用于保存某种类型有效值的内存位置，可能会因为各种原因而不再继续保存该值。
> 正如我们将要看到的，这对指针会产生影响。

</explanation>
</lifetime-section>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-3" name="tab-lt">
<label for="tab-lt-3"><b>引用 & 指针</b></label>
<panel><div>

<lifetime-section>
<lifetime-example>
    <section-header class="arrowed">引用类型</section-header>
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(1)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
        </labels>
        <subtext>引用作为指针</subtext>
        <!-- <subtext><code>let r = &mut a;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let a = S(1);
let r: &S = &a;
```

- **引用类型**，比如 `&S` 或 `&mut S`，可以保存某个 `s` 的**位置**。
- 这里，类型 `&S`，被绑定为名字 `r`，保存了变量 `a` 的_位置_ (`0x3`)，它必须是类型 `S`，通过 `&a` 获得。
- 如果你把变量 `c` 看作是_特定位置_，那么引用 **`r` 是一个_位置的交换机_**。
- 引用的类型，和所有其他类型一样，通常可以被推断出来，所以我们可以从现在开始省略它：
    ```
    let r: &S = &a;
    let r = &a;
    ```
<!-- - References on their own are **never** concerned with the _value within_ the location they point to. -->

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <section-header class="arrowed">（可变）引用</section-header>
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 57px;">S(2)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
            <value class="t byte2" style="left: 213px;">S(1)</value>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
            <label class="byte4" style="left: 193px;"><code>d</code></label>
        </labels>
        <subtext>访问非自有内存</subtext>
        <!-- <subtext><code>let d = r.clone(); *r = S(2);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let mut a = S(1);
let r = &mut a;
let d = r.clone();  // Valid to clone (or copy) from r-target.
*r = S(2);          // Valid to set new S value to r-target.
```


- 引用可以**读取**（`&S`）并**写入**（`&mut S`）它们指向的位置。
- *解引用* `*r` 意味着使用 **`r` 所指向的位置**（_不是_ `r` 自身的_位置_或者_值_）
- 在这个例子中，从 `*r` 创建了克隆 `d`，并将 `S(2)` 写入到 `*r`。
  - 我们假设 `S` 实现了 `Clone`，`r.clone()` 克隆的是 `r` 所指向的目标，而不是 `r` 本身。
  - 在赋值 `*r = …` 时，位置中的旧值也被释放（上面未显示）。

</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">S(2)</value>
            <value class="ptr byte4" style="left: 171px;">0x3</value>
            <value class="atomic byte4" style="top:-36px; left: 20px;">M { x }</value>
            <denied style="left: -71px; top:-36px;">⛔</denied>
            <denied style="left: -131px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 57px;"><code>a</code></label>
            <label class="byte4" style="left: 171px;"><code>r</code></label>
            <label class="byte4" style="left: 193px;"><code>d</code></label>
        </labels>
        <subtext>引用守卫引用</subtext>
        <!-- <subtext><code>let d = *r; *r = M::new();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let mut a = …;
let r = &mut a;
let d = *r;       // Invalid to move out value, `a` would be empty.
*r = M::new();    // invalid to store non S value, doesn't make sense.
```

- 绑定保证始终_保存_有效数据，而引用则保证始终_指向_有效数据。
- 尤其是 `&mut T` 必须提供与变量相同的保证，甚至更多，因为它们不能破坏目标：
  - 它们**不允许写入无效**数据。
  - 它们**不允许移动**数据出去（这会使目标为空，而所有者不知情）。

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <arrows>
            <arrow style="left: 62px; width: 176px; border-color: red;">&nbsp;<tip style="color: red">▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">C(2)</value>
            <value class="ptr byte4 unsafe" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 57px;"><code>c</code></label>
            <label class="byte4" style="left: 171px;"><code>p</code></label>
        </labels>
        <subtext>原始指针</subtext>
        <!-- <subtext><code>let p: *const S = ...;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let p: *const S = questionable_origin();
```

- 与引用相比，指针几乎没有任何保证。
- 它们可能指向无效或不存在的数据。
- 对它们进行解引用是 `unsafe` 的，且将无效的 `*p` 视为有效的操作会导致未定义行为。{{ below(target="#unsafe-unsound-undefined") }}

</explanation>
</lifetime-section>

</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-10" name="tab-lt">
<label for="tab-lt-10"><b>生命周期基础</b></label>
<panel><div>


<lifetime-section>
<lifetime-example>
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 57px;">C(2)</value>
            <value class="ptr byte4 hide" style="left: 171px;">0x3</value>
        </values>
        <labels>
            <!-- <label class="byte2" style="left: 37px;"><code>'a</code></label>
            <label class="byte4" style="left: 59px;"><code>'b: 'c</code></label>
            <label class="byte2" style="left: 81px;"><code>'c</code></label>
            <label class="byte4" style="left: 139px;"><code>'d</code></label> -->
        </labels>
        <subtext>事物的“生命周期”</subtext>
        <!-- <subtext><code>f(); g(); h();</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

- 程序中的每个实体在其相关的某段（时间/空间）范围内都是_存活_的。
- 宽泛地说，这个_存活时间_可以是<sup>1</sup>：
  1. **代码行（LOC）**，即一个**项目可用**的范围（例如，一个模块名称）。
  1. **代码行（LOC）**，即一个_位置_被**初始化**为某个值到该位置被**放弃**之间的范围。
  1. **代码行（LOC）**，即一个位置第一次以某种方式被**使用**，直到该**使用停止**之间的范围。
  1. **代码行（LOC 或实际时间）**，即一个_值_被创建，直到该值被释放之间的范围。
- 在本节余下部分，我们将使用以下术语来指代上述项目：
  1. **项目的作用域**，在这里无关紧要。
  1. **变量或位置的作用域**。
  1. **该使用的生命周期**<sup>2</sup>。
  1. **该值的生命周期**，当讨论打开的文件描述符时可能有用，但在这里无关紧要。
- 同样，代码中的生命周期参数，例如 `r: &'a S`，
  - 关注的是某个**位置 r _指向_**在任何代码行（LOC）中需要是可访问或被锁定的；
  - 与 `r` 自身的'存在时间'（作为代码行）无关（当然，它的存在时间必须更短，仅此而已）。
- `&'static S` 意味着地址在_所有代码行期间_都必须有效。

> <sup>1</sup> 在文档中，有时对各种_作用域_和_生命周期_的区分可能存在歧义。
> 我们在此尽量采取务实的态度，但欢迎提供建议。
>
> <sup>2</sup> _活跃代码行_ 可能是一个更合适的术语……

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 192px; width: 120px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0xa</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte2 hide" style="left: 78px;"><code>b</code></label>
            <label class="byte2" style="left: 118px;"><code>c</code></label>
            <label class="byte4" style="left: 177px;"><code>r</code></label>
        </labels>
        <subtext><code>r: &'c S</code> 的含义</subtext>
        <!-- <subtext><code>r: &mut 'c S</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

- 假设你从某处得到了一个 `r: &'c S`，这意味着：
  - `r` 保存了某个 `S` 的地址，
  - `r` 所指向的任何地址必须且将至少存在于 `'c` 的生命周期内，
  - 变量 `r` 自身不能比 `'c` 的生命周期更长。



</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 118px; width: 193px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(3)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0x6</value>
            <denied style="left: -125px; top:-25px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte2" style="left: 78px;"><code>b</code></label>
            <label class="byte2" style="left: 118px;"><code>c</code></label>
            <label class="byte4" style="left: 177px;"><code>r</code></label>
        </labels>
        <subtext>生命周期的类型相似性</subtext>
        <!-- <subtext><code>r = &mut b;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
{
    let b = S(3);
    {
        let c = S(2);
        let r: &'c S = &c;      // Does not quite work since we can't name lifetimes of local
        {                       // variables in a function body, but very same principle applies
            let a = S(0);       // to functions next page.

            r = &a;             // Location of `a` does not live sufficient many lines -> not ok.
            r = &b;             // Location of `b` lives all lines of `c` and more -> ok.
        }
    }
}
```

- 假设你从某处得到了一个 `mut r: &mut 'c S`。
  - 即一个可变的位置，可以保存一个可变引用。
- 如前所述，该引用必须保护目标内存。
- 然而，**`'c` 部分**，就像类型一样，也**保护了允许放入 `r` 的内容**。
- 在这里，将 `&b` (`0x6`) 赋给 `r` 是有效的，但将 `&a` (`0x3`) 赋给 `r` 则不是，因为只有 `&b` 的生命周期与 `'c` 相等或更长。

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 118px; width: 193px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">&nbsp;</value>
            <value class="t byte2 hide" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">0x6</value>
            <failed style="left: -40px;"><value class="t bytes">S(4)</value></failed>
            <denied style="left: -83px;">⛔</denied>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte2" style="left: 78px;"><code>b</code></label>
            <label class="byte2 hide" style="left: 118px;"><code>c</code></label>
            <label class="byte4 hide" style="left: 177px;"><code></code></label>
        </labels>
        <subtext>借用状态</subtext>
    </memory-row>
</lifetime-example>
<explanation>

```
let mut b = S(0);
let r = &mut b;

b = S(4);   // Will fail since `b` in borrowed state.

print_byte(r);
```

- 一旦通过 `&b` 或 `&mut b` 获取了一个变量的地址，该变量就会被标记为**已借用**。
- 在被借用期间，不能通过原始绑定 `b` 修改该地址的内容。
- 一旦通过 `&b` 或 `&mut b` 获取的地址不再被使用（在代码行的范围内），原始绑定 `b` 将再次生效。


</explanation>
</lifetime-section>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-11" name="tab-lt">
<label for="tab-lt-11"><b>函数中的生命周期</b></label>
<panel>
<div>


<lifetime-section>
<lifetime-example>
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">?</value>
            <value class="ptr byte4" style="left: 201px;">0x6</value>
            <value class="ptr byte4" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2 hide" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4" style="left: 165px;"><code>x</code></label>
            <label class="byte4" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>函数参数</subtext>
        <!-- <subtext><code>let r = f(&b, &c);</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f(x: &S, y:&S) -> &u8 { … }

let b = S(1);
let c = S(2);

let r = f(&b, &c);
```

- 当调用接受并返回引用的函数时，会发生两件有趣的事情：
  - 使用的局部变量会被置于借用状态，
  - 但在编译期间并不知道将返回哪个地址。



</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte class="t maybe-borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2 hide" style="left: 38px;">S(0)</value>
            <value class="t byte2" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">?</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>“借用”传播问题</subtext>
        <!-- <subtext><code>let a = b;</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
let b = S(1);
let c = S(2);

let r = f(&b, &c);

let a = b;   // Are we allowed to do this?
let a = c;   // Which one is _really_ borrowed?

print_byte(r);
```

- 因为 `f` 只能返回一个地址，所以在某些情况下，`b` 和 `c` 不一定需要保持锁定。
- 在许多情况下，我们可以获得更好的使用体验。
  - 特别是，当我们知道某个参数_不可能_再被用作返回值时。


</explanation>
</lifetime-section>



<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <arrows>
            <arrow style="left: 210px; width: 102px;">&nbsp;<tip>▼</tip></arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t borrowed"></byte>
            <byte class="t borrowed"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(1)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2" style="left: 119px;">S(2)</value>
            <value class="ptr byte4" style="left: 177px;">y + _</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <subtext>生命周期传播借用状态</subtext>
        <!-- <subtext><code>f(x: &'x S, y: &'y S) -> &'y u8</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
fn f<'b, 'c>(x: &'b S, y: &'c S) -> &'c u8 { … }

let b = S(1);
let c = S(2);

let r = f(&b, &c); // We know returned reference is `c`-based, which must stay locked,
                   // while `b` is free to move.

let a = b;

print_byte(r);
```

- 签名中的生命周期参数，例如上面的 `'c`，解决了这个问题。
- 它们的主要目的是：
  - **在函数外部**，解释输出地址是基于哪个输入地址生成的，
  - **在函数内部**，保证只分配至少在 `'c` 生命周期内存在的地址。
- 实际的生命周期 `'b`、`'c` 会由编译器在**调用点**透明地选择，基于开发者提供的被借用的变量。
- 它们**不等于**_作用域_（作用域是从初始化到销毁的代码行范围），而是其作用域的最小子集，称为_生命周期_，即一组最小的代码行范围，基于 `b` 和 `c` 需要被借用的时间，以便执行这个调用并使用获得的结果。
- 在某些情况下，比如如果 `f` 有 `'c: 'b`，我们仍然无法区分，这样两个都需要保持锁定。

</explanation>
</lifetime-section>




<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop class="past" style="padding-left: 7px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte class="atomic"></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop class="past" style="padding-left: 3px;">
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(2)</value>
            <value class="t byte2 hide" style="left: 79px;">S(1)</value>
            <value class="t byte2 hide" style="left: 119px;">S(2)</value>
            <value class="ptr byte4 hide" style="left: 177px;">y + 1</value>
            <value class="ptr byte4 hide" style="left: 201px;">0x6</value>
            <value class="ptr byte4 hide" style="left: 224px;">0xa</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4 hide" style="left: 59px;"><code>b</code></label>
            <label class="byte2" style="left: 81px;"><code>c</code></label>
            <label class="byte4 hide" style="left: 139px;"><code>r</code></label>
            <label class="byte4 hide" style="left: 165px;"><code>x</code></label>
            <label class="byte4 hide" style="left: 188px;"><code>y</code></label>
        </labels>
        <!-- <subtext><code>{ let r = ... }</code></subtext> -->
        <subtext>解锁</subtext>
    </memory-row>
</lifetime-example>
<explanation>

```
let mut c = S(2);

let r = f(&c);
let s = r;
                    // <- Not here, `s` prolongs locking of `c`.

print_byte(s);

let a = c;          // <- But here, no more use of `r` or `s`.


```
- 一旦最后一次使用任何可能指向该变量的位置的引用结束，该变量位置就会重新 _解锁_。

</explanation>
</lifetime-section>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-lt-12" name="tab-lt">
<label for="tab-lt-12"><b>高级 {{ esoteric() }}</b></label>
<panel>
<div>




<lifetime-section>
<lifetime-example>
    <memory-row>
        <arrows>
            <arrow style="left: 53px; width: 92px;">&nbsp;<tip>▼</tip></arrow>
            <arrow style="left: 57px; width: 104px;">&nbsp;<tip>▼</tip></arrow>
            <arrow style="left: -155px; width: 320px; top: -5px; border-style: dashed;">&nbsp;</arrow>
        </arrows>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte class="ptr"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <value class="t byte2" style="left: 38px;">S(1)</value>
            <value class="ptr byte4" style="left: 80px;">0x2</value>
            <value class="ptr byte4" style="left: 120px;">0x6</value>
            <value class="ptr byte4" style="left: 162px;">0x2</value>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>a</code></label>
            <label class="byte4" style="left: 79px;"><code>ra</code></label>
            <label class="byte2" style="left: 139px;"><code>rb</code></label>
            <label class="byte2" style="left: 216px;"><code>rval</code></label>
        </labels>
        <subtext>引用的引用</subtext>
        <!-- <subtext><code>f(x: &'x S, y: &'y S) -> &'y u8</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
// Return short ('b) reference
fn f1sr<'b, 'a>(rb: &'b     &'a     S) -> &'b     S { *rb }
fn f2sr<'b, 'a>(rb: &'b     &'a mut S) -> &'b     S { *rb }
fn f3sr<'b, 'a>(rb: &'b mut &'a     S) -> &'b     S { *rb }
fn f4sr<'b, 'a>(rb: &'b mut &'a mut S) -> &'b     S { *rb }

// Return short ('b) mutable reference.
// f1sm<'b, 'a>(rb: &'b     &'a     S) -> &'b mut S { *rb } // M
// f2sm<'b, 'a>(rb: &'b     &'a mut S) -> &'b mut S { *rb } // M
// f3sm<'b, 'a>(rb: &'b mut &'a     S) -> &'b mut S { *rb } // M
fn f4sm<'b, 'a>(rb: &'b mut &'a mut S) -> &'b mut S { *rb }

// Return long ('a) reference.
fn f1lr<'b, 'a>(rb: &'b     &'a     S) -> &'a     S { *rb }
// f2lr<'b, 'a>(rb: &'b     &'a mut S) -> &'a     S { *rb } // L
fn f3lr<'b, 'a>(rb: &'b mut &'a     S) -> &'a     S { *rb }
// f4lr<'b, 'a>(rb: &'b mut &'a mut S) -> &'a     S { *rb } // L

// Return long ('a) mutable reference.
// f1lm<'b, 'a>(rb: &'b     &'a     S) -> &'a mut S { *rb } // M
// f2lm<'b, 'a>(rb: &'b     &'a mut S) -> &'a mut S { *rb } // M
// f3lm<'b, 'a>(rb: &'b mut &'a     S) -> &'a mut S { *rb } // M
// f4lm<'b, 'a>(rb: &'b mut &'a mut S) -> &'a mut S { *rb } // L

// Now assume we have a `ra` somewhere
let mut ra: &'a mut S = …;

let rval = f1sr(&&*ra);       // OK
let rval = f2sr(&&mut *ra);
let rval = f3sr(&mut &*ra);
let rval = f4sr(&mut ra);

//  rval = f1sm(&&*ra);       // Would be bad, since rval would be mutable
//  rval = f2sm(&&mut *ra);   // reference obtained from broken mutability
//  rval = f3sm(&mut &*ra);   // chain.
let rval = f4sm(&mut ra);

let rval = f1lr(&&*ra);
//  rval = f2lr(&&mut *ra);   // If this worked we'd have `rval` and `ra` …
let rval = f3lr(&mut &*ra);
//  rval = f4lr(&mut ra);     // … now (mut) aliasing `S` in compute below.

//  rval = f1lm(&&*ra);       // Same as above, fails for mut-chain reasons.
//  rval = f2lm(&&mut *ra);   //                    "
//  rval = f3lm(&mut &*ra);   //                    "
//  rval = f4lm(&mut ra);     // Same as above, fails for aliasing reasons.

// Some fictitious place where we use `ra` and `rval`, both alive.
compute(ra, rval);
```

<footnotes>

这里 (`M`) 表示编译失败是由于可变性错误，(`L`) 表示生命周期错误。
另外，解引用 `*rb` 并非严格必要，仅为了清晰而添加。

</footnotes>

- `f_sr` 情况总是有效，短引用（仅存活于 `'b`）总是可以生成。
- `f_sm` 情况通常会失败，原因是需要返回 `&mut S` 的_可变链_到 `S`。
- `f_lr` 情况可能会失败，因为从 `&'a mut S` 返回 `&'a S` 给调用者意味着现在会有两个引用（一个是可变引用）指向相同的 `S`，这是非法的。
- `f_lm` 情况总是由于以上各种原因组合而失败。


</explanation>
</lifetime-section>


<lifetime-section>
<lifetime-example class="not-first">
    <memory-row>
        <memory-backdrop>
            <byte></byte>
            <byte></byte>
            <byte class="t"></byte>
            <byte class="t"></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
            <byte></byte>
        </memory-backdrop>
        <values>
            <drop><value class="t byte2" style="left: 38px;">S(1)</value><droparrow style="left:17px;">▼</droparrow></drop>
        </values>
        <labels>
            <label class="byte2" style="left: 37px;"><code>_</code></label>
            <!-- <label class="byte2" style="left: 136.5px;"><code>c</code></label> -->
        </labels>
        <subtext>丢弃和<code>_</code></subtext>
        <!-- <subtext><code>{ let a = ...; }</code></subtext> -->
    </memory-row>
</lifetime-example>
<explanation>

```
{
    let f = |x, y| (S(x), S(y)); // Function returning two 'Droppables'.

    let (    x1, y) = f(1, 4);  // S(1) - Scope   S(4) - Scope
    let (    x2, _) = f(2, 5);  // S(2) - Scope   S(5) - Immediately
    let (ref x3, _) = f(3, 6);  // S(3) - Scope   S(6) - Scope

    println!("…");
}
```

<footnotes>

这里 `Scope` 表示包含的值会存活到作用域结束，即在 `println!()` 之后。

</footnotes>

- 生成可移动值的函数或表达式必须由被调用者处理。
- 存储在“普通”绑定中的值会保持到作用域结束，然后被释放。
- 存储在 `_` 绑定中的值通常会立刻被释放。
- 然而，有时引用（例如 `ref x3`）可以让值（例如元组 `(S(3), S(6))`）存活更久，因此 `S(6)` 作为该元组的一部分，只有在对其兄弟 `S(3)` 的引用消失后才会被释放。



</explanation>
</lifetime-section>



</div></panel></tab>
</tabs>


<footnotes>

↕️ 单击即可展开示例。

</footnotes>



{{ tablesep() }}


</magic>


---


# Memory Layout

常见类型的字节表示。


## Basic Types

语言核心中内置的基本类型。



#### 布尔 {{ ref(page="types/boolean.html") }} 和数字类型 {{ ref(page="types/numeric.html") }}

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>bool</code></name>
    <visual class="bool">
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>u8</code>, <code>i8</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced" >
    <name><code>u16</code>, <code>i16</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u32</code>, <code>i32</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u64</code>, <code>i64</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum  class="spaced">
    <name><code>u128</code>, <code>i128</code></name>
    <visual class="bytes">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>usize</code>, <code>isize</code></name>
    <visual class="sized">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte style="border-color: #888;"><code></code></byte>
        <byte style="border-color: #888;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
        <byte style="border-color: #aaa;"><code></code></byte>
    </visual>
    <zoom>
        与平台上的 <code>ptr</code> 相同。
    </zoom>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f16</code> {{ experimental() }} </name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f32</code></name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f64</code></name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>f128</code> {{ experimental() }} </name>
    <visual class="float">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
</datum>



<br/>


{{ tablesep() }}


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-1" name="tab-group-numeric" checked>
<label for="tab-numeric-1"><b>无符号类型</b></label>
<panel><div>



|类型|最大值|
|---|---|
|`u8`| `255` |
|`u16` | `65_535` |
|`u32`| `4_294_967_295` |
|`u64`| `18_446_744_073_709_551_615` |
|`u128`| `340_282_366_920_938_463_463_374_607_431_768_211_455` |
|`usize`| 取决于平台指针大小，与`u16`、`u32`或`u64`相同。|


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-3" name="tab-group-numeric">
<label for="tab-numeric-3"><b>有符号类型</b></label>
<panel><div>



|类型|最大值|
|---|---|
|`i8`| `127` |
|`i16` | `32_767` |
|`i32`| `2_147_483_647` |
|`i64`| `9_223_372_036_854_775_807` |
|`i128`| `170_141_183_460_469_231_731_687_303_715_884_105_727` |
|`isize`| 取决于平台指针大小，与`i16`、`i32`或`i64`相同。|

{{ tablesep() }}

|类型|最小值|
|---|---|
|`i8`| `-128` |
|`i16` | `-32_768` |
|`i32`| `-2_147_483_648` |
|`i64`| `-9_223_372_036_854_775_808` |
|`i128`| `-170_141_183_460_469_231_731_687_303_715_884_105_728` |
|`isize`| 取决于平台指针大小，与`i16`、`i32`或`i64`相同。|


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-6" name="tab-group-numeric">
<label for="tab-numeric-6"><b>浮点类型</b></label>
<panel><div>


| 类型 | 最大值 | 最小正值 | 最大无损整数<sup>1</sup> |
|---|---|---| ---|
| `f16` {{ experimental() }} | 65536.0 {{ todo() }} | {{ todo() }} | `2048` {{ todo() }} |
| `f32` | 3.40 ⋅ 10 <sup>38</sup> | 3.40 ⋅ 10 <sup>-38</sup> | `16_777_216` |
| `f64` | 1.79 ⋅ 10 <sup>308</sup> | 2.23 ⋅ 10 <sup>-308</sup> | `9_007_199_254_740_992` |
| `f128` {{ experimental() }} | {{ todo() }} | {{ todo() }} | {{ todo() }} |

<footnotes>

<sup>1</sup> 最大整数 `M`，使得所有其他整数 `0 <= X <= M` 都可以在该类型中无损表示。换句话说，可能存在更大的整数仍然可以无损表示（例如 `f16` 的 `65536`），但直到该值为止，保证是无损表示的。

</footnotes>

{{ tablesep() }}

> 浮点值为了视觉上的清晰进行了近似处理。负数的界限是相应值乘以 -1。

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-2" name="tab-group-numeric">
<label for="tab-numeric-2"><b>浮点区间</b>{{ esoteric() }}</label>
<panel><div>


`f32` 的示例位表示<sup>*</sup>：

<!-- NEW ENTRY -->
<datum style="opacity:0.7; margin-bottom:10px;">
    <visual class="float">
    <bitgroup>
        <bit><code>S</code></bit>
    </bitgroup>
    <bitgroup>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
        <bit><code>E</code></bit>
    </bitgroup>
    <bitgroup>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
        <bit><code>F</code></bit>
    </bitgroup>
    </visual>
</datum>

{{ tablesep() }}

解释：

| f32 | S (1) | E (8) | F (23) | Value |
|------| ---------| ---------| ---------| ---------|
| 规格化数 | ± | 1 to 254 | any | ±(1.F)<sub>2</sub> * 2<sup>E-127</sup>  |
| 非规格化数 | ± | 0 | non-zero | ±(0.F)<sub>2</sub> * 2<sup>-126</sup>  |
| 零 | ± | 0 | 0 | ±0  |
| 无穷大 | ± | 255 | 0 | ±∞  |
| NaN | ± | 255 | non-zero | NaN  |

{{ tablesep() }}

同样，对于 <code>f64</code> 类型，这将类似于：

| f64 | S (1) | E (11) | F (52) | Value |
|------| ---------| ---------| ---------| ---------|
| 规格化数 | ± | 1 to 2046 | any | ±(1.F)<sub>2</sub> * 2<sup>E-1023</sup>  |
| 非规格化数 | ± | 0 | non-zero | ±(0.F)<sub>2</sub> * 2<sup>-1022</sup>  |
| 零 | ± | 0 | 0 | ±0  |
| 无穷大 | ± | 2047 | 0 | ±∞  |
| NaN | ± | 2047 | non-zero | NaN  |

<footnotes>
    <sup>*</sup> 浮点类型遵循 <a href="https://en.wikipedia.org/wiki/IEEE_754-2008_revision">IEEE 754-2008</a> 规范，并取决于平台大小端序。
</footnotes>

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-4" name="tab-group-numeric">
<label for="tab-numeric-4"><b>类型转换陷阱</b> {{ bad() }}</label>
<panel><div class="">


| 类型转换<sup>1</sup> | 结果 | 说明 |
| --- | --- | --- |
| `3.9_f32 as u8` | `3` | 截断，考虑先使用 `x.round()`。|
| `314_f32 as u8` | `255` | 取最接近的可用数字。|
| `f32::INFINITY as u8` | `255` | 同样，将 `INFINITY` 视为 _非常_ 大的数字。|
| `f32::NAN as u8` | `0` | - |
| `_314 as u8` | `58` | 截断多余的位。|
| `_257 as i8` | `1` | 截断多余的位。|
| `_200 as i8` | `-56` | 截断多余的位，最高有效位（MSB）可能表示负数。|

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-numeric-5" name="tab-group-numeric">
<label for="tab-numeric-5"><b>算术陷阱</b> {{ bad() }}</label>
<panel><div class="">

| 操作<sup>1</sup> | 结果 | 说明 |
| --- | --- | --- |
| `200_u8 / 0_u8` | 编译错误。 | - |
| `200_u8 / _0` <sup>d, r</sup> | Panic。 | 常规数学可能会导致 panic；这里是除以零。 |
| `200_u8 + 200_u8` | 编译错误。 | - |
| `200_u8 + _200` <sup>d</sup> | Panic。 | 考虑使用 `checked_`，`wrapping_` 等代替。{{ std(page="std/primitive.isize.html#method.checked_add") }} |
| `200_u8 + _200` <sup>r</sup> | `144` | 在 release 模式下，这会溢出。 |
| `-128_i8 * -1` | 编译错误。 | 会导致溢出（`128_i8` 不存在）。 |
| `-128_i8 * _1neg` <sup>d</sup> | Panic。 | - |
| `-128_i8 * _1neg` <sup>r</sup> | `-128` | 在 release 模式下溢出回到 `-128`。 |
| `1_u8 / 2_u8` | `0` | 其他整数除法会截断。 |
| `0.8_f32 + 0.1_f32` | `0.90000004` | - |
| `1.0_f32 / 0.0_f32` | `f32::INFINITY` | - |
| `0.0_f32 / 0.0_f32` | `f32::NAN` | - |
| `x < f32::NAN` | `false` | `NAN` 的比较总是返回 false。 |
| `x > f32::NAN` | `false` | `NAN` 的比较总是返回 false。 |
| `f32::NAN == f32::NAN` | `false` | 使用 `f32::is_nan()` {{ std(page="std/primitive.f32.html#method.is_nan") }} 代替。 |

</div></panel></tab>


<!-- End tabs -->
</tabs>

<!-- End overflow prevention -->
</div></div>


<footnotes>

<sup>1</sup> 表达式 `_100` 表示任何可能包含值 `100` 的内容，例如 `100_i32`，但对编译器来说是不可见的。<br/>
<sup>d</sup> Debug 构建。<br/>
<sup>r</sup> Release 构建。<br/>

</footnotes>


{{ tablesep() }}



#### 文本类型 {{ ref(page="types/textual.html") }}


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>char</code></name>
    <visual class="char">
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
        <byte><code></code></byte>
    </visual>
    <description>任何 Unicode 标量。</description>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>str</code></name>
    <visual>
        <note>…</note>
        <byte class="bytes"><code>U</code></byte>
        <byte class="bytes"><code>T</code></byte>
        <byte class="bytes"><code>F</code></byte>
        <byte class="bytes"><code>-</code></byte>
        <byte class="bytes"><code>8</code></byte>
        <note>… unspecified times</note>
    </visual>
    <description>很少单独出现，而是以 <code>&str</code> 的形式出现。</description>
</datum>


{{ tablesep() }}

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-3" name="tab-group-textual" checked>
<label for="tab-textual-3"><b>基础</b></label>
<panel><div>

| 类型 | 描述 |
|---------|-------------|
| `char` | 总是占用 4 字节，并且只保存一个 Unicode **标量值** {{ link(url="https://www.unicode.org/glossary/#unicode_scalar_value") }}. |
| `str` | 一个未知长度的 `u8` 数组，保证保存的是 **UTF-8 编码的代码点**。|

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-1" name="tab-group-textual">
<label for="tab-textual-1"><b>用法</b></label>
<panel><div>



<!-- Notice how:

- `char` is always 4 bytes and only holds a single Unicode **scalar value** {{ link(url="https://www.unicode.org/glossary/#unicode_scalar_value") }}, thus possibly wasting space.
- `str` is a byte-array of unknown length guaranteed to hold **UTF-8 encoded code points** (but harder to index).
 -->

| 字符 | 描述 |
|---------|-------------|
| `let c = 'a';` | 通常情况下，一个 `char`（Unicode 标量）可以符合你对 _字符_ 的直觉。 |
| `let c = '❤';` | 它也可以保存许多 Unicode 符号。|
| `let c = '❤️';` | 但并非总是如此。给定的表情符号是**两个** `char`（参见编码部分），因此 **无法** {{ bad() }} 由 `c` 保存。<sup>1</sup> |
| `c = 0xffff_ffff;` | 此外，`char` **不允许** {{ bad() }} 保存任意的位模式。|

<footnotes>
    <sup>1</sup> 有趣的是，由于 <a href="https://en.wikipedia.org/wiki/Zero-width_joiner">零宽度连接符</a> (⨝)，用户<em>感知为一个字符</em>的内容可能会变得更加不可预测：👨‍👩‍👧 实际上是 5 个字符 👨⨝👩⨝👧，渲染引擎可以根据它们的能力自由地将它们显示为一个合并的符号，或分别显示为三个。
</footnotes>


{{ tablesep() }}

| 字符串 | 描述 |
|---------|-------------|
| `let s = "a";` | `str` 通常不会直接持有，而是通过 `&str`，比如这里的 `s`。 |
| `let s = "❤❤️";` | 它可以保存任意文本，每个字符长度不固定，且难以索引。 |


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-textual-2" name="tab-group-textual">
<label for="tab-textual-2"><b>编码</b>{{ esoteric() }}</label>
<panel><div>


`let s = "I ❤ Rust"; ` <br>
`let t = "I ❤️ Rust";`

| 变体 | 内存表示<sup>2<sup> |
|---------|-------------|
| `s.as_bytes()` | `49` `20` <span class="force-code-color same-black"><b>`e2 9d a4`</b> </span> `20 52 75 73 74` <sup>3<sup> |
| `t.as_bytes()` | `49` `20` <span class="force-code-color same-black"><b>`e2 9d a4`</b> </span> <span class="force-code-color same-red"><b>`ef b8 8f`</b></span> `20 52 75 73 74` <sup>4<sup> |
| `s.chars()`<sup>1<sup> | `49 00 00 00 20 00 00 00` <span class="force-code-color same-black"><b>`64 27 00 00` </b></span> `20 00 00 00 52 00 00 00 75 00 00 00 73 00` &hellip; |
| `t.chars()`<sup>1<sup> | `49 00 00 00 20 00 00 00` <span class="force-code-color same-black"><b>`64 27 00 00`</b></span> <span class="force-code-color same-red"><b>`0f fe 01 00`</b></span> `20 00 00 00 52 00 00 00 75 00` &hellip; |

{{ tablesep() }}

<footnotes>
    <sup>1</sup> 然后将结果收集到数组中，并转变为字节。<br>
    <sup>2</sup> 在 x86 上以十六进制表示的值。<br>
    <sup>3</sup> 请注意，<code>❤</code> 具有 <a href="https://codepoints.net/U+2764">Unicode 码点 (U+2764)</a>，在 <code>char</code> 中表示为 <span class="force-code-color same-black"><b>64 27 00 00</b></span>，但在 <code>str</code> 中被 <a href="https://en.wikipedia.org/wiki/UTF-8#Description">UTF-8 编码为</a> <span class="force-code-color same-black"><b>e2 9d a4</b></span>。<br>
    <sup>4</sup> 还要注意，表情符号 <a href="https://emojipedia.org/red-heart/">红色爱心 <code>❤️</code></a> 是 <code>❤</code> 和 <a href="https://codepoints.net/U+FE0F">U+FE0F 变体选择符</a> 的组合，因此 <code>t</code> 的字符数比 <code>s</code> 多。
</footnotes>

{{ tablesep() }}


<footnotes>

> <sup>⚠️</sup> 由于一些似乎是浏览器的错误，Safari 和 Edge 会错误地渲染脚注 3 和 4 中的爱心符号，尽管它们在上面的 `s` 和 `t` 中可以正确区分。

</footnotes>

</div></panel></tab>


<!-- End tabs -->
</tabs>


{{ tablesep() }}


## Custom Types

用户可以定义的基本类型。实际的<b>布局</b> {{ ref(page="type-layout.html") }} 取决于<b>表示</b>；{{ ref(page="type-layout.html#representations") }} 可能包含填充。


<!-- NEW ENTRY -->
<datum class="spaced">
    <name class="nogrow"><code>T</code></name>
    <name class="hidden">x</name>
    <visual>
       <framed class="any t"><code>T</code></framed>
    </visual>
    <description>Sized {{ below(target = "#sized-types") }} </description>
</datum>

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>T: ?Sized</code></name>
    <visual>
       <framed class="any unsized"><code>T</code></framed>
    </visual>
    <description>可能是 DST {{ below(target = "#sized-types") }} </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>[T; n]</code></name>
    <visual>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <note>… n 次</note>
    </visual>
    <description>固定长度的 <code>n</code> 元素数组。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>[T]</code></name>
    <visual>
       <note>…</note>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <framed class="any t"><code>T</code></framed>
       <note>… 不定次数</note>
    </visual>
    <description><b>切片类型</b>，包含未知数量的元素。既不是<br> <code>Sized</code>（也不携带 <code>len</code> 信息），通常<br>在引用后面，如 <code>&[T]</code>。{{ below(target="#references-pointers-ui") }}</description>
</datum>

<!-- NEW ENTRY -->
<datum style="margin-right:70px; position: relative; width: 70px;">
    <name class="nogrow"><code>struct S;</code></name>
    <name class="hidden"><code>;</code></name>
    <visual style="width: 15px;" class="zst">
        <code></code>
    </visual>
    <description>零大小 {{ below(target = "#sized-types") }} </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>(A, B, C)</code></name>
    <visual style="width: 182px;">
       <framed class="any"><code>A</code></framed>
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <andor>或者可能是</andor>
    <visual style="width: 182px;">
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any"><code>A</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <description>除非强制指定了表示方式<br>（例如，通过 <code>#[repr(C)]</code>），类型布局<br>是未指定的。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>struct S { b: B, c: C } </code></name>
    <visual style="width: 166px;">
       <framed class="any" style="width: 100px;"><code>B</code></framed>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
    </visual>
    <andor>或者可能是</andor>
    <visual>
       <framed class="any" style="width: 50px;"><code>C</code></framed>
       <pad><code style="">↦</code></pad>
       <framed class="any" style="width: 100px;"><code>B</code></framed>
    </visual>
    <description>编译器可能还会添加填充。</description>
</datum>



<blockquote>
<footnotes>

另请注意，两个具有完全相同字段的类型 `A(X, Y)` 和 `B(X, Y)` 仍然可以具有不同的布局；在没有表示保证的情况下，绝不要 `transmute()` {{ std(page="std/mem/fn.transmute.html") }}。

</footnotes>
</blockquote>



{{ tablesep() }}

这些 **和类型** 保存其子类型中的某一个值：

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>enum E { A, B, C }</code></name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any">
            <code>A</code>
        </framed>
    </visual>
    <andor>互斥地或</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 100px;">
            <code>B</code>
        </framed>
    </visual>
    <andor>互斥地或</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 50px;">
            <code>C</code>
        </framed>
    </visual>
    <description>
        安全地保存 A、B 或 C，也<br>称为'标记联合'，但<br>编译器可能将标签压缩<br>到'未使用'的位中。
    </description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>union { … }</code></name>
    <visual style="text-align: left;">
        <framed class="any">
            <code>A</code>
        </framed>
    </visual>
    <andor>不安全地或</andor>
    <visual style="text-align: left;">
        <framed class="any" style="width: 100px;">
            <code>B</code>
        </framed>
    </visual>
    <andor>不安全地或</andor>
    <visual style="text-align: left;">
        <framed class="any" style="width: 50px;">
            <code>C</code>
        </framed>
    </visual>
    <description>
        可以不安全地重新解释<br>内存。结果可能<br>是未定义的。
    </description>
</datum>



## References & Pointers {#references-pointers-ui}

引用提供对第三方内存的安全访问，而原始指针 `unsafe` 访问。对应的 `mut` 类型和它们的不可变对应类型具有相同的数据布局。


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>必须指向一些有效的 <code>t</code> 类型为 <code>T</code>，<br> 并且任何这样的目标必须至少存在于 <br> 生命周期 <code>'a</code> 之内。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>*const T</code></name>
    <visual class="unsafe">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <zoom>
        没有任何保证。
    </zoom>
</datum>

<br/>


### Pointer Meta {#pointer-meta}

许多引用和指针类型可以携带一个额外的字段，称为 **指针元数据**。{{ std(page="nightly/std/ptr/trait.Pointee.html#pointer-metadata") }} 它可以是目标的元素长度或字节长度，或指向一个 <i>虚表（vtable）</i> 的指针。具有元数据的指针称为 **胖指针**，否则称为 **瘦指针**。

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any t"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>对于已知大小的目标没有元数据。<br>（指针是瘦的）。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a T</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry>
        <memory-link style="left:46%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>如果 <code>T</code> 是一个 DST <code>struct</code>，如 <br> <code>S { x: [u8] }</code>，元数据字段 <code>len</code> 表示 <br>动态大小内容的计数。</description>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a [T]</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:24%;">|</memory-link>
        <memory class="anymem">
            …
            <framed class="any" style="width: 30px;"><code>T</code></framed>
            <framed class="any" style="width: 30px;"><code>T</code></framed>
            …
        </memory>
    </memory-entry>
    <description>常规的<b>切片引用</b>（即，切片类型 <code>[T]</code> 的引用类型）{{ above (target="#custom-types") }} <br> 通常写作 <code>&[T]</code>，如果省略了 <code>'a</code>。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>&'a str</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:24%;">|</memory-link>
        <memory class="anymem">
            …
            <byte class="bytes"><code>U</code></byte>
            <byte class="bytes"><code>T</code></byte>
            <byte class="bytes"><code>F</code></byte>
            <byte class="bytes"><code>-</code></byte>
            <byte class="bytes"><code>8</code></byte>
            …
        </memory>
    </memory-entry>
    <description><b>字符串切片引用</b>（即，字符串类型 <code>str</code> 的引用类型），<br>元数据 <code>len</code> 表示字节长度。</description>
</datum>

<br>

<!-- NEW ENTRY -->
<datum class="spaced" style="padding-bottom: 165px; position: relative;">
    <name><code>&'a dyn Trait</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <ptr>
            <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <memory-entry>
        <memory-link style="left:49%;">|</memory-link>
        <memory class="anymem">
            <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <memory-entry style="width:220px; position: absolute;">
        <memory-link style="left:22%;">|</memory-link>
        <memory class="static-vtable" style="width: 210px;">
            <table>
                <tr class="vtable"><td><code>*Drop::drop(&mut T)</code></td></tr>
                <tr class="vtable"><td><code>size</code></td></tr>
                <tr class="vtable"><td><code>align</code></td></tr>
                <tr class="vtable"><td><code>*Trait::f(&T, …)</code></td></tr>
                <tr class="vtable"><td><code>*Trait::g(&T, …)</code></td></tr>
            </table>
        </memory>
        <description>元数据指向虚表，其中 <code>*Drop::drop()</code>，<code>*Trait::f()</code> 等为指向 <code>T</code> 相应 <code>impl</code> 的指针。</description>
    </memory-entry>

</datum>


## Closures {#closures-data}

具有自动管理数据块的特设函数，它**捕获**{{ ref(page="types/closure.html#capture-modes") }}<sup>1</sup>定义闭包时的环境。例如，如果你有：

```rust
let y = ...;
let z = ...;

with_closure(move |x| x + y.f() + z); // y and z are moved into closure instance (of type C1)
with_closure(     |x| x + y.f() + z); // y and z are pointed at from closure instance (of type C2)
```

那么传递给 `with_closure()` 的生成的匿名闭包类型 `C1` 和 `C2` 将如下所示：

<!-- NEW ENTRY -->
<datum class="doublespaced">
    <name><code>move |x| x + y.f() + z</code></name>
    <visual>
       <framed class="any" style="width: 100px;"><code>Y</code></framed>
       <framed class="any" style="width: 50px;"><code>Z</code></framed>
    </visual>
    <zoom>匿名闭包类型 C1</zoom>
    <!-- <description>Also produces anonymous <br><code>f<sub>c1</sub> (c: C1, x: T)</code>. Details depend<br> which <code>FnOnce</code>, <code>FnMut</code>, <code>Fn</code> is allowed.</description> -->
</datum>


<!-- NEW ENTRY -->
<datum class="">
    <name><code>|x| x + y.f() + z</code></name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <zoom>匿名闭包类型 C2</zoom>
    <memory-entry>
        <memory-link style="left:44%;">|</memory-link>
        <memory class="anymem">
            <framed class="any" style="width: 30px;"><code>Y</code></framed>
        </memory>
    </memory-entry>
    <memory-entry>
        <memory-link style="left:44%;">|</memory-link>
        <memory class="anymem">
            <framed class="any" style="width: 30px;"><code>Z</code></framed>
        </memory>
    </memory-entry>
    <!-- <description>Similar, but captured context by<br> reference. Details might differ <br> depending on types involved.</description> -->
</datum>

<!-- Little hack as description below was too cluttered. -->
<!-- <datum>
    <name>&nbsp;</name>
    <description>
    Also produces anonymous <code>fn</code> such as <code>f_c1 (C1, X)</code> or <br>
    <code>f_c2 (&C2, X)</code>. Details depend which <code>FnOnce</code>, <code>FnMut</code>, <code>Fn</code> ...<br>
    is supported, based on properties of captured types.
    </description>
</datum> -->

<blockquote>
<footnotes>

还会生成匿名 <code>fn</code>，例如 <code>f<sub>c1</sub>(C1, X)</code> 或 <code>f<sub>c2</sub>(&C2, X)</code>。细节取决于根据捕获类型的属性支持哪种 <code>FnOnce</code>，<code>FnMut</code>，<code>Fn</code> 等。

</footnotes>
</blockquote>


<footnotes>

<sup>1</sup> 简单来说，闭包是一种便于书写的“迷你函数”，它接受参数，而且还需要一些局部变量来完成它的工作。因此它既是一个类型（包含所需的局部变量），也是一个函数。_“捕获环境”_ 是一种花哨的说法，用于描述闭包类型如何持有这些局部变量，或者通过_移动值_，或者通过_指针_。请参见 **API 中的闭包** {{ below(target="#closures-in-apis") }} 了解各种相关影响。

</footnotes>


## Standard Library Types


Rust 的标准库将上述原始类型组合成具有特殊语义的有用类型，例如：


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>UnsafeCell&lt;T&gt;</code> {{ std(page="std/cell/struct.UnsafeCell.html") }}</name>
    <visual class="cell">
           <framed class="any unsized"><code>T</code></framed>
    </visual>
    <description>允许别名可变性的<br>神奇类型。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Cell&lt;T&gt;</code> {{ std(page="std/cell/struct.Cell.html") }}</name>
    <visual>
           <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <description>允许 <code>T</code> 移入<br>和移出。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>RefCell&lt;T&gt;</code> {{ std(page="std/cell/struct.RefCell.html") }}</name>
    <visual>
        <sized class="celled"><code>borrowed</code></sized>
        <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <description>也支持 <code>T</code> 的动态借用。<br>类似于 <code>Cell</code>，<code>RefCell</code> 是 <code>Send</code>，但不是 <code>Sync</code>。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>ManuallyDrop&lt;T&gt;</code> {{ std(page="std/mem/struct.ManuallyDrop.html") }}</name>
    <visual>
           <framed class="any unsized"  style="width: 100px;"><code>T</code></framed>
    </visual>
    <description>防止调用 <code>T::drop()</code>。</description>
</datum>

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>AtomicUsize</code> {{ std(page="std/sync/atomic/index.html") }}</name>
    <visual class="atomic">
        <ptr class="atomic">
            <code>usize</code><sub>2/4/8</sub>
        </ptr>
    </visual>
    <description>其他原子类型类似。</description>
</datum>


<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Option&lt;T&gt;</code> {{ std(page="std/option/enum.Option.html") }}</name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
    </visual>
    <andor>or</andor>
    <visual class="enum">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 100px;">
            <code>T</code>
        </framed>
    </visual>
    <description>对于某些类型 T，可以省略标签，<br>例如 <code>NonNull</code>。{{ std(page="std/ptr/struct.NonNull.html") }}</description>
</datum>



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Result&lt;T, E&gt;</code> {{ std(page="std/result/enum.Result.html") }}</name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 50px;">
            <code>E</code>
        </framed>
    </visual>
    <andor>or</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any" style="width: 100px;">
            <code>T</code>
        </framed>
    </visual>
    <description>要么是一些错误 <code>E</code>，要么是<br>值 <code>T</code>。</description>
</datum>

<!-- NEW ENTRY -->
<datum>
    <name><code>MaybeUninit&lt;T&gt;</code><span style="position: absolute;"> {{ std(page="std/mem/union.MaybeUninit.html") }}</span></name>
    <visual class="enum">
        <framed class="uninit" style="width: 100px;">
            <code>U̼̟̔͛n̥͕͐͞d̛̲͔̦̳̑̓̐e̱͎͒̌fị̱͕̈̉͋ne̻̅ḓ̓</code>
        </framed>
    </visual>
    <andor>unsafe or</andor>
    <visual class="enum">
        <framed class="any" style="width: 100px;">
            <code>T</code>
        </framed>
    </visual>
    <description>未初始化的内存或某些<br><code>T</code>。唯一合法处理未初始化数据的方法。</description>
</datum>


> {{bad()}} 所有描述均为 **示意** 用途。
> 字段应存在于最新的 `stable` 中，但 Rust 对它们的布局没有任何保证，除非文档允许，否则不应尝试 _不安全_ 访问任何内容。

{{ tablesep() }}


#### Order-Preserving Collections



<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Box&lt;T&gt;</code> {{ std(page="std/boxed/struct.Box.html") }}</name>
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <memory-entry>
        <memory-link style="left:49%;">|</memory-link>
        <memory class="heap">
        <framed class="any unsized"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>对于某些 <code>T</code>，栈代理可能携带<br>元数据{{ above (target="#custom-types") }}（例如 <code>Box<[T]></code>）。</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>Vec&lt;T&gt;</code> {{ std(page="std/vec/struct.Vec.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap capacity">
            <div>
                <framed class="any t"><code>T</code></framed>
                <framed class="any t"><code>T</code></framed>
                <note>… len</note>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
    <description>单一类型的常规<i>可增长数组</i>向量。</description>
</datum>

<spacer>
</spacer>


<!-- NEW ENTRY -->
<datum>
    <name><code>LinkedList&lt;T&gt;</code> {{ std(page="std/collections/struct.LinkedList.html") }}{{ esoteric() }} </name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>head</code><sub>2/4/8</sub>
        </ptr>
        <ptr>
           <code>tail</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry style="width: 265px; left:0%; display: block;">
        <memory-link style="left:25%;">|</memory-link>
        <memory-link style="left:50%;">|</memory-link>
        <memory class="heap capacity">
            <ptr>
            <code>next</code><sub>2/4/8</sub>
            </ptr>
            <ptr>
            <code>prev</code><sub>2/4/8</sub>
            </ptr>
            <framed class="any t"><code>T</code></framed>
        </memory>
    </memory-entry>
    <description>元素 <code>头部</code> 和 <code>尾部</code> 均为 <code>null</code> 或指向堆上的节点。<br>每个节点都可以指向其 <code>上一个</code> 和 <code>下一个</code> 节点。<br>吞噬你的缓存（看看这个东西吧！）；除非显然必须使用，<br>否则不要用。{{ bad() }} </description>
</datum>


<spacer>
</spacer>



<!-- NEW ENTRY -->
<datum>
    <name><code>VecDeque&lt;T&gt;</code> {{ std(page="std/collections/struct.VecDeque.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <sized>
            <code>head</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry></memory-entry>
    <memory-entry></memory-entry>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap capacity">
            <div>
                <!-- <framed class="any t"><code>T<sub>x</sub></code></framed> -->
                <framed class="any t"><code>T</code></framed>
                <!-- <framed class="any t"><code>T</code></framed> -->
                <note>… empty …</note>
                <framed class="any t"><code>T&#x2063;<sup>H</sup></code></framed>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
    <description>索引 <code>头部</code> 在数组中选择作为环形缓冲区。这意味着内容可能<br>是不连续的，且中间可能是空的，如上例所示。</description>
</datum>



{{ tablesep() }}

#### Other Collections


<!-- NEW ENTRY -->
<datum>
    <name><code>HashMap&lt;K, V&gt;</code> {{ std(page="std/collections/struct.HashMap.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <sized>
            <code>bmask</code><sub>2/4/8</sub>
        </sized>
        <ptr>
           <code>ctrl</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>left</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry></memory-entry>
    <memory-entry style="width: 265px; left:-5%">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap oversimplified">
            <framed class="any t"><code>K:V</code></framed>
            <framed class="any t"><code>K:V</code></framed>
            …
            <framed class="any t"><code>K:V</code></framed>
            …
            <framed class="any t"><code>K:V</code></framed>
            <capacity><note style="font-weight: bolder;">Oversimplified!</note></capacity>
        </memory>
    </memory-entry>
    <description>根据哈希值将键和值存储在堆上，使用 <a href="https://www.youtube.com/watch?v=ncHmEUmJZf4">SwissTable</a><br> 实现方式通过 <a href="https://github.com/rust-lang/hashbrown">hashbrown</a>。<code>HashSet</code> {{ std(page="std/collections/struct.HashSet.html") }} 与 <code>HashMap</code> 相同，<br>仅类型 <code>V</code> 消失了。堆视图过度简化了。{{bad()}} </description>
</datum>


<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>BinaryHeap&lt;T&gt;</code> {{ std(page="std/collections/struct.BinaryHeap.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry style="width: 265px">
        <memory-link style="left:20%;">|</memory-link>
        <memory class="heap capacity">
            <div>
                <framed class="any t"><code>T&#x2063;<sup style="color:black; font-weight: bolder;">0</sup></code></framed>
                <framed class="any t" style="background-color: #f9b172;"><code>T&#x2063;<sup style="color:black; font-weight: bolder;">1</sup></code></framed>
                <framed class="any t" style="background-color: #f9b172;"><code>T&#x2063;<sup style="color:black; font-weight: bolder;">1</sup></code></framed>
                <framed class="any t" style="background-color: #f9d372;"><code>T&#x2063;<sup style="color:black; font-weight: bolder;">2</sup></code></framed>
                <framed class="any t" style="background-color: #f9d372;"><code>T&#x2063;<sup style="color:black; font-weight: bolder;">2</sup></code></framed>
                <note>… len</note>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
    <description>堆作为数组存储，每层有 <code>2<sup>N</sup></code> 个元素。每个 <code>T</code><br> 在其下层可以有两个子节点。每个 <code>T</code> 大于其子节点。</description>
</datum>



#### Owned Strings


<!-- NEW ENTRY -->
<datum>
    <name><code>String</code> {{ std(page="std/string/struct.String.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>capacity</code><sub>2/4/8</sub>
        </sized>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>U</code></byte>
                <byte class="bytes"><code>T</code></byte>
                <byte class="bytes"><code>F</code></byte>
                <byte class="bytes"><code>-</code></byte>
                <byte class="bytes"><code>8</code></byte>
                <note>… len</note>
            </div>
            <capacity>← <note>capacity</note> →</capacity>
        </memory>
    </memory-entry>
    <description>观察 <code>String</code> 如何不同于 <code>&str</code> 和 <code>&[char]</code>。</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>CString</code> {{ std(page="std/ffi/struct.CString.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual>
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <sized>
            <code>len</code><sub>2/4/8</sub>
        </sized>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code>A</code></byte>
                <byte class="bytes"><code>B</code></byte>
                <byte class="bytes"><code>C</code></byte>
                <note>… len …</note>
                <byte class="bytes"><code>∅</code></byte>
            </div>
        </memory>
    </memory-entry>
    <description>以 NUL 结尾，但中间没有 NUL。</description>
</datum>


<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>OsString</code> {{ std(page="std/ffi/struct.OsString.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual class="platformdefined">
        Platform Defined
    </visual>
    <memory-entry class="double">
        <memory-link style="left:25%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code> </code></byte>
                <byte class="bytes"><code> </code></byte>
                /
                <word class="bytes"><code> </code></word>
                <word class="bytes"><code> </code></word>
            </div>
        </memory>
    </memory-entry>
    <description>封装操作系统表示字符串的方式<br>（例如，在 Windows 上使用 <a href="https://simonsapin.github.io/wtf-8/">WTF-8</a>）。</description>
</datum>

<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum>
    <name><code>PathBuf</code> {{ std(page="std/path/struct.PathBuf.html") }}</name>
    <!-- For some reason we need the width for mobile not to line break -->
    <visual class="platformdefined">
        <payload>
            <code>OsString</code>
        </payload>
    </visual>
    <memory-entry class="double">
        <memory-link style="left:40%;">|</memory-link>
        <memory class="heap">
            <div>
                <byte class="bytes"><code> </code></byte>
                <byte class="bytes"><code> </code></byte>
                /
                <word class="bytes"><code> </code></word>
                <word class="bytes"><code> </code></word>
            </div>
        </memory>
    </memory-entry>
    <description>封装操作系统<br>表示路径的方式。</description>
</datum>


{{ tablesep() }}

#### Shared Ownership

如果类型不包含 `Cell` 对 `T`，这些类型通常与上述 `Cell` 类型之一结合使用，以允许共享的事实上的可变性。

<!-- NEW ENTRY -->
<datum>
    <name><code>Rc&lt;T&gt;</code> {{ std(page="std/rc/struct.Rc.html") }}</name>
    <visual style="width: 180px;">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <div>
        <memory-entry class="quad">
            <memory-link style="left:15%;">|</memory-link>
            <memory class="heap">
                <sized class="celled"><code>strng</code><sub>2/4/8</sub></sized>
                <sized class="celled"><code>weak</code><sub>2/4/8</sub></sized>
                <framed class="any unsized"><code>T</code></framed>
            </memory>
        </memory-entry>
    </div>
    <description>在同一个线程中共享 <code>T</code> 的所有权。需要嵌套的 <code>Cell</code><br> 或 <code>RefCell</code> 以允许修改。既不是 <code>Send</code> 也不是 <code>Sync</code>。</description>
</datum>


<!-- NEW ENTRY -->
<datum>
    <name><code>Arc&lt;T&gt;</code> {{ std(page="std/sync/struct.Arc.html") }}</name>
    <visual style="width: 180px;">
        <ptr>
           <code>ptr</code><sub>2/4/8</sub>
        </ptr>
        <payload>
            <code>meta</code><sub>2/4/8</sub>
        </payload>
    </visual>
    <div style="width: 0px;">
        <memory-entry class="quad">
            <memory-link style="left:15%;">|</memory-link>
            <memory class="heap">
                <sized class="atomicx"><code>strng</code><sub>2/4/8</sub></sized>
                <sized class="atomicx"><code>weak</code><sub>2/4/8</sub></sized>
                <framed class="any unsized"><code>T</code></framed>
            </memory>
        </memory-entry>
    </div>
    <description>相同，但允许在线程之间共享<br>前提是所包含的 <code>T</code> 本身是 <code>Send</code> 和 <code>Sync</code>。</description>
</datum>

<br>

<!-- NEW ENTRY -->
<datum>
    <name><code>Mutex&lt;T&gt;</code> {{ std(page="std/sync/struct.Mutex.html") }} / <code>RwLock&lt;T&gt;</code> {{ std(page="std/sync/struct.RwLock.html") }}</name>
    <visual style="width: 230px;">
        <payload><code>inner</code></payload>
        <sized class="atomicx"><code>poison</code><sub>2/4/8</sub></sized>
        <framed class="any unsized celled"><code>T</code></framed>
    </visual>
    <description>内部字段取决于平台。需要在 <code>Arc</code> 中才能在分离的<br>线程之间共享，或通过 <code>scope()</code> {{ std(page="std/thread/fn.scope.html") }} 用于有作用域的线程。</description>
</datum>

<spacer>
</spacer>
<spacer>
</spacer>

<!-- NEW ENTRY -->
<datum class="spaced">
    <name><code>Cow&lt;'a, T&gt;</code> {{ std(page="std/borrow/enum.Cow.html") }}</name>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="any unsized" style="width: 100px; text-align: center;">
            <code>T::Owned</code>
        </framed>
    </visual>
    <andor>or</andor>
    <visual class="enum" style="text-align: left;">
        <pad><code>Tag</code></pad>
        <framed class="ptr" style="width: 50px;">
           <code>ptr</code><sub>2/4/8</sub>
        </framed>
    </visual>
    <div>
        <memory-entry style="width: 40px;"></memory-entry>
        <memory-entry>
            <memory-link style="left:15%;">|</memory-link>
            <memory class="anymem">
                <framed class="any unsized"><code>T</code></framed>
            </memory>
        </memory-entry>
    </div>
    <description>保存对某些 <code>T</code> 的只读引用，<br>或拥有其 <code>ToOwned</code> {{ std(page="std/borrow/trait.ToOwned.html") }} 类似物。</description>
</datum>




---


# Standard Library


## One-Liners

一些常见的代码片段，但可能容易被遗忘。请参阅 **Rust Cookbook** {{ link(url="https://rust-lang-nursery.github.io/rust-cookbook/") }} 获取更多信息。


<!--
PRs for this section are very welcome. Idea is:
- Should be `std` only for now, no 3rd party libs (maybe exception for `rand`?)
- "Most people" should have encountered the problem
- Is not just a trival method on an 'obvious' struct (e.g., Sort a slice by `x.sort()` is probably too obvious.)
-->

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


<tabs>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-2" name="tab-api-sized" checked>
<label for="tab-api-2"><b>字符串</b></label>
<panel><div class="color-header one-liners cheats">

| 用途 | 代码片段 |
|---------|-------------|
| 拼接字符串（任何实现了 `Display` 的类型）{{ below(target="#string-output") }}。 {{ std(page="std/fmt/index.html") }} <sup>1</sup>  {{ edition(ed="'21") }} | `format!("{x}{y}")` |
| 附加字符串（任何 `Display` 到任何 `Write`）。  {{ edition(ed="'21") }} {{ std(page="std/fmt/index.html#write") }} | `write!(x, "{y}")` |
| 按分隔符模式分割字符串。 {{ std(page="std/str/pattern/trait.Pattern.html") }} {{ link(url="https://stackoverflow.com/a/38138985") }} | `s.split(pattern)` |
| {{ tab() }} … 使用 `&str` | `s.split("abc")` |
| {{ tab() }} … 使用 `char` | `s.split('/')` |
| {{ tab() }} … 使用闭包 | `s.split(char::is_numeric)`|
| 按空白符分割字符串。 {{ std(page="std/primitive.str.html#method.split_whitespace") }} | `s.split_whitespace()` |
| 按换行符分割字符串。 {{ std(page="std/primitive.str.html#method.lines") }}  | `s.lines()` |
| 按正则表达式分割字符串。 {{ link(url="https://docs.rs/regex/latest/regex/struct.Regex.html#method.split") }} <sup>2</sup> | `Regex::new(r"\s")?.split("one two three")` |

<footnotes>

<sup>1</sup> 会分配内存；如果 `x` 或 `y` 之后不再使用，可以考虑使用 `write!` 或 `std::ops::Add`。<br>
<sup>2</sup> 需要 [regex](https://crates.io/crates/regex) crate。

</footnotes>


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-1" name="tab-api-sized">
<label for="tab-api-1"><b>I/O</b></label>
<panel><div class="color-header one-liners cheats">

| 用途 | 代码片段 |
|---------|-------------|
| 创建新文件 {{ std(page="std/fs/struct.File.html#method.open") }} | `File::create(PATH)?`  |
| {{ tab() }} 使用 OpenOptions 创建新文件 | `OpenOptions::new().create(true).write(true).truncate(true).open(PATH)?` |
| 将文件读取为 `String` {{ std(page="std/fs/fn.read_to_string.html") }} | `read_to_string(path)?` |

<!-- <footnotes>

<sup>*</sup> We're a bit short on space here, <code>t</code> means true.

</footnotes> -->

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-4" name="tab-api-sized">
<label for="tab-api-4"><b>宏</b></label>
<panel><div class="color-header one-liners cheats">

| 用途 | 代码片段 |
|---------|-------------|
| 使用可变参数的宏 | `macro_rules! var_args { ($($args:expr),*) => {{ }} }` |
| {{ tab() }} 使用 `args`，例如多次调用 `f` | {{ tab() }} ` $( f($args); )*` |

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-5" name="tab-api-sized">
<label for="tab-api-5"><b>转换 {{ hot() }}</b></label>
<panel><div class="color-header one-liners cheats">

| 起始类型 | 资源 |
|---------|-------------|
| `Option<T> -> …` | 请参阅 [基于类型的速查表](https://upsuper.github.io/rust-cheatsheet/) |
| `Result<T, R> -> …` | 请参阅 [基于类型的速查表](https://upsuper.github.io/rust-cheatsheet/) |
| `Iterator<Item=T> -> …` | 请参阅 [基于类型的速查表](https://upsuper.github.io/rust-cheatsheet/) |
| `&[T] -> …` | 请参阅 [基于类型的速查表](https://upsuper.github.io/rust-cheatsheet/) |
| `Future<T> -> …` | 请参阅 [Futures 速查表](https://rufflewind.com/img/rust-futures-cheatsheet.html) |

<!-- <footnotes>

<sup>*</sup> We're a bit short on space here, <code>t</code> means true.

</footnotes> -->

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-api-3" name="tab-api-sized">
<label for="tab-api-3"><b>深奥用法</b>{{ esoteric() }}</label>
<panel><div class="color-header one-liners cheats">

| 用途 | 代码片段 |
|---------|-------------|
| 更干净的闭包捕获 | <code>wants_closure({ let c = outer.clone(); move &vert;&vert; use_clone(c) })</code> |
| 在 `try` 闭包中修复类型推断 | <code>iter.try_for_each(&vert;x&vert; { Ok::<(), Error>(()) })?;</code> |
| 迭代并编辑 `&mut [T]`，前提 `T` 是 Copy。 | `Cell::from_mut(mut_slice).as_slice_of_cells()` |
| 获取具有特定长度的子切片。 | `&original_slice[offset..][..length]` |
| 使用 canary 使 trait `T` 成为对象安全。 | `const _: Option<&dyn T> = None;` |
| 使用 _语义版本控制技巧_ 统一类型。{{ link(url="https://github.com/dtolnay/semver-trick") }} | 在 `Cargo.toml` 中使用 `my_crate = "next.version"` 并重新导出类型。 |
| 在自己的 crate 中使用宏。{{ link(url="https://users.rust-lang.org/t/use-macro-inside-proc-macro-crate/61095/4") }} | 使用 `macro_rules! internal_macro {}` 并加上 `pub(crate) use internal_macro;` |


</div></panel></tab>


</tabs>


</div></div>



## Thread Safety {#thread-safety}

假设你在线程1中持有一些变量，并希望将它们**移动**到线程2，或者将它们的**引用**传递给线程3。
是否允许这样做由 **`Send`** {{ std(page="std/marker/trait.Send.html") }} 和 **`Sync`**{{ std(page="std/marker/trait.Sync.html") }} 共同决定：

{{ tablesep() }}

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto; padding-top: 10px;">
<div style="min-width: 100%; width: 650px; ">
<div class="color-header number">


<threading-section>
    <thread-row>
        <thread-backdrop><hr></thread-backdrop>
        <values>
            <value class="both" style="left: 57px;"><thread-link>|<br>|<br>|</thread-link>&nbsp;Mutex&lt;u32&gt;</value>
            <value class="one" style="left: 97.5px;"><thread-link>|<br>|<br>|</thread-link>&nbsp;Cell&lt;u32&gt;</value>
            <value class="one" style="left: 137.5px;"><thread-link>|<br>|<br>|</thread-link>&nbsp;MutexGuard&lt;u32&gt;</value>
            <value class="none" style="left: 177.5px;"><thread-link>|<br>|<br>|</thread-link>&nbsp;Rc&lt;u32&gt;</value>
        </values>
        <subtext><blank-background>Thread 1</blank-background></subtext>
    </thread-row>
    <thread-row>
        <thread-backdrop><hr></thread-backdrop>
        <values>
            <value class="both" style="left: 77px;">&nbsp;Mutex&lt;u32&gt;</value>
            <value class="one" style="left: 117.5px;">&nbsp;Cell&lt;u32&gt;</value>
            <value class="disabled" style="left: 157.5px;">&nbsp;MutexGuard&lt;u32&gt;</value>
            <value class="disabled" style="left: 197.5px;">&nbsp;Rc&lt;u32&gt;</value>
        </values>
        <subtext><blank-background>Thread 2</blank-background></subtext>
    </thread-row>
    <thread-row>
        <thread-backdrop><hr></thread-backdrop>
        <values>
            <value class="both" style="left: 77px;"><b>&</b>Mutex&lt;u32&gt;</value>
            <value class="disabled" style="left: 117.5px;"><b>&</b>Cell&lt;u32&gt;</value>
            <value class="one" style="left: 157.5px;"><b>&</b>MutexGuard&lt;u32&gt;</value>
            <value class="disabled" style="left: 197.5px;"><b>&</b>Rc&lt;u32&gt;</value>
        </values>
        <subtext><blank-background>Thread 3</blank-background></subtext>
    </thread-row>
</threading-section>

</div>
</div>
</div>

{{ tablesep() }}

<div class="color-header sendsync">

| 示例 | 解释 |
| --- | --- |
| **`Mutex<u32>`** | 既是 `Send` 也是 `Sync`。可以安全地传递或借用到其他线程。 |
| **`Cell<u32>`** | `Send`，但不是 `Sync`。可以移动，但其引用可能会导致并发的非原子写入。 |
| **`MutexGuard<u32>`** | `Sync`，但不是 `Send`。锁定与线程绑定，但引用使用不会导致数据竞争。 |
| **`Rc<u32>`** | 既不是 `Send` 也不是 `Sync`，因为它是易于克隆的堆代理，带有非原子计数器。 |

</div>

{{ tablesep() }}

<!-- Shamelessly stolen from https://www.reddit.com/r/rust/comments/ctdkyr/understanding_sendsync/exk8grg/ -->
<table class="sendsync">
    <thead>
        <tr><th>Trait</th><th><code>Send</code></th><th><code>!Send</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Sync</code></td><td><i>Most types</i> … <code>Arc&lt;T&gt;</code><sup>1,2</sup>, <code>Mutex&lt;T&gt;</code><sup>2</sup></td><td><code>MutexGuard&lt;T&gt;</code><sup>1</sup>, <code>RwLockReadGuard&lt;T&gt;</code><sup>1</sup></td></tr>
        <tr><td><code>!Sync</code></td><td><code>Cell&lt;T&gt;</code><sup>2</sup>, <code>RefCell&lt;T&gt;</code><sup>2</sup></td><td><code>Rc&lt;T&gt;</code>, <code>&dyn Trait</code>, <code>*const T</code><sup>3</sup></td></tr>
    </tbody>
</table>

<footnotes>

<sup>1</sup> 如果 `T` 是 `Sync`。<br>
<sup>2</sup> 如果 `T` 是 `Send`。<br>
<sup>3</sup> 如果你需要发送一个裸指针，可以创建一个新类型 `struct Ptr(*const u8)` 并 `unsafe impl Send for Ptr {}`。只需确保你确实可以发送它。

</footnotes>



## Iterators {#iterators}

处理集合中的元素。

<tabs class="color-header iterators">

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-p0" name="tab-group-trait-iter" checked>
<label for="tab-trait-iter-p0"><b>基础</b></label>
<panel><div>


迭代集合主要有以下四种 _风格_：

| 风格 | 描述 |
| --- | --- |
| `for x in c { ... }` | _命令式_，适用于有副作用、相互依赖或需要提前中止流程的情况。 |
| `c.iter().map().filter()` | _函数式_，当只需要感兴趣的结果时通常更为简洁。 |
| `c_iter.next()` | _底层_，通过显式调用 `Iterator::next()` {{ std(page="std/iter/trait.Iterator.html#tymethod.next") }}。{{ esoteric() }} |
| `c.get(n)` | _手动_，绕过官方的迭代机制。 |

{{ tablesep() }}

> **观点** {{ opinionated() }} &mdash; 函数式风格通常最易于理解，但如果 `.iter()` 链条变得混乱，不妨使用 `for`。对于容器的实现，迭代器支持是理想的，但在赶时间时，只实现 `.len()` 和 `.get()` 有时更为实用。 


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-1" name="tab-group-trait-iter">
<label for="tab-trait-iter-1"><b>获取</b></label>
<panel><div>



**基础**

假设你有一个集合 `c`，其类型为 `C`，你想使用它：

* **`c.into_iter()`**<sup>1</sup>  &mdash; 将集合 `c` 转换为 **`Iterator`** {{ std(page="std/iter/trait.Iterator.html") }} `i`，并且 **消耗**<sup>2</sup> `c`。这是获取迭代器的标准方式。
* **`c.iter()`** &mdash; 一些集合提供的方便方法，返回一个 **借用的** 迭代器，不会消耗 `c`。
* **`c.iter_mut()`** &mdash; 相同，但返回的是 **可变借用的** 迭代器，可以修改集合。


**迭代器**

一旦你有了 `i`：

* **`i.next()`** &mdash; 返回集合 `c` 的下一个元素 `Some(x)`，如果没有了则返回 `None`。


**For 循环**

* **`for x in c {}`** &mdash; 语法糖，调用 `c.into_iter()` 并在迭代器 `i` 上循环直到 `None`。



<footnotes>

<sup>1</sup> 需要 `C` 实现 **`IntoIterator`** {{ std(page="std/iter/trait.IntoIterator.html") }}。生成的元素类型取决于 `C`。

<sup>2</sup> 如果看起来好像没有消耗 `c`，那可能是因为类型是 `Copy`。例如，如果你调用 `(&c).into_iter()`，它会在 `&c` 上调用 `.into_iter()`（这将消耗引用的 _副本_ 并将其转换为迭代器），但原始的 `c` 保持不变。

</footnotes>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-2" name="tab-group-trait-iter">
<label for="tab-trait-iter-2"><b>创建</b></label>
<panel><div>

**要点**

假设你编写了一个 `struct Collection<T> {}`。你还应该实现：


* **`struct IntoIter<T> {}`** &mdash; 创建一个结构体来保存迭代状态（例如索引），用于值迭代。
* **`impl Iterator for IntoIter<T> {}`** &mdash; 实现 `Iterator::next()`，以便它可以生成元素。

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted"><code>Collection&lt;T&gt;</code></type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>IntoIter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = T;</code></associated-type>
    </entry>
</mini-zoo>

{{ tablesep() }}

> 此时，你有了一个可以充当 **Iterator** {{ std(page="std/iter/trait.Iterator.html") }} 的结构体，但还没有实际获取它的方法。请参见下一个标签页了解通常如何实现。


</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-3" name="tab-group-trait-iter">
<label for="tab-trait-iter-3"><b>For 循环</b></label>
<panel><div>

**原生循环支持**

许多用户希望你的集合能在 `for` 循环中 _直接使用_。你需要实现：

* **`impl IntoIterator for Collection<T> {}`** &mdash; 现在 `for x in c {}` 可以使用。
* **`impl IntoIterator for &Collection<T> {}`** &mdash; 现在 `for x in &c {}` 可以使用。
* **`impl IntoIterator for &mut Collection<T> {}`** &mdash; 现在 `for x in &mut c {}` 可以使用。

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted"><code>Collection&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = T;</code></associated-type>
        <associated-type class="grayed"><code>To = IntoIter&lt;T&gt;</code></associated-type>
        <note>迭代 <code>T</code>.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted grayed"><code>&Collection&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &T;</code></associated-type>
        <associated-type class="grayed"><code>To = Iter&lt;T&gt;</code></associated-type>
        <note>迭代 <code>&T</code>.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry class="wide">
        <type class="generic dotted grayed"><code>&mut Collectn&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">IntoIterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &mut T;</code></associated-type>
        <associated-type class="grayed"><code>To = IterMut&lt;T&gt;</code></associated-type>
        <note>迭代 <code>&mut T</code>.</note>
    </entry>
</mini-zoo>

{{ tablesep() }}

> 正如你所看到的，**IntoIterator** {{ std(page="std/iter/trait.IntoIterator.html") }} 特性实际上将你的集合与前一个标签页中创建的 **IntoIter** 结构体连接了起来。**IntoIter** 的两个兄弟（**Iter** 和 **IterMut**）将在下一个标签页中讨论。


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-2b" name="tab-group-trait-iter">
<label for="tab-trait-iter-2b"><b>借用</b></label>
<panel><div>



**共享与可变迭代器**

此外，如果你希望你的集合在被借用时也能正常使用，则应实现：

* **`struct Iter<T> {}`** &mdash; 创建结构体来保存 `&Collection<T>` 状态，用于共享迭代。
* **`struct IterMut<T> {}`** &mdash; 类似，但保存 `&mut Collection<T>` 状态，用于可变迭代。
* **`impl Iterator for Iter<T> {}`** &mdash; 实现共享迭代。
* **`impl Iterator for IterMut<T> {}`** &mdash; 实现可变迭代。

还可以添加便捷方法：

- `Collection::iter(&self) -> Iter`,
- `Collection::iter_mut(&mut self) -> IterMut`.



<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>Iter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &T;</code></associated-type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>IterMut&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">Iterator</code></trait-impl>
        <associated-type class="grayed"><code>Item = &mut T;</code></associated-type>
    </entry>
</mini-zoo>

{{ tablesep() }}

> 借用迭代器支持的代码基本上是前面步骤的重复，只是类型稍有不同，例如 `&T` 和 `T`。


</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-trait-iter-4" name="tab-group-trait-iter">
<label for="tab-trait-iter-4"><b>互操作性</b></label>
<panel><div>


**迭代器互操作性**

要允许 **第三方迭代器** '收集为' 你的集合，需实现：

* **`impl FromIterator for Collection<T> {}`** &mdash; 现在 `some_iter.collect::<Collection<_>>()` 可以使用。
* **`impl Extend for Collection<T> {}`** &mdash; 现在 `c.extend(other)` 可以使用。

此外，还可以考虑为前面的结构体添加 **`std::iter`** {{ std(page="std/iter/index.html#") }} 中的额外特性：

<mini-zoo class="zoo" style="margin-right: 20px;">
    <entry class="wide">
        <type class="generic dotted"><code>Collection&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">FromIterator</code></trait-impl>
        <trait-impl class="">⌾ <code style="">Extend</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry class="wide">
        <type class="generic dotted"><code>IntoIter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">DoubleEndedIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">ExactSizeIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">FusedIterator </code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry class="wide">
        <type class="generic dotted"><code>Iter&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">DoubleEndedIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">ExactSizeIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">FusedIterator </code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry class="wide">
        <type class="generic dotted"><code>IterMut&lt;T&gt;</code></type>
        <trait-impl class="">⌾ <code style="">DoubleEndedIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">ExactSizeIt… </code></trait-impl>
        <trait-impl class="">⌾ <code style="">FusedIterator </code></trait-impl>
    </entry>
</mini-zoo>



{{ tablesep() }}

> 编写集合可能需要工作，但好消息是，如果你按照这些步骤，你的集合会感觉像 _一等公民_ 一样自然。


</div></panel></tab>

</tabs>



<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">
<div class="color-header number">


## Number Conversions


尽可能<b style="">准确</b>的数字转换。

| ↓ 拥有的类型 / 需要的类型 → | `u8` &hellip; `i128` |  `f32` / `f64` | 字符串 |
| --- | --- |  --- |--- |
| `u8` &hellip; `i128` | `u8::try_from(x)?` <sup>1</sup> |  `x as f32` <sup>3</sup> | `x.to_string()` |
| `f32` / `f64` | `x as u8` <sup>2</sup> |  `x as f32` | `x.to_string()` |
| `String` | `x.parse::<u8>()?` | `x.parse::<f32>()?` | `x` |


<footnotes>

<sup>1</sup> 如果目标类型是子集，可以直接使用 `from()`，例如 `u32::from(my_u8)`。<br/>
<sup>2</sup> 会进行截断操作（`11.9_f32 as u8` 会得到 `11`）和饱和转换（`1024_f32 as u8` 会得到 `255`）；参见下文。<br/>
<sup>3</sup> 可能会造成数字失真（`u64::MAX as f32`）或产生 `Inf`（`u128::MAX as f32`）。

</footnotes>

{{ tablesep() }}

> 另见 **转换-** 和 **算术陷阱** {{ above(target="#numeric-types") }}，了解更多关于数字操作可能出错的情况。


<!-- end overflow -->
</div>
</div>
</div>



## String Conversions


如果你**需要**一个类型为&hellip;的字符串

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-1" name="tab-group-str" checked>
<label for="tab-str-1"><code>String</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`x`|
|`CString`|`x.into_string()?` |
|`OsString`|`x.to_str()?.to_string()`|
|`PathBuf`|`x.to_str()?.to_string()`|
|`Vec<u8>` <sup>1</sup> |`String::from_utf8(x)?`|
|`&str`|`x.to_string()` <sup>`i`</sup> |
|`&CStr`|`x.to_str()?.to_string()` |
|`&OsStr`|`x.to_str()?.to_string()`|
|`&Path`|`x.to_str()?.to_string()`|
|`&[u8]` <sup>1</sup> |`String::from_utf8_lossy(x).to_string()`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-2" name="tab-group-str" >
<label for="tab-str-2"><code>CString</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`CString::new(x)?`|
|`CString`|`x`|
|`OsString` |`CString::new(x.to_str()?)?`|
|`PathBuf`|`CString::new(x.to_str()?)?`|
|`Vec<u8>` <sup>1</sup> |`CString::new(x)?`|
|`&str`|`CString::new(x)?`|
|`&CStr`|`x.to_owned()` <sup>`i`</sup> |
|`&OsStr` |`CString::new(x.to_os_string().into_string()?)?`|
|`&Path`|`CString::new(x.to_str()?)?`|
|`&[u8]` <sup>1</sup> |`CString::new(Vec::from(x))?`|
|`*mut c_char` <sup>2</sup> |`unsafe { CString::from_raw(x) }`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-3" name="tab-group-str" >
<label for="tab-str-3"><code>OsString</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`OsString::from(x)` <sup>`i`</sup> |
|`CString`|`OsString::from(x.to_str()?)`|
|`OsString`|`x`|
|`PathBuf`|`x.into_os_string()`|
|`Vec<u8>` <sup>1</sup> |`unsafe { OsString::from_encoded_bytes_unchecked(x) }`|
|`&str`|`OsString::from(x)` <sup>`i`</sup>|
|`&CStr`|`OsString::from(x.to_str()?)`|
|`&OsStr`|`OsString::from(x)` <sup>`i`</sup>|
|`&Path`|`x.as_os_str().to_owned()`|
|`&[u8]` <sup>1</sup> |`unsafe { OsString::from_encoded_bytes_unchecked(x.to_vec()) }`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-35" name="tab-group-str" >
<label for="tab-str-35"><code>PathBuf</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`PathBuf::from(x)` <sup>`i`</sup>|
|`CString`|`PathBuf::from(x.to_str()?)`|
|`OsString`|`PathBuf::from(x)` <sup>`i`</sup>|
|`PathBuf`|`x`|
|`Vec<u8>` <sup>1</sup> |`unsafe { PathBuf::from(OsString::from_encoded_bytes_unchecked(x)) }` |
|`&str`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&CStr`|`PathBuf::from(x.to_str()?)`|
|`&OsStr`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&Path`|`PathBuf::from(x)` <sup>`i`</sup>|
|`&[u8]` <sup>1</sup> |`unsafe { PathBuf::from(OsString::from_encoded_bytes_unchecked(x.to_vec())) }` |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-4" name="tab-group-str" >
<label for="tab-str-4"><code>Vec&lt;u8&gt;</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`x.into_bytes()`|
|`CString`|`x.into_bytes()`|
|`OsString`|`x.into_encoded_bytes()`|
|`PathBuf`|`x.into_os_string().into_encoded_bytes()`|
|`Vec<u8>` <sup>1</sup> |`x`|
|`&str`|`Vec::from(x.as_bytes())`|
|`&CStr`|`Vec::from(x.to_bytes_with_nul())`|
|`&OsStr`|`Vec::from(x.as_encoded_bytes())`|
|`&Path`|`Vec::from(x.as_os_str().as_encoded_bytes())`|
|`&[u8]` <sup>1</sup> |`x.to_vec()`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-5" name="tab-group-str" >
<label for="tab-str-5"><code>&str</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`x.as_str()`|
|`CString`|`x.to_str()?`|
|`OsString`|`x.to_str()?`|
|`PathBuf`|`x.to_str()?`|
|`Vec<u8>` <sup>1</sup> |`std::str::from_utf8(&x)?`|
|`&str`|`x`|
|`&CStr`|`x.to_str()?`|
|`&OsStr`|`x.to_str()?`|
|`&Path`|`x.to_str()?`|
|`&[u8]` <sup>1</sup> |`std::str::from_utf8(x)?`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-6" name="tab-group-str" >
<label for="tab-str-6"><code>&CStr</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`CString::new(x)?.as_c_str()`|
|`CString`|`x.as_c_str()`|
|`OsString`|`x.to_str()?`|
|`PathBuf`| {{ todo() }}<sup>,3</sup> |
|`Vec<u8>` <sup>1</sup><sup>,4</sup> |`CStr::from_bytes_with_nul(&x)?`|
|`&str`| {{ todo() }}<sup>,3</sup> |
|`&CStr`|`x`|
|`&OsStr` | {{ todo() }} |
|`&Path`| {{ todo() }} |
|`&[u8]` <sup>1</sup><sup>,4</sup> |`CStr::from_bytes_with_nul(x)?`|
|`*const c_char` <sup>1</sup> |`unsafe { CStr::from_ptr(x) }`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-8" name="tab-group-str" >
<label for="tab-str-8"><code>&OsStr</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`OsStr::new(&x)`|
|`CString`| {{ todo() }} |
|`OsString`|`x.as_os_str()`|
|`PathBuf`|`x.as_os_str()`|
|`Vec<u8>` <sup>1</sup> |`unsafe { OsStr::from_encoded_bytes_unchecked(&x) }`|
|`&str`|`OsStr::new(x)`|
|`&CStr`| {{ todo() }} |
|`&OsStr`|`x`|
|`&Path`|`x.as_os_str()`|
|`&[u8]` <sup>1</sup> | `unsafe { OsStr::from_encoded_bytes_unchecked(x) }` |


</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-85" name="tab-group-str" >
<label for="tab-str-85"><code>&Path</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`Path::new(x)` <sup>`r`</sup>|
|`CString`|`Path::new(x.to_str()?)` |
|`OsString`|`Path::new(x.to_str()?)` <sup>`r`</sup>|
|`PathBuf`|`Path::new(x.to_str()?)` <sup>`r`</sup>|
|`Vec<u8>` <sup>1</sup> |`unsafe { Path::new(OsStr::from_encoded_bytes_unchecked(&x)) }`|
|`&str`|`Path::new(x)` <sup>`r`</sup>|
|`&CStr`|`Path::new(x.to_str()?)` |
|`&OsStr`|`Path::new(x)` <sup>`r`</sup>|
|`&Path`|`x`|
|`&[u8]` <sup>1</sup> |`unsafe { Path::new(OsStr::from_encoded_bytes_unchecked(x)) }` |

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-7" name="tab-group-str" >
<label for="tab-str-7"><code>&[u8]</code></label>
<panel><div class="stringconversion">

| 如果你**有** `x` 类型为 &hellip;| 使用这个 &hellip; |
| --- | --- |
|`String`|`x.as_bytes()`|
|`CString`|`x.as_bytes()`|
|`OsString`|`x.as_encoded_bytes()`|
|`PathBuf`|`x.as_os_str().as_encoded_bytes()`|
|`Vec<u8>` <sup>1</sup> |`&x`|
|`&str`|`x.as_bytes()`|
|`&CStr`|`x.to_bytes_with_nul()`|
|`&OsStr`|`x.as_encoded_bytes()`|
|`&Path`|`x.as_os_str().as_encoded_bytes()`|
|`&[u8]` <sup>1</sup> |`x`|

</div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-str-9" name="tab-group-str" >
<label for="tab-str-9"><b>Other</b></label>
<panel><div class="stringconversion">

| 你**需要** | 且**有** `x` | 使用这个 &hellip; |
| --- | --- | --- |
|<b>`*const c_char`</b>|<b>`CString`</b>|`x.as_ptr()`|


</div></panel></tab>

<!-- End tabs -->
</tabs>

<!-- End overflow protection -->
</div></div>


<footnotes>

<sup>i</sup> 如果可以推断类型，则可以使用简写形式 `x.into()`。<br>
<sup>r</sup> 如果可以推断类型，则可以使用简写形式 `x.as_ref()`。<br>
<sup>1</sup> 你必须确保 `x` 对应于该字符串类型的有效表示（例如，对于 `String`，需要是 UTF-8 数据）。<br>
<sup>2</sup> `c_char` **必须** 来自于之前的 `CString`。如果来自于 FFI，请查看 `&CStr` 代替。<br>
<sup>3</sup> 因为 `x` 缺少终止的 `0x0`，没有已知的简便方法，最好通过 `CString`。<br>
<sup>4</sup> 必须确保 `x` 实际以 `0x0` 结尾。<br>

</footnotes>


## String Output

如何将类型转换为 `String` 或输出它们。

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-1" name="tab-group-strop" checked>
<label for="tab-strop-1"><b>APIs</b></label>
<panel><div class="color-header undefined-color-3">

Rust 有这些将类型转换为字符串输出的 API，统称为 _格式化_ 宏：

| 宏 | 输出 | 备注 |
| --- | --- | --- |
|`format!(fmt)` | `String` | 核心的“转换为 `String`”的转换器。 |
|`print!(fmt)`| 控制台 | 写入标准输出。 |
|`println!(fmt)`| 控制台 | 写入标准输出。 |
| `eprint!(fmt)`| 控制台 | 写入标准错误。 |
|`eprintln!(fmt)`| 控制台 | 写入标准错误。 |
|`write!(dst, fmt)` | 缓冲区 | 别忘了同时 `use std::io::Write;` |
|`writeln!(dst, fmt)` | 缓冲区 | 别忘了同时 `use std::io::Write;` |

{{ tablesep() }}

| 方法 | 备注 |
| --- | --- |
|`x.to_string()` {{ std(page="std/string/trait.ToString.html") }} | 产生 `String`，对于任何实现了 `Display` 的类型都有效。|

{{ tablesep() }}

这里 `fmt` 是字符串字面量，例如 `"hello {}"`，它指定输出格式（比较“格式化”选项卡）和附加参数。


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-2" name="tab-group-strop">
<label for="tab-strop-2"><b>可打印类型</b></label>
<panel><div class="color-header undefined-color-3">

在 `format!` 和其他类似宏中，类型通过 trait `Display` `"{}"` {{ std(page="std/fmt/trait.Display.html") }} 或 `Debug` `"{:?}"` {{ std(page="std/fmt/trait.Debug.html") }} 来转换，部分类型列表如下：

| 类型 | 实现 |  |
| --- | --- | --- |
|`String`| `Debug, Display` | |
|`CString`| `Debug` | |
|`OsString`| `Debug` | |
|`PathBuf`| `Debug` |  |
|`Vec<u8>` | `Debug` | |
|`&str`|`Debug, Display` | |
|`&CStr`|`Debug` | |
|`&OsStr`| `Debug` | |
|`&Path`| `Debug` | |
|`&[u8]` |`Debug` | |
|`bool` |`Debug, Display` | |
|`char` |`Debug, Display` | |
|`u8` &hellip; `i128` |`Debug, Display` | |
|`f32`, `f64` |`Debug, Display` | |
|`!` |`Debug, Display` | |
|`()` |`Debug` | |

{{ tablesep() }}

简而言之，几乎所有类型都实现了 `Debug`；更为特殊的类型可能需要特殊处理或转换 {{ above(target="#string-conversions" ) }} 成为 `Display`。

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-strop-3" name="tab-group-strop">
<label for="tab-strop-3"><b>格式化</b></label>
<panel><div>

在格式化宏中，每个参数设计符要么是空 `{}`，要么是 `{argument}`，或者遵循基本[**语法**](https://doc.rust-lang.org/std/fmt/index.html#syntax)：


```
{ [argument] ':' [[fill] align] [sign] ['#'] [width [$]] ['.' precision [$]] [type] }
```

<div class="color-header undefined-color-3">

| 元素 | 含义 |
|---------| ---------|
| `argument` | 数字（`0`，`1`，…），变量 {{ edition(ed="'21") }} 或名称，{{ edition(ed="'18") }} 例如 `print!("{x}")`。 |
| `fill` | 填充空格的字符（例如 `0`），如果指定了 `width`。 |
| `align` | 左对齐（`<`），居中（`^`），右对齐（`>`），如果指定了宽度。 |
| `sign` | 可以是 `+`，使符号总是显示。 |
| `#` | [备用格式化](https://doc.rust-lang.org/std/fmt/index.html#sign0)，例如美化 `Debug`{{ std(page="std/fmt/trait.Debug.html") }} 格式器 `?` 或为十六进制前加 `0x`。 |
| `width` | 最小宽度 (&geq; 0)，用 `fill` 填充（默认为空格）。如果以 `0` 开头，表示零填充。 |
| `precision` | 数字的十进制位数 (&geq; 0)，或非数字的最大宽度。 |
| `$` | 将 `width` 或 `precision` 解释为参数标识符，从而允许动态格式化。 |
| **`type`** | `Debug`{{ std(page="std/fmt/trait.Debug.html") }} (`?`) 格式化，十六进制 (`x`)，二进制 (`b`)，八进制 (`o`)，指针 (`p`)，指数 (`e`) … [查看更多](https://doc.rust-lang.org/std/fmt/index.html#traits)。 |

</div>


{{ tablesep() }}


<div class="color-header undefined-color-3">

| 格式示例 | 解释 |
|---------|-------------|
| `{}` | 使用 `Display`{{ std(page="std/fmt/trait.Display.html") }} 打印下一个参数。 |
| `{x}` | 相同，但使用作用域中的变量 `x`。{{ edition(ed="'21") }} |
| `{:?}` | 使用 `Debug`{{ std(page="std/fmt/trait.Debug.html") }} 打印下一个参数。 |
| `{2:#?}` | 使用 `Debug`{{ std(page="std/fmt/trait.Debug.html") }} 格式化漂亮地打印第三个参数。 |
| `{val:^2$}` | 将名为 `val` 的参数居中，宽度由第三个参数指定。 |
| `{:<10.3}` | 左对齐，宽度为 10，精度为 3。|
| `{val:#x}` | 将 `val` 参数格式化为十六进制，前缀 `0x`（`x` 的备用格式）。 |

</div>

{{ tablesep() }}


<div class="color-header undefined-color-3">

| 完整示例 | 解释 |
|---------|-------------|
| `println!("{}", x)` | 使用 `Display`{{ std(page="std/fmt/trait.Display.html") }} 打印 `x` 到标准输出，并追加新行。{{ edition(ed="'15") }} {{ deprecated() }} |
| `println!("{x}")` | 相同，但使用作用域中的变量 `x`。{{ edition(ed="'21") }} |
| `format!("{a:.3} {b:?}")` | 将 `a` 转换为具有 3 位精度，添加空格，再将 `b` 以 `Debug` {{ std(page="std/fmt/trait.Debug.html") }} 格式打印，返回 `String`。{{ edition(ed="'21") }} |

</div>


</div></panel></tab>


</tabs>

{{ tablesep() }}




---

# Tooling


## Project Anatomy

`cargo` 常用的基本项目布局及常见文件和文件夹。{{ below(target="#cargo") }}

<div class="color-header red">

| 项目条目 | 代码 |
|--------| ---- |
| 📁 `.cargo/` | **项目局部 cargo 配置**，可能包含 **`config.toml`**。{{ link( url="https://doc.rust-lang.org/cargo/reference/config.html") }} {{ esoteric() }} |
| 📁 `benches/` | 项目基准测试，可通过 **`cargo bench`** 运行，默认情况下需要 nightly 版本。<sup>*</sup> {{ experimental() }} |
| 📁 `examples/` | 包含项目的示例，用法类似外部用户使用项目。|
| {{ tab() }} {{ tab() }} `my_example.rs` | 每个示例可以通过 **`cargo run --example my_example`** 运行。 |
| 📁 `src/` | 项目的实际源代码。 |
| {{ tab() }} {{ tab() }} `main.rs` | 应用程序的默认入口点，即 **`cargo run`** 使用的文件。 |
| {{ tab() }} {{ tab() }} `lib.rs` | 库的默认入口点。从这里开始查找 `my_crate::f()`。 |
| 📁 `src/bin/` | 额外的二进制文件的存放位置，即使是库项目也可以有。 |
| {{ tab() }} {{ tab() }} `extra.rs` | 额外的二进制文件，可以通过 `cargo run --bin extra` 运行。 |
| 📁 `tests/` | 集成测试放在这里，通过 **`cargo test`** 调用。单元测试通常留在 `src/` 文件中。 |
| `.rustfmt.toml` | 如果你想[**自定义**](https://rust-lang.github.io/rustfmt/) **`cargo fmt`** 的行为。 |
| `.clippy.toml` | 某些 [**clippy lints**](https://rust-lang.github.io/rust-clippy/master/index.html) 的特殊配置，可通过 **`cargo clippy`** 使用。{{ esoteric() }} |
| `build.rs` | **预构建脚本**，{{ link(url="https://doc.rust-lang.org/cargo/reference/build-scripts.html") }} 适用于编译 C / FFI，等。|
| <code class="ignore-auto language-bash">Cargo.toml</code> | 项目主要的**清单文件**，{{ link(url="https://doc.rust-lang.org/cargo/reference/manifest.html") }} 定义依赖关系、产物等。|
| <code class="ignore-auto language-bash">Cargo.lock</code> | 用于可重现构建。应用程序建议提交到 git，库项目可以考虑不提交。{{ opinionated() }} {{ link(url="https://blog.rust-lang.org/2023/08/29/committing-lockfiles.html" )}} {{ link(url="https://web.archive.org/web/20240108203227/https://old.reddit.com/r/rust/comments/164qfjm/change_in_guidance_on_committing_lockfiles_rust/jya8ouf/" )}} |
| `rust-toolchain.toml` | 为此项目定义**工具链覆盖**{{ link(url="https://rust-lang.github.io/rustup/overrides.html" )}}（频道、组件、目标）。 |
</div>

<footnotes>

<sup>*</sup> 在稳定版上可以考虑使用 [Criterion](https://github.com/bheisler/criterion.rs)。

</footnotes>


{{ tablesep() }}


各种入口点的**最小示例**如下：

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-1" name="tab-group-anatomy" checked>
<label for="tab-anatomy-1"><b>应用程序</b></label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/main.rs (default application entry point)

fn main() {
    println!("Hello, world!");
}
```

</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-2" name="tab-group-anatomy" >
<label for="tab-anatomy-2"><b>库</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/lib.rs (default library entry point)

pub fn f() {}      // Is a public item in root, so it's accessible from the outside.

mod m {
    pub fn g() {}  // No public path (`m` not public) from root, so `g`
}                  // is not accessible from the outside of the crate.
```
</div></div></div></panel></tab>





<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-3" name="tab-group-anatomy" >
<label for="tab-anatomy-3"><b>单元测试</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/my_module.rs (any file of your project)

fn f() -> u32 { 0 }

#[cfg(test)]
mod test {
    use super::f;           // Need to import items from parent module. Has
                            // access to non-public members.
    #[test]
    fn ff() {
        assert_eq!(f(), 0);
    }
}
```
</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-4" name="tab-group-anatomy" >
<label for="tab-anatomy-4"><b>集成测试</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// tests/sample.rs (sample integration test)

#[test]
fn my_sample() {
    assert_eq!(my_crate::f(), 123); // Integration tests (and benchmarks) 'depend' to the crate like
}                                   // a 3rd party would. Hence, they only see public items.
```
</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-5" name="tab-group-anatomy" >
<label for="tab-anatomy-5"><b>基准测试</b>{{ experimental() }}</label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// benches/sample.rs (sample benchmark)

#![feature(test)]   // #[bench] is still experimental

extern crate test;  // Even in '18 this is needed for … reasons.
                    // Normally you don't need this in '18 code.

use test::{black_box, Bencher};

#[bench]
fn my_algo(b: &mut Bencher) {
    b.iter(|| black_box(my_crate::f())); // `black_box` prevents `f` from being optimized away.
}
```
</div></div></div></panel></tab>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-6" name="tab-group-anatomy" >
<label for="tab-anatomy-6"><b>构建脚本</b></label>
<panel><div>

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// build.rs (sample pre-build script)

fn main() {
    // You need to rely on env. vars for target; `#[cfg(…)]` are for host.
    let target_os = env::var("CARGO_CFG_TARGET_OS");
}
```

<sup>*</sup>[这里可以查看](https://doc.rust-lang.org/cargo/reference/environment-variables.html#environment-variables-cargo-sets-for-build-scripts) 由 cargo 设置的环境变量。

</div></div></div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-anatomy-25" name="tab-group-anatomy" >
<label for="tab-anatomy-25"><b>过程宏</b>{{ esoteric() }}</label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
// src/lib.rs (default entry point for proc macros)

extern crate proc_macro;  // Apparently needed to be imported like this.

use proc_macro::TokenStream;

#[proc_macro_attribute]   // Crates can now use `#[my_attribute]`
pub fn my_attribute(_attr: TokenStream, item: TokenStream) -> TokenStream {
    item
}
```


```
// Cargo.toml

[package]
name = "my_crate"
version = "0.1.0"

[lib]
proc-macro = true
```


</div></div></div></panel></tab>


</tabs>



{{ tablesep() }}


模块树和导入：

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-module-import-1" name="tab-group-module-import" checked>
<label for="tab-module-import-1"><b>模块树</b></label>
<panel><div>


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

**模块** {{ book(page="ch07-02-defining-modules-to-control-scope-and-privacy.html") }} {{ ex(page="mod.html#modules") }} {{ ref(page="items/modules.html#modules") }} 和 **源文件**的工作方式如下：

- **模块树** 需要显式定义，**不是** 自动从 **文件系统树** 构建。{{ link(url="http://www.sheshbabu.com/posts/rust-module-system/") }}
- **模块树的根** 等于库、应用程序等的入口点（例如 `lib.rs`）。

实际的 **模块定义** 工作方式如下：
- 使用 **`mod m {}`** 在文件中定义模块，或者使用 **`mod m;`** 读取 `m.rs` 或 `m/mod.rs`。
- `.rs` 文件路径基于 **嵌套**，例如 `mod a { mod b { mod c; }}}` 可以是 `a/b/c.rs` 或 `a/b/c/mod.rs`。
- 如果文件未通过某些 `mod m;` 从模块树的根访问，则编译器不会触碰它们！{{ bad() }}

<!-- - **Visibility** of items (e.g., functions, fields) between modules governed by: "Is there visible path to item?"
    - Visibility like `pub fn f() {}` does not mean "`f` is public", but "`f` at most public if all parents public`. -->


</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-module-import-2" name="tab-group-module-import">
<label for="tab-module-import-2"><b>命名空间</b>{{ esoteric() }}</label>
<panel><div>


Rust 有三种 **命名空间**：

<table>
    <thead>
        <tr>
            <th>命名空间 <i>类型</i></th>
            <th>命名空间 <i>函数</i></th>
            <th>命名空间 <i>宏</i></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>mod X {}</code></td>
            <td><code>fn X() {}</code></td>
            <td><code>macro_rules! X { … }</code></td>
        </tr>
        <tr>
            <td><code>X</code> (crate)</td>
            <td><code>const X: u8 = 1;</code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>trait X {}</code></td>
            <td><code>static X: u8 = 1;</code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>enum X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>union X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td><code>struct X {}</code></td>
            <td><code></code></td>
            <td><code></code></td>
        </tr>
        <tr>
            <td colspan="2" style="text-align: center; padding-right: 50px;"> <span style="opacity: 50%">←</span> <code>struct X;</code><sup>1</sup> <span style="opacity: 50%">→</span> </td>
            <td></td>
        </tr>
        <tr>
            <td colspan="2" style="text-align: center; padding-right: 50px;"> <span style="opacity: 50%">←</span> <code>struct X();</code><sup>2</sup> <span style="opacity: 50%">→</span> </td>
            <td></td>
        </tr>
    </tbody>
</table>

<footnotes>

<sup>1</sup> 在 <i>类型</i> 和 <i>函数</i> 中都有，定义了类型 `X` 和常量 `X`。<br>
<sup>2</sup> 在 <i>类型</i> 和 <i>函数</i> 中都有，定义了类型 `X` 和函数 `X`。

</footnotes>

- 在任何给定的作用域中，例如在一个模块中，每个命名空间只能有一个同名项，例如：
    - `enum X {}` 和 `fn X() {}` 可以共存
    - `struct X;` 和 `const X` 不能共存
- 使用 `use my_mod::X;` 时，所有名为 `X` 的项都会被导入。

> 由于命名约定（例如，`fn` 和 `mod` 按惯例小写）以及常识（大多数开发者不会将所有东西命名为 `X`），在大多数情况下你无需担心这些 _种类_ 的问题。但在设计宏时，它们可能会成为一个因素。


</div></panel></tab>


</tabs>


{{ tablesep() }}



## Cargo

一些有用的命令和工具。


<div class="color-header tooling">

| 命令 | 描述 |
|--------| ---- |
| `cargo init` | 为最新版本创建一个新项目。 |
| <code>cargo <span class="cargo-prefix">b</span>uild</code> | 在调试模式下构建项目（<code>--<span class="cargo-prefix">r</span>elease</code> 进行完全优化）。 |
| <code>cargo <span class="cargo-prefix">c</span>heck</code> | 检查项目是否可以编译（更快）。 |
| <code>cargo <span class="cargo-prefix">t</span>est</code> | 运行项目的测试。 |
| <code>cargo <span class="cargo-prefix">d</span>oc --open</code> | 为你的代码和依赖项本地生成文档。 |
| <code>cargo <span class="cargo-prefix">r</span>un</code> | 运行项目，如果生成了可执行文件（如 main.rs）。 |
| {{ tab() }} `cargo run --bin b` | 运行二进制文件 `b`。将特性统一与其他依赖项（可能会混淆）。 |
| {{ tab() }} <code>cargo run --<span class="cargo-prefix">p</span>ackage w</code> | 运行子工作区 `w` 的主程序。更好地处理特性。 |
| <code>cargo … --timings</code> | 显示哪些 crate 导致构建时间变长。{{ hot() }} |
| `cargo tree` | 显示依赖关系图。 |
| `cargo info …` | 显示 crate 元数据（默认为此项目使用的版本）。 |
| <code>cargo +{nightly, stable} …</code>  | 使用指定工具链执行命令，例如对于“仅限夜间”的工具。 |
| `cargo +nightly …` | 一些仅限于夜间版本的命令（将 `…` 替换为下列命令） |
| {{ tab() }} `rustc -- -Zunpretty=expanded` | 显示展开的宏。{{ experimental() }} |
| `rustup doc` | 打开离线 Rust 文档（包括书籍），适合在飞机上阅读！ |

</div>

<footnotes>

这里 <code>cargo <span class="cargo-prefix">b</span>uild</code> 意味着你可以键入 `cargo build` 或 `cargo b`；而 <code>--<span class="cargo-prefix">r</span>elease</code> 可以替换为 `-r`。

</footnotes>


{{ tablesep() }}


这些是可选的 `rustup` 组件。
使用 `rustup component add [tool]` 安装它们。


<div class="color-header tooling">

| 工具 | 描述 |
|--------| ---- |
| `cargo clippy` | 额外的 ([lints](https://rust-lang.github.io/rust-clippy/master/)) ，可以捕捉常见 API 误用和不符合惯用法的代码。{{ link(url = "https://github.com/rust-lang/rust-clippy") }} |
| `cargo fmt` | 自动代码格式化工具 (`rustup component add rustfmt`)。{{ link(url = "https://github.com/rust-lang/rustfmt") }} |

</div>

{{ tablesep() }}

大量的 cargo 插件 [**可以在这里找到**](https://crates.io/categories/development-tools::cargo-plugins?sort=downloads)。


{{ tablesep() }}


## Cross Compilation

<!-- <div class="steps"> -->

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

🔘 检查 [目标是否受支持](https://doc.rust-lang.org/rustc/platform-support.html)。

🔘 通过 **`rustup target install aarch64-linux-android`** 安装目标（例如）。

🔘 安装本地工具链（用于 _链接_，取决于目标）。

从目标供应商（例如 Google、Apple 等）获取，可能并非所有主机系统都支持（例如，Windows 上没有 iOS 工具链）。

**某些工具链需要额外的构建步骤**（例如 Android 的 `make-standalone-toolchain.sh`）。

🔘 更新 **`~/.cargo/config.toml`**，例如：

```
[target.aarch64-linux-android]
linker = "[PATH_TO_TOOLCHAIN]/aarch64-linux-android/bin/aarch64-linux-android-clang"
```

   或者

```
[target.aarch64-linux-android]
linker = "C:/[PATH_TO_TOOLCHAIN]/prebuilt/windows-x86_64/bin/aarch64-linux-android21-clang.cmd"
```

🔘 设置 **环境变量**（可选，直到编译器抱怨再设置）：

```
set CC=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android21-clang.cmd
set CXX=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android21-clang.cmd
set AR=C:\[PATH_TO_TOOLCHAIN]\prebuilt\windows-x86_64\bin\aarch64-linux-android-ar.exe
…
```

是否设置这些变量取决于编译器的报错情况，并不一定全部需要。

> 一些平台 / 配置对路径的指定**非常敏感**（例如，`\` 与 `/` 的区别）以及是否引用。


✔️ 使用 **`cargo build --target=aarch64-linux-android`** 进行编译。


<!-- End overflow area -->
</div>
</div>

<!-- End steps  -->
<!-- </div> -->

{{ tablesep() }}




## Tooling Directives

嵌入在源代码中的用于工具或预处理的特殊标记。

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-1" name="tab-group-preprocessing" checked>
<label for="tab-preprocessing-1"><b>宏片段</b></label>
<panel><div class="color-header undefined-color-3">

<fixed-2-column class="color-header special_example">

<!-- Tool: **Preprocessor (Automatic)** -->


<!-- ```
macro_rules! my_macro {
    ($x:ty) => { ... }
}
``` -->

在 **声明式** {{ book(page="ch19-06-macros.html#declarative-macros-with-macro_rules-for-general-metaprogramming") }} **示例宏** {{book(page="ch19-06-macros.html")}} {{ex(page="macros.html#macro_rules")}} {{ref(page="macros-by-example.html")}} 的 `macro_rules!` 实现中，这些 **片段说明符** {{ ref(page="macros-by-example.html#metavariables") }} 可用：

| 宏内部使用 | 解释 |
|---------|---------|
| `$x:ty`  | 宏捕获（这里 `$x` 是捕获部分，`ty` 表示 `x` 必须是类型）。 |
| {{ tab() }} `$x:block`   | 代码块 `{}`，如 `{ let x = 5; }`。 |
| {{ tab() }} `$x:expr`    | 表达式，例如 `x`、`1 + 1`、`String::new()` 或 `vec![]`。 |
| {{ tab() }} `$x:ident`   | 标识符，例如在 `let x = 0;` 中，标识符是 `x`。 |
| {{ tab() }} `$x:item`    | 项，如函数、结构体、模块等。 |
| {{ tab() }} `$x:lifetime` | 生命周期，例如 `'a`、`'static` 等。 |
| {{ tab() }} `$x:literal` | 字面量，例如 `3`、`"foo"`、`b"bar"` 等。 |
| {{ tab() }} `$x:meta`    | 元项；放在 `#[…]` 和 `#![…]` 属性中的内容。 |
| {{ tab() }} `$x:pat`     | 模式，例如 `Some(t)`、`(17, 'a')` 或 `_`。 |
| {{ tab() }} `$x:path`    | 路径，例如 `foo`、`::std::mem::replace`、`transmute::<_, int>`。 |
| {{ tab() }} `$x:stmt`    | 语句，例如 `let x = 1 + 1;`、`String::new();` 或 `vec![];`。 |
| {{ tab() }} `$x:tt`      | 单个 token 树，更多详情见[这里](https://stackoverflow.com/a/40303308)。 |
| {{ tab() }} `$x:ty`      | 类型，例如 `String`、`usize` 或 `Vec<u8>`。 |
| {{ tab() }} `$x:vis`    | 可见性修饰符；如 `pub`、`pub(crate)` 等。 |
| `$crate` | 特殊卫生变量，表示定义宏的 crate。 {{ todo() }} |

</fixed-2-column>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-2" name="tab-group-preprocessing">
<label for="tab-preprocessing-2"><b>文档注释</b></label>
<panel><div class="color-header undefined-color-2">

<fixed-2-column  class="color-header special_example">

<!-- ```
/// Accepts an [`S`].
///
/// ```rust
///     f(s);
/// ```
``` -->

在 **文档注释** {{ book(page="ch14-02-publishing-to-crates-io.html#making-useful-documentation-comments") }} {{ ex(page="meta/doc.html#documentation") }} {{ ref(page="comments.html#doc-comments") }} 中可以使用以下内容：

| 文档注释内使用 | 解释 |
|--------|-------------|
| ` ```…``` ` | 包含一个 [**文档测试**](https://doc.rust-lang.org/rustdoc/documentation-tests.html)（在 `cargo test` 上运行的文档代码）。 |
| ` ```X,Y …``` ` | 同上，并包括可选配置；`X`、`Y` 的含义如下： |
| {{ tab() }} <code style="color: gray;">rust</code> | 明确指定测试是用 Rust 编写的；被 Rust 工具隐含。 |
| {{ tab() }} <code style="color: gray; opacity: 0.3;">-</code> | 编译测试，运行测试。如果发生 panic 则失败。**默认行为**。 |
| {{ tab() }} <code style="color: gray;">should_panic</code> | 编译测试，运行测试。执行时应 panic，如果没有，则测试失败。 |
| {{ tab() }} <code style="color: gray;">no_run</code> | 编译测试。如果代码无法编译则测试失败，但不运行测试。 |
| {{ tab() }} <code style="color: gray;">compile_fail</code> | 编译测试，但如果代码可以编译则测试失败。 |
| {{ tab() }} <code style="color: gray;">ignore</code> | 不编译，不运行。建议使用上述选项。 |
| {{ tab() }} <code style="color: gray;">edition2018</code> | 以 Rust '18 版本执行代码；默认是 '15。 |
| `#` | 从文档中隐藏行 (` ```   # use x::hidden; ``` `)。 |
| <code>[&#96;S&#96;]</code> | 创建到结构体、枚举、trait、函数等 `S` 的链接。 |
| <code>[&#96;S&#96;]&#40;crate::S&#41;</code> | 路径也可以使用，形式类似于 Markdown 链接。 |


</fixed-2-column>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-7" name="tab-group-preprocessing">
<label for="tab-preprocessing-7"><b><code>#![globals]</code></b></label>
<panel><div class="color-header undefined-color-3">

<!-- ```
// Attributes usually found in toplevel project file.
#![no_std]
#![feature(xxx)]
``` -->
<fixed-3-column  class="color-header special_example">

影响整个 crate 或应用程序的属性：

| Opt-Out 的属性 | 开启 | 解释 |
|--------|---|----------|
| `#![no_std]` | `C` | 不（自动）导入 **`std`**{{ std(page="std/") }}；改为使用 **`core`**{{ std(page="core/") }}。{{ ref(page="names/preludes.html#the-no_std-attribute") }} |
| `#![no_implicit_prelude]` | `CM` | 不添加 **`prelude`**{{ std(page="std/prelude/index.html") }}，需要手动导入 `None`，`Vec` 等。{{ ref(page="names/preludes.html#the-no_implicit_prelude-attribute") }} |
| `#![no_main]` |  `C` | 如果你自己实现了 `main()`，则不再生成 `main()` 函数。{{ ref(page="crates-and-source-files.html#the-no_main-attribute") }} |

<!-- | `#![no_builtins]` | `C` | Does ... something ... probably important. {{ todo() }} {{ ref(page="attributes/codegen.html#the-no_builtins-attribute") }}| -->

{{ tablesep() }}

| Opt-In 的属性 | 开启 | 解释 |
|--------|---|----------|
| `#![feature(a, b, c)]` | `C` | 依赖可能无法稳定的功能，_c._ [**不稳定功能手册**](https://doc.rust-lang.org/unstable-book/the-unstable-book.html)。{{ experimental() }} |

{{ tablesep() }}

| 构建相关 | 开启 | 解释 |
|--------|---|----------|
| `#![crate_name = "x"]` | `C` | 指定当前 crate 的名称，例如在不使用 `cargo` 时使用。{{ todo() }} {{ ref(page="crates-and-source-files.html#the-crate_name-attribute") }} {{ esoteric() }} |
| `#![crate_type = "bin"]` | `C` | 指定当前 crate 的类型（`bin`，`lib`，`dylib`，`cdylib` 等）。{{ ref(page="linkage.html") }} {{ esoteric() }} |
| `#![recursion_limit = "123"]` | `C` | 设置 _编译时_ 的递归限制，例如解引用、宏等。{{ ref(page="attributes/limits.html#the-recursion_limit-attribute") }} {{ esoteric() }} |
| `#![type_length_limit = "456"]` | `C` | 限制类型替换的最大数量。{{ ref(page="attributes/limits.html#the-type_length_limit-attribute") }} {{ esoteric() }} |
| `#![windows_subsystem = "x"]` | `C` | 在 Windows 上，指定为 `console` 或 `windows` 应用程序。{{ ref(page="runtime.html#the-windows_subsystem-attribute") }} {{ esoteric() }} |


{{ tablesep() }}

| 处理器 | 开启 | 解释 |
|--------|---|----------|
| `#[alloc_error_handler]` | `F` | 使某些 `fn(Layout) -> !` 成为 **分配失败处理器**。{{ link(url="https://github.com/rust-lang/rust/issues/51540") }} {{ experimental() }} |
| `#[global_allocator]` | `S` | 使静态项实现 `GlobalAlloc` {{ std(page="alloc/alloc/trait.GlobalAlloc.html") }} **全局分配器**。{{ ref(page="runtime.html#the-global_allocator-attribute") }} |
| `#[panic_handler]` | `F` | 使某些 `fn(&PanicInfo) -> !` 成为应用程序的 **panic 处理器**。{{ ref(page="runtime.html#the-panic_handler-attribute") }} |


</fixed-3-column>


</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-4" name="tab-group-preprocessing">
<label for="tab-preprocessing-4"><b><code>#[code]</code></b></label>
<panel><div class="color-header undefined-color-3">

主要控制生成代码的属性：

<fixed-3-column  class="color-header special_example">

| 开发者 UX | 开启 | 解释 |
|-------|---|-------------|
| `#[non_exhaustive]` | `T` | 使 `struct` 或 `enum` 具备向前兼容性；提示可能在未来扩展。{{ ref(page="attributes/type_system.html#the-non_exhaustive-attribute") }} |
| `#[path = "x.rs"]` | `M` | 从非标准文件中获取模块。{{ ref(page="items/modules.html#the-path-attribute") }} |
| `#[diagnostic::on_unimplemented]` | `X` | 在未实现某个 trait 时给出更好的错误信息。{{ rfc(page="3368-diagnostic-attribute-namespace.html") }} |

{{ tablesep() }}

| 代码生成 | 开启 | 解释 |
|-------|---|-------------|
| `#[cold]` | `F` | 提示函数可能不会被调用。{{ ref(page="attributes/codegen.html#the-cold-attribute") }} |
| `#[inline]` | `F` | 友好地建议编译器在调用点内联函数。{{ ref(page="attributes/codegen.html#the-inline-attribute") }} |
| `#[inline(always)]` | `F` | 强烈要求编译器内联调用。{{ ref(page="attributes/codegen.html#the-inline-attribute") }} |
| `#[inline(never)]` | `F` | 指示编译器尽量不要内联函数。{{ ref(page="attributes/codegen.html#the-inline-attribute") }} |
| `#[repr(X)]`<sup>1</sup> | `T` | 使用除默认 **`rust`** {{ ref(page="type-layout.html#the-default-representation") }} 以外的另一种表示方式： |
| `#[target_feature(enable="x")]` | `F` | 为 `unsafe fn` 启用 CPU 特性（如 `avx2`）。{{ ref(page="attributes/codegen.html#the-target_feature-attribute") }} |
| `#[track_caller]` | `F` | 允许 `fn` 查找 **`caller`**{{ std(page="core/panic/struct.Location.html#method.caller") }} 以提供更好的 panic 信息。{{ ref(page="attributes/codegen.html#the-track_caller-attribute") }} |
| {{ tab() }} `#[repr(C)]` | `T` | 使用 C 兼容的布局（适用于 FFI，确定性更高，例如 `transmute`）。{{ ref(page="type-layout.html#the-c-representation") }} |
| {{ tab() }} `#[repr(C, u8)]` | `enum` | 为 `enum` 指定判别式的类型。{{ ref(page="type-layout.html#the-c-representation") }} |
| {{ tab() }} `#[repr(transparent)]` | `T` | 使单元素类型的布局与包含字段相同。{{ ref(page="type-layout.html#the-transparent-representation") }} |
| {{ tab() }} `#[repr(packed(1))]` | `T` | 降低结构体及其字段的对齐要求，可能导致轻微未定义行为。{{ ref(page="type-layout.html#the-alignment-modifiers") }} |
| {{ tab() }} `#[repr(align(8))]` | `T` | 提高结构体的对齐要求，例如用于 SIMD 类型。{{ ref(page="type-layout.html#the-alignment-modifiers") }} |

<!-- {{ tablesep() }}

| Representation | On | Explanation |
|-------|---|-------------|
| `-` | `T`  | In absence of `#[repr]` the **`rust` representation** is used {{ ref(page="type-layout.html#the-default-representation") }} |
| `#[repr(C)]` | `T`  | Use a predictable, C-compatible representation. {{ ref(page="type-layout.html#the-c-representation") }}|
| `#[repr(C, u8)]` | `enum`  | Give `enum` discriminant the specified type. {{ ref(page="type-layout.html#the-c-representation") }}|
| `#[repr(transparent)]` | `T`  | Give single-element type same layout as contained field. {{ ref(page="type-layout.html#the-transparent-representation") }}|
| `#[repr(packed(1))]` | `T`  | Lower alignment of struct and contained fields, mildly UB prone. {{ ref(page="type-layout.html#the-alignment-modifiers") }}|
| `#[repr(align(8))]` | `T`  | Raise alignment of struct to given value, e.g., for SIMD types. {{ ref(page="type-layout.html#the-alignment-modifiers") }}| -->

<footnotes>

<sup>1</sup> 某些表示修饰符可以组合使用，例如 `#[repr(C, packed(1))]`。

</footnotes>

{{ tablesep() }}

| 链接 | 开启 | 解释 |
|-------|---|-------------|
| `#[unsafe(no_mangle)]` | `*` | 直接使用项目名称作为符号名称，而不是进行符号混淆。{{ ref(page="abi.html#the-no_mangle-attribute") }} |
| `#[unsafe(export_name = "foo")]` | `FS` | 以不同的名称导出 `fn` 或 `static`。{{ ref(page="abi.html#the-export_name-attribute") }} |
| `#[unsafe(link_section = ".x")]` | `FS` | 指定对象文件中项目应放置的部分名称。{{ ref(page="abi.html#the-link_section-attribute") }} |
| `#[link(name="x", kind="y")]` | `X` | 指定查找符号时要链接的原生库。{{ ref(page="items/external-blocks.html#the-link-attribute") }} |
| `#[link_name = "foo"]` | `F` | 查找用于解析 `extern fn` 的符号的名称。{{ ref(page="items/external-blocks.html#the-link_name-attribute") }} |
| `#[no_link]` | `X` | 当只想要宏时，不链接 `extern crate`。{{ ref(page="items/extern-crates.html#the-no_link-attribute") }} |
| `#[used]` | `S` | 即使看起来未被使用，也不要优化掉 `static` 变量。{{ ref(page="abi.html#the-used-attribute") }} |



</fixed-3-column>

</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-3" name="tab-group-preprocessing">
<label for="tab-preprocessing-3"><b><code>#[quality]</code></b></label>
<panel><div class="color-header undefined-color-3">

用于改进代码质量的 Rust 工具属性：

<fixed-3-column  class="color-header special_example">

| 代码模式 | 开启 | 解释 |
|-------|---|-------------|
| `#[allow(X)]` | `*` | 指示 `rustc` / `clippy` 忽略类别 `X` 的可能问题。{{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[expect(X)]` <sup>1</sup> | `*` | 如果未触发某个 lint，则发出警告。{{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[warn(X)]` <sup>1</sup> | `*` | 发出警告，与 `clippy` 的 lints 很好地结合。{{ hot() }} {{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[deny(X)]` <sup>1</sup> | `*` | 阻止编译通过。{{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[forbid(X)]` <sup>1</sup> | `*` | 阻止编译并防止后续 `allow` 覆盖。{{ ref(page="attributes/diagnostics.html#lint-check-attributes") }} |
| `#[deprecated = "msg"]` | `*` | 让用户知道设计中的错误。{{ ref(page="diagnostics.html#the-deprecated-attribute") }} |
| `#[must_use = "msg"]` | `FTX` | 确保返回值由调用者处理。{{ hot() }} {{ ref(page="attributes/diagnostics.html#the-must_use-attribute") }} |

<footnotes>

<sup>1</sup> {{ opinionated() }} 关于哪种方式是确保高质量 crate 的最佳方法存在争议。积极维护的多人开发 crate 可能受益于更积极的 `deny` 或 `forbid` lints；而更新不频繁的 crate 则可能从保守使用 `warn` 中获益（因为将来编译器或 `clippy` 更新可能会突然因小问题而破坏原本工作的代码）。

</footnotes>

{{ tablesep() }}

</fixed-3-column>

<fixed-3-column  class="color-header special_example">

| 测试 | 开启 | 解释 |
|-------|---|-------------|
| `#[test]` | `F` | 将函数标记为测试，用 `cargo test` 运行。{{ hot() }} {{ ref(page="attributes/testing.html#the-test-attribute") }} |
| `#[ignore = "msg"]` | `F` | 编译但不执行某些 `#[test]`。{{ ref(page="attributes/testing.html#the-ignore-attribute") }} |
| `#[should_panic]` | `F` | 测试必须 `panic!()` 才能成功。{{ ref(page="attributes/testing.html#the-ignore-attribute") }} |
| `#[bench]` | `F` | 将 `bench/` 中的函数标记为基准测试，使用 `cargo bench` 运行。{{ experimental() }} {{ ref(page="") }} |

{{ tablesep() }}


| 格式化 | 开启 | 解释 |
|-------|---|-------------|
| `#[rustfmt::skip]` |  `*` | 防止 `cargo fmt` 清理项目。{{ link(url="https://github.com/rust-lang/rustfmt") }} |
| `#![rustfmt::skip::macros(x)]` |  `CM` | 防止清理宏 `x`。{{ link(url="https://github.com/rust-lang/rustfmt") }} |
| `#![rustfmt::skip::attributes(x)]` |  `CM` | 防止清理属性 `x`。{{ link(url="https://github.com/rust-lang/rustfmt") }} |

</fixed-3-column>

{{ tablesep() }}

<fixed-3-column class="color-header special_example extra-wide">


| 文档 | 开启 | 解释 |
|-------|---|-------------|
| `#[doc = "Explanation"]` | `*` | 等同于添加 `///` 文档注释。{{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html") }} |
| `#[doc(alias = "other")]` | `*` | 为文档搜索提供其他名称。{{ link(url="https://github.com/rust-lang/rust/issues/50146") }} |
| `#[doc(hidden)]` | `*` | 防止项目出现在文档中。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#hidden") }} |
| `#![doc(html_favicon_url = "")]` | `C` | 设置文档的 `favicon`。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#html_favicon_url") }} |
| `#![doc(html_logo_url  = "")]` | `C` | 设置文档中使用的 logo。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#html_logo_url") }} |
| `#![doc(html_playground_url  = "")]` | `C` | 生成 `Run` 按钮并使用给定服务。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#html_playground_url") }} |
| `#![doc(html_root_url  = "")]` | `C` | 链接到外部 crate 的基本 URL。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#html_root_url") }} |
| `#![doc(html_no_source)]` | `C` | 防止源代码包含在文档中。{{ link(url="https://doc.rust-lang.org/rustdoc/write-documentation/the-doc-attribute.html#html_no_source") }} |

<!-- | `#![doc(issue_tracker_base_url  = "")]` | `C` | Mostly for `std::`, where issue numbers link. {{ link(url="https://doc.rust-lang.org/rustdoc/the-doc-attribute.html#issue_tracker_base_url") }}| -->

</fixed-3-column>




</div></panel></tab>




<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-8" name="tab-group-preprocessing">
<label for="tab-preprocessing-8"><b><code>#[macros]</code></b></label>
<panel><div class="color-header undefined-color-3">

<fixed-3-column  class="color-header special_example">

与宏的创建和使用相关的属性：

| 示例宏 | 开启 | 解释 |
|-------|---|-------------|
| `#[macro_export]` |  `!` | 将 `macro_rules!` 作为 `pub` 导出到 crate 级别 {{ ref(page="macros-by-example.html#path-based-scope") }} |
| `#[macro_use]` | `MX` | 使宏在模块中持久化；或从 `extern crate` 导入。{{ ref(page="macros-by-example.html#the-macro_use-attribute") }} |

{{ tablesep() }}

| 过程宏 | 开启 | 解释 |
|-------|---|-------------|
| `#[proc_macro]` | `F`  | 将 `fn` 标记为**函数式**过程宏，可以像 `m!()` 一样调用。{{ ref(page="procedural-macros.html#function-like-procedural-macros") }} |
| `#[proc_macro_derive(Foo)]` | `F`  | 将 `fn` 标记为**派生宏**，可以用于 `#[derive(Foo)]`。{{ ref(page="procedural-macros.html#derive-macros") }} |
| `#[proc_macro_attribute]` | `F`  | 将 `fn` 标记为**属性宏**，用于新的 `#[x]`。{{ ref(page="procedural-macros.html#attribute-macros") }} |

{{ tablesep() }}

| 派生 | 开启 | 解释 |
|-------|---|-------------|
| `#[derive(X)]` | `T` | 让某些过程宏提供 `trait X` 的实现。{{ hot() }} {{ ref(page="") }} |

<!-- | `#[derive(Eq)]` |  | xxx{{ ref(page="") }}|
| `#[derive(PartialEq)]` | |  xxx|
| `#[derive(Ord)]` | |  xxx|
| `#[derive(PartialOrd)]` | |  xxx|
| `#[derive(Clone)]` | |  xxx|
| `#[derive(Copy)]` | |  xxx|
| `#[derive(Hash)]` | |  xxx|
| `#[derive(Default)]` | |  xxx|
| `#[derive(Debug)]` | |  xxx| -->


</fixed-3-column>


</div></panel></tab>






<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-5" name="tab-group-preprocessing">
<label for="tab-preprocessing-5"><b><code>#[cfg]</code></b></label>
<panel><div class="color-header undefined-color-3">

控制条件编译的属性：

<fixed-3-column class="color-header special_example extra-wide">

| 配置属性 | 开启 | 解释 |
|-------|---|-------------|
| `#[cfg(X)]` | `*` | 如果配置 `X` 成立，则包含项目。{{ ref(page="conditional-compilation.html#the-cfg-attribute") }} |
| `#[cfg(all(X, Y, Z))]` | `*` | 如果所有选项成立，则包含项目。{{ ref(page="conditional-compilation.html#conditional-compilation") }} |
| `#[cfg(any(X, Y, Z))]` | `*` | 如果至少一个选项成立，则包含项目。{{ ref(page="conditional-compilation.html#conditional-compilation") }} |
| `#[cfg(not(X))]` | `*` | 如果 `X` 不成立，则包含项目。{{ ref(page="conditional-compilation.html#conditional-compilation") }} |
| `#[cfg_attr(X, foo = "msg")]` | `*` | 如果配置 `X` 成立，则应用 `#[foo = "msg"]`。{{ ref(page="conditional-compilation.html#the-cfg_attr-attribute") }} |

{{ tablesep() }}

> ⚠️ 注意，选项通常可以设置多次，即同一个键可以出现多个值。可以预期 `#[cfg(target_feature = "avx")]` **和** `#[cfg(target_feature = "avx2")]` 同时为 true。

{{ tablesep() }}

| 已知选项 | 开启 | 解释 |
|-------|---|-------------|
| `#[cfg(debug_assertions)]` | `*` | 是否会因 `debug_assert!()` 等函数而 panic。{{ ref(page="conditional-compilation.html#debug_assertions") }} |
| `#[cfg(feature = "foo")]` | `*` | 是否启用了功能 `foo`。{{ hot() }} {{ ref(page="conditional-compilation.html#conditional-compilation") }} |
| `#[cfg(target_arch = "x86_64")]` | `*` | Crate 编译的 CPU 架构。{{ ref(page="conditional-compilation.html#target_arch") }} |
| `#[cfg(target_env = "msvc")]` | `*` | 在操作系统上如何与 DLL 和函数进行交互。{{ ref(page="conditional-compilation.html#target_env") }} |
| `#[cfg(target_endian = "little")]` | `*` | 零成本抽象的主要原因失败。{{ ref(page="conditional-compilation.html#target_endian") }} |
| `#[cfg(target_family = "unix")]` | `*` | 操作系统所属的家族。{{ ref(page="conditional-compilation.html#target_family") }} |
| `#[cfg(target_feature = "avx")]` | `*` | 是否可用特定类的指令集。{{ ref(page="conditional-compilation.html#target_feature") }} |
| `#[cfg(target_os = "macos")]` | `*` | 代码运行的操作系统。{{ ref(page="conditional-compilation.html#target_os") }} |
| `#[cfg(target_pointer_width = "64")]` | `*` | 指针、`usize` 和字长的位数。{{ ref(page="conditional-compilation.html#target_pointer_width") }} |
| `#[cfg(target_vendor = "apple")]` | `*` | 目标的制造商。{{ ref(page="conditional-compilation.html#target_vendor") }} |
| `#[cfg(panic = "unwind")]` | `*` | panic 时是 `unwind` 还是 `abort`。{{ todo() }} |
| `#[cfg(proc_macro)]` | `*` | 是否将 crate 编译为过程宏。{{ ref(page="conditional-compilation.html#proc_macro") }} |
| `#[cfg(test)]` | `*` | 是否使用 `cargo test` 编译。{{ hot() }} {{ ref(page="conditional-compilation.html#test") }} |

</fixed-3-column>



</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-preprocessing-6" name="tab-group-preprocessing">
<label for="tab-preprocessing-6"><b><code>build.rs</code></b></label>
<panel><div class="color-header undefined-color-3">

与预构建脚本相关的环境变量和输出。

<fixed-2-column class="color-header special_example extra-wide">

| 输入环境 | 解释 {{ link(url="https://doc.rust-lang.org/cargo/reference/environment-variables.html") }} |
|-------|-------------|
| `CARGO_FEATURE_X` | 为每个激活的特性 `x` 设置的环境变量。 |
| {{ tab() }} `CARGO_FEATURE_SOMETHING` | 如果启用了特性 `something`。 |
| {{ tab() }} `CARGO_FEATURE_SOME_FEATURE` | 如果启用了特性 `some-feature`；破折号 `-` 会转换为 `_`。 |
| `CARGO_CFG_X` | 暴露 cfg 的信息；通过 `,` 连接多个选项，并将 `-` 转换为 `_`。|
| {{ tab() }} `CARGO_CFG_TARGET_OS=macos` | 如果 `target_os` 设置为 `macos`。 |
| {{ tab() }} `CARGO_CFG_TARGET_FEATURE=avx,avx2` | 如果 `target_feature` 设置为 `avx` 和 `avx2`。 |
| `OUT_DIR` | 输出文件应放置的位置。 |
| `TARGET` | 正在编译的目标三元组。 |
| `HOST` | 运行此构建脚本的主机三元组。 |
| `PROFILE` | 可以是 `debug` 或 `release`。 |

<footnotes>

可以在 `build.rs` 中通过 `env::var()?` 获取。不完全列表。

</footnotes>

</fixed-2-column>

<fixed-2-column class="color-header special_example extra-wide">

{{ tablesep() }}

| 输出字符串 | 解释 {{ link(url="https://doc.rust-lang.org/cargo/reference/build-scripts.html") }} |
|-------|-------------|
| `cargo:rerun-if-changed=PATH` | 仅当 `PATH` 更改时再次运行此 `build.rs`。 |
| `cargo:rerun-if-env-changed=VAR` | 仅当环境变量 `VAR` 更改时再次运行此 `build.rs`。 |
| `cargo:rustc-cfg=KEY[="VALUE"]` | 发出给定的 `cfg` 选项，以便用于后续编译。 |
| `cargo:rustc-cdylib-link-arg=FLAG` | 在构建 `cdylib` 时，传递链接器标志。 |
| `cargo:rustc-env=VAR=VALUE` | 发出可在编译期间通过 `env!()` 获取的变量。 |
| `cargo:rustc-flags=FLAGS` | 向编译器添加特殊标志。{{ todo() }} |
| `cargo:rustc-link-lib=[KIND=]NAME` | 链接原生库，如同使用 `-l` 选项。 |
| `cargo:rustc-link-search=[KIND=]PATH` | 查找原生库路径，如同使用 `-L` 选项。 |
| `cargo:warning=MESSAGE` | 发出编译器警告。 |

<footnotes>

通过 `build.rs` 中的 `println!()` 发出。不完全列表。

</footnotes>

</fixed-2-column>

</div></panel></tab>


</tabs>


<footnotes>

在属性的 _On_ 列中：<br>
`C` 表示在 crate 级别（通常在顶级文件中以 `#![my_attr]` 给出）。<br>
`M` 表示在模块上。<br>
`F` 表示在函数上。<br>
`S` 表示在静态变量上。<br>
`T` 表示在类型上。<br>
`X` 表示一些特殊情况。<br>
`!` 表示在宏上。<br>
`*` 表示几乎可以在任何项上使用。<br>

</footnotes>


---

# Working with Types


## Types, Traits, Generics

允许用户**自定义类型**并避免代码重复。

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-1" name="tab-group-types" checked>
<label for="tab-types-1"><b>Types & Traits</b></label>
<panel><div>


<!-- Section -->
<generics-section id="ttg-types">
<header>Types</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Device</code></type>
    </entry>
</mini-zoo>

- 一组具有特定语义、布局&hellip;的值

<mini-table>

| Type |   Values |
| --- | --- |
| `u8`  |  <code>{ 0<sub>u8</sub>, 1<sub>u8</sub>, …, 255<sub>u8</sub> }</code> |
| `char`  | `{ 'a', 'b', … '🦀' }` |
| `struct S(u8, char)`  | <code>{ (0<sub>u8</sub>, 'a'), … (255<sub>u8</sub>, '🦀') }</code> |

<subtitle>Sample types and sample values.</subtitle>

</mini-table>

</description>
</generics-section>


<!-- Section -->
<generics-section id="ttg-equivalence">
<header>类型等价与转换</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>&u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>&mut u8</code></type>
    </entry>
    <entry>
        <type class="primitive"><code>[u8; 1]</code></type>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
    </entry>
</mini-zoo>



<!-- - Question: which of the types above is different from all others?
    - Trick question: all of these types are totally different -->
- 虽然看起来简单，但 `u8`，`&u8`，`&mut u8` 完全是不同的类型。
- 任何 `t: T` 只接受完全属于 `T` 类型的值，例如，
    - `f(0_u8)` 不能调用 `f(&0_u8)`，
    - `f(&mut my_u8)` 不能调用 `f(&my_u8)`，
    - `f(0_u8)` 不能调用 `f(0_i8)`。

> 是的，`0 != 0`（在数学意义上）在类型转换中成立！在语言中，操作 <code>==(0<sub>u8</sub>, 0<sub>u16</sub>)</code> 甚至未定义，以防止意外错误。

<mini-table>

| Type | Values |
| --- | --- |
| `u8`  | <code>{ 0<sub>u8</sub>, 1<sub>u8</sub>, …, 255<sub>u8</sub> }</code> |
| `u16`  | <code>{ 0<sub>u16</sub>, 1<sub>u16</sub>, …, 65_535<sub>u16</sub> }</code> |
| `&u8`  | <code>{ 0xffaa<sub>&u8</sub>, 0xffbb<sub>&u8</sub>, … }</code> |
| `&mut u8`  | <code>{ 0xffaa<sub>&mut u8</sub>, 0xffbb<sub>&mut u8</sub>, … }</code> |

<subtitle>不同类型间的值如何不同。</subtitle>

</mini-table>



- 不过，Rust 有时会帮助**类型之间的转换**<sup>1</sup>
    - **强制转换** 手动将值从一个类型转换到另一个，例如 `0_i8 as u8`
    - **类型协作** {{ above(target="#language-sugar") }} 如果安全的话自动转换，例如 `let x: &u8 = &mut 0_u8;`




<footnotes>

<sup>1</sup> 强制转换和类型协作是将一个集合的值（例如 `u8`）转换为另一个集合的值（例如 `u16`），可能需要额外的 CPU 指令；这与**子类型**的概念不同，后者意味着类型和子类型属于相同的集合（例如 `u8` 是 `u16` 的子类型，`0_u8` 和 `0_u16` 相同），这种转换仅是编译时检查。Rust 对常规类型不使用子类型机制（`0_u8` 和 `0_u16` 确实不同），但对生命周期有类似机制。{{ link(url = "https://featherweightmusings.blogspot.com/2014/03/subtyping-and-coercion-in-rust.html") }}

<sup>2</sup> 此处的安全性不仅是物理概念（例如 <code>&u8</code> 不能强制转换为 <code>&u128</code>），还包括“历史经验是否表明这种转换容易引发编程错误”。

</footnotes>

</description>
</generics-section>



<!-- Section -->
<generics-section id="ttg-impl-s">
<header>Implementations &mdash; <code>impl S { }</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
        <impl><code>impl { … }</code></impl>
    </entry>
    <entry>
        <type class="composed"><code>String</code></type>
        <impl><code>impl { … }</code></impl>
    </entry>
    <entry>
        <type class="composed"><code>Port</code></type>
        <impl><code>impl { … }</code></impl>
    </entry>
</mini-zoo>

```
impl Port {
    fn f() { … }
}
```

- 类型通常伴随着**固有实现**，{{ ref(page="items/implementations.html#inherent-implementations") }} 例如 `impl Port {}`，这是与类型 _相关_ 的行为：
    - **关联函数** `Port::new(80)`
    - **方法** `port.close()`

> 什么被认为是 _相关的_ 更偏向哲学而非技术，没有任何东西（除了良好的编程品味）阻止你写 `u8::play_sound()`。


</description>
</generics-section>


<!-- Section -->
<generics-section id="ttg-traits">
<header>Traits &mdash; <code>trait T { }</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
    </entry>
    <entry>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

- **特征** …
    - 是抽象行为的一种方式，
    - 特征作者声明此特征在语义上表示 X，
    - 其他人可以为其类型实现该行为。
- 可以将特征视为类型的“成员列表”：


<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Copy Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>u16</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Clone Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>String</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Sized Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>char</code></td></tr>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

<subtitle>特征视作成员表，<code>Self</code> 表示包含在其中的类型。</subtitle>

</mini-table>


- **凡是在该成员列表中的类型将会遵循该特征的行为。**
- 特征也可以包括关联方法、函数……

```
trait ShowHex {
    // Must be implemented according to documentation.
    fn as_hex() -> String;

    // Provided by trait author.
    fn print_hex() {}
}
```

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
</mini-zoo>

```
trait Copy { }
```

- 没有方法的特征通常称为**标记特征**。
- `Copy` 是一个标记特征，意味着 _内存可以按位复制_。

<mini-zoo class="zoo">
    <entry>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
    </entry>
</mini-zoo>


- 一些特征完全不受显式控制
- `Sized` 是编译器为具有 _已知大小_ 的类型提供的；要么是，要么不是。


</description>
</generics-section>


<!-- Section -->
<generics-section>
<header>Implementing Traits for Types &mdash; <code>impl T for S { }</code></header>
<description>


```
impl ShowHex for Port { … }
```
- 特征为类型在某个时刻实现。
- 实现 `impl A for B` 将类型 `B` 加入到特征的成员列表：

<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr><th>ShowHex Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td></tr>
    </tbody>
</table>

</mini-table>
</mini-table>

- 从视觉上看，您可以将类型视为获得了特征的“徽章”：

<mini-zoo class="zoo">
    <entry>
        <type class="primitive"><code>u8</code></type>
        <impl><code>impl { … }</code></impl>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry>
        <type class="composed"><code>Device</code></type>
        <impl><code>impl { … }</code></impl>
        <trait-impl>⌾ <code>Transport</code></trait-impl>
    </entry>
    <entry>
        <type class="composed"><code>Port</code></type>
        <impl><code>impl { … }</code></impl>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

</description>
</generics-section>




<!-- Section -->
<generics-section>
<header>Traits vs. Interfaces</header>
<description>


<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px; width: 130px;">
    <person></person>
    <entry>
        <code style="text-align:center; width: 100%;"></code>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>venison.eat()</code>
    </entry>
</mini-zoo>

{{ tablesep() }}

**接口**

- 在 **Java** 中，Alice 创建接口 `Eat`。
- 当 Bob 编写 `Venison` 时，他必须决定是否实现 `Eat`。
- 换句话说，所有的成员资格必须在类型定义时详尽声明。
- 使用 `Venison` 时，Santa 可以利用 `Eat` 提供的行为：

```
// Santa imports `Venison` to create it, can `eat()` if he wants.
import food.Venison;

new Venison("rudolph").eat();
```


{{ tablesep() }}
{{ tablesep() }}


<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Venison</code></type>
        <code style="text-align:center; width: 100%;">+</code>
        <trait-impl>⌾ <code>Eat</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>venison.eat()</code>
    </entry>
</mini-zoo>

{{ tablesep() }}

**特征**

- 在 **Rust** 中，Alice 创建特征 `Eat`。
- Bob 创建类型 `Venison` 并决定不实现 `Eat`（他甚至可能不知道 `Eat`）。
- 某人<sup>*</sup> 后来决定为 `Venison` 添加 `Eat` 是个好主意。
- 使用 `Venison` 时，Santa 必须单独导入 `Eat`：

```
// Santa needs to import `Venison` to create it, and import `Eat` for trait method.
use food::Venison;
use tasks::Eat;

// Ho ho ho
Venison::new("rudolph").eat();
```

<footnotes>

<sup>*</sup> 为防止两个人分别以不同方式实现 `Eat`，Rust 限制此选择权仅属于 Alice 或 Bob；也就是说，`impl Eat for Venison` 只能在 `Venison` 或 `Eat` 所在的 crate 中实现。详细信息请参阅一致性。{{todo()}}

</footnotes>


</description>
</generics-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-2" name="tab-group-types">
<label for="tab-types-2"><b>Generics</b></label>
<panel><div>


<!-- Section -->
<generics-section>
<header>类型构造器 &mdash; <code>Vec&lt;&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Vec&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Vec&lt;char&gt;</code></type>
    </entry>
</mini-zoo>

- `Vec<u8>` 是 "字节向量" 类型；`Vec<char>` 是 "字符向量" 类型，但 `Vec<>` 是什么？

<mini-table>

| Construct |   Values |
| --- | --- |
| `Vec<u8>`  |  `{ [], [1], [1, 2, 3], … }` |
| `Vec<char>`  |  `{ [], ['a'], ['x', 'y', 'z'], … }` |
| `Vec<>`  |  - |

<subtitle>Types vs type constructors.</subtitle>

</mini-table>



<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>Vec&lt;&gt;</code></type>
    </entry>
</mini-zoo>

- `Vec<>` 不是一个类型，不占用内存，甚至无法被翻译成代码。
- `Vec<>` 是**类型构造器**，是创建类型的“模板”或“配方”：
    - 允许第三方通过参数构造具体类型，
    - 这样 `Vec<UserType>` 才会成为一个真正的类型。

</description>
</generics-section>


<!-- Section -->
<generics-section>
<header>泛型参数 &mdash; <code>&lt;T&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>[T; 128]</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&T</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&mut T</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
</mini-zoo>

- `Vec<>` 的参数通常命名为 `T`，因此有 `Vec<T>`。
- `T` 是类型的“变量名”，用户可以插入特定类型，例如 `Vec<f32>`，`S<u8>`，&hellip;


<mini-table>

| 类型构造器 |  产生的类型族 |
| --- | --- |
| `struct Vec<T> {}`  |  `Vec<u8>`, `Vec<f32>`, `Vec<Vec<u8>>`, … |
| `[T; 128]`  |  `[u8; 128]`, `[char; 128]`, `[Port; 128]` … |
| `&T`  |  `&u8`, `&u16`, `&str`,  … |

<subtitle>Type vs type constructors.</subtitle>

</mini-table>


```
// S<> is type constructor with parameter T; user can supply any concrete type for T.
struct S<T> {
    x: T
}

// Within 'concrete' code an existing type must be given for T.
fn f() {
    let x: S<f32> = S::new(0_f32);
}

```

</description>
</generics-section>


<!-- Section -->
<generics-section >
<header>Const Generics &mdash; <code>[T; N]</code> and <code>S&lt;const N: usize&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>[T; n]</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>S&lt;const N&gt;</code></type>
    </entry>
</mini-zoo>

- 有些类型构造器不仅接受特定类型，还接受**特定常量**。
- `[T; n]` 构造持有类型 `T` 的数组，长度为 `n`。
- 对于自定义类型，可以声明为 `MyArray<T, const N: usize>`。

<mini-table>

| Type Constructor |  Produces Family |
| --- | --- |
| `[u8; N]`  |  `[u8; 0]`, `[u8; 1]`, `[u8; 2]`, … |
| `struct S<const N: usize> {}`  |  `S<1>`, `S<6>`, `S<123>`,  … |

<subtitle>基于常量的类型构造器。</subtitle>

</mini-table>


```
let x: [u8; 4]; // "array of 4 bytes"
let y: [f32; 16]; // "array of 16 floats"

// `MyArray` is type constructor requiring concrete type `T` and
// concrete usize `N` to construct specific type.
struct MyArray<T, const N: usize> {
    data: [T; N],
}
```

</description>
</generics-section>


<!-- Section -->
<!-- <generics-section >
<header>Generics in Types</header>
<description>

</description>
</generics-section> -->




<!-- Section -->
<generics-section >
<header>边界（简单） &mdash; <code>where T: X</code></header>
<description>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="generic dotted"><code>Num&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <person>🎅</person>
    <entry>
        <type class="composed"><code>Num&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Num&lt;f32&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Num&lt;Cmplx&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 50px;">&nbsp;</code>
    </narrow-entry>
    <entry class="">
        <type class="primitive"><code>u8</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="composed"><code>Port</code></type>
        <trait-impl>⌾ <code>Clone</code></trait-impl>
        <trait-impl>⌾ <code>ShowHex</code></trait-impl>
    </entry>
</mini-zoo>

- 如果 `T` 可以是任何类型，那么如何为这种 `Num<T>` 编写代码并推理呢？
- 参数**边界**：
    - 限制允许的类型（**特征边界**）或值（**常量边界** {{ todo() }}），
    - 现在我们可以利用这些限制！
- 特征边界的作用是“成员资格检查”：

<mini-table>

<div style="display: inline-block;">

```
// Type can only be constructed for some `T` if that
// T is part of `Absolute` membership list.
struct Num<T> where T: Absolute {
    …
}

```

</div>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Absolute Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>u16</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>
</mini-table>


<!--
// Constant `N` must be `usize`
struct Arrayf32<const N: usize> {
    data: [f32; N],
} -->

<footnotes>

我们在此处为结构体添加边界。实际上，将边界添加到相应的 `impl` 块中会更好，参见本节稍后的内容。

</footnotes>

<!-- > Note to self, is `const N: usize` a "const bound"? It seemingly acts as one, limiting the choice of values for N (albeit to specific types only). -->

</description>
</generics-section>


<!-- Section -->
<generics-section>
<header>边界（复合） &mdash; <code>where T: X + Y</code></header>
<description>

<mini-zoo class="zoo">
    <entry class="grayed">
        <type class="primitive"><code>u8</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="primitive"><code>f32</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="primitive"><code>char</code></type>
    </entry>
    <entry>
        <type class="composed"><code>Cmplx</code></type>
        <trait-impl>⌾ <code>Absolute</code></trait-impl>
        <trait-impl>⌾ <code>Dim</code></trait-impl>
        <trait-impl>⌾ <code>Mul</code></trait-impl>
        <trait-impl>⌾ <code>DirName</code></trait-impl>
        <trait-impl>⌾ <code>TwoD</code></trait-impl>
    </entry>
    <entry class="grayed">
        <type class="composed"><code>Car</code></type>
        <trait-impl>⌾ <code>DirName</code></trait-impl>
    </entry>
</mini-zoo>



```
struct S<T>
where
    T: Absolute + Dim + Mul + DirName + TwoD
{ … }
```

- 长特征边界可能看起来令人望而生畏。
- 实际上，每个 `+ X` 的添加只是缩小了符合条件的类型范围。

</description>
</generics-section>



<!-- Section -->
<generics-section>
<header>Implementing Families &mdash; <code>impl&lt;&gt;</code></header>
<description>

{{ tablesep() }}

当我们编写如下代码时：
```
impl<T> S<T> where T: Absolute + Dim + Mul {
    fn f(&self, x: T) { … };
}
```
可以理解为：
- 这是为任何类型 `T` 提供的实现配方（`impl <T>` 部分），
- 其中<!--sup>*</sup--> `T` 必须是 `Absolute + Dim + Mul` 特征的成员，
- 可以将实现块添加到类型族 `S<>` 中，
- 包含的方法……

可以将 `impl<T> … {}` 代码视为**抽象地实现一系列行为**。{{ ref(page="items/implementations.html#generic-implementations") }} 最值得注意的是，它们允许第三方透明地实现类似于类型构造器生成具体类型的实现方式：

```
// If compiler encounters this, it will
// - check `0` and `x` fulfill the membership requirements of `T`
// - create two new version of `f`, one for `char`, another one for `u32`.
// - based on "family implementation" provided
s.f(0_u32);
s.f('x');
```


</description>
</generics-section>


<!-- Section -->
<generics-section>
<header>Blanket Implementations &mdash; <code>impl&lt;T&gt X for T { … }</code></header>
<description>

{{ tablesep() }}

还可以编写“族实现”，使得特征可以应用于许多类型：

```
// Also implements Serialize for any type if that type already implements ToHex
impl<T> Serialize for T where T: ToHex { … }
```

这些称为**泛型覆盖实现**。

<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>ToHex</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>Device</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

<div style="display: inline-block; width: 100px;">

→  无论左侧表格中是什么类型，都可以基于以下配方（`impl`）将其添加到右侧表格中 →

</div>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th>Serialize Trait</th></tr>
        <tr class="subheader"><th><code>Self</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u8</code></td></tr>
        <tr><td><code>Port</code></td></tr>
        <tr><td><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

</mini-table>


这是一种简洁的方式，可以在模块化的方式中为外部类型提供功能，只要它们实现了另一个接口。

</description>
</generics-section>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-types-3" name="tab-group-types">
<label for="tab-types-3"><b>高级概念</b>{{ esoteric() }}</label>
<panel><div>


<!-- Section -->
<!-- <generics-section >
<header>Pseudo-Specialization</header>
<description>

</description>
</generics-section> -->




<!-- Section -->
<generics-section>
<header>特征参数 &mdash; <code>Trait&lt;In&gt; { type Out; } </code></header>
<description>

{{ tablesep() }}

注意有些特征可以多次“附加”，而有些只能附加一次。

<mini-zoo class="zoo">
    <entry style="left:300px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>From&lt;u16&gt;</code></trait-impl>
    </entry>
    <entry style="left:400px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>type u8;</code></associated-type>
    </entry>
</mini-zoo>

<!--
<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>A&lt;T&gt;</code></trait-impl>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;u8&gt;</code></trait-impl>
    </entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;f32&gt;</code></trait-impl>
    </entry>
    <entry>
        <trait-impl class="">⌾ <code>A&lt;str&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<br>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>type T;</code></associated-type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>T = u8;</code></associated-type>
    </entry>
</mini-zoo> -->

<br>

{{ tablesep() }}

为什么会这样？

- 特征本身可以基于两种**类型参数**进行泛型：
    - `trait From<I> {}`
    - `trait Deref { type O; }`
- 记得我们说过特征是类型的“成员列表”，并将这个列表称为 `Self` 吗？
- 事实证明，参数 `I`（表示**输入**）和 `O`（表示**输出**）只是这个特征列表中的更多 _列_：

```
impl From<u8> for u16 {}
impl From<u16> for u32 {}
impl Deref for Port { type O = u8; }
impl Deref for String { type O = str; }
```


<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">From</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>I</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>u16</code></td><td><code>u8</code></td></tr>
        <tr><td><code>u32</code></td><td><code>u16</code></td></tr>
        <tr><td colspan="2"><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">Deref</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>O</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Port</code></td><td><code>u8</code></td></tr>
        <tr><td><code>String</code></td><td><code>str</code></td></tr>
        <tr><td colspan="2"><code>…</code></td></tr>
    </tbody>
</table>

</mini-table>

<subtitle>输入和输出参数。</subtitle>

</mini-table>


现在有个转折点：
- **任何输出参数 `O` 必须唯一由输入参数 `I` 决定**，
- （就像关系 `X Y` 代表一个函数一样），
- `Self` 也算作输入。

更复杂的示例：

```
trait Complex<I1, I2> {
    type O1;
    type O2;
}
```

- 这会创建一个名为 `Complex` 的类型关系，
- 包含 3 个输入（`Self` 始终是一个）和 2 个输出，表示 `(Self, I1, I2) => (O1, O2)`

<mini-table>

<table>
    <thead>
        <tr style=""><th colspan="5">Complex</th></tr>
        <tr class="subheader"><th><code>Self [I]</code></th><th><code>I1</code></th><th><code>I2</code></th><th><code>O1</code></th><th><code>O2</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Player</code></td><td><code>u8</code></td><td><code>char</code></td><td><code>f32</code></td><td><code>f32</code></td></tr>
        <tr><td><code>EvilMonster</code></td><td><code>u16</code></td><td><code>str</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>EvilMonster</code></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>NiceMonster</code></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u8</code></td></tr>
        <tr><td><code>NiceMonster</code><sup>{{ bad() }}</sup></td><td><code>u16</code></td><td><code>String</code></td><td><code>u8</code></td><td><code>u16</code></td></tr>
    </tbody>
</table>

<subtitle>各种特征实现。最后一个无效，因为 `(NiceMonster, u16, String)` 已经<br>唯一确定了输出。</subtitle>

</mini-table>

</description>
</generics-section>



<!-- Section -->
<generics-section>
<header>特征编写考量（抽象）</header>
<description>

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>A&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
        <trait-impl class="dotted">⌾ <code>A&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>car.a(0_u8)</code>
        <code>car.a(0_f32)</code>
    </entry>
</mini-zoo>

<br>

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
    </entry>
</mini-zoo>


<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>👩‍🦰</person> / <person>🧔</person>
    <entry>
        <type class="composed"><code>Car</code></type>
        <trait-impl class="">⌾ <code>B</code></trait-impl>
        <associated-type class=""><code>T = u8;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="margin-left: 10px;">
    <person>🎅</person>
    <entry>
        <code>car.b(0_u8)</code>
        <code style="text-decoration: line-through;">car.b(0_f32)</code>
    </entry>
</mini-zoo>

- 参数的选择（输入 vs. 输出）也决定了谁可以添加成员：
    - 输入参数 `I` 允许“实现家族”转发给用户（圣诞老人），
    - 输出参数 `O` 必须由特征实现者决定（Alice 或 Bob）。

```
trait A<I> { }
trait B { type O; }

// Implementor adds (X, u32) to A.
impl A<u32> for X { }

// Implementor adds family impl. (X, …) to A, user can materialze.
impl<T> A<T> for Y { }

// Implementor must decide specific entry (X, O) added to B.
impl B for X { type O = u32; }
```



<mini-table>

<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">A</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>I</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>X</code></td><td><code>u32</code></td></tr>
        <tr><td><code>Y</code></td><td><code>…</code></td></tr>
    </tbody>
</table>

<subtitle>圣诞老人可以通过提供他自己的类型 <code>T</code> 来添加更多成员。</subtitle>

</mini-table>


<mini-table style="width: 200px; display:inline-block;">

<table>
    <thead>
        <tr style=""><th colspan="2">B</th></tr>
        <tr class="subheader"><th><code>Self</code></th><th><code>O</code></th></tr>
    </thead>
    <tbody>
        <tr><td><code>Player</code></td><td><code>String</code></td></tr>
        <tr><td><code>X</code></td><td><code>u32</code></td></tr>
    </tbody>
</table>

<subtitle>对于给定的输入集（这里是 <code>Self</code>），实现者必须预选 <code>O</code>。</subtitle>

</mini-table>

</mini-table>


</description>
</generics-section>


<!-- Section -->
<generics-section id="trait-authoring-examples">
<header>特征编写考量（示例）</header>
<description>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>



{{ tablesep() }}

参数的选择取决于特征需要满足的目的。

<hr>


**无额外参数**

```
trait Query {
    fn search(&self, needle: &str);
}

impl Query for PostgreSQL { … }
impl Query for Sled { … }

postgres.search("SELECT …");
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
    </entry>
</mini-zoo>

{{ tablesep() }}

特征编写者假设：
- 实现者和用户都不需要定制 API。

{{ tablesep() }}

<hr>

**输入参数**

```
trait Query<I> {
    fn search(&self, needle: I);
}

impl Query<&str> for PostgreSQL { … }
impl Query<String> for PostgreSQL { … }
impl<T> Query<T> for Sled where T: ToU8Slice { … }

postgres.search("SELECT …");
postgres.search(input.to_string());
sled.search(file);
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query&lt;&str&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>Query&lt;String&gt;</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="dotted">⌾ <code>Query&lt;T&gt;</code></trait-impl>
        <note><span style="margin-left: 10px; display: inline-block; transform: rotate(90deg); font-size: 100%">↲</span> where <code>T</code> is <code>ToU8Slice</code>.</note>
    </entry>
</mini-zoo>


{{ tablesep() }}

特征编写者假设：
- 实现者可能希望为相同的 `Self` 类型定制 API，
- 用户可能希望决定哪些 `I` 类型的行为是可能的。

{{ tablesep() }}


<hr>


**输出参数**

```
trait Query {
    type O;
    fn search(&self, needle: Self::O);
}

impl Query for PostgreSQL { type O = String; …}
impl Query for Sled { type O = Vec<u8>; … }

postgres.search("SELECT …".to_string());
sled.search(vec![0, 1, 2, 4]);
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>O = String;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="">⌾ <code>Query</code></trait-impl>
        <associated-type class=""><code>O = Vec&lt;u8&gt;;</code></associated-type>
    </entry>
</mini-zoo>


{{ tablesep() }}

特征编写者假设：
- 实现者会为 `Self` 类型定制 API（但只定制一次），
- 用户不需要也不应该影响对特定 `Self` 的定制。

> 正如您在这里看到的，术语**输入**或**输出**与 `I` 或 `O` 是否是函数的输入或输出**没有**必然的关系！

{{ tablesep() }}

<hr>

**多个输入和输出参数**

```
trait Query<I> {
    type O;
    fn search(&self, needle: I) -> Self::O;
}

impl Query<&str> for PostgreSQL { type O = String; … }
impl Query<CString> for PostgreSQL { type O = CString; … }
impl<T> Query<T> for Sled where T: ToU8Slice { type O = Vec<u8>; … }

postgres.search("SELECT …").to_uppercase();
sled.search(&[1, 2, 3, 4]).pop();
```

<mini-zoo class="zoo">
    <person>👩‍🦰</person>
    <entry>
        <trait-impl class="dotted">⌾ <code>Query&lt;I&gt;</code></trait-impl>
        <associated-type class=""><code>type O;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo">
    <person>🧔</person>
    <entry>
        <type class="composed"><code>PostgreSQL</code></type>
        <trait-impl class="">⌾ <code>Query&lt;&str&gt;</code></trait-impl>
        <associated-type class=""><code>O = String;</code></associated-type>
        <trait-impl class="">⌾ <code>Query&lt;CString&gt;</code></trait-impl>
        <associated-type class=""><code>O = CString;</code></associated-type>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <entry>
        <type class="composed"><code>Sled</code></type>
        <trait-impl class="dotted">⌾ <code>Query&lt;T&gt;</code></trait-impl>
        <associated-type class=""><code>O = Vec&lt;u8&gt;;</code></associated-type>
        <note><span style="margin-left: 10px; display: inline-block; transform: rotate(90deg); font-size: 100%">↲</span> where <code>T</code> is <code>ToU8Slice</code>.</note>
    </entry>
</mini-zoo>


{{ tablesep() }}

和上面的示例类似，特征编写者假设：
- 用户可能希望决定哪些 `I` 类型的功能应该可用，
- 对于给定的输入，实施者应确定结果的输出类型。


</description>
</generics-section>



<!-- Section -->
<generics-section>
<header>Dynamic / Zero Sized Types</header>
<description>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="composed"><code>MostTypes</code></type>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <note>Normal types.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo">
    <narrow-entry style="width: 60px;">
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="zero"><code>Z</code></type>
        <trait-impl>⌾ <code>Sized</code></trait-impl>
        <note>Zero sized.</note>
    </entry>
</mini-zoo>


<mini-zoo class="zoo">
    <narrow-entry style="width: 60px;">
        <code style="text-align:center; width: 100%;">vs.</code>
    </narrow-entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>str</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
        <note>Dynamically sized.</note>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>[u8]</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>dyn Trait</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>

<mini-zoo class="zoo" style="">
    <entry>
        <type class="primitive"><code>…</code></type>
        <trait-impl class="grayed">⌾ <code style="text-decoration: line-through">Sized</code></trait-impl>
    </entry>
</mini-zoo>


- 如果在编译时已知类型 `T` 占用了多少字节，那么 `T` 就是 **`Sized`**{{ std(page="std/marker/trait.Sized.html") }}，例如 `u8` 和 `&[u8]` 是 `Sized`，而 `[u8]` 不是。
- 被 `Sized` 的类型表示 `impl Sized for T {}` 成立。这会自动发生，用户无法实现。
- 未被 `Sized` 的类型称为**动态大小类型**（DSTs），有时也称为**无大小类型**。{{ book(page="ch19-04-advanced-types.html#dynamically-sized-types-and-the-sized-trait") }} {{ nom(page="exotic-sizes.html#dynamically-sized-types-dsts") }} {{ ref(page="dynamically-sized-types.html#dynamically-sized-types") }}
- 没有数据的类型称为**零大小类型**（ZSTs），它们不占用内存。{{ nom(page="exotic-sizes.html#zero-sized-types-zsts") }}

<div class="color-header sized cheats">

| 示例 | 解释 |
|---------|-------------|
| `struct A { x: u8 }` | 类型 `A` 是 `Sized` 的，即 `impl Sized for A` 成立，这是一个“常规”类型。 |
| `struct B { x: [u8] }` | 由于 `[u8]` 是 DST，因此 `B` 变成 DST，即不实现 `Sized`。 |
| `struct C<T> { x: T }` | 类型参数**具有**隐式的 `T: Sized` 约束，例如 `C<A>` 有效，而 `C<B>` 无效。 |
| `struct D<T: ?Sized> { x: T }` | 使用 **`?Sized`** {{ ref(page="trait-bounds.html#sized") }} 可以选择退出该约束，即 `D<B>` 也有效。 |
| `struct E;` | 类型 `E` 是零大小类型（也是 `Sized` 的），不占用内存。 |
| `trait F { fn f(&self); }` | 特征**没有**隐式的 `Sized` 约束，即 `impl F for B {}` 有效。 |
| {{ tab() }} `trait F: Sized {}` | 特征可以通过超特征来选择加入 `Sized`。{{ above(target="#functions-behavior") }} |
| `trait G { fn g(self); }` | 对于类似 `Self` 的参数，DST 实现可能仍会失败，因为参数不能放入栈中。 |

</div>


</description>
</generics-section>


<!-- Section -->
<generics-section>
<header><code>?Sized</code></header>
<description>


<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;char&gt;</code></type>
    </entry>
    <entry>
        <type class="composed grayed"><code>S&lt;str&gt;</code></type>
    </entry>
</mini-zoo>

```
struct S<T> { … }
```

- `T` 可以是任何具体类型。
- 然而，存在一个不可见的默认约束 `T: Sized`，所以 `S<str>` 不能直接使用。
- 需要添加 `T : ?Sized` 以选择退出该约束：

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;T&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;u8&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;char&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;str&gt;</code></type>
    </entry>
</mini-zoo>

```
struct S<T> where T: ?Sized { … }
```



</description>
</generics-section>


<!-- Section -->
<generics-section>
<header>泛型与生命周期 &mdash; <code>&lt;'a&gt;</code></header>
<description>

<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;'a&gt;</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&'a f32</code></type>
    </entry>
    <entry>
        <type class="generic dotted"><code>&'a mut u8</code></type>
    </entry>
</mini-zoo>

- 生命周期在一定程度上充当类型参数：
    - 用户必须提供具体的 `'a` 来实例化类型（编译器会在方法内提供帮助），
    - `S<'p>` 和 `S<'q>` 是不同的类型，就像 `Vec<f32>` 和 `Vec<u8>` 是不同类型一样，
    - 这意味着你不能直接将 `S<'a>` 类型的值赋给期望 `S<'b>` 的变量（例外情况：生命周期的子类型关系，即 `'a` 长于 `'b`）。


<mini-zoo class="zoo">
    <entry>
        <type class="generic dotted"><code>S&lt;'a&gt;</code></type>
    </entry>
    <narrow-entry>
        <code style="text-align:center; width: 100%;">→</code>
    </narrow-entry>
    <entry>
        <type class="composed"><code>S&lt;'auto&gt;</code></type>
    </entry>
    <entry>
        <type class="composed"><code>S&lt;'static&gt;</code></type>
    </entry>
</mini-zoo>


- `'static` 是生命周期 _种类_ 中唯一可用的全局类型。

```
// `'a is free parameter here (user can pass any specific lifetime)
struct S<'a> {
    x: &'a u32
}

// In non-generic code, 'static is the only nameable lifetime we can explicitly put in here.
let a: S<'static>;

// Alternatively, in non-generic code we can (often must) omit 'a and have Rust determine
// the right value for 'a automatically.
let b: S;
```

<footnotes>

<sup>*</sup> 生命周期和类型参数之间存在微妙的差异，例如你可以显式地创建一个类型 `u32` 的实例 `0`，但除了 `'static` 之外，你不能真正创建一个生命周期（例如“行 80 - 100”），编译器会为你处理这些细节。{{ link(url="https://medium.com/nearprotocol/understanding-rust-lifetimes-e813bcd405fa" )}}

</footnotes>

</description>
</generics-section>


<!-- Section -->
<!-- <generics-section>
<header>Types of types: kinds</header>
<description>

Rust does not support higher-kinded types or even mention kinds, but knowing a
bit of theory can shed some light on how generics work. Note that the following
uses Rust-like syntax for explanations, but is not actually valid Rust.

- Values have types, e.g. `true` has type `bool`, written `true: bool`.
- Types have _kinds_, e.g. `bool` has kind `*`, also written `bool: *`. (`*` is
  pronounced _star_ or, sometimes a bit confusingly, _type_.)
- (Kinds have _sorts_, which is beyond scope here. Type theories ran out of
  English synonyms for _type_ afterwards, but luckily value/type/kind is enough
  for most type systems anyway.)

Rust conceptually uses three kinds: `*`, `kind1 -> kind2` (type constructors),
and `lifetime`.

- All values have a type of kind `*`.
- The opposite is not true: there are types of kind `*` that have no values,
  e.g. `!` (the empty type).
- Type constructors such as `Vec` take a type of kind `*`, e.g. `bool`, to a
  new type of kind `*`, in this case `Vec<bool>`. We can say `Vec: * -> *`.
- `lifetime` is the kind of lifetimes, e.g. `'static: lifetime`. Since
  `lifetime` is not `*`, types of kind `lifetime` cannot have values. They can
  however be used as parameters to create types. For example in

  ```rust
  struct S<'a> {
      x: &'a u32
  }
  ```

  the kind of `S` is `lifetime -> *`.
- Note that `Vec<'static>` is a kind error, because `Vec: * -> *`, not
  `lifetime -> *`.

</description>
</generics-section> -->


<!-- Section -->
<!-- <generics-section >
<header>Another <code>?X</code></header>
<description>

- `Sized` is trait, automatically implemented **and** automatically used as default bound
- Could there (ever) be another trait `T` so that:
    - `S<T>` means `S<T> where T: Sized + X` by default and
    - you'd have to opt out with `S<T> where T: ?X` ?
- Issue:
    - Any `S<T>` written today does not know `X`, so can't opt into supporting it
    - If `X` were introduced and not implemented for any existing type, `S<T>` would stop working on that type

</description>
</generics-section> -->


<!-- Section -->
<!-- <generics-section >
<header>GAT {{ experimental() }}</header>
<description>


</description>
</generics-section> -->



<!-- Section -->
<!-- <generics-section >
<header>(Co-/Contra-) Variance </header>
<description>


</description>
</generics-section>
 -->

<!-- Section -->
<!-- <generics-section id="zoo_todo">
<header>Todo</header>
<description>


</description>
</generics-section>
 -->


</div></panel></tab>

</tabs>

<footnotes>

点击示例以展开。

</footnotes>




## Foreign Types and Traits

您库和上游库中的类型和特征的可视化概览。

<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 750px;">


<zoo class="zoo">

<!-- REGION -->
<region style="height: 310px;">
<!-- Primitives -->
<group style="left:6%; width: 200px;">
    <entry style="left:100px; top: 10%;">
        <type class="primitive"><code>u8</code></type>
    </entry>
    <entry style="left:20px; top: 32%;">
        <type class="primitive"><code>u16</code></type>
    </entry>
    <entry style="left:30px; top: 20%;">
        <type class="primitive"><code>f32</code></type>
    </entry>
    <entry style="left:0px; top: 7%;">
        <type class="primitive"><code>bool</code></type>
    </entry>
    <entry style="left:120px; top: 32%;">
        <type class="primitive"><code>char</code></type>
    </entry>
    <label style="left:8px; top: 43%;">基本类型</label>
</group>
<!-- Composed -->
<group style="left:50%; width: 350px;">
    <entry style="left:110px; top: 60px;">
        <type class="composed"><code>File</code></type>
    </entry>
    <entry style="left:180px; top: 34%;">
        <type class="composed"><code>String</code></type>
    </entry>
    <entry style="left:230px; top: 13%;">
        <type class="composed"><code>Builder</code></type>
    </entry>
    <label style="left:150px; top: 43%;">复合类型</label>
</group>
<!-- Type constructors -->
<group style="left: 30px; top:53%; width: 200px;">
    <!-- Group -->
    <entry style="left:50px; top: 8%;">
        <type class="composed"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry style="left:45px; top: 9%;">
        <type class="composed"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <entry style="left:40px; top: 10%;">
        <type class="generic dotted"><code>Vec&lt;T&gt;</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:170px; top: 2%;">
        <type class="primitive"><code>&'a T</code></type>
    </entry>
    <entry style="left:165px; top: 3%;">
        <type class="primitive"><code>&'a T</code></type>
    </entry>
    <entry style="left:160px; top: 4%;">
        <type class="generic dotted"><code>&'a T</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:140px; top: 18%;">
        <type class="primitive"><code>&mut 'a T</code></type>
    </entry>
    <entry style="left:135px; top: 19%;">
        <type class="primitive"><code>&mut 'a T</code></type>
    </entry>
    <entry style="left:130px; top: 20%;">
        <type class="generic dotted"><code>&mut 'a T</code></type>
    </entry>
    <!-- Group -->
    <entry style="left:40px; top: 28%;">
        <type class="primitive"><code>[T; n]</code></type>
    </entry>
    <entry style="left:35px; top: 29%;">
        <type class="primitive"><code>[T; n]</code></type>
    </entry>
    <entry style="left:30px; top: 30%;">
        <type class="generic dotted"><code>[T; n]</code></type>
    </entry>
    <label style="left:80px; top: 40%;">类型构造器</label>
</group>
<!-- Functrions -->
<group style="left: 50%; top:53%; width: 200px;">
    <!-- Group -->
    <entry style="left:10px; top: 8%;">
        <function class=""><code>Vec&lt;T&gt;</code></function>
    </entry>
    <entry style="left:5px; top: 9%;">
        <function class=""><code>Vec&lt;T&gt;</code></function>
    </entry>
    <entry style="left:0px; top: 10%;">
        <function class="dotted"><code>f&lt;T&gt;() {}</code></function>
    </entry>
    <!-- Group -->
    <entry style="left:20px; top: 24%;">
        <function><code>drop() {}</code></function>
    </entry>
    <label style="left:10px; top: 40%;">函数</label>
</group>
<!-- Unsized -->
<!-- <group style="left: 50%; top:53%;">
    <entry style="left:30%; top: 10%;">
        <type class="unsized"><code>str</code></type>
    </entry>
    <entry style="left:35%; top: 20%;">
        <type class="unsized"><code>[u8]</code></type>
    </entry>
    <entry style="left:28%; top: 30%;">
        <type class="unsized"><code>dyn Trait</code></type>
    </entry>
    <label style="left:30%; top: 40%;">Unsized Types</label>
</group> -->
<!-- Macros -->
<group class="grayed" style="left: 80%; top:53%; width: 140px;">
    <entry style="left:5px; top: 15%;">
        <macro><code>PI</code></macro>
    </entry>
    <entry style="left:0px; top: 28%;">
        <macro><code>dbg!</code></macro>
    </entry>
    <label style="left:20px; top: 40%;">其他</label>
</group>
<!-- Traits -->
<group style="left:36%; width: 30px;">
    <entry style="left:20px; top: 20px;">
        <trait-impl>⌾ <code>Copy</code></trait-impl>
    </entry>
    <entry style="left:60px; top: 90px;">
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class=""><code>type Tgt;</code></associated-type>
    </entry>
    <entry style="left:90px; top: 50px;">
        <trait-impl class="">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <entry style="left:85px; top: 55px;">
        <trait-impl class="">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <entry style="left:80px; top: 60px;">
        <trait-impl class="dotted">⌾ <code>From&lt;T&gt;</code></trait-impl>
    </entry>
    <label style="left:60px; top: 43%;">Traits</label>
</group>
</region>
<region-label>上游库中定义的项。</region-label>

<!-- REGION -->
<region class="your-crate" style="height: 190px;">
<!-- traits -->
<group style="left:5px; width: 200px;">
    <entry style="left:10px; top: 25px;">
        <trait-impl class="">⌾ <code>Serialize</code></trait-impl>
    </entry>
    <entry style="left:30px; top: 65px;">
        <trait-impl class="">⌾ <code>Transport</code></trait-impl>
    </entry>
    <entry style="left:15px; top: 105px;">
        <trait-impl class="">⌾ <code>ShowHex</code></trait-impl>
    </entry>
    <!-- <label style="left:60px; top: 165px">Traits</label> -->
</group>
<!-- types -->
<group style="left:150px; width: 200px;">
    <entry style="left:0px; top: 25px;">
        <type class="composed"><code>Device</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <!-- <trait-impl class="grayed">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>type Thing;</code></associated-type> -->
        <note>Foreign trait impl. for local type.</note>
    </entry>
    <entry style="left:100px; top: 25px;">
        <type class="grayed composed"><code>String</code></type>
        <trait-impl class="">⌾ <code>Serialize</code></trait-impl>
        <note>Local trait impl. for foreign type.</note>
    </entry>
    <entry style="left:200px; top: 25px;">
        <type class="composed grayed"><code>String</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <note>{{ bad() }} Illegal, foreign trait for f. type.</note>
    </entry>
    <entry style="left:200px; top: 110px;">
        <type class="composed grayed"><code>String</code></type>
        <trait-impl class="grayed">⌾ <code>From&lt;Port&gt;</code></trait-impl>
        <note>Exception: Legal if used type local.</note>
    </entry>
    <entry style="left:300px; top: 25px;">
        <type class="composed"><code>Port</code></type>
        <trait-impl class="">⌾ <code>From&lt;u8&gt;</code></trait-impl>
        <trait-impl class="">⌾ <code>From&lt;u16&gt;</code></trait-impl>
        <note>Mult. impl. of trait with differing <b>IN</b> params.</note>
    </entry>
    <entry style="left:400px; top: 25px;">
        <type class="composed"><code>Container</code></type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>Tgt = u8;</code></associated-type>
        <trait-impl class="">⌾ <code>Deref</code></trait-impl>
        <associated-type class="grayed"><code>Tgt = f32;</code></associated-type>
        <note>{{ bad() }} Illegal impl. of trait with differing <b>OUT</b> params.</note>
    </entry>
    <entry style="left:510px; top: 15px;">
        <type class="composed"><code>T</code></type>
    </entry>
    <entry style="left:505px; top: 20px;">
        <type class="composed"><code>T</code></type>
    </entry>
    <entry style="left:500px; top: 25px;">
        <type class="generic dotted"><code>T</code></type>
        <trait-impl class="">⌾ <code>ShowHex</code></trait-impl>
        <note>Blanket impl. of trait for any type.</note>
    </entry>
</group>
</region>
<region-label>Your crate.</region-label>

<!-- REGION -->
<!-- <region style="height: 90px;">
<group style="left:324px; width: 200px;">
    <entry style="left:20px; top: 30px;">
        <code>ccc.f();</code>
    </entry>
</group>
</region>
<region-label>Downstream crates.</region-label> -->

</zoo>

<footnotes>

特征和类型的示例，以及可以为哪种类型实现哪些特征。

</footnotes>



<!-- End scrollable overflow-->
</div>
</div>




## Type Conversions

当你拥有 `A` 时，如何获取 `B`？

<div class="color-header variance">

<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-1" name="tab-variance" checked>
<label for="tab-variance-1"><b>Intro</b></label>
<panel><div>

```
fn f(x: A) -> B {
    // How can you obtain B from A?
}
```

| 方法 | 解释 |
|--------| -----------|
| **身份转换** | 平凡的情况，`B` **正是** `A`。 |
| **计算** | 通过**编写代码**变换数据来创建并操纵 `B` 的实例。 |
| **类型转换** | 在需要谨慎时进行类型之间的**按需转换**。 |
| **强制转换** | 在 _弱化规则集_ 内进行的**自动**转换。<sup>1</sup> |
| **子类型** | 在 _相同布局但不同生命周期规则集_ 内的**自动**转换。<sup>1</sup> |

{{ tablesep() }}

<footnotes>

<sup>1</sup> 尽管两者都将 `A` 转换为 `B`，但**强制转换**通常与不相关的 `B` 相关联（即类型“可以合理预期具有不同方法”），而**子类型**仅与生命周期不同的 `B` 相关联。

</footnotes>

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-2" name="tab-variance">
<label for="tab-variance-2"><b>Computation (Traits)</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x.into()
}
```

从`A`获取`B`的 _基本_ 方法。一些特征提供了规范的、用户可计算的类型关系：

| Trait | Example | Trait implies … |
|--------| -----------|-----------|
| `impl From<A> for B {}` | `a.into()` | 明显，总是有效的关系。 |
| `impl TryFrom<A> for B {}` | `a.try_into()?` | 明显，有时有效的关系。 |
| `impl Deref for A {}` | `*a` | `A` 是包含 `B` 的智能指针；也支持强制转换。 |
| `impl AsRef<B> for A {}` | `a.as_ref()` | `A` 可以被视为 `B`。 |
| `impl AsMut<B> for A {}` | `a.as_mut()` | `A` 可以被可变地视为 `B`。 |
| `impl Borrow<B> for A {}` | `a.borrow()` | `A` 有一个借用的类似物 `B`（在 `Eq` 等行为下相同）。 |
| `impl ToOwned for A { … }` | `a.to_owned()` | `A` 有一个拥有的类似物 `B`。 |


<!--
<footnotes>

<sup>1</sup> Pretty much any function, like `is_signed(x)`, puts values of two types in a _specific_ relationship, especially if their _meaning_ is highly _overloaded_ (e.g., `true` in the `is_signed` relation is proxy for a different concept than `true` in an `is_odd` one). In contrast, the traits above (and type conversions in general) are mainly about unambiguous conversions across any possible meaning.

</footnotes>
 -->

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-3" name="tab-variance">
<label for="tab-variance-3"><b>类型转换</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x as B
}
```

如果转换是 _相对显然_ 的，但可能**引发问题**，则使用关键字 `as` 进行类型转换。{{ nom(page="casts.html") }}


|  A | B | 示例 | 解释 |
|----|----| ----| -----------|
| `指针` | `指针` | `device_ptr as *const u8` | 如果 `*A`，`*B` 是 `Sized`。 |
| `指针` | `整数` | `device_ptr as usize` |  |
| `整数` | `指针` | `my_usize as *const Device` |  |
| `数字` | `数字` | `my_u8 as u16` | 通常有意外行为。{{ above(target="#numeric-types-ref") }} |
| `无字段枚举` | `整数` | `E::A as u8` |  |
| `bool` | `整数` | `true as u8` |  |
| `char` | `整数` | `'A' as u8` |  |
| `&[T; N]` | `*const T` | `my_ref as *const u8` |  |
| `fn(…)` | `指针` | `f as *const u8` | 如果指针是 `Sized`。  |
| `fn(…)` | `整数` | `f as usize` |  |

{{ tablesep() }}

<footnote>

其中 `指针`，`整数`，`数字` 只是为了简洁，实际含义如下：
- `指针` 代表任意 `*const T` 或 `*mut T`；
- `整数` 代表任意计数类型，例如 `u8` 到 `i128`；
- `数字` 代表任意 `整数`，`f32`，`f64`。

</footnote>

> **观点** {{ opinionated() }} &mdash; 类型转换，尤其是 `数字 - 数字`，很容易出错。
> 如果你关心正确性，考虑使用更明确的方法代替。

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-4" name="tab-variance">
<label for="tab-variance-4"><b>强制转换</b></label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

自动将类型 `A` **弱化**为 `B`；类型可以是**完全**不同的。{{ nom(page="coercions.html") }}


|  A | B |  解释 |
|----|----| -----------|
| `&mut T` | `&T` | **指针弱化**。 |
| `&mut T` | `*mut T` | - |
| `&T` | `*const T` | - |
| `*mut T` | `*const T` | - |
| `&T` | `&U` | **Deref**，如果 `impl Deref<Target=U> for T`。 |
| `T` | `U` | **非定大小**，如果 `impl CoerceUnsized<U> for T`。<sup>2</sup> {{ experimental() }} |
| `T` | `V` | **传递性**，如果 `T` 可强制为 `U`，`U` 可强制为 `V`。 |
| <code>&vert;x&vert; x + x</code> | `fn(u8) -> u8` | **无捕获闭包**，等同于函数指针。 |

{{ tablesep() }}

<footnote>

<sup>1</sup> _完全_ 代表你通常可以期待一个强制转换结果 `B` 是与原始类型 `A` **完全不同的类型**（即，具有完全不同的方法）。

<sup>2</sup> 在上面的例子中不完全有效，因为非定大小类型不能位于栈上；想象 `f(x: &A) -> &B`。非定大小类型的默认工作包括：
- `[T; n]` 到 `[T]`
- 如果 `impl Trait for T {}`，则 `T` 到 `dyn Trait`。
- 在复杂情况下，`Foo<…, T, …>` 到 `Foo<…, U, …>`。{{ link(url="https://doc.rust-lang.org/nomicon/coercions.html") }}

</footnote>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-5" name="tab-variance">
<label for="tab-variance-5"><b>子类型</b>{{ esoteric() }}</label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

自动将 `A` 转换为 `B`，前提是它们的类型**仅在生命周期上有所不同**{{ nom(page="subtyping.html") }} - 子类型**示例**：


| A<sup>(子类型)</sup>  | B<sup>(超类型)</sup> | 解释 |
|--------| -----------| -----------|
| `&'static u8` | `&'a u8` | 有效，永久指针也是临时指针。 |
| `&'a u8` | `&'static u8` | {{ bad() }} 无效，临时不应变为永久。 |
| `&'a &'b u8` | `&'a &'b u8` | 有效，相同类型。**但现在事情变得有趣了，继续往下看。** |
| `&'a &'static u8` | `&'a &'b u8` | 有效，`&'static u8` 也是 `&'b u8`；在 `&` 内是协变的。 |
| `&'a mut &'static u8` | `&'a mut &'b u8` | {{ bad() }} 无效且令人意外；在 `&mut` 内是不变的。 |
| `Box<&'static u8>` | `Box<&'a u8>` | 有效，包含永久的 `Box` 也是包含临时的 `Box`；协变的。 |
| `Box<&'a u8>` | `Box<&'static u8>` | {{ bad() }} 无效，包含临时的 `Box` 不得是包含永久的。 |
| `Box<&'a mut u8>` | `Box<&'a u8>` | {{ bad() }} ⚡ 无效，见下表，`&mut u8` 从未是 `&u8`。 |
| `Cell<&'static u8>` | `Cell<&'a u8>` | {{ bad() }} 无效，`Cell` 永远不能是其他东西；不变的。 |
| `fn(&'static u8)` | `fn(&'a u8)` | {{ bad() }} 如果 `fn` 需要永久指针，可能会出错；**逆变**。|
| `fn(&'a u8)` | `fn(&'static u8)` | 但能接受临时的 `fn` 也能接受永久的。 |
| `for<'r> fn(&'r u8)` | `fn(&'a u8)` | 高阶类型 `for<'r> fn(&'r u8)` 也是 `fn(&'a u8)`。 |


{{ tablesep() }}

对比之下，这些**不是**{{ bad() }} 子类型的示例：

|  A | B |  解释 |
|----|----| -----------|
| `u16` | `u8` | {{ bad() }} **显然无效**；`u16` 不应自动变为 `u8`。 |
| `u8` | `u16` | {{ bad() }} **设计上无效**；具有不同数据的类型仍然不会成为子类型，即使它们“可以”。 |
| `&'a mut u8` | `&'a u8` | {{ bad() }} 木马，不是子类型；而是强制转换（仍然有效，但不是子类型）。 |

{{ tablesep() }}

</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-variance-8" name="tab-variance">
<label for="tab-variance-8"><b>Variance</b>{{ esoteric() }}</label>
<panel><div>

```
fn f(x: A) -> B {
    x
}
```

自动将 `A` 转换为 `B`，前提是它们的类型**仅在生命周期上有所不同**{{ nom(page="subtyping.html") }} - 子类型**协变规则**：

- 一个较长的生命周期 `'a` 超过一个较短的 `'b` 是 `'b` 的子类型。
- 意味着 `'static` 是所有其他生命周期 `'a` 的子类型。
- 使用下表来判断具有参数（例如 `&'a T`）的类型是否彼此互为子类型：

| 构造<sup>1</sup> | `'a` | `T` | `U` |
|--------| -----------| -------| -------|
| `&'a T` | 协变 | 协变 |  |
| `&'a mut T` | 协变 | 不变 |  |
| `Box<T>` |  | 协变 |  |
| `Cell<T>` |  | 不变 |  |
| `fn(T) -> U` |  | **逆变** | 协变 |
| `*const T` |  | 协变 |  |
| `*mut T` |  | 不变 |  |

<footnotes>

**协变**意味着如果 `A` 是 `B` 的子类型，则 `T[A]` 是 `T[B]` 的子类型。<br>
**逆变**意味着如果 `A` 是 `B` 的子类型，则 **`T[B]`** 是 `T[A]` 的子类型。<br>
**不变**意味着即使 `A` 是 `B` 的子类型，`T[A]` 和 `T[B]` 也不会是彼此的子类型。<br>
<!-- <br> -->

<sup>1</sup> 复合类型如 `struct S<T> {}` 通过其字段的使用获得协变性，如果混合了多种协变性，通常变为不变。<br>

</footnotes>

> 💡 **换句话说**，“常规”类型永远不会互为子类型（例如，`u8` 不是 `u16` 的子类型），
> `Box<u32>` 也永远不会是其他任何类型的子类型或超类型。
> 然而，通常 `Box<A>` 可以是 `Box<B>` 的子类型（通过协变），如果 `A` 是 `B` 的子类型，
> 而这通常发生在 `A` 和 `B` 是“只在生命周期上有所不同的同类型”时，例如 `A` 是 `&'static u32`，`B` 是 `&'a u32`。

</div></panel></tab>

</tabs>

</div>


{{ tablesep() }}




---

# Coding Guides


## Idiomatic Rust

如果您习惯于 Java 或 C，考虑以下内容。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px; ">
<div class="color-header number">


| 习惯用法 | 代码 |
|--------| ---- |
| **以表达式思考** | `y = if x { a } else { b };` |
|  | `y = loop { break 5 };`  |
|  | `fn f() -> u32 { 0 }`  |
| **以迭代器思考** | `(1..10).map(f).collect()` |
|  | <code>names.iter().filter(&vert;x&vert; x.starts_with("A"))</code> |
| **用 `?` 测试不存在性** | `y = try_something()?;` |
|  | `get_option()?.run()?` |
| **使用强类型** | `enum E { Invalid, Valid { … } }` 优于 `ERROR_INVALID = -1` |
|  | `enum E { Visible, Hidden }` 优于 `visible: bool` |
|  | `struct Charge(f32)` 优于 `f32` |
| **非法状态：不可能** | `my_lock.write().unwrap().guaranteed_at_compile_time_to_be_locked = 10;` <sup>1</sup>|
|  | <code>thread::scope(&vert;s&vert; { /* 线程无法存在于 scope() 之外 */ });</code> |
| **避免 _全局_ 状态** | 多版本依赖时可能会偷偷复制静态变量。{{ bad() }} {{ link(url="https://doc.rust-lang.org/cargo/reference/resolver.html#version-incompatibility-hazards") }} |
| **提供构建器** | `Car::new("Model T").hp(20).build();` |
| **不要恐慌** | Panic 不是异常，它意味着进程应立即中止！ |
|  | 只在编程错误时 panic；否则使用 `Option<T>`{{ std(page="std/option/enum.Option.html") }} 或 `Result<T, E>`{{ std(page="std/result/enum.Result.html") }}。|
|  | 如果是用户明确要求，例如调用 `obtain()` 与 `try_obtain()`，panic 也是可以的。|
| **适度使用泛型** | 一个简单的 `<T: Bound>`（例如，`AsRef<Path>`）可以使 API 更易用。|
| | 复杂的边界使理解变得困难，如果不确定就不要在泛型上过于创新。|
| **分割实现** | 类似 `Point<T>` 的泛型可以为每个 `T` 进行单独的 `impl` 来进行特定化。|
|   | `impl<T> Point<T> { /* 添加通用方法 */ }` |
|   | `impl Point<f32> { /* 仅添加与 Point<f32> 相关的方法 */ }` |
| **不安全代码** | 避免使用 `unsafe {}`，{{ below(target="#unsafe-unsound-undefined") }} 通常有更安全、更快的解决方案。|
| **实现特征** | 使用 `#[derive(Debug, Copy, …)]` 并在需要时自定义 `impl`。|
| **工具** | 定期运行 [**clippy**](https://github.com/rust-lang/rust-clippy) 以显著提高代码质量。{{ hot() }} |
|  | 使用 [**rustfmt**](https://github.com/rust-lang/rustfmt) 格式化代码以保持一致性。{{ hot() }} |
|  | 添加 **单元测试** {{ book(page="ch11-01-writing-tests.html") }} (`#[test]`) 确保代码正常工作。|
|  | 添加 **文档测试** {{ book(page="ch14-02-publishing-to-crates-io.html") }} (` ``` my_api::f() ``` `) 确保文档与代码一致。|
| **文档** | 使用文档注释标注您的 API，这些注释可以在 [**docs.rs**](https://docs.rs) 上显示。|
|  | 别忘了包含**摘要句**和**示例**标题。|
|  | 如果适用：**Panics**，**Errors**，**Safety**，**Abort** 和 **Undefined Behavior**。|


</div>
</div>
</div>

<footnotes>

<sup>1</sup> 在大多数情况下，您应该优先使用 `?` 而不是 `.unwrap()`。但是对于锁的情况，返回的 [**`PoisonError`**](https://doc.rust-lang.org/stable/std/sync/struct.PoisonError.html) 表示另一个线程发生了 panic，因此传播 panic 通常是更好的选择。


</footnotes>

{{ tablesep() }}

> 🔥 我们**强烈**建议您在任何共享项目中遵循
> [**API 指南**](https://rust-lang.github.io/api-guidelines/)（[**检查列表**](https://rust-lang.github.io/api-guidelines/checklist.html)）！🔥


{{ tablesep() }}


## Performance Tips {#performance-tips}

"我的代码很慢" 的问题有时会在将微基准测试移植到 Rust 或分析后出现。

<div class="color-header blue">

| 评级 | 名称 | 描述 |
| --- | --- |--- |
| 🚀🍼 | **发布模式** {{ book(page="ch01-03-hello-cargo.html") }} {{ hot() }} |  总是使用 `cargo build --release` 来大幅提高速度。|
| {{ noemoji1() }}🍼{{ noemoji1() }}⚠️ | **目标为本机 CPU** {{ link(url="https://doc.rust-lang.org/rustc/codegen-options/index.html#target-cpu") }} | 将 `rustflags = ["-Ctarget-cpu=native"]` 添加到 `config.toml`。{{ above(target = "#project-anatomy") }} |
| {{ noemoji1() }}🍼⚖️ | **代码生成单元** {{ link(url="https://doc.rust-lang.org/rustc/codegen-options/index.html#codegen-units") }} | 代码生成单元设置为 `1` 可能会使代码更快，但编译速度变慢。|
| {{ noemoji1() }}🍼 | **保留容量** {{ std(page="std/?search=with_capacity") }} | 预分配集合可以减少分配压力。|
| {{ noemoji1() }}🍼 | **回收集合** {{ std(page="std/index.html?search=clear") }} | 调用 `x.clear()` 并重用 `x` 可以避免分配。|
| {{ noemoji1() }}🍼 | **追加到字符串** {{ std(page="std/macro.write.html") }} | 使用 `write!(&mut s, "{}")` 可以防止额外分配。|
| {{ noemoji1() }}🍼⚖️ | **全局分配器** {{ std(page="std/alloc/index.html#the-global_allocator-attribute") }} | 在某些平台上，使用外部分配器（如 **mimalloc** {{ link(url="https://crates.io/crates/mimalloc") }}) 可能更快。|
| | **分配缓冲** {{ link(url="https://docs.rs/bumpalo/latest/bumpalo/") }} | 特别适用于热循环中临时的、动态的内存分配。|
|  | **批量 API** | 设计 API 来一次处理多个相似元素，例如切片。|
|  {{ noemoji2() }}⚖️ | **SoA** / **AoSoA** {{ link(url="https://www.rustsim.org/blog/2020/03/23/simd-aosoa-in-nalgebra/") }} | 除此之外，还可以考虑使用 _数组的结构_ (SoA) 和类似方式。|
| 🚀{{ noemoji1() }}⚖️ | **SIMD** {{ std(page="std/simd/index.html") }} {{ experimental() }} | 在（数学密集的）批量 API 中使用 SIMD 可以获得 2x - 8x 的加速。|
|  | **减少数据大小**  | 使用小类型（例如，`u8` 对比 `u32`，存在空隙{{ todo() }}) 更好地利用缓存。|
|  | **保持数据邻近** {{ link(url="https://en.wikipedia.org/wiki/Data-oriented_design" ) }} | 存储常用数据相邻可以提高内存访问时间。|
|  | **按大小传递** {{ link(url="https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#reason-45" ) }} | 小（2-3 个字）的结构最好按值传递，较大的按引用传递。|
|  {{ noemoji2() }}⚖️ | **异步等待** {{ link( url = "https://rust-lang.github.io/async-book/01_getting_started/01_chapter.html") }} | 如果经常发生并行等待（例如，服务器 I/O）`async` 是个好主意。|
|  | **线程** {{ std(page="std/thread/index.html") }} | 线程允许您一次对多个项目执行并行工作。|
| 🚀 | ... **在应用中** | 通常适用于应用，因为较短的等待时间意味着更好的用户体验。|
| 🚀{{ noemoji1() }}⚖️ | ... **在库内** | 在库内的模糊任务使用异步往往不是好主意，可能过于主观。|
| 🚀{{ noemoji1() }} | ... **为库调用者** | 然而，让您的用户并行处理您是个好主意。|
| {{ noemoji1() }}🍼 | **缓冲 I/O** {{ std(page="std/io/index.html#bufreader-and-bufwriter") }} {{ hot() }} | 如果没有缓冲，原始 `File` I/O 高度低效。|
| {{ noemoji1() }}🍼{{ noemoji1() }}⚠️ | **更快的哈希器** {{ link(url="https://lib.rs/crates/seahash") }} | 默认 `HashMap` {{ std(page="std/collections/struct.HashMap.html") }} 的哈希器对 DoS 攻击有抵抗力，但较慢。|
| {{ noemoji1() }}🍼{{ noemoji1() }}⚠️ | **更快的 RNG**  | 如果您使用加密 RNG，考虑换成非加密的。|
| {{ noemoji2() }}⚖️ | **避免特征对象** {{ link(url="https://stackoverflow.com/questions/28621980/what-are-the-actual-runtime-performance-costs-of-dynamic-dispatch") }} | 特征对象减小代码体积，但增加内存间接访问。|
| {{ noemoji2() }}⚖️ | **延迟释放** {{ link(url="https://abrams.cc/rust-dropping-things-in-another-thread") }} | 在转储线程中释放 _重型_ 对象可以释放当前线程。|
| {{ noemoji1() }}🍼{{ noemoji1() }}⚠️ | **不检查的 API**  {{ std(page="std/?search=unchecked") }} | 如果您 100% 确信，使用 `unsafe { unchecked_ }` 跳过检查。|

</div>


<footnotes>

标记为 🚀 的条目通常会带来显著（> 2 倍）性能提升，🍼 的条目在之后实现也很简单，⚖️ 的条目可能有高昂的副作用（例如内存、复杂性），⚠️ 的条目有特殊风险（例如安全性、正确性）。

</footnotes>

{{ tablesep() }}

> **性能分析提示** {{ opinionated() }}
>
> 分析器对于识别代码中的热点至关重要。为了获得最佳体验，将以下内容添加到您的 <code class="ignore-auto language-bash">Cargo.toml</code>：
> ```cargo
> [profile.release]
> debug = true
> ```
> 然后执行 `cargo build --release` 并使用 [**Superluminal**](https://superluminal.eu/rust/)（Windows）或 [**Instruments**](https://en.wikipedia.org/wiki/Instruments_%28software%29)（macOS）运行结果。
> 也就是说，有很多性能机会是分析器找不到的，而是需要被 _设计进_ 代码中。

{{ tablesep() }}



## Async-Await 101

如果您熟悉 C# 或 TypeScript 中的 `async` / `await`，这里有一些需要注意的事项：


<tabs class="color-header orange">

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-1" name="tab-async" checked>
<label for="tab-async-1"><b>基础</b></label>
<panel><div>



| 构造 | 解释 |
|---------|-------------|
| `async`  | 声明为 `async` 的任何内容总是返回一个 `impl Future<Output=_>`。{{ std(page="std/future/trait.Future.html") }} |
| {{ tab() }} `async fn f() {}`  | 函数 `f` 返回一个 `impl Future<Output=()>`。 |
| {{ tab() }} `async fn f() -> S {}`  | 函数 `f` 返回一个 `impl Future<Output=S>`。 |
| {{ tab() }} `async { x }`  | 将 `{ x }` 转换为一个 `impl Future<Output=X>`。 |
| `let sm = f();`   | 调用 `f()`（一个 `async` 函数）不会立即执行 `f`，而是生成状态机 `sm`。{{ note(note="1") }} {{ note(note="2") }} |
| {{ tab() }} `sm = async { g() };`  | 同样地，这不会执行 `{ g() }` 代码块，而是生成状态机。 |
| `runtime.block_on(sm);`  | 在 `async {}` 之外，调度 `sm` 以实际运行，将执行 `g()`。{{ note(note="3") }} {{ note(note="4") }} |
| `sm.await` | 在 `async {}` 中，运行 `sm` 直到完成。如果 `sm` 没有准备好，则将控制权交还给运行时。|



<footnotes>

<sup>1</sup> `async` 实际上会将后续代码转换为匿名的、由编译器生成的状态机类型；`f()` 实例化该状态机。 <br>
<sup>2</sup> 状态机总是 `impl Future`，可能会是 `Send` 和其他特征，取决于在 `async` 中使用的类型。 <br>
<sup>3</sup> 状态机由工作线程通过运行时直接调用 `Future::poll()` 或通过父级 `.await` 间接调用来驱动。 <br>
<sup>4</sup> Rust 不自带运行时，需要使用外部 crate，例如 [tokio](https://crates.io/crates/tokio)。更多的帮助可见 [futures crate](https://github.com/rust-lang-nursery/futures-rs)。

</footnotes>



</div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-2" name="tab-async">
<label for="tab-async-2"><b>执行流程</b></label>
<panel><div>


在每个 `x.await` 处，状态机将控制权交给下级状态机 `x`。某些时候，通过 `.await` 调用的低级状态机可能还没有准备好。在这种情况下，工作线程返回给运行时，使其可以驱动其他 Future。稍后运行时：
- **可能**恢复执行。通常会恢复，除非 `sm` / `Future` 被丢弃。
- **可能**恢复时由之前的工作线程 **或其他** 工作线程执行（取决于运行时）。

对于在 `async` 代码块内编写的代码，简化流程图如下：


<!-- Create a horizontal scrollable area on small displays to preserve layout-->
<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```
       consecutive_code();           consecutive_code();           consecutive_code();
START --------------------> x.await --------------------> y.await --------------------> READY
// ^                          ^     ^                               Future<Output=X> ready -^
// Invoked via runtime        |     |
// or an external .await      |     This might resume on another thread (next best available),
//                            |     or NOT AT ALL if Future was dropped.
//                            |
//                            Execute `x`. If ready: just continue execution; if not, return
//                            this thread to runtime.
```

</div>
</div>

</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-async-3" name="tab-async">
<label for="tab-async-3"><b>Caveats</b> {{ bad() }} </label>
<panel><div>


考虑到执行流程，在 `async` 构造中编写代码时需注意以下几点：

<div class="color-header orange">


| 构造 {{ note(note="1") }} | 解释 |
|---------|-------------|
| `sleep_or_block();` | 绝对不可取 {{ bad() }}，不要阻塞当前线程，会阻塞执行器。 |
| `set_TL(a); x.await; TL();` | 绝对不可取 {{ bad() }}，`await` 可能会从另一个线程恢复， [线程本地存储](https://doc.rust-lang.org/std/macro.thread_local.html) 会失效。|
| `s.no(); x.await; s.go();` | 可能有问题 {{ bad() }}，如果 `Future` 在等待期间被丢弃，`await` 不会恢复。{{ note(note="2") }} |
| `Rc::new(); x.await; rc();` | 非 `Send` 类型会阻止 `impl Future` 成为 `Send`；兼容性降低。|

</div>

<footnotes>

<sup>1</sup> 这里假设 `s` 是任何可能被置于无效状态的非局部变量；`TL` 是任何线程本地存储，并且该代码块所在的 `async {}` 没有假设执行器的具体细节。<br/>
<sup>2</sup> 因为 [Drop](https://doc.rust-lang.org/std/ops/trait.Drop.html) 会在 `Future` 被丢弃时执行，所以考虑使用删除守卫来清理或修复跨越 `.await` 点时可能遗留的无效状态。

</footnotes>

</div></panel></tab>

<!-- end tabs -->
</tabs>


{{ tablesep() }}



## Closures in APIs

在 Rust 中，存在 `Fn` : `FnMut` : `FnOnce` 的子特征关系。这意味着实现了 `Fn` {{ std(page="std/ops/trait.Fn.html") }} 的闭包也实现了 `FnMut` 和 `FnOnce`。同样地，任何实现了 `FnMut` {{ std(page="std/ops/trait.FnMut.html") }} 的闭包也实现了 `FnOnce`。{{ std(page="std/ops/trait.FnOnce.html") }}

从调用的角度来看，这意味着：

<div class="color-header green">

| 签名 | 函数 `g` 可以调用 &hellip; | 函数 `g` 接受 &hellip; |
|--------| -----------| -----------|
| `g<F: FnOnce()>(f: F)`  | `f()` 最多调用一次。 |  `Fn`，`FnMut`，`FnOnce`  |
| `g<F: FnMut()>(mut f: F)`  | 可以多次调用 `f()`。 | `Fn`，`FnMut` |
| `g<F: Fn()>(f: F)`  | 可以多次调用 `f()`。  | `Fn` |

</div>

<footnotes>

注意，**要求**闭包是 `Fn` 是对调用者的最严格限制，但**拥有** `Fn` 闭包是对任何函数最兼容的情况。

</footnotes>



{{ tablesep() }}

从定义闭包的人的角度来看：

<div class="color-header green">

| 闭包 | 实现<sup>*</sup> | 说明 |
|--------| -----------| --- |
| <code> &vert;&vert; { moved_s; } </code> | `FnOnce` | 调用者必须放弃 `moved_s` 的所有权。|
| <code> &vert;&vert; { &mut s; } </code> | `FnOnce`，`FnMut` | 允许 `g()` 更改调用者的局部状态 `s`。|
| <code> &vert;&vert; { &s; } </code> | `FnOnce`，`FnMut`，`Fn` | 不允许修改状态，但可以共享和重用 `s`。|

</div>

<div class="footnotes">

<sup>*</sup> Rust [倾向于捕获](https://doc.rust-lang.org/stable/reference/expressions/closure-expr.html) 引用（结果是最“兼容”的 `Fn` 闭包），但可以通过 `move || {}` 语法强制捕获其环境的副本或移动。

</div>

{{ tablesep() }}

这带来了以下优缺点：

<div class="color-header green">

| 要求 | 优势 | 劣势 |
|--------| -----------| -----------|
| `F: FnOnce`  | <span class="good">调用者很容易满足。</span> | <span class="bad">只能调用一次，`g()` 可能只能调用 `f()` 一次。</span> |
| `F: FnMut`  | <span class="good">允许 `g()` 更改调用者的状态。</span> | <span class="bad">在 `g()` 中调用者可能不能重用捕获。</span> |
| `F: Fn`  | <span class="good">可以同时存在多个实例。</span> | <span class="bad">对调用者来说最难实现。</span> |

</div>


{{ tablesep() }}



<!-- ## Macro Hygiene -->
<!-- {{ tablesep() }} -->





## Unsafe, Unsound, Undefined

不安全代码导致非健全。非健全代码导致未定义行为。未定义行为将导致陷入黑暗面。



<tabs>

<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-0" name="tab-unsafe" checked>
<label for="tab-unsafe-0"><b>Safe Code</b></label>
<panel><div>


**Safe Code**

- 在 Rust 中，_安全_ 的定义非常狭隘，模糊地表示“固有地防止未定义行为（UB）”。
- “固有地”意味着语言本身不会让你使用它的特性导致 UB。
- 使飞机坠毁或删除数据库并不是 UB，因此从 Rust 的角度来看是“安全”的。
- 写入 `/proc/[pid]/mem` 以自我修改代码也是“安全”的，最终引起的 UB 并非由 Rust 语言本身引起。
<!-- In other words, _safe_ only means the language will produce binary code that, when reasonably invoked, executes in a manner consistent with what was written in source code. -->

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```rust
let y = x + x;  // Safe Rust only guarantees the execution of this code is consistent with
print(y);       // 'specification' (long story …). It does not guarantee that y is 2x
                // (X::add might be implemented badly) nor that y is printed (Y::fmt may panic).
```
</div></div>


</div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-1" name="tab-unsafe">
<label for="tab-unsafe-1"><b>Unsafe Code</b></label>
<panel><div>


**Unsafe Code**

- 标记为 `unsafe` 的代码具有特殊权限，例如解引用原始指针，或调用其他 `unsafe` 函数。
- 与之而来的还有特别的 **作者对编译器的承诺**，编译器将信任这些承诺。
- `unsafe` 本身并不坏，但很危险，并且在 FFI 或一些特殊的数据结构中是必须的。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```rust
// `x` must always point to race-free, valid, aligned, initialized u8 memory.
unsafe fn unsafe_f(x: *mut u8) {
    my_native_lib(x);
}
```
</div></div></div></panel></tab>


<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-2" name="tab-unsafe" >
<label for="tab-unsafe-2"><b>Undefined Behavior</b></label>
<panel><div>


**Undefined Behavior (UB)**
- 如前所述，`unsafe` 代码意味着对编译器做出了[特别的承诺](https://doc.rust-lang.org/stable/reference/behavior-considered-undefined.html)（否则它就不需要是 `unsafe` 了）。
- 未能兑现任何承诺会导致编译器生成错误代码，执行这些代码会导致 UB。
- 一旦触发了未定义行为，_任何事情_ 都可能发生。危险的是，后果可能 1）非常微妙，2）远离违规的代码，或者 3）仅在某些条件下显现。
- 看似_正常运行_的程序（包括任何数量的单元测试）并不能证明 UB 代码不会随时崩溃。
- 含有 UB 的代码是客观上危险的、无效的，绝不应该存在。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">


```rust
if maybe_true() {
    let r: &u8 = unsafe { &*ptr::null() };   // Once this runs, ENTIRE app is undefined. Even if
} else {                                     // line seemingly didn't do anything, app might now run
    println!("the spanish inquisition");     // both paths, corrupt database, or anything else.
}
```
</div></div></div></panel></tab>



<!-- NEW TAB -->
<tab>
<input type="radio" id="tab-unsafe-3" name="tab-unsafe" >
<label for="tab-unsafe-3"><b>Unsound Code</b></label>
<panel><div>


**Unsound Code**
- 任何可能（甚至是理论上）为用户输入产生 UB 的_安全_ Rust 代码总是**非健全的**。
- 任何可能因未兑现上述承诺而导致 UB 的 `unsafe` 代码也被视为非健全。
- 非健全的代码是不稳定的、安全风险，并且违反了许多 Rust 用户对代码安全的基本假设。

<div style="overflow:auto;">
<div style="min-width: 100%; width: 650px;">

```rust
fn unsound_ref<T>(x: &T) -> &u128 {      // Signature looks safe to users. Happens to be
    unsafe { mem::transmute(x) }         // ok if invoked with an &u128, UB for practically
}                                        // everything else.
```

</div></div></div></panel></tab>

</tabs>

{{ tablesep() }}

>
> **Responsible use of Unsafe** {{ opinionated() }}
>
> - 除非绝对必要，否则不要使用 `unsafe`。
> - 遵循 [Nomicon](https://doc.rust-lang.org/nightly/nomicon/)、[不安全代码指南](https://rust-lang.github.io/unsafe-code-guidelines/)，**始终**遵循**所有**安全规则，**绝不**触发 [UB](https://doc.rust-lang.org/stable/reference/behavior-considered-undefined.html)。
> - 将 `unsafe` 使用最小化，并将其封装在小且易于审查的模块中。
> - 切勿创建非健全的抽象；如果无法正确封装 `unsafe`，那就不要使用。
> - 每个 `unsafe` 单元都应该伴有文本解释，说明它的安全性原因。


{{ tablesep() }}



## Adversarial Code {{ esoteric() }}

_对抗性_ 代码是指符合 Rust 规范的第三方代码，但它不遵循 API 的约定，从而干扰您自己的（安全）保证。


<div class="color-header redred">


| 您编写的代码 | 用户代码可能做… |
|---------|---------|
| `fn g<F: Fn()>(f: F) { … }` | 意外地 panic。|
| `struct S<X: T> { … }` | 错误地实现 `T`，例如滥用 `Deref` 等。|
| `macro_rules! m { … }` | 执行上述所有情况；调用可能会具有_奇怪_的作用域。|

{{ tablesep() }}

| 风险模式 | 描述 |
|---------|---------|
| `#[repr(packed)]` | 紧凑对齐可能使引用 `&s.x` 无效。|
| `impl std::… for S {}`  | 实现任何 trait（特别是 `std::ops`）都可能被破坏，尤其是 … |
| {{ tab() }} `impl Deref for S {}` | 可能会随机 `Deref`，例如 `s.x != s.x`，或者 panic。|
| {{ tab() }} `impl PartialEq for S {}` | 可能违反等价性规则；panic。|
| {{ tab() }} `impl Eq for S {}`  | 可能导致 `s != s`；panic；不能将 `s` 用于 `HashMap` 等容器。|
| {{ tab() }} `impl Hash for S {}`  | 可能违反哈希规则；panic；不能将 `s` 用于 `HashMap` 等容器。|
| {{ tab() }} `impl Ord for S {}`  | 可能违反排序规则；panic；不能将 `s` 用于 `BTreeMap` 等容器。|
| {{ tab() }} `impl Index for S {}` | 可能随机索引，例如 `s[x] != s[x]`；panic。|
| {{ tab() }} `impl Drop for S {}` | 可能在范围结束 `{}` 或赋值 `s = new_s` 时运行代码或 panic。|
| `panic!()` | 用户代码可以随时 panic，导致进程终止或恢复。|
| <code>catch_unwind(&vert;&vert; s.f(panicky))</code> | 调用方也可能迫使在 `s` 的坏状态下继续观察。|
| `let … = f();` | 变量名称可能影响 `Drop` 的执行顺序。<sup>1</sup> {{ bad() }} |

<footnotes>

<sup>1</sup> 特别是，当你将变量名从 <code>_x</code> 改为 <code>&lowbar;</code> 时，你也会改变 `Drop` 行为，因为你改变了语义。变量名为 <code>_x</code> 将在其范围结束时调用 <code>Drop::drop()</code>，而变量名为 <code>&lowbar;</code> 会立即执行删除操作，因为命名为 <code>&lowbar;</code> 意味着是通配符，表示“丢弃此内容”，这将尽可能立即执行。

</footnotes>

{{ tablesep() }}

</div>


> **Implications**
>
> - 如果安全性依赖于类型协作（例如大部分 `std::` traits），则泛型代码无法是安全的。
> - 如果需要类型协作，必须使用 `unsafe` trait（可能需要自己实现）。
> - 你必须考虑代码在意想不到的地方（例如重新赋值、范围结束）随机执行。
> - 在最坏的 panic 情况下你仍可能被观察到。
>
> 综上所述，_安全但致命_ 的代码（例如 `airplane_speed<T>()`）可能也应遵循这些指导原则。


{{ tablesep() }}


## API Stability

更新 API 时，这些更改可能会破坏客户端代码。{{ rfc(page="1105-api-evolution.html") }} 重大更改（🔴）**肯定是破坏性的**，而次要更改（🟡）**可能是破坏性的**：

<div class="color-header api-stability">


{{ tablesep() }}

| Crates |
|---------|
| 🔴 使之前在 _stable_ 编译的 crate 现在需要 _nightly_。|
| 🟡 更改 Cargo 特性使用（例如，添加或删除特性）。|

{{ tablesep() }}


| Modules |
|---------|
| 🔴 重命名 / 移动 / 删除任何公共项。|
| 🟡 添加新的公共项，可能会破坏 `use your_crate::*` 的代码。|

{{ tablesep() }}

| Structs |
|---------|
| 🔴 在所有当前字段都是公有的情况下添加私有字段。|
| 🔴 在没有私有字段的情况下添加公有字段。|
| 🟡 添加或删除至少已有一个私有字段时的私有字段。|
| 🟡 从拥有所有私有字段（至少一个字段）的元组结构转换为正常结构，或反之亦然。|

{{ tablesep() }}

| Enums |
|---------|
| 🔴 添加新变体；可以通过早期使用 `#[non_exhaustive]` {{ ref(page="attributes/type_system.html#the-non_exhaustive-attribute") }} 来缓解此问题。|
| 🔴 向变体中添加新字段。|


{{ tablesep() }}

| Traits |
|---------|
| 🔴 添加非默认项，会破坏所有现有的 `impl T for S {}`。|
| 🔴 对项签名的任何非琐碎更改，都会影响使用者或实现者。|
| 🔴 实现任何“基本”特性，因为未实现基本特性已经是一种承诺。|
| 🟡 添加默认项，可能会与现有特性产生调度冲突。|
| 🟡 添加默认类型参数。|
| 🟡 实现任何非基本特性，可能也会导致调度冲突。|

{{ tablesep() }}

| 固有实现 |
|---------|
| 🟡 添加任何固有项，可能导致客户端更倾向于该项而不是 trait 方法，从而产生编译错误。|

{{ tablesep() }}

| 类型定义中的签名 |
|---------|
| 🔴 加强边界（例如，从 `<T>` 到 `<T: Clone>`）。|
| 🟡 放宽边界。|
| 🟡 添加默认类型参数。|
| 🟡 泛化到泛型。|

| 函数中的签名 |
|---------|
| 🔴 添加 / 删除参数。|
| 🟡 引入新类型参数。|
| 🟡 泛化到泛型。|


{{ tablesep() }}

| 行为变化 |
|---------|
| 🔴 / 🟡 **更改语义可能不会导致编译器错误，但可能会导致客户端代码做出错误的行为**。|


</div>


{{ tablesep() }}


<!-- ## Authoring Quality Crates

> **Note** <sup>💬</sup> &mdash; This chapter is mildly **subjective**. That said, it tries to be observational with respect to successful Rust crates (i.e., crates with most downloads should check most of these boxes).


<div class="color-header quality_crate">

#### Code Patterns

| What | Why |
|--------| ---- |
| ☐ Write idiomatic code, follow API guides. |  |
| ☐ Regularly use `clippy`, `fmt` |   |
| ☐ Err on the side of `#[deny]`, not `#[allow]` | asdasd |


#### Infrastructure

| What | Why |
|--------| ---- |
| ☐ Minimize dependencies. | asds |
| ☐ Add optional deps. to essential `trait` crates |  asds |
| ☐ Have unit & integration tests |  asds |
| ☐ Have benchmarks |  asds |


#### Site

| What | Why |
|--------| ---- |
| ☐ Feature **prominent** API example, screenshot … | asds |
| ☐ Have permissive license for libs. | asds |

</div>

<footnotes>


</footnotes> -->


<!-- Don't render this section for printing, won't be helpful -->
<noprint>

---

# Misc


## Links & Services

以下是其他很棒的指南和表格。


<div class="color-header lavender">


<!-- This is for major other "cheat sheet" like material on the web. Main question when adding: does it add something
    significant not found elsewhere? -->
| Cheat Sheets | Description |
|--------| -----------|
| [Rust Learning⭐](https://github.com/ctjhoa/rust-learning) | 可能是关于学习 Rust 最好的链接集合。|
| [Functional Jargon in Rust](https://github.com/JasonShin/functional-programming-jargon.rs) | Rust 中解释了函数式编程术语的集合。|
| [Rust Iterator Cheat Sheet](https://danielkeep.github.io/itercheat_baked.html) | 汇总了 `std::iter` 和 `itertools` 的与迭代器相关的方法。|

</div>


{{ tablesep() }}


Rust 社区开发的主要 Rust 书籍。


<div class="color-header lavender">

<!-- Official Rust online "books" about Rust itself or major components (e.g., WebAssembly, Embedded, …). Good test
    for inclusion can be official community involvement, +1k Github stars, … -->
| 书籍&nbsp;️📚 | 描述 |
|--------| -----------|
| [The Rust Programming Language](https://doc.rust-lang.org/stable/book/) | 标准 Rust 入门书籍，**如果你是新手，建议从这里开始**。|
| {{ tab() }} [API Guidelines](https://rust-lang.github.io/api-guidelines/) | 如何编写惯用且可重用的 Rust 代码。|
| {{ tab() }} [Asynchronous Programming](https://rust-lang.github.io/async-book/)  {{ experimental() }} | 解释了 `async` 代码、`Futures`, … |
| {{ tab() }} [Design Patterns](https://rust-unofficial.github.io/patterns//) | Idioms, Patterns, Anti-Patterns. |
| {{ tab() }} [Edition Guide](https://doc.rust-lang.org/nightly/edition-guide/) | 处理 Rust 2015、Rust 2018 及未来的版本。|
| {{ tab() }} [Error Handling](https://nrc.github.io/error-docs/intro.html) | 语言特性、库以及如何编写良好的错误代码。|
| {{ tab() }} [Guide to Rustc Development](https://rustc-dev-guide.rust-lang.org/index.html) | 解释了编译器的内部工作原理。|
| {{ tab() }} [Little Book of Rust Macros](https://veykril.github.io/tlborm/introduction.html) | 社区收集的 Rust 宏知识。|
| {{ tab() }} [Reference](https://doc.rust-lang.org/stable/reference/) {{ experimental() }}  | Rust 语言的参考文档。|
| {{ tab() }} [RFC Book](https://rust-lang.github.io/rfcs/) | 查找已接受的 RFC 及其如何改变语言的细节。|
| {{ tab() }} [Performance Book](https://nnethercote.github.io/perf-book/) | 改善速度和内存使用的技术。|
| {{ tab() }} [Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/) | 展示良好实践的简单示例集合。|
| {{ tab() }} [Rust in Easy English](https://dhghomon.github.io/easy_rust/Chapter_3.html) | 使用简化英语解释概念，**是一个很好的替代入门**。|
| {{ tab() }} [Rust for the Polyglot Programmer](https://www.chiark.greenend.org.uk/~ianmdlvl/rust-polyglot/index.html) | 适合有编程经验的人的指南。|
| {{ tab() }} [Rustdoc Book](https://doc.rust-lang.org/stable/rustdoc/) | 提供了如何自定义 `cargo doc` 和 `rustdoc` 的技巧。|
| {{ tab() }} [Rustonomicon](https://doc.rust-lang.org/nomicon/) | 关于高级和不安全 Rust 编程的黑魔法。|
| {{ tab() }} [Unsafe Code Guidelines](https://rust-lang.github.io/unsafe-code-guidelines/)  {{ experimental() }} | 关于编写 `unsafe` 代码的简明信息。|
| {{ tab() }} [Unstable Book](https://doc.rust-lang.org/unstable-book/index.html) | 关于不稳定项的信息，例如 `#![feature(…)]`。|
| [The Cargo Book](https://doc.rust-lang.org/cargo/) | 如何使用 `cargo` 及编写 `Cargo.toml`。|
| [The CLI Book](https://rust-lang-nursery.github.io/cli-wg/) | 关于创建命令行工具的信息。|
| [The Embedded Book](https://docs.rust-embedded.org/book/intro/index.html) | 在嵌入式和 `#![no_std]` 设备上工作。|
| {{ tab() }} [The Embedonomicon](https://docs.rust-embedded.org/embedonomicon/) | 第一个从零编写 `#![no_std]` 在 Cortex-M 上运行的示例。|
| [The WebAssembly Book](https://rustwasm.github.io/docs/book/) | 处理 Web 和生成 `.wasm` 文件。|
| {{ tab() }} [The `wasm-bindgen` Guide](https://rustwasm.github.io/docs/wasm-bindgen/) | 特别是关于如何绑定 Rust 和 JavaScript API 的手册。|

</div>

<footnotes>

更多非官方书籍请查看 [Little Book of Rust Books](https://lborb.github.io/book/title-page.html)。

</footnotes>

<!-- Disabled for now as looks abandoned w/o content -->
<!-- | {{ tab() }} [SIMD Performance Guide](https://rust-lang.github.io/packed_simd/perf-guide/) {{ experimental() }} | Work with `u8x32` or `f32x8` to speed up your computations.  | -->


{{ tablesep() }}

常用组件的综合查找表。

<div class="color-header lavender">

<!-- Table-like sites, often auto-generated. -->
| 表格&nbsp;📋 | 描述 |
|--------| -----------|
| [Rust Forge](https://forge.rust-lang.org/) | 列出了版本发布进度以及编译器开发者的链接。|
| {{ tab() }} [Rust Platform Support](https://doc.rust-lang.org/rustc/platform-support.html) | 所有支持的平台及其 Tier 级别。|
| {{ tab() }} [Rust Component History](https://rust-lang.github.io/rustup-components-history/) | 检查 **nightly** 版本中不同工具在不同平台的状态。|
| [ALL the Clippy Lints](https://rust-lang.github.io/rust-clippy/master/) | 所有 [**clippy**](https://github.com/rust-lang/rust-clippy) 可能有的警告。|
| [Configuring Rustfmt](https://rust-lang.github.io/rustfmt/) | 所有 [**rustfmt**](https://github.com/rust-lang/rustfmt) 可以在 `.rustfmt.toml` 中使用的选项。|
| [Compiler Error Index](https://doc.rust-lang.org/error-index.html) | 有没有想过 `E0404` 是什么意思？|
</div>

{{ tablesep() }}


提供信息或工具的在线服务。

<div class="color-header lavender">

<!-- Other online web services related to Rust. As a heuristic, things here should
    be essential (or at least address a major concern as "best of class") and be
    a self-contained, user-facing web site. -->

| 服务&nbsp;⚙️ | 描述 |
|--------| -----------|
| [crates.io](https://crates.io/) | 所有第三方 Rust 库。|
| [std.rs](https://std.rs/) | 快速访问 `std` 文档。|
| [stdrs.dev](https://stdrs.dev/) | 快速访问 `std` 文档，包括编译器内部模块。{{ esoteric() }} |
| [docs.rs](https://docs.rs/) | 为第三方库自动生成的文档。|
| [lib.rs](https://lib.rs/) | URust 库和应用的非官方质量概览。|
| [caniuse.rs](https://caniuse.rs/) | 检查哪些 Rust 版本引入或稳定了某个特性。|
| [releases.rs](https://releases.rs/) | 之前和即将发布的版本的发行说明。|
| [query.rs](https://query.rs/) | Rust 的搜索引擎。|
| [Rust Playground](https://play.rust-lang.org/) | 试验并分享 Rust 代码片段。|

</div>

{{ tablesep() }}


## Printing & PDF

> 想要这份 Rust 速查表的 PDF 版吗？下载 <a href="https://cheats.rs/dl/rust_cheat_sheet_a4.pdf"><b>最新 PDF（A4）</b></a> 或者 <a href="https://cheats.rs/dl/rust_cheat_sheet_letter.pdf"><b>Letter</b></a> 版本。或者，通过 <i>文件 > 打印</i> 然后选择“保存为 PDF”来生成（在 Chrome 中效果很好，但在 Firefox 中可能有问题）。

</noprint>

<footer>

[Ralf Biedert](https://xr.io), {{ year() }} &mdash; [cheats.rs](https://cheats.rs)

<noprint>

[Legal & Privacy](legal) - [FAQ](faq)

</noprint>

</footer>
