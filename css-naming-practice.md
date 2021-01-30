# CSS 命名实践 | CSS Naming Practice

## 相关背景 | Related Background

CSS 自诞生以来，基本语法和核心机制一直没有本质上的变化，它的发展几乎全是表现力层面上的提升。不同于 JS，CSS 本身不具有高级编程属性，无法使用变量、运算、函数等，无法管理依赖，而全局作用域使得在编写 CSS 样式的时候需要更多人工去处理优先级的问题、样式名冲突问题以及压缩极限的问题，为此，出现了很多“编译工具”和“开发方案”为 CSS 赋予“编程能力”。

Since the birth of CSS, the basic grammar and core mechanism have not changed in essence. It's development is almost entirely an improvement in expressiveness. Unlike JS, CSS itself does not have advanced programming properties, can not use variables, operations, functions, etc., and can not manage dependencies, and the global scope makes it necessary to deal with priority issues, style name conflicts, and compression limits when writing CSS styles, for this, many "compiler tools" and "development programs" have appeared to give CSS "programming capabilities".

为了结构化 CSS，主要方法论有 BEM、OOCSS 和 SMACSS。

To structure CSS, the major methodologies are BEM, OOCSS, and SMACSS.

### BEM

BEM 是一种 CSS 命名规范，旨在解决样式名的全局冲突问题。BEM 是块（block）、元素（element）、修饰符（modifier）的简写，我们常用这三个实体开发组件。

- 块(block)：一种布局或者设计上的抽象，每一个块拥有一个命名空间（前缀）。
- 元素(element)：是.block 的后代，和块一起形成一个完整的实体。
- 修饰符(modifier)：代表一个块的状态，表示它持有的一个特定属性。

BEM is a CSS naming convention designed to solve the global conflict of style names. BEM is an abbreviation of block, element, and modifier. We often use these three entity development components.

- Block: A layout or design abstraction, each block has a namespace (prefix).
- Element: It is the descendant of `.block` and forms a complete entity with the block.
- Modifier: Represents the state of a block and represents a specific attribute it holds.

在选择器中，BEM 要求只使用类名，不允许使用 id，由以下三种符号来表示扩展的关系：

- 中划线(`-`) ：仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。
- 双下划线(`__`)：双下划线用来连接块和块的子元素。
- 单下划线(`_`)：单下划线用来描述一个块或者块的子元素的一种状态。

In the selector, BEM requires only the class name to be used, and the id is not allowed. The following three symbols represent the extended relationship:

- Underline (`-`): Used only as a hyphen, to indicate a connection mark between multiple words in a block or a sub-element.
- Double underscore (`__`): Double underscores are used to connect the block and its sub-elements.
- Single underscore (`_`): Single underscore is used to describe a state of a block or its sub-elements.

```scss
//  There are a few variations on the idea but the most common one looks like this:
.block {}
.block__element {}
.block--modifier {}
.block__element--modifier {}
.block_modifier{}
.block__element_modifier{}
```

从上面 BEM 的命名要求可以看到，类名都很长，这就导致在对 CSS 文件进行压缩的时候，我们无法得到更大的优化空间。而且 BEM 仅仅是一种规范，需要团队中的开发者自行遵守，在可靠性上无法得到有效保障，而且还可能和第三方库的命名冲突。

From the above BEM naming requirements, we can see that the class names are very long, which leads to the fact that we can not get more optimization space when compressing CSS files. Moreover, BEM is only a specification that needs to be complied with by the developers in the team. It cannot be effectively guaranteed in terms of reliability, and it may conflict with third-party libraries.

### SMACSS

> 官网 | Official website: <http://smacss.com/>

SMACSS(Scalable and Modular Architecture for CSS) 是可扩展模块化的 CSS，它的核心就是结构化 CSS 代码，则有三个主要规则。

- CSS 分类规则：将 CSS 分成 Base、Layout、Module、State、Theme 这5类。
- 命名规则：考虑用命名体现样式对应的类别，如 `layout-`这样的前缀。
- 最小化适配深度：降低对特定 html 结构的依赖。

SMACSS (Scalable and Modular Architecture for CSS) is a scalable and modular CSS. Its core is structured CSS code. There are three main rules.

