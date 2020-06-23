Data Structure
--------------

小甲鱼-数据结构与算法 (2014)

##  算法的时间复杂度
O(1) < O(logn) < O(n) < O(nlogn) < O(n^2) < O(n^3) < O(2^n) < O(n!) < O(n^n)

## 	空间复杂度：
算法所需存储空间	
求闰年：可以查表，也可以做个算法算出来

## 	线性表
抽象数据类型(abstract data type, ADT)：一组性质相同的值的集合及定义在集合上的一些操作的总称：int, float, char
原子类型（整型），结构类型（整型数组）
自定义抽象数据类型：3D游戏角色的坐标（x,y,z）
- ADT
    - Data：数据元素之间的逻辑关系
    - Operation： 操作
- endADT

### 线性表
ADT （List）
Data: 都是一种datatype, 第一个没有前驱，最后一个没有后继；其余每个只有个前驱和后继元素；元素之间是一对一的关系。
Operation: InitList(*L), ListEmpty(L), ClearList(*L), GetElem(L, I, *e), LocateElem(L, e), ListInsert(*L, I, e), ListDelete(*L, I, *e), ListLength(L)
endADT

两个线性表的并集: 遍历B集合，判断当前元素是否存在A中，若不存在则插入A中
    4.	ListLength(L)
    5.	GetElem(L, I, *e)
    6.	LocateElem(L, e)
    7.	ListInsert(*L, I, e)

元素	A1	A2	…	Ai-1	Ai	…	An	空闲空间
下标	0	1	…	i-2	    i-1	…	n-1

### 顺序存贮结构：
（eg数组）起始位置、最大存储容量、当前长度（会改变）
从1开始， Loc(ai+1) = Loc(ai)+c (c是每个元素的存储空间)
		 Loc(ai+1) = Loc(a1) + (i-1)*c
通过公式可以算出任意位置的地址，存储时间性能为O(1)，称为随机存储结构
查询：LocateElem(L, e)很简单， 有下标就找到了， O(1)
插入：操作需要挪动i后面的元素, O(n)
删除：O(n)


### 链式存储结构：
数据域：存储数据元素
指针域：每个元素多一个位置指向下一个元素的位置

### 单链表
s->next = p->next;
p->next = s;

单链表的删除


插入和删除都需要遍历链表： O(n)。但是每次插入都是O(1)，如果频繁插入，比顺序存储结构效率高。

单链表的整表删除
```shell script
LinkList p, q;
p = (*L)->next;
While(p) {
	q = p->next;
	Free(p);
	p = q; }
(*L)->next = NULL;
Return OK;
```


•	若线性表需要频繁查找，很少进行插入和删除操作时，宜采用顺序存储结构。
•	若需要频繁插入和删除时，宜采用单链表结构。


### 静态链表
语言（Basic, Fortran）用来描述但链表的方法：用数组来代替指针，叫游标实现法
第一个元素data为空，游标为第一个可以使用的元素；最后一个元素的游标是0；最后一个下标的游标为1（第一个有data的元素）

游标	6	5	3	4	0	2	7	…	1
数据		A	C	D	E	B		…
下标	0	1	2	3	4	5	6	…	999


静态链表的插入操作

循环链表

第一个元素：rear->next->next
判断为空：rear == rear->next
循环链表的特点：无需增加存储量，仅对连接方式稍作改变，即可使表的处理更加灵活

题目：实现将两个线性表（a1, a2, …, an） 和 (b1, b2, …, bm) 连接成一个线性表 (a1, …, an, b1, … bm)的运算。
分析：
•	若在单链表或头指针表示的单循环表上这种连接操作，都需要遍历第一个链表，周到节点an，然后将节点b1链到an的后面，其执行时间是O(n)。
•	若在尾指针表示的单循环链表上实现，则只需修改指针，无需遍历，其执行时间是O(1)。



判断单链表中是否有环

有环的定义：链表的尾节点指向了链表中的某个节点
•	方法一：使用p、q两个指针，p总是向前走，但q每次都从头开始走，对于每个节点，看p走的步数是否和q一样。如图，当p从6走到3时，用了6步，此时若q从head出发，则只需两步就到3，因而不是不等，出现矛盾，存在环。
•	方法二：使用p、q两个指针，p每次向前走一步，q每次向前走2步，若在某个时候p==q，则存在环。


### 双向链表



双向链表的插入操作

	s->next = p;
	s->prior = p->prior
	p->prior->next = s;
	p->next = s;
	
可以有效提高时间效率
双向循环链表实践
课堂掩饰题目：
•	要求实现用户输入一个数使得26个字母的排列发生变化，例如用户输入3，输出结果：
-	DEFGHIJKLMNOPQRSTUVWXYZABC
•	同时需要支持负数，例如输入-3，输出结果：
-	XYZABCDEFGHIJKLMNOPQRSTUVW



头节点没有数据，不参与循环

