# C语言结构体知识点总结

## 一、结构体的定义
1. **基本定义形式**
   - 结构体是一种用户自定义的数据类型，用于将不同类型的数据组合在一起。其基本定义形式如下：
```c
struct 结构体名 {
    数据类型 成员1;
    数据类型 成员2;
    //...
};
```
   - 例如，定义一个表示学生信息的结构体：
```c
struct student {
    char name[20];
    int age;
    float score;
};
```
   - 这里定义了一个名为`student`的结构体，它包含了一个字符数组`name`用于存储学生姓名，一个整型变量`age`表示学生年龄，一个浮点型变量`score`代表学生成绩。



## 二、结构体变量的定义与初始化
1. **定义结构体变量**
   - 在定义结构体后，可以通过以下方式定义结构体变量：
   - 方式一：紧跟结构体定义之后定义变量。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student stu1, stu2;
```
   - 方式二：在定义结构体时同时定义变量。
```c
struct student {
    char name[20];
    int age;
    float score;
} stu3, stu4;
```
   - 方式三：使用`typedef`关键字为结构体类型定义别名后再定义变量。
```c
typedef struct student {
    char name[20];
    int age;
    float score;
} STU;
STU stu5, stu6;
```
2. **结构体变量的初始化**
   - 可以在定义结构体变量时对其进行初始化。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student stu1 = {"Tom", 18, 90.5};
```
   - 也可以先定义变量，再进行初始化。
```c
struct student stu2;
stu2 = {"Jerry", 19, 88.0};
```

## 三、结构体成员的访问
1. **使用点运算符（`.`）访问成员**
   - 对于结构体变量，可以使用点运算符来访问其成员。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student stu = {"Alice", 20, 92.0};
printf("姓名：%s\n", stu.name);
printf("年龄：%d\n", stu.age);
printf("成绩：%f\n", stu.score);
```
2. **通过指针访问成员（使用`->`运算符）**
   - 当有结构体指针时，使用`->`运算符来访问结构体成员。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student stu = {"Bob", 21, 89.5};
struct student *p = &stu;
printf("姓名：%s\n", p->name);
printf("年龄：%d\n", p->age);
printf("成绩：%f\n", p->agenda.score);
```

## 四、结构体数组
1. **定义结构体数组**
   - 结构体数组是一个数组，其中每个元素都是一个结构体。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student class[3];
```
   - 这里定义了一个名为`class`的结构体数组，它可以存储3个`student`结构体类型的元素。
2. **初始化结构体数组**
   - 可以在定义结构体数组时进行初始化。
```c
struct student {
    char name[20];
    int age;
    float score;
};
struct student class[3] = {{"Tom", 18, 90.5}, {"Jerry", 19, 88.0}, {"Alice", 20, 92.0}};
```
3. **访问结构体数组元素的成员**
   - 与普通结构体变量类似，可以使用点运算符或指针运算符来访问结构体数组元素的成员。
```c
for (int i = 0; i < 3; i++) {
    printf("学生%d的姓名：%s，年龄：%d，成绩：%f\n", i + 1, class[i].name, class[i].age, class[i].score);
}
```

## 五、结构体嵌套
1. **定义嵌套结构体**
   - 结构体中的成员可以是另一个结构体类型。
```c
struct date {
    int year;
    int month;
    int day;
};
struct student {
    char name[20];
    struct date birthday;
    float score;
};
```
   - 这里`student`结构体中嵌套了`date`结构体，用于表示学生的生日信息。
2. **访问嵌套结构体的成员**
   - 对于嵌套结构体的成员访问，需要使用多层的点运算符。
```c
struct student stu = {"Bob", {2000, 5, 10}, 89.5};
printf("学生的生日：%d年%d月%d日\n", stu.birthday.year, stu.birthday.month, stu.birthday.day);
```

## 六、结构体在函数中的使用
1. **结构体作为函数参数**
   - 可以将结构体变量作为函数参数传递给函数。
```c
struct student {
    char name[20];
    int age;
    float score;
};
void printStudent(struct student s) {
    printf("姓名：%s，年龄：%d，成绩：%f\n", s.name, s.age, s.score);
}
int main() {
    struct student stu = {"Tom", 18, 90.5};
    printStudent(stu);
    return 0;
}
```
   - 这种方式是值传递，函数内部对结构体参数的修改不会影响到原结构体变量。
2. **结构体指针作为函数参数**
   - 更常用的是将结构体指针作为函数参数，这样可以在函数内部修改原结构体变量的值。
```c
struct student {
    char name[20];
    int age;
    float score;
};
void modifyStudent(struct student *s) {
    s->age++;
    s->score += 5;
}
int main() {
    struct student stu = {"Tom", 18, 90.5};
    modifyStudent(&stu);
    printf("姓名：%s，年龄：%d，成绩：%f\n", stu.name, stu.age, stu.score);
    return 0;
}
```
# C语言中内存申请与结构体结合的知识点总结

## 一、结构体变量的内存分配
1. **静态内存分配**
   - 在定义结构体变量时，如果不使用动态内存分配，结构体变量将在栈上分配内存。例如：
```c
struct student {
    char name[20];
    int age;
    float score;
};

