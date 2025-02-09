# queue-in-c

#include <stdio.h>
#include <stdlib.h>

// Estrutura do nó da fila
typedef struct Node {
    int data;
    struct Node* next;
} Node;

// Estrutura da fila
typedef struct Queue {
    Node* front;
    Node* rear;
} Queue;

// Função para criar uma fila vazia
Queue* createQueue() {
    Queue* queue = (Queue*)malloc(sizeof(Queue));
    queue->front = queue->rear = NULL;
    return queue;
}

// Função para inserir um elemento na fila
void enqueue(Queue* queue, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->data = value;
    newNode->next = NULL;
    
    if (queue->rear == NULL) { // Se a fila estiver vazia
        queue->front = queue->rear = newNode;
        return;
    }
    
    queue->rear->next = newNode;
    queue->rear = newNode;
}

// Função para remover um elemento da fila
int dequeue(Queue* queue) {
    if (queue->front == NULL) { // Se a fila estiver vazia
        printf("Fila vazia!\n");
        return -1;
    }
    
    Node* temp = queue->front;
    int value = temp->data;
    queue->front = queue->front->next;
    
    if (queue->front == NULL) // Se a fila ficou vazia após remoção
        queue->rear = NULL;
    
    free(temp);
    return value;
}

// Função para retornar o elemento da frente da fila sem removê-lo
int peek(Queue* queue) {
    if (queue->front == NULL) {
        printf("Fila vazia!\n");
        return -1;
    }
    return queue->front->data;
}

// Função para verificar se a fila está vazia
int isEmpty(Queue* queue) {
    return queue->front == NULL;
}

// Função para imprimir os elementos da fila
void printQueue(Queue* queue) {
    Node* temp = queue->front;
    while (temp) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

// Função principal para testar a fila
int main() {
    Queue* queue = createQueue();
    
    enqueue(queue, 10);
    enqueue(queue, 20);
    enqueue(queue, 30);
    
    printf("Fila atual: ");
    printQueue(queue);
    
    printf("Elemento removido: %d\n", dequeue(queue));
    printf("Fila após remoção: ");
    printQueue(queue);
    
    printf("Elemento da frente: %d\n", peek(queue));
    
    return 0;
}