Vigenere(维吉尼亚)加密
当输入明文，自动生成随即密钥匹配明文中每个字母并移位加密。
明文	I	L	O	V	E	F	I	S	H	C
随机密钥	3	15	23	2	52	1	33	49	13	19
密文	L	A	L	X	E	G	P	P	U	V
建议：随机密钥生成后不能丢掉。建议把随机密钥和密文加密存储在一起。

## 	栈 Stack
Last in first out, LIFO的特殊线性表，要求只在表尾进行删除和插入操作。栈尾称top，栈首bottom，插入push，出栈pop。也分为顺序存储和链式存储。一般为顺序存储。



清空栈： s->top = s->base; 数据并没有清除
销毁栈：从物理空前销毁
容量 = s.top – s.base （不是两个地址的差）；注意指针不能相加，但可以相减

应用：2进制转换到10进制； 2进制->8进制

单链表：表头就是栈顶


中缀表达式：(1-2)*(3+4)
逆波兰表达式(Jan. Lukasiewicz)：RPN, 后缀表达式：1 2 – 4 5 + *

中缀表达式转换为后缀表达式 1+(2-3)*4+10/5
If (“)” == c) { }  //避免写成 c = “)”;

## 	队列 Queue
只允许在一段（尾）进行插入操作，而在另一端（头）进行删除操作的线性表。 FIFO。

比如键盘输入缓冲区。浏览器的历史记录是栈的例子。
队列一般用链表来实现。
对头指针->头节点（头节点不是必须的）


循环队列
循环队列的实现只要灵活改变front和rear指针即可。就是让他们不断加1，即使超出地址范围，也会从头开始。我们采取取模处理：
(rear+1)%QueueSize
(front+1)%QueueSize

## 	递归
能用迭代，就不用递归（效率低）
Sierpinski三角形
Fibonacci数列的递归实现

