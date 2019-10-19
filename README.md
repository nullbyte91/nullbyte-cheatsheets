# nullbyte-cheatsheets

### Data structures and algorithms cheat sheet

#### Queue implementation with single linked list:

1. Insert   - Average O(1)  - Worst O(1)  
2. BFS      - O(V + E)  V stands for vertices and E stands for edges
3. DFS      - O(V + E)  V stands for vertices and E stands for edges

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

#### Binary Search Tree
1. Insert   - Average Θ(log(n))  - Worst O(n)
2. Delete   - Average Θ(log(n))  - Worst O(n)
3. Acccess  - Average Θ(log(n))  - Worst O(n)
4. Search   - Average Θ(log(n))  - Worst O(n)

structure:

```c
struct node{
    int data;
    struct node* left;
    struct node* right;
};
```

GetNewNode:

```c
struct node* 
getNewnode(int data){   
    struct node* newNode = malloc(sizeof(struct node));
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode; 
}
```

Insert:

```c
struct node*
insert(struct node* rootPtr, int data){
    if (rootPtr == NULL){
        rootPtr = getNewnode(data);
    } else if (data <= rootPtr->data){
        rootPtr->left = insert(rootPtr->left, data);
    } else if (data >= rootPtr->data){
        rootPtr->right = insert(rootPtr->right, data);
    }
    return rootPtr;
}

```

DFS:
```c
void 
pre_order(struct node* rootPtr){
    if (rootPtr == NULL){
        return;
    }
    printf("Data:%d ", rootPtr->data);
    pre_order(rootPtr->left);
    pre_order(rootPtr->right);
}

void
in_order(struct node* rootPtr){
    if (rootPtr == NULL){
        return;
    }
    pre_order(rootPtr->left);
    printf("Data:%d ", rootPtr->data);
    pre_order(rootPtr->right);
}

void
post_order(struct node* rootPtr){
    if (rootPtr == NULL){
        return;
    }
    pre_order(rootPtr->left);
    pre_order(rootPtr->right);
    printf("Data:%d ", rootPtr->data);

}
```

BFS:

structure:
```c
struct node{
    int data;
    struct node* left;
    struct node* right;
};

struct elt{
    struct node* bstnode;
    struct elt* next;
};

struct queue{
    struct elt* head;
    struct elt* tail;
};
```

Queue Implementation:
```c
struct queue*
createEmptyQueue(){
    struct queue* q = malloc(sizeof(struct queue));
    q->head = NULL;
    q->tail = NULL;
    return q;
}

void
enQueue(struct queue* q, struct node* rootPtr){
    struct elt* e = malloc(sizeof(struct elt));
    e->bstnode = rootPtr;
    e->next = NULL;
    
    if (q->head == NULL){
        q->head = e;
    } else {
        q->tail->next = e;
    }
    q->tail = e;
}

struct node*
deQueue(struct queue* q){
    struct elt* e;
    struct node* temp;
    /* check queue is empty*/
    if (isEmpty(q) == 1){
        return 0;
    }
    e = q->head;
    temp = e->bstnode;
    q->head = e->next;
    free(e);
    return temp;
}

/* check is Queue empty */
int
isEmpty(struct queue* q){
    return (q->head == 0);
}
```

Level order - BFS:

```c
void 
level_order(struct node* rootPtr){
    // Create a Empty queue
    struct queue* Queue = createEmptyQueue();
    struct node* current = rootPtr;
    //enQueue(Queue, rootPtr);
    while(current){
        printf("Data:%d ", current->data);

        // Enqueue left 
        if (current->left != NULL){
            enQueue(Queue, current->left);
        }
        // Enqueue right 
        if (current->right != NULL){
            enQueue(Queue, current->right);
        }
        current = deQueue(Queue);
    }
}
```