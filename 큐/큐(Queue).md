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
//1번 문제

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX_QUEUE_SIZE 4

typedef char Element;
typedef struct {
	Element queue[MAX_QUEUE_SIZE];
	int front, rear;
} QueueType;


// 공백 순차 큐를 생성하는 연산
QueueType* createQueue() {
	QueueType* Q;
	Q = (QueueType*)malloc(sizeof(QueueType));
	Q->front = -1;
	Q->rear = -1;
	return Q;
}

// 순차 큐가 공백 상태인지 검사하는 연산
int isEmpty(QueueType* Q) {
	if (Q->front == Q->rear) {
		printf("Queue is empty!");
	}
	else return 0;
}
// 순차 큐가 가득 찼을때
bool isFull(QueueType* Q) {
	int tmp = Q->rear;
	if (tmp == MAX_QUEUE_SIZE-1) {
		printf("Queue is Full!");
		return true;
	}
	else return false;
}

// 순차 큐의 rear에 원소를 삽입하는 연산
void enQueue(QueueType* Q, Element item) {
	if (isFull(Q)) {

	}
	else {
		Q->rear = Q->rear + 1;
		Q->queue[Q->rear] = item;
	}


}

Element deQueue(QueueType* Q) {
	if (isEmpty(Q)) return 0;
	else {
		Q->front++;
		return Q->queue[Q->front];
	}
}

// 순차 큐의 가장 앞에 있는 원소를 검색하는 연산
Element peek(QueueType* Q) {
	if (isEmpty(Q)) exit(1);
	else return Q->queue[Q->rear];
}



// 순차 큐의 원소를 출력하는 연사
void printfQ(QueueType* Q) {
	int i;
	printf(" Queue : [");
	for (i = Q->front + 1; i <= Q->rear; i++) {
		printf(" %3c", Q->queue[i]);
	}
	printf(" ]");
}