- Categorizing CSS Rules: Divide CSS into 5 categories: Base, Layout, Module, State, and Theme.
- Naming Rules: Consider using naming to reflect the category corresponding to the style, such as a prefix like `layout-`.
- Minimizing the depth of Applicability: Reduce the dependence on specific html structure.

### OOCSS

OOCSS(Object Oriented CSS) 即面向对象的 CSS，旨在编写高可复用、低耦合和高扩展的 CSS 代码，有两个主要原则，它们都是用来规定应该把什么属性定义在什么样式类中。

- 分离结构和主题
- 分离容器和内容

OOCSS (Object Oriented CSS) is object-oriented CSS, which aims to write highly reusable, low-coupling, and highly scalable CSS code. There are two main principles, which are used to specify what attributes should be defined in what style class in.

- Separate structure and skin
- Separate container and content

```scss
// examples: https://www.keycdn.com/blog/oocss
/*
1. Separation of structure and skin 

The structure ("invisible" things):
  - Height
  - Width
  - Margins
  - Padding
  - Overflow
An skin (visual properties):
  - Colors
  - Fonts
  - Shadows
  - Gradients 
*/
.button {
    width: 150px;
    height: 50px;
    background: #FFF;
    border-radius: 5px;
}
.button-2 {
    width: 150px;
    height: 50px;
    background: #000;
    border-radius: 5px;
}
// ====>
.button {
    background: #FFF;
}
.button-2 {
    background: #000;
}
.skin {
    width: 150px;
    height: 50px;
    border-radius: 5px;
}

/*
2. Separation of container and content 

As a general rule, styles should never be scoped to particular containers.
*/
#sidebar {
    padding: 2px;
    left: 0;
    margin: 3px;
    position: absolute;
    width: 140px;
}
#sidebar .list {
    margin: 3px;
}
#sidebar .list .list-head {
    font-size: 16px;
    color: red;
}
#sidebar .list .list-body {
    font-size: 12px;
    color: #FFF;
    background-color: red;
}
// ====>
.sidebar {
    padding: 2px;
    left: 0;
    margin: 3px;
    position: absolute;
    width: 140px;
}
.list {
    margin: 3px;
}
.list-head {
    font-size: 16px;
    color: red
}
.list-body {
    font-size: 12px;
    color: #FFF;
    background-color: red;
}

/* 
3. Using OOCSS with Sass
*/
 a.twitter {
    min-width: 100px;
    padding: 1em;
    border-radius: 1em;
    background: #55acee;
    color: #fff;
}
span.facebook {
    min-width: 100px;
    padding: 1em;
    border-radius: 1em;
    background: #3b5998;
    color: #fff;
}
// ====>
%button {
    min-width: 100px;
    padding: 1em;
    border-radius: 1em;
}
%twitter-background {
    color: #fff;
    background: #55acee;
}
%facebook-background {
    color: #fff;
    background: #3b5998;
}
.btn {
    &--twitter {
        @extend %button;
        @extend %twitter-background;
    }
    &--facebook {
        @extend %button;
        @extend %facebook-background;
    }
}
```

## 面向属性的 CSS | Property Oriented CSS

### What is POCSS?

确切地说，这里描述的只是一种关于 CSS 命名的方法论，只是它是面向 CSS 属性的，应该更准确地称作“面向属性的 CSS 命名方法（Property Oriented CSS Naming Method）”；但为了方便后文简称，同时参考 OOCSS 的命名，就权且将它命名为 POCSS (Property Oriented CSS)。那为什么不是 AOCSS (Attribute Oriented CSS) 呢？一开始是打算取 Attribute 进行命名，后来为了和社区统一，就参照了 [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference) 中的说法，取 Property 而非 Attribute 进行命名。

To be precise, what is described here is just a methodology for CSS naming, it’s CSS properties oriented, which should be more accurately called "Property Oriented CSS Naming Method"; but for the convenience of the following abbreviation, and refer to the naming of OOCSS, it is right and named POCSS (Property Oriented CSS). Then the second question is why not AOCSS (Attribute Oriented CSS)? At first, I planned to name with Attribute. But later, in order to unify with the community, I referred to the statement in [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Properties_Reference) use Property instead of Attribute for naming.