struct student stu;
```
   - 这里`stu`是一个`student`结构体类型的变量，它的内存是在栈上静态分配的。栈内存由编译器自动管理，其大小在编译时确定。`stu`的大小等于结构体中所有成员变量大小之和（考虑内存对齐），在这个例子中，`name`数组占20字节，`age`占4字节（假设32位系统），`score`占4字节，总共28字节（考虑内存对齐可能会有一些填充字节）。

2. **动态内存分配**
   - 使用`malloc`函数可以在堆上动态分配结构体所需的内存。
   - 例如：
```c
struct student *pstu;
pstu = (struct student *) malloc(sizeof(struct student));
if (pstu == NULL) {
    // 内存分配失败处理
    perror("malloc");
    return 1;
}
```
   - 这里`pstu`是一个指向`student`结构体的指针。`malloc`函数根据`student`结构体的大小在堆上分配一块内存，并返回指向这块内存的指针。需要注意的是，`malloc`函数返回的是`void *`类型的指针，所以需要进行类型转换为`struct student *`。如果`malloc`返回`NULL`，表示内存分配失败，需要进行相应的错误处理。

## 二、动态分配结构体数组
1. **分配单个结构体数组元素的内存**
   - 可以动态分配结构体数组中的单个元素的内存。
```c
struct student *pstu;
pstu = (struct student *) malloc(sizeof(struct student));
// 对pstu指向的结构体成员进行初始化等操作
```
2. **分配结构体数组的内存**
   - 要动态分配结构体数组的内存，可以使用以下方式：
```c
struct student *arr;
int n = 5;  // 假设要分配5个元素的结构体数组
arr = (struct student *) malloc(n * sizeof(struct student));
if (arr == NULL) {
    // 内存分配失败处理
    perror("malloc");
    return 1;
}
```
   - 这里`arr`是一个指向`student`结构体数组的指针。通过`malloc`函数分配了能够容纳`n`个`student`结构体的内存空间。同样，如果`malloc`返回`NULL`，表示内存分配失败。

   - 访问动态分配的结构体数组元素的成员与普通结构体数组类似，可以使用`arr[i].成员名`（当`arr`被当作数组使用时）或者`(arr + i)->成员名`（当把`arr`当作指针使用时）。

## 三、结构体嵌套与动态内存分配
1. **简单嵌套结构体的动态内存分配**
   - 当结构体中有嵌套的结构体时，动态分配内存需要注意顺序。
   - 例如：
```c
struct date {
    int year;
    int month;
    int day;
};

struct student {
    char name[20];
    struct date birthday;
    float score;
};

struct student *pstu;
pstu = (struct student *) malloc(sizeof(struct student));
if (pstu!= NULL) {
    // 可以进一步对嵌套结构体成员进行操作
    pstu->birthday.year = 2000;
}
```
   - 这里先为外层的`student`结构体分配内存，然后可以直接访问嵌套的`date`结构体成员并进行赋值等操作。

2. **多层嵌套结构体的动态内存分配**
   - 对于多层嵌套的结构体，需要从最内层的结构体开始逐步向外层进行动态内存分配。
   - 假设存在如下多层嵌套结构体：
```c
struct sub {
    int num;
};

struct mid {
    struct sub s;
    char ch;
};

struct outer {
    struct mid m;
    float f;
};

struct outer *pouter;
pouter = (struct outer *) malloc(sizeof(struct outer));
if (pouter!= NULL) {
    // 对于多层嵌套结构体，可能需要单独为内部结构体成员分配内存或进行初始化
    // 例如：pouter->m.s.num = 10;
}
```

## 四、释放动态分配的结构体内存
1. **释放单个结构体的内存**
   - 当使用`malloc`动态分配了一个结构体的内存后，使用`free`函数来释放内存。
   - 例如：
```c
struct student *pstu;
pstu = (struct student *) malloc(sizeof(struct student));
// 使用pstu指向的结构体
free(pstu);
pstu = NULL;
```
   - 在释放内存后，将指针赋值为`NULL`是一个良好的编程习惯，这样可以避免产生野指针。

2. **释放结构体数组的内存**
   - 对于动态分配的结构体数组内存，也使用`free`函数释放。
```c
struct student *arr;
int n = 5;
arr = (struct student *) malloc(n * sizeof(struct student));
// 使用arr指向的结构体数组
free(arr);
arr = NULL;
```