int main(int argc, char* argv[]) {
	char arr[3] = { 'A', 'B', 'C' };
	int i;
	QueueType* Q = createQueue();
;	for (i = 0; i < sizeof(arr); i++) {
		printf("삽입 %c >> ", arr[i]);
		enQueue(Q, arr[i]);
		printfQ(Q);
		printf(" \n Q->front / Q->rear : %d / %d \n", Q->front, Q->rear);
		printf("\n");
	}
	printf("peek item: %c \n", peek(Q));

	for (i = 0; i < sizeof(arr); i++) {
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

~~~c
//2번문제
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX_QUEUE_SIZE 10

typedef int Element;
typedef struct {
	Element queue[MAX_QUEUE_SIZE];
	int front, rear;
} QueueType;


// 공백 순차 큐를 생성하는 연산
QueueType* createQueue() {
	QueueType* Q;
	Q = (QueueType*)malloc(sizeof(QueueType));
	Q->front = 0;
	Q->rear = 0;
	return Q;
}

// 순차 큐가 공백 상태인지 검사하는 연산
int isEmpty(QueueType* Q) {
	if (Q->front == Q->rear) {
		printf("Queue is empty!");
	}
	else return 0;
}
// 순차 큐가 가득 찼을때
bool isFull(QueueType* Q) {
	if ((Q->rear + 1) % MAX_QUEUE_SIZE == Q->front) {
		printf("Queue is Full!");
		return true;
	}
	else return false;
}

// 순차 큐의 rear에 원소를 삽입하는 연산
void enQueue(QueueType* Q, Element item) {
	if (isFull(Q)) {

	}
	else {
		Q->queue[Q->rear] = item;
		Q->rear = (Q->rear + 1) % MAX_QUEUE_SIZE;
	}


}

Element deQueue(QueueType* Q) {
	if (isEmpty(Q)) return 0;
	else {
		Q->front = (Q->front+1)%MAX_QUEUE_SIZE;
		return Q->queue[Q->front];
	}
}

// 순차 큐의 가장 앞에 있는 원소를 검색하는 연산
Element peek(QueueType* Q) {
	if (isEmpty(Q)) exit(1);
	else return Q->queue[(Q->rear)%MAX_QUEUE_SIZE];
}



// 순차 큐의 원소를 출력하는 연사
void printfQ(QueueType* Q) {
	int i;
	printf(" Queue : [");
	for (i = (Q->front)%MAX_QUEUE_SIZE; i < (Q->rear)%MAX_QUEUE_SIZE; i++) {
		printf(" %3d", Q->queue[i]);
	}
	printf(" ]");
}

int main(int argc, char* argv[]) {
	int i;
	QueueType* Q = createQueue();
;	for (i = 1; i < MAX_QUEUE_SIZE; i++) {
		printf("삽입 %d >> ", i);
		enQueue(Q, i);
		printfQ(Q);
		printf(" \n Q->front / Q->rear : %d / %d \n", Q->front, Q->rear);
		printf("\n");
	}
	printf("peek item: %d \n", peek(Q));

	for (i = 1; i < MAX_QUEUE_SIZE-5; i++) {
		printf("삭제 >> ");
		deQueue(Q);
		printfQ(Q);
		printf(" \n Q->front / Q->rear : %d / %d \n", Q->front, Q->rear);
		printf("\n");
	}
	printfQ(Q);
	return 0;
}
~~~

~~~c
//3번 문제
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX_QUEUE_SIZE 10

typedef struct BanckCustomer {
	int id;
	int tArrival;
	int tService;
} Customer;
typedef Customer Element;

int front, rear = -1;

int nSimulation;
double probArrival;
int tMaxService;
int totalWaitTime;
int nCustomers =0;
int nServedCustomers;

double rand0to1() { return rand() / (double)RAND_MAX; }
Element Bank[MAX_QUEUE_SIZE];

// 순차 큐가 공백 상태인지 검사하는 연산
int isEmpty() {
	if (front == rear) {
		return 1;
	}
	else return 0;
}
// 순차 큐가 가득 찼을때
bool isFull() {
	if ((rear + 1) == MAX_QUEUE_SIZE) {
		printf("Queue is Full!");
		return true;
	}
	else return false;
}

// 순차 큐의 rear에 원소를 삽입하는 연산
void enqueue( Element item) {
	if (isFull()) {
		printf("Queue is Full");
	}
	else {
		rear = rear + 1;
		Bank[rear] = item;
	}


}

Element deQueue() {
	if (isEmpty()) return Bank[0];
	else {
		front = front + 1;
		return Bank[front];
	}
}

// 순차 큐의 가장 앞에 있는 원소를 검색하는 연산
Element peek() {
	if (isEmpty()) exit(1);
	else return Bank[rear%MAX_QUEUE_SIZE];
}

//여기서부터 은행 시뮬레이션 테스트 프로그램코드
void insert_customer(int arrivalTime) {
	Customer a;
	nCustomers = nCustomers + 1;
	a.id = nCustomers;
	a.tArrival = arrivalTime;
	a.tService = (int)(tMaxService * rand0to1()) + 1;
	printf(" 고 객 %d 방 문 ( 서 비 스 시 간 :%d 분 )\n", a.id,a.tService);
	enqueue(a);
}
void read_sim_params() {
	printf("시뮬레이션 할 최대 시간 (예:10) = ");
	scanf_s("%d", &nSimulation);
	printf("단위시간에 도착하는 고객 수 (예:0.5) = ");
	scanf_s("%lf", &probArrival);
	printf("한 고객에 대한 최대 서비스 시간 (예:5) = ");
	scanf_s("%d", &tMaxService);
	printf("==================================================== \n");
}
void init_queue() {
	front = 0;
	rear = 0;
}
void run_simulation() {
	Customer a;
	int clock = 0;
	int serviceTime = -1;
	init_queue();
	nCustomers = totalWaitTime = nServedCustomers = 0;
	while (clock < nSimulation) {
		clock++;
		printf("현재시각=%d\n", clock);
		if (rand0to1() > probArrival)
			insert_customer(clock);
		if (serviceTime > 0) serviceTime--;
		else {
			if (isEmpty()) continue;
			a = deQueue();
			nServedCustomers++;
			totalWaitTime += clock - a.tArrival;
			printf(" 고객 %d 서비스 시작 (대기시간:%d분)\n",a.id, clock - a.tArrival);
			serviceTime = a.tService - 1;
		}
	}
}

void print_result() {
	printf("=================================================\n");
	printf(" 서비스 받은 고객수 = %d\n", nServedCustomers);
	printf(" 전체 대기 시간 = %d분\n", totalWaitTime);
	printf(" 서비스고객 평균대기시간 = %-5.2f분\n",
		(double)totalWaitTime / nServedCustomers);
	printf(" 현 재 대 기 고 객 수 = %d\n", nCustomers -
		nServedCustomers);
}



int main(int argc, char* argv[]) {
	srand((unsigned int)time(NULL));
	read_sim_params();
	run_simulation();
	print_result();
	return 0;
}

~~~



~~~c
//4번 문제
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#define MAX_QUEUE_SIZE 10
//타입은 int형이다
typedef int Element;
//초기값은 0;
int rear, front = 0;
//원형큐 크기는 10이다.
Element data[MAX_QUEUE_SIZE];

//큐초기화 함수
void init_queue() {
	rear = 0;
	front = 0;
}

//데큐초기화
void init_deque() {
	rear = 0;
	front = 0;
}

//
void enqueue(Element val) {
	if (rear < 0) {
		rear = (rear + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	rear = rear % MAX_QUEUE_SIZE;
	data[rear++] = val;
}

Element dequeue() {
	if (front < 0) {
		front = (front + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	if (rear < front) {
		return data[front++];
	}
	else {
		return data[front--];
	}

}

Element peek() {
	if (front < 0) {
		front = (front + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	return data[front];
}
void add_rear(Element val)
{
	enqueue(val);
}

void add_front(Element val) {
	front -= 1;
	if (front < 0) {
		front = (front + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	data[front] = val;
}

Element delete_front() {
	return dequeue();
}

Element delete_rear() {
	if (rear < 0) {
		rear = (rear + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	return data[--rear];
}

Element get_front() {
	return peek();
}

void print_queue(char msg[]) {
	printf("%s  \n", msg);
	int tmp = front;
	if (tmp < 0) {
		tmp = (tmp + MAX_QUEUE_SIZE) % MAX_QUEUE_SIZE;
	}
	while (tmp != rear) {
		printf("tmp : %d .... %3d\n", tmp, data[tmp]);
		tmp = (tmp + 1) % MAX_QUEUE_SIZE;
	}
	printf("\n");
}

int main(int argc, char* argv[]) {
	int i;
	init_deque();
	for (i = 1; i < 10; i++) {
		if (i % 2 == 0) {
			add_front(i);
			printf("front : %d   rear : %d\n", front, rear);
		}
		else {
			add_rear(i);
			printf("front : %d   rear : %d\n", front, rear);
		}
	}
	print_queue("원형 덱 홀수 - 짝수");
	printf("front : %d   rear : %d\n", front, rear);
	printf("\t delete_front() --> %d\n", delete_front());
	printf("front : %d   rear : %d\n", front, rear);
	printf("\t delete_rear --> %d\n", delete_rear());
	printf("front : %d   rear : %d\n", front, rear);
	printf("\t delete_front() --> %d\n", delete_front());
	printf("front : %d   rear : %d\n", front, rear);
	print_queue("원형 덱 삭제-홀짝홀");
	return 0;
}


~~~