POCSS 来源呢应该是有三个阶段：
第一阶段，启蒙阶段。这里是受到 [Bootstrap Utilities](https://getbootstrap.com/docs/4.0/utilities/borders/) 的启发，整理了一些通用的 CSS 工具类，这时候还处于一种使用的时候手动拷贝需要的 CSS 类到项目中的状态。

The source of POCSS should have three stages:
The first stage is the enlightenment stage. Here is inspired by the subject of [Bootstrap Utilities](https://getbootstrap.com/docs/4.0/utilities/borders/), I have organized some general CSS tool classes. At this time, it is still in a state of manually copying the required CSS classes to the project when using it.

```html
<!-- Bootstrap Utility Examples -->
<!-- Border utilities -->
<span class="border"></span>
<span class="border-top"></span>
<span class="border-right"></span>
<span class="border-bottom"></span>
<span class="border-left"></span>
<!-- Width and height utilities -->
<div class="w-25 p-3" style="background-color: #eee;">Width 25%</div>
<div class="w-50 p-3" style="background-color: #eee;">Width 50%</div>
<div class="w-75 p-3" style="background-color: #eee;">Width 75%</div>
<div class="w-100 p-3" style="background-color: #eee;">Width 100%</div>
```

第二阶段是，成长阶段。随着整理的工具类越来越多，就索性建了一个 CSS3-Utilities 的项目，并发布到了 NPM，同时为了避免遗忘一些工具类的名称还建了个所谓的官网 [CSS3-Utilities](https://cjiali.github.io/css3-utilities/#/?id=css3-utilities)。这一阶段就可以在项目中直接引入相应的 NPM 包啦。

The second stage is the growth stage. As more and more tools were sorted out, a CSS3-Utilities project was simply built and published to NPM. At the same time, in order to avoid forgetting the names of some tool classes, I also built the so-called official website [CSS3-Utilities](https://cjiali.github.io/css3-utilities/#/?id=css3-utilities). At this stage, the corresponding NPM package can be directly imported into the project.

第三阶段，推广阶段。在机缘巧合之下有拜读到 [张鑫旭](https://www.zhangxinxu.com/) 大牛的一篇文章 [精简高效的CSS命名准则/方法](https://www.zhangxinxu.com/wordpress/2010/09/%E7%B2%BE%E7%AE%80%E9%AB%98%E6%95%88%E7%9A%84css%E5%91%BD%E5%90%8D%E5%87%86%E5%88%99%E6%96%B9%E6%B3%95/)，他还为这篇文章专门配套一个项目 [zxx.lib.css](https://github.com/zhangxinxu/zxx.lib.css/)。当时还因为自己能与一位前端大牛在这个特定的领域有着共同理念而特别地高兴，还从中吸纳了【面向属性的命名方法】这一概念从而衍生出了 POCSS 这个名词，并沿用到了现在这篇文章中。同时受到同事的推荐，还了解到了目前业界比很成熟的一个产品 [tailwindcss](https://tailwindcss.com/)，由此诞生了推广 POCSS 想法。

The third stage is the promotion stage. I read [Xinxu Zhang](https://www.zhangxinxu.com/) An article by Daniel [精简高效的CSS命名准则/方法](https://www.zhangxinxu.com/wordpress/2010/09/%E7%B2%BE%E7%AE%80%E9%AB%98%E6%95%88%E7%9A%84css%E5%91%BD%E5%90%8D%E5%87%86%E5%88%99%E6%96%B9%E6%B3%95), he also provided a special project [zxx.lib.css](https://github.com/zhangxinxu/zxx.lib.css/) for this article. At that time, I was particularly happy because I could share a common philosophy with a front-end big cow in this specific field. I also absorbed the concept of [property-oriented naming method] from which the term POCSS was derived, and it has been used today in this article. At the same time, it was recommended by [Tian Lan](lantian.tlan@bytedance.com) and also learned a product [tailwindcss](https://tailwindcss.com/) that is relatively mature in the industry, which gave birth to the idea of ​​promoting POCSS.

### How to use POCSS?

POCSS 不是一个的语言，仅仅是一种 CSS 命名的方法论。任何了解CSS的人都可以轻松掌握POCSS方法。

POCSS is not a language, just a methodology for CSS naming. Anyone who understands CSS can easily grasp the POCSS approach.

**使用原则** | The principles

POCSS 的原则：无 ID、无层级、无标签，仅仅是带有属性和值的 CSS 类。

Principles of POCSS: no IDs, no levels, no tags, just CSS classes with attributes and values.

```scss
// examples
.w-20{
  width: 20% !important;
}
.w-20vw{
  width: 20vw !important;
}
.w-min-20{
  min-width: 20% !important;
}
.w-max-20{
  max-width: 20% !important;
}
.h-20,{
  height: 20% !important;
}
.h-20vh,{
  height: 20vh !important;
}
.h-min-20,{
  min-height: 20% !important;
}
.h-max-20,{
  max-height: 20% !important;
}
```

**面临的问题** | The Problems

- 使用门槛 | Using Thresholds

POCSS 的使用门槛一方面在于在构建一个组件或页面时，通常会要求我们必须预先写出一堆可能用的着工具类以便使用，当然我们可以通过构建类库来解决这个问题，就像 [zxx.lib.css](https://github.com/zhangxinxu/zxx.lib.css/) 和 [CSS3-Utilities](https://cjiali.github.io/css3-utilities/#/?id=css3-utilities) 一样，但相比于我们日常即用即写的方式而言还是有一些门槛的。

On the one hand, the threshold for using POCSS is that when building a component or page, we usually require us to write a bunch of possible tool classes in advance for using. Of course, we can solve this problem by building a class library, like [zxx.lib.css](https://github.com/zhangxinxu/zxx.lib.css/) and [CSS3-Utilities](https://cjiali.github.io/css3-utilities/#/?id=css3-utilities), but there are still some thresholds compared to our daily write-and-use method.

另一方面在于我们工具类库不一定写得全面，写得全面的时候我们使用时就不一定记得住工具类库中的类名，这也是我之前构建了 [CSS3-Utilities](https://cjiali.github.io/css3-utilities/#/?id=css3-utilities) 这个网站的原因，但这也只能提供一种辅助性的解决方案。然后我就又从工具类库中 CSS 类名的简洁性、规范性上面下了一番功夫，包括可选地提供单词简写、全写两种方式以及严格参照 CSS 属性名等，以期达到有律可循、不易遗忘的目的。

On the other hand, our tool library may not be written comprehensively. When written comprehensively, we may not remember the class name in the tool library when using. This is also why I built the website [CSS3-Utilities](https://cjialigithub.io/css3-utilities/#/?id=css3-utilities) before, but this just can provide an auxiliary solution. Then I worked hard on the conciseness and standardization of CSS class names in the tool class library, including optionally providing word abbreviations and writing in full, and strictly referring to CSS property names, etc., in order to achieve the Purpose that can be followed and not easily forgotten.

```scss
.w-20,
.width-20 {
  width: 20% !important;
}
.w-20vw,
.width-20vw {
  width: 20vw !important;
}
.w-min-20,
.width-min-20 {
  min-width: 20% !important;
}
.w-max-20,
.width-max-20 {
  max-width: 20% !important;
}
.h-20vh,
.height-20vh {
  height: 20vh !important;
}
.h-20,
.height-20 {
  height: 20% !important;
}
.h-min-20,
.height-min-20 {
  min-height: 20% !important;
}
.h-max-20,
.height-max-20 {
  max-height: 20% !important;
}
```

- 文件压缩 | File Compression

这里借用 [tailwindcss](https://tailwindcss.com/) 官网中的例子来做说明。

Here, borrowing the example in the [tailwindcss](https://tailwindcss.com/) official website to illustrate the problem about file compression when using POCSS.

```html
<ul class="space-y-4">
  <li>
    <div class="w-64 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-56 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-48 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-40 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-32 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-24 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-20 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-16 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-12 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
  <li>
    <div class="w-10 h-3 bg-gradient-to-br from-fuchsia-500 to-purple-600"></div>
  </li>
</ul>
```

首先需要肯定的一点在于 POCSS 相较于 BEM 而言，是可以极大地压缩 CSS 文件大小的。但上面的例子就说明，当在 HTML 文件中使用 POCSS 时我们大概率无法做到有效地压缩文件大小。这时候往往需要从开发规范层面去要求开发者们配合 OOCSS 或 BEM 去解决 HTML 中 class 属性过长的情况。

The first thing to be sure is that compared to BEM, POCSS can greatly reduce the size of CSS files. But the above example shows that when using POCSS in HTML files, we probably cannot effectively compress the file size. At this time, it is often necessary to require developers to cooperate with OOCSS or BEM to solve the problem of too long class attribute in HTML from the level of development conventions.

**注：** 上面的例子也说明了为什么我们在使用 POCSS 通常需要预先写出工具类库，因为我们在进行 CSS 样式设置的时候往往需要用到大量的 CSS 属性，这时候我们即写即用 POCSS 的成本往往是大于使用 POCSS 工具类库的。

**Note:** The above example also explains why we usually need to write tool libraries in advance when we use POCSS, because we often need to use a lot of CSS properties when setting CSS styles. At this time, the cost of our write-and-use POCSS is often greater than using the POCSS class library.

### Why should use POCSS?

至于为什么应该使用 POCSS 呢，具体可以参考这篇文章 [精简高效的CSS命名准则/方法](https://www.zhangxinxu.com/wordpress/2010/09/%E7%B2%BE%E7%AE%80%E9%AB%98%E6%95%88%E7%9A%84css%E5%91%BD%E5%90%8D%E5%87%86%E5%88%99%E6%96%B9%E6%B3%95/)。在这里我总结起来主要有两个 POCSS 优点：
一是我们可以很容易地写出精简高效的CSS代码。这个是因为 POCSS 本身是面向 CSS 属性的，我们可以很容易地为 CSS 类命名，同时 POCSS 的类名本身只是关于 CSS 属性的键值对，也可以很容易地做到精简。
二是我们可以很容易地实现 CSS 代码的高度可重用性。这是因为 POCSS 自带“通用工具类”的属性和定位。

As for why we should use POCSS, for details, please refer to this article
 [精简高效的CSS命名准则/方法](https://www.zhangxinxu.com/wordpress/2010/09/%E7%B2%BE%E7%AE%80%E9%AB%98%E6%95%88%E7%9A%84css%E5%91%BD%E5%90%8D%E5%87%86%E5%88%99%E6%96%B9%E6%B3%95/). Here I sum up there are two main advantages of POCSS: One is that we can easily write streamlined and efficient CSS code. This is because POCSS itself is oriented to CSS properties. We can easily name CSS classes. At the same time, the class name of POCSS itself is just a key-value pair of CSS properties, which can be easily simplified. The second is that we can easily achieve high reusability of CSS code. This is because POCSS comes with the attributes and positioning of the "universal tool class".

### POCSS vs BEM

POCSS 相较于 BEM 的优点其实也很明显，主要两个：
一是 POCSS 本身足够精简，可以极其有效地压缩 CSS 文件大小。
二是 POCSS 具有更高的可复用性。因为 POCSS 是面向 CSS 属性的，相较于 BEM 块（block）的概念来说，粒度更细，复用的场景更多、概率更高。

Compared with BEM, POCSS has obvious advantages, mainly two: One is that POCSS itself is streamlined enough to compress CSS file size extremely effectively. The second is that POCSS has higher reusability. Because POCSS is oriented to CSS properties, compared to the concept of BEM blocks, it has thinner granularity, more reusable scenarios and higher reusable probability.

但是 POCSS 和 BEM 使用场景上是有较大地差别的。
However, the usage scenarios of POCSS and BEM are quite different.

对于通用组件来说，POCSS 即不在适用（或者说不再推荐使用），因为对于使用 POCSS 的组件而言，如果开发者想自定义组件的某些样式就不得不从增减 POCSS 样式类的角度入手，而这将变得极其地困难；而对于使用 BEM 的组件来说，开发者只需要覆盖该组件的某个样式类的定义即可达到自定义该组件样式的目的。
For general-purpose components, POCSS is no longer applicable (or no longer recommended), because for components that use POCSS, if developers want to customize certain styles of the component, they have to add or subtract POCSS style classes, and this will become extremely difficult; for components using BEM, developers only need to override the definition of a certain style class of the component to achieve the purpose of customizing the component style.

对于通用组件内部的样式（无须对外暴露的样式）或者复杂页面的样式而言，我们与其花费极大地精力去处理 CSS 样式命名的问题、命名冲突的问题、样式层级的问题以及状态修饰的问题，还不如直接上手 POCSS。
For the internal styles of common components (styles that do not need to be exposed) or the styles of complex pages, we spend a lot of energy to deal with the problems of CSS style naming, naming conflicts, style level issues, and state modification Problem, it's better to get started with POCSS directly.
