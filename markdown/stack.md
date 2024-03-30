# 学习日志：栈的实现
## 栈(stack)的实现
元素在栈中保持先进后出，后进先出的原则
```c
typedef struct snode{
    int data;
    struct snode* next;

}
typedef struct Stack{
    struct snode* top;//指向栈顶(在最下方)
    int size;
    int capicity;
}Stack;

Stack *init(int capicity){
    Stack *stack=(Stack*)malloc(sizeof(Stack));
    stack->top=NULL;
    stack->size=0;
    stack->capicity=capicity;
    return stack;
}

bool isempty(Stack *stack){
    return stack->size==0;
}

bool isfull(Stack *stack){
    return stack->size==stack->capicity;
}

void push(Stack *stack,int data){
    if(isfull(stack)){
        printf("栈已满");
        return;
    }
    snode* node=(snode*)malloc(sizeof(snode));
    node->next=stack->top;
    stack->top=node;
    node->data=data;
    stack->size++;
}

void pop(Stack *stack){
    if(isempty(stack)){
        printf("栈已空");
        return;
    }
    snode* node=stack->top;
    stack->top=stack->top->next;
    free(node);
    stack->size--;
}

void printStack(Stack *stack){
    snode* node=stack->top;
    while(node){
        printf("%d ",node->data);
        node=node->next;
    }
    printf("\n");
}
```

## 应用
```
在算法中，栈也有许多应用场景，其中一些包括：

深度优先搜索（DFS）：深度优先搜索通常使用递归或栈来实现。在遍历图或树时，可以使用栈来存储遍历的路径，以便在需要回溯时能够正确地返回上一层。

括号匹配：在算法中，经常需要检查表达式中的括号是否匹配。可以使用栈来存储左括号，在遇到右括号时进行匹配。

逆波兰表达式求解：逆波兰表达式是一种不需要括号的数学表达式表示方法，可以使用栈来求解逆波兰表达式。

表达式求值：在计算表达式的值时，可以使用栈来处理运算符的优先级和括号的匹配，从而实现正确的计算顺序。

迷宫求解：在迷宫求解算法中，可以使用栈来存储路径上的点，以便在需要回溯时能够正确地返回上一步。

汉诺塔问题：汉诺塔问题可以使用栈来实现。将盘子移动的步骤压入栈中，然后按照相应的步骤执行移动操作。

回文字符串判断：判断一个字符串是否是回文字符串（正读和反读都相同）时，可以使用栈来实现。将字符串的一半字符压入栈中，然后依次弹出与剩余部分字符进行比较。

这些是栈在算法中常见的应用场景，栈的后进先出特性使得它在处理递归、回溯和顺序问题时非常有用。----from gpt
```
