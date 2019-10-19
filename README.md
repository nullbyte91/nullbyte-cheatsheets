# nullbyte-cheatsheets

### Data structures and algorithms cheat sheet

#### Queue implementation with single linked list:

1. Insert   - Average O(1)  - Worst O(1)  
2. Delete   - Average O(1)  - Worst O(1)
3. Acccess  - Average O(n)  - Worst O(n)
4. Search   - Average O(n)  - Worst O(n)

Structure:
```c
struct elt{
    int data;
    struct elt* next;
};

struct queue{
    struct elt* head; /* dequeue */
    struct elt* tail; /* enqueue */
};
```

Enqueue - Insert:
```c
/* Add value to queue */
void
enQueue(struct queue* q, int data){
    struct elt* e = malloc(sizeof(struct elt));
    e->data = data;
    e->next = NULL;

    if (q->head == NULL){
        q->head = e;
    } else {
        q->tail->next = e;
    }
    q->tail = e;
}
```

Dequeue - Delete:
```c
/* delete the value from head pointer */
int
deQueue(struct queue* q){
    struct elt *e;
    int deQueue_val;

    /* check queue is empty*/
    assert(!isEmpty(q));

    deQueue_val = q->head->data;
    e = q->head;
    q->head = e->next;
    free(e);
    return deQueue_val;   
}
```

Access/search:
```c
/* function to travel queue */
void
traversal(struct queue* q){
    struct elt* e;

    assert(!isEmpty(q));

    for(e=q->head; e!=0; e = e->next){
        printf("Data:%d ", e->data);
    }
}
```

Helper Function's:
```c
/* create a new empty queue */
struct queue*
createQueue(){
    struct queue* q = malloc(sizeof(struct queue));
    q->head = NULL;
    q->tail = NULL;
}

/* check is Queue empty */
int
isEmpty(struct queue* q){
    return (q->head == 0);
}
```
