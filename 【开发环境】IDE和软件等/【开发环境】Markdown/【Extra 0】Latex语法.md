#### 【Extra 0】 Latex常用语法

------------------------------------------------

**摘抄自：**

[LaTeX公式手册](https://www.cnblogs.com/1024th/p/11623258.html)

[Markdown公式指导手册](https://www.zybuluo.com/codeep/note/163962#%E4%B8%83%E4%BA%A4%E6%8D%A2%E5%9B%BE%E8%A1%A8%E4%BD%BF%E7%94%A8%E5%8F%82%E8%80%83)

[维基百科Latex公式](https://zh.wikipedia.org/wiki/Help:%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F)

* 常见字母
  $$
  \phi,\mathrm{d},\psi,\nabla,\partial
  $$

  $$
  \alpha,\beta,\gamma,\delta,\epsilon,\zeta,\eta,\theta
  $$

  $$
  \iota,\kappa,\sigma,\mu,\nu,\omicron,\xi,\pi
  $$

  $$
  \rho,\sigma,\tau,\upsilon,\phi,\chi,\psi,\omega
  $$

  

* 常用符号，表达式

  `^`表示上标，`_`表示下标，多余一个字符需要`{}`
  $$
  a_{i,j},a^2,a_2,x_2^3
  $$
  前置上下标
  $$
  {}_1^2X
  $$
  导数，向量
  $$
  X^\prime,\vec{x},\overleftarrow{x},\overrightarrow{x}
  $$
  上括号
  $$
  \begin{matrix} 5050 \\ \overbrace{1+2+\cdots+100} \end{matrix}
  $$
  求和，求积
  $$
  \sum_{k=1}^N k^2,\prod_{i=1}^N x_i
  $$
  极限
  $$
  \lim_{n \to \infty}x_n
  $$
  积分 integral
  $$
  \int_{-N}^{N} e^x,{\rm d}x
  $$
  ​	*其中 {\rm d} 等价于 \mathrm{d}，即转为罗马数学体*  

  双重积分
  $$
  \iint_{D}^{W} \, \mathrm{d}x\,\mathrm{d}y
  $$
  三重积分
  $$
  \iiint_{E}^{V} \, \mathrm{d}x\,\mathrm{d}y\,\mathrm{d}z
  $$
  闭合曲线积分
  $$
  \oint_{C} x^3\, \mathrm{d}x + 4y^2\, \mathrm{d}y
  $$

* 分数
  $$
  \frac{2}{4}
  $$
  小型分数
  $$
  \tfrac{2}{4}
  $$
  

  嵌套型分数
  $$
  \cfrac{2}{c + \cfrac{2}{d + \cfrac{2}{4}}} = a
  $$
  二项式系数
  $$
  \binom{n}{r}=\binom{n}{n-r}=\mathrm{C}_n^r=\mathrm{C}_n^{n-r}
  $$

* 矩阵
  $$
  \begin{matrix}
  x & y \\
  z & v
  \end{matrix}
  $$
  有框矩阵： pmatrix 椭圆框(), bmatrix, Bmatrix   方框[], vmatrix, Vmaxtrix 竖直||

* 省略号
  $$
  \cdots  \ddots \vdots
  $$

* 条件表达式
  $$
  f(n) =
  \begin{cases} 
  n/2,  & \text{if }n\text{ is even} \\
  3n+1, & \text{if }n\text{ is odd}
  \end{cases}
  $$

* 多行等式、同余式
  $$
  \begin{aligned}
  f(x) & = (m+n)^2 \\
       & = m^2+2mn+n^2 \\
  \end{aligned}
  $$

* 方程组
  $$
  \begin{cases}
  3x + 5y +  z \\
  7x - 2y + 4z \\
  -6x + 3y + 2z
  \end{cases}
  $$

* 数组与表格

  插入竖线 |， 对齐方式 lcr，分隔符 &

  横线： \hline
  $$
  \begin{array}{c|lcr}
  n & \text{左对齐} & \text{居中对齐} & \text{右对齐} \\
  \hline
  1 & 0.24 & 1 & 125 \\
  2 & -1 & 189 & -8 \\
  3 & -20 & 2000 & 1+10i
  \end{array}
  $$
  数组实现带分隔符的矩阵
  $$
  \left[
      \begin{array}{cc|c}
        1&2&3\\
        4&5&6
      \end{array}
  \right]
  $$

* 部分字体的简称

  | 输入 |   说明   |     显示     | 输入  |    说明    |     显示     |
  | :--: | :------: | :----------: | :---: | :--------: | :----------: |
  | \rm  |  罗马体  | SampleSample | \cal  |    花体    | SAMPLESAMPLE |
  | \it  | 意大利体 | SampleSample | \Bbb  |  黑板粗体  | SAMPLESAMPLE |
  | \bf  |   粗体   | SampleSample | \mit  |  数学斜体  | SAMPLESAMPLE |
  | \sf  |  等线体  | SampleSample | \scr  |   手写体   | SAMPLESAMPLE |
  | \tt  | 打字机体 | SampleSample | \frak | 旧德式字体 |    Sample    |

* 根号

  `\surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{\frac{x^3+y^3}{2}}`
  $$
  \surd, \sqrt{2}, \sqrt[n]{}, \sqrt[3]{\frac{x^3+y^3}{2}}
  $$

* 微分及导数

  `dt, \mathrm{d}t, \partial t, \nabla\psi`
  $$
  dt, \mathrm{d}t, \partial t, \nabla\psi
  $$