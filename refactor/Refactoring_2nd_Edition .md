# Refactoring_ Improving the Design of Existing Code 2nd Edition - 2019

[TOC]

## Preface

### What’s in This Book?

**Chapter  1**  

- takes  a  small  program  with some common design ﬂaws and refactors it into a program that’s **easier to understand and  change.**

**Chapter 2**

- **I** cover more of the general principles of refactoring, some deﬁnitions,  and  the  reasons  for  doing  refactoring.  I outline  some  of  the  challenges with  refactoring.  

**Chapter  3**

-  bad smells in code 
-  how to clean them up with refactorings

**Chapter 4** 

-  how to build tests into code

**Chapter5** 

- The heart of the book—the catalog of refactorings—takes up the rest of its volume.

## Chapter1 Refactoring:A First Example

#### Decomposing the statement Function

- When  refactoring  a  long  function  like  this,  I  mentally  try  to  identify  points  that separate different parts of the overall behavior. 

## Chapter2 Principles in Refactoring

### 2.1 Defining Refactoring 

**Refactoring  (noun):**  a  change  made  to  the  internal  structure  of  software  to make  it  easier  to  understand  and  cheaper  to  modify  without  changing  its observable behavior.

**Refactoring (verb):** to restructure software by applying a series of refactorings without changing its observable behavior.

I use “**restructuring**” as a general term to  mean  any  kind  of  reorganizing  or cleaning  up  of  a  code  base,  and  see refactoring as a particular kind of restructuring.

**Refactoring**  is  always  done  to  make  the  code “**easier to understand and cheaper to modify**.” 

### 2.2 The Two Hats 

 **Two  Hats**: adding functionality and refactoring

**adding functionality** :When  I  refactor,  I  make  a  point  of  not  adding functionality;  I  only  restructure  the  code.  I  don’t  add  any  tests  (unless  I  ﬁnd  a case I missed earlier); I only change tests when I have to accommodate a changein an interface.
As I develop 

### 2.3 Why Should We Refactor?

 It  is  no  “silver bullet".Refactoring is a tool that can—and should—be used for several purposes
  - Refactoring Improves the Design of Software
      - Without  refactoring,  the  internal  design—the  architecture—of  software  tends  to decay.
      - Poorly  designed  code  usually  takes  more  code  to  do  the  same  things.
- Refactoring Makes Software Easier to Understand
- Refactoring Helps Me Find Bugs
- Refactoring Helps Me Program Faster

### 2.4 When Should We Refactor?

- The Rule of Three
- Preparatory Refactoring—Making It Easier to Add a Feature
- Comprehension Refactoring: Making Code Easier to Understand
- Litter-Pickup Refactoring
- Planned and Opportunistic Refactoring
  - You have to refactor when you run into ugly code—but excellent code needs plenty of refactoring too.
- Long-Term Refactoring
- Refactoring in a Code Review

### 2.5 Problems with Refactoring

#### 2.5.1 Slowing Down New Features

- The whole purpose of refactoring   is   to   make   us  program
  faster,  producing  more  value with less effort.
- 当重构的点相对于要实现新的代码改动量太大时，会权衡不重构而是只增加新功能
- I’m more likely to not refactor if it’s part of the code I rarely touch and the cost of the inconvenience isn’t something I feel very often
- 管理者应该表现出很在意重构
-   We  refactor  because  it  makes  us  faster—faster  to add features, faster to ﬁx bugs.

#### 2.5.2 Code Ownership

- 代码边界会导致无法重构客户端接口代码，导致重构后会有很多遗留代码

- allow team ownership of code

#### 2.5.3 Branches

-  Many of us have seen feature-branching teams that ﬁnd refactorings so exacerbate merge problems that they stop refactoring
- 使用ci可以小步提交，可以减小冲突的概率，解决次问题

#### 2.5.4 Testing

#### 2.5.5 Legacy Code

- Refactoring can be a fantastic tool to help understand a legacy system.
- The  best  advice  I  can  give  is  to get a copy of Working Effectively with Legacy Code [Feathers] and follow its guidance.
- Even  when  I  do  have  tests,  I  don’t  advocate  trying  to  refactor  a  complicated legacy  mess  into  beautiful  code  all  at  once. 
- If this  is  a  large  system,  I’ll  do  more  refactoring  in  areas  I  visit  frequently

### 2.6 Refactoring, Architecture, and Yagni

