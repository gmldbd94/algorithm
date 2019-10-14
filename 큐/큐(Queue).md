# 큐(Queue)

- 큐 : 먼저 들어온 데이터가 먼저 나가는 자료 구조
- 선입선출(FIFO: First-In First-Out)
  - 삽입한 순서대로 원소가 나열되어 가장 먼저 삽입한 원소는 맨 앞에 있다가 가장 먼저 삭제됨

## 큐 연산

- init() : 큐를 초기화 한다.
- enqueue(e) : 주어진 요소 e를 큐의 맨 뒤에 추가한다.
- dequeque() : 큐가 비어있지 않으면 맨 앞 요소를 삭제하고 반환한다.
- is_empty() : 큐가 비어있지않으면 true 아니면 false를 반환한다.
- peek() : 큐가 비어있지 않으면 맨 앞 요소를 삭제하지 않고 반환한다.
- is_full() : 큐가 가득 차 있으면 true을 아니면 false 반환한다.
- size() : 큐의 모든 요소들의 개수를 반환한다.



~~~c
#include <stdio.h>
#include <stdlib.h>
#define MAX_QUEUE_SIZE 4
/* run this program using the console pauser or add your own getch, system("pause") or input loop */

typedef char Element;
typedef struct{
	Element queue[MAX_QUEUE_SIZE];
	int front, rear;
} QueueType;


// 공백 순차 큐를 생성하는 연산 
QueueType *createQueue(){
	QueueType *Q;
	Q = (QueueType *)malloc(sizeof(QueueType));
	Q->front = -1;
	Q->rear = -1;
	return Q;
}

// 순차 큐가 공백 상태인지 검사하는 연산 
int isEmpty(QueueType *Q){
	if(Q->front == Q->rear){
		printf("Queue is empty!");
	}
	else return 0;
}

// 순차 큐의 rear에 원소를 삽입하는 연산 
void enQueue(QueueType *Q, Element item){
	if(isFull(Q)) return;
	else{
		Q->rear++;
		Q->queue[Q->rear] = item;
	}
}

Element deQueue(QueueType *Q){
	if(isEmpty(Q)) return 0;
	else{
		Q->front++;
		return Q->queue[Q->front];
	}
}

// 순차 큐의 가장 앞에 있는 원소를 검색하는 연산
Element peek(QueueType *Q){
	if(isEmpty(Q)) exit(1);
	else return Q->queue[Q->rear +1];
} 

void isFull(){
	
}

// 순차 큐의 원소를 출력하는 연사
void printfQ(QueueType *Q){
	int i;
	printf(" Queue : [");
	for(i = Q->front + 1; i<= Q->rear; i++){
		printf("%3c", Q->queue[i]);
	}
	printf(" ]");
} 

int main(int argc, char *argv[]) {
	char arr[3] = {'A', 'B', 'C'};
	int i ;
	QueueType *Q = createQueue();
	for(i=0; i<sizeof(arr); i++){
		printf("삽입 %c >> ", arr[i]);
		enQueue(Q, arr[i]);
		printfQ(Q);
		printf("\n");
	}
	printf("peek item: %c", peek(Q));
	
	for(i=0; i<sizeof(arr); i++){
		printf("삭제 >> ");
		deQueue(Q);
		printfQ(Q);
		printf("\n");
	}
	enQueue(Q, 'D');
	enQueue(Q, 'E');
	printfQ(Q);
	return 0;
}
~~~

