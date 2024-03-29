# 学习日志：广度优先算法(代码实现)
## 队列和图实现
图的结构体:邻接表实现
```c
typedef struct Enode{
    int data;
    struct Enode* next;
}Enode;

typedef struct Adjlist{
    int index;
    Enode* first;
}Adjlist;

typedef struct Graph{
    Adjlist adjlist[N];
}Graph;

```
图的方法实现
```c
Graph *initGraph(){
    Graph* gp=(Graph*)malloc(sizeof(Graph));
    for(int i=0;i<N;i++){
        gp->adjlist[i].index=i+1;
        gp->adjlist[i].first=NULL;
    }
    return gp;
}

void insertEdge(Graph* gp,int start,int end){
    if(gp==NULL){
        printf("图为空\n");
        
    }
    if(start<1||start>N||end<1||end>N){
        printf("无效的点\n");
    }
    Enode *en=(Enode*)malloc(sizeof(Enode));
    en->next=gp->adjlist[start-1].first;
    en->data=end-1;
    gp->adjlist[start-1].first=en;

    Enode *en1=(Enode*)malloc(sizeof(Enode));
    en1->next=gp->adjlist[end-1].first;
    en1->data=start-1;
    gp->adjlist[end-1].first=en1;
    
}
```


队列的结构体
```c
typedef struct Qnode{
    int data;
    struct Qnode* next;
}Qnode;

typedef struct Queue{
   Qnode* front,*rear; 
}Queue;
```

队列的方法实现
```c
bool isempty(Queue *q){
    return q->front==NULL;
}

Queue *initqueue(){
    Queue* q=(Queue*)malloc(sizeof(Queue));
    q->front=NULL;
    q->rear=NULL;
    return q;
}

void enqueue(Queue *q,int value){
    Qnode *node=(Qnode*)malloc(sizeof(Qnode));
    node->data=value;
    node->next=NULL;
    if(isempty(q)){
        q->front=node;
        q->rear=node;
    }else{
        q->rear->next=node;
        q->rear=node;
    }
}

void dequeue(Queue *q){
	if (isempty(q)) {
        printf("队列为空\n");
    }
    Qnode *node=q->front;
	q->front=q->front->next;
    free(node);
    if (q->front == NULL) {
        q->rear = NULL;
    }
}
```
## bfs算法
### bfs算法原理(待补充)
待完善
### bfs算法的实现
```c
void bfs(Graph* p,int start,int* distance){
	start=start-1;
    int visited[N];//访问过的顶点
    //int distance[N]各节点到初始节点的最短距离
    int path[N];//各节点的前驱节点
    for(int i=0;i<N;i++){
        distance[i]=9999999;
    }
    Queue *q=initqueue();//初始化队列
    enqueue(q,start);//初始结点入队
    visited[start]=1;
    distance[start]=0;
    while(!isempty(q)){//队列不为空
        int now=q->front->data;//队列第一个元素
        Enode *node=p->adjlist[now].first;
        while(node){//让队头结点的所有未曾入队的后继入队
            int index=node->data;
            if(visited[index]!=1){
                distance[index]=distance[now]+1;
                visited[index]=1;
                enqueue(q,index);
            }
            node=node->next;
        }
        dequeue(q);
    }
    
}
```
一个测试用例
![本例的示意图](![Alt text](08dc4f89f1c4b90db6b95ef55abde3a.jpg))
```c
int main() {
	//主函数输入下标从1开始 
    Graph *gp=initGraph();
	insertEdge(gp, 1, 2);
	insertEdge(gp, 2, 3);
	insertEdge(gp, 3, 4);
	insertEdge(gp, 3, 5);
	insertEdge(gp, 5, 6);
	insertEdge(gp, 6, 7);
	insertEdge(gp, 7, 8);
	int res[N];
	bfs(gp,3,res);
	for(int i=0;i<N;i++){
		printf("%d ",res[i]);
	}
    return 0;
}
```