案例：
1.	兔子繁殖：每2月就可以繁殖： F(n) = F(n-1) + F(n-2);
2.	Factorial(n) = n*Factorial(n-1);
3.	输入任意长度得到字符串，将其反向输出。
Void print() {
	Char a;
	Scanf(“%c”, &a);
	If(a != ‘#’) print();  //调用自己
	If(a != ‘#’) printf(“%c”, a); }

分治思想
当一个为你痛规模较大，不易求解的时候，考虑将问题分成几个小的模块，逐一解决。
4.	折半查找
5.	汉诺塔 Hanoi
以为法国数学家曾编写过一个印度的古老传说：在世界中心贝纳勒斯的圣庙里，一块黄铜板上插着三根宝石针。印度教的主神梵天在创造世界的时候，在其中一根针上从下到时的穿好了由大到小的64片金片，这就是所谓的汉诺塔。不论白天黑夜，纵欲一个僧侣在按照下面的法则移动这些金片：一次只移动一片，不管在哪根针上，小片必须在大片上面。


//将n个盘子从x借助y移动到z
Void move(int n, char x, char y, char z) {
 	If ( n == 0) { print(“%c  %c \n”, x, z); }
	Else {
		Move(n-1, x, z, y); //将n个盘子从x借助z移动到y

print(“%c  %c \n”, x, z);  // 将n个盘子从x移动到z
move(n-1, y, x, z) ; //将n个盘子从y借助x移动到z
}
}

八皇后问题
该问题是19世纪注明的数学家高斯1850年提出：
在8x8格的国际象棋上摆了八个皇后，使其不能互相攻击，即任意两个皇后都不能处于同一行、同一列或同一斜线上，问有多少种摆法。
高斯先生当年由于没有学好计算机变成，没日没夜的的计算呀，得出结论是76中，硬生生把自己给“搞死”了！对了，当年还没有计算机……
正确的结果应该是92中，小甲鱼这节客和大家一起边敲代码边总结思路！


## 	字符串
子串
字符串比较大小：比ASCII码大小！小写比大写大。A-65, a-97
字符串是否相等
29.8.	BF算法 brute force
一个个比较，最坏要比较M*(N-M+1)次，O(M*N)


## 	KMP算法
D.E. Knuth, J.H. Morris and V.R. Pratt，大大避免重复遍历
问题由模式串决定，不是由目标串决定
给模式匹配串添加一个k数组（也就i是KMP算法中非著名的next数组）

Next数组：当模式匹配串T失配的时候，next数组对应的元素知道应该用T串的哪个元素进行下一轮的匹配。

## 	树
n>0时，根节点唯一；
m>0时，子树的个数没有限制，但是互相不会相交。
节点(node), 度(degree)
Degree=0: 叶节点 leaf
Degree>0：分支节点或非终端节点；除根节点，也称为内部节点。

Child, parent, sibling;
Level, depth (最大level, 上面为3)
有序树：各子树从左至右是有序的
Forest: 是m(m>0)颗互不相交的树的集合。

树的存储方式
双亲表示法


孩子表示法
方案一：根据树的度，声明足够的空间来存放子树指针的节点，但是浪费空间。
方案二：初始化和维护难度大；节省了空间，但是浪费了时间

双亲孩子表示法：


## 	二叉树
度最大是2（可以是0, 1, 2）；左子树和右子树是有顺序的，不能颠倒。
5种基本形态

有3个节点的二叉树（普通数只有2种）

斜树

满二叉树（所有分支节点都有左右子树，叶子都在同一层上）
完全二叉树
（编号为i的节点与同样深度的满二叉树中i节点的位置完全相同）
	叶子节点只能出现在最下两层；
	最下层的叶子一定集中在做不连续位置；
	倒数第2层，如果有叶子，则一定在右部连续位置。
	如果节点度为1，则该节点只有左孩子；
	同样节点树的二叉树，完全二叉树的深度最小。


二叉树的性质
1.	第i层上之多有2^(i-1)个节点
2.	深度为k，至多有2^k-1个节点
3.	如果终端节点数为n0, 度为2的节点数为n2, 则n0 = n2 + 1
4.	有n个节点的完全二叉树的深度为  (下限)
5.	如果对一颗有那个节点的完全二叉树的节点按层序号变厚啊，对任一个节点i(1 <= I <=n)，则：
•	如果I = 1, 则i是根；如果i>1，则其双亲是[i/2]
•	如果2i>n, 则节点Iwu 左孩子，否则其左孩子是节点2i
•	如果2i+1>n，则节点i无右孩子；否则其右孩子是即诶但2i+1

线索二叉树

前树遍历

中树遍历: HDIBEAFCG，可以有效利用^存放前驱后继

节点扩容：

ltag为0时lchild指向该节点的左孩子；为1时lchild指向该节点的前驱。
rtag为0时rchild指向该节点的左孩子；为1时rchild指向该节点的前驱。
线索二叉树代码实现

转换到二叉树
普通树到二叉树


森林到二叉树


二叉树到树和森林

树的遍历：先根遍历，后跟遍历

森里遍历：前序遍历，后序遍历
发现：树、森林的前根（序）遍历和二叉树的前序遍历结果相同；后根（序）和二叉树的中序遍历结果相同。

### 赫夫曼树 Huffman Tree
是首个数据压缩编码方案，1921




先把两颗二叉树简化成叶子带权的二叉树
节点的路径长度（从根节点到该节点）
树的路径长度（每个叶子的路径长度之和）
节点的带权路径长度（路径长度与路径权值的乘积）
树的带权路径长度(weighted path length, WPL): WPL越小，性能越优->最优二叉树/赫夫曼树

构造赫夫曼树过程


赫夫曼编码C语言实现

## 	图 Graph
线性表：线性关系，一对一
树：层次关系，一对多
图：多对多
由定点的有穷非空集合和定点之间变的集合组成，通常表示为：G(V,E)，其中G表示一个图，V是图G中定点的集合，E是边的集合。
数据：线性表中叫元素，树中叫节点，图中交定点（Vertex）
可以有空表，空树，但是图里顶点集合要有穷非空
无向边：Edge，用无序偶(Vi, Vj)来表示
有向边：Arc（弧）, 用有序偶表示<Vi, Vj>，Vi是弧尾，Vj是弧头，弧尾指向弧头
简单图：不存在定点到自己的边，且无重复边
无向完全图：任意两个定点之间都有边, n个定点，有n*(n-1)/2条边
有向完全图：任意两个定点之间都存在互为相反的边, n*(n-1)条边
稀疏图和稠密图：相对而言，边<n*logn为稀疏图
网络：带权(weight)的图

子图：G1=(V1,E1)和G2=(V2,E2);
图的定点与边之间的关系
对无向图，邻接点(Adjacent); 边(V1, V2)依附(incident)于定点V1和V2，或者说边(V1,V2)与顶点V1和V2相关联。
顶点V的度(degree)是和V相关联的边的数目，记为TD(V)
顶点V1到V2的路径(Path)

对有向图，<V1,V2>, V1邻接到顶点V2，顶点V2邻接自顶点V1；
以顶点V为头的弧的数目称为V的入度(InDegree)，记为ID(V)；以V为尾的弧的数目称为V的出度(OutDegree)，记为OD(V)；有TD(V)=ID(V)+OD(V)。
顶点V1到V2的路径(Path)也会有方向

路径的长度是路径上边或弧的数目。
第一个顶点到最后一个顶点相同的路径称为回路或环（cycle）
简单路径：序列中顶点不重复出现

连通图（无向图）：
如果V1到V2有路径，称为他们是联通的。如果任意两个顶点都连通，称为连通图。
连通分量：无向图中的极大连通子图；含有极大顶点数；具有极大顶点数的连通子图包含依附于这些顶点的所有边。

强连通图（有向图）：
强连通分量

连通图的生成树：极小的连通子图，它含有途中全部的n个顶点，但只有足以构成一棵树的n-1条边。



如果一个有向图有月hi个顶点入度为0，其余入度为1，则是一颗有向树。