### 2.7 Refactoring and the Wider Software Development Process

### 2.8 Refactoring and Performance

### 2.9 Where Did Refactoring Come From?

### 2.10 Automated Refactorings

### 2.11 Going Further

- Refactoring Workbook

  I suggest Bill Wake’s Refactoring Workbook [Wake] that contains many exercises to practice refactoring.

- Refactoring to Patterns 

  which looks at the most valuable patterns from the hugely inﬂuential “Gang of Four” book [gof] and shows how to use refactoring to evolve towards them.

-  Working  Effectively  with  Legacy  Code  [Feathers]

  which  is  primarily  a book  about  how  to  think  about  refactoring  an  older  codebase  with  poor  test
  coverage

## 3. Bad Smells in Code

### 3.1 Mysterious Name

Sadly, however, naming is one of the two hard things [mf-2h] in programming.So, perhaps the most common refactorings we do are the renames: **Change Function Declaration**  (124) (to rename a function), **Rename  Variable**  (137), and **Rename  Field** (244).

### 3.2 Duplicated Code

- **when you have the same expression in  two  methods  of  the  same  class**.Then  all  you  have  to  do  is  **Extract  Function**
  (106) and invoke the code from both places.

- **If you have code that’s similar, but not  quite  identical,**  see  if  you  can  use  **Slide  Statements  (223)**  to  arrange  the  code
  so the similar items are all together for **easy extraction.**

  - 参数重复

  - 调用性重复

  - 回调型重复

    [^正交设计]: 额外添加正交设计关于重复部分

    

- **If the duplicate fragments are  in  subclasses  of  a  common  base  class**,  you  can  use  **Pull  Up  Method  (350)**  to avoid calling one from another.

- 如果两个毫不相关的类出现Duplicate Code，应该将重复代码提取出来放到合适的类中，可以是这两个类，也可以时一个独立的第三个类。

<!--此处讲的关于类的也可以引申到微服务，包，文件。在此处，本质上都是模块化的对象-->



### 3.3 Long Function

- Ninety-nine  percent  of  the  time,  all  you  have  to  do  to  shorten  a  function  is **Extract  Function** (106). Find parts of the function that seem to go nicely together and make a new one.
- If  you  have  a  function  with  lots  of  parameters  and  temporary  variables,  you  end  up passing  so  many  parameters  to  the  extracted  method  that  the  result  is  scarcely more readable than the original.You can often use **Replace Temp with Query (178)** to  eliminate  the  temps.  Long  lists  of  parameters  can  be  slimmed  down  with Introduce  **Parameter  Object  (140)** and **Preserve  Whole  Object  (319)**.
- If you’ve tried that and you still have too many temps and parameters, it’s time to get out the heavy artillery: Replace  **Function  with  Command  (337)**.

**How  do  you  identify  the  clumps  of  code  to  extract?**

-  A block of code with a comment that tells you what it is doing can be replaced by a method
  whose  name  is  based  on  the  **comment**
- **Conditionals** and loops also give signs for extractions. Use **Decompose Conditional (260)**  to  deal  with  conditional  expressions.
- A  big  **switch  statemen**t  should  have its legs turned into single function calls with **Extract Function** (106), If there’s more than  one  switch  statement  switching  on  the  same  condition,  you  should  apply **Replace  Conditional  with  Polymorphism  (272).**
- **With loops**, extract the loop and the code within the loop into its own method, If  you  ﬁnd  it  hard  to  give  an  extracted  loop  a  name, that  may  be  because  it’s doing  two  different  things—in  which  case  don’t  be  afraid  to  use  **Split  Loop  (227)** to break out the separate tasks

### 3.4 Long Parameter list 

- If  you  can  **obtain  one  parameter  by  asking  another  parameter**  for  it,  you  can use  **Replace  Parameter  with  Query  (324)**  to  remove  the  second  parameter
- **Rather than  pulling  lots  of  data  out  of  an  existing  data  structure**,  you  can  use  **Preserve Whole Object (319)** to pass the original data structure instead.
- If several parameters always  ﬁt  together,  combine  them  with  **Introduce  Parameter  Object  (140)**
-  If  a  parameter is used as a ﬂag to dispatch different behavior, use **Remove Flag Argument (314)**

-  When multiple  functions  share  several  parameter  values.  Then,  you  can use Combine  Functions  into  Class  (144) to capture those common values as ﬁelds

### 3.5 Global Data

### 