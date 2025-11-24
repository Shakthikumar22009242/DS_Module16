# Ex18 Simulation of a Ticket Counter Using Queue (Linked List Implementation)
## DATE: 01-11-25
## AIM:
To simulate the functioning of a ticket counter that operates on a First-In-First-Out (FIFO) basis using a queue implemented via a linked list in Java.
## Algorithm
1. Start the program.
2. Create a Queue using the LinkedList class.
3. Enqueue (add) customers to the queue as they arrive.
4. Display the current queue of customers.
5. Dequeue (remove) customers from the queue one by one as they are served.
6. Display which customer is being served and the remaining queue.
7. Repeat until all customers are served.
  

## Program:
```
/*
Program to functioning of a ticket counter that operates on a First-In-First-Out (FIFO)
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

class Node {
    String data;
    Node next;
    Node(String data) {
        this.data = data;
        this.next = null;
    }
}

class Queue {
    Node front, rear;
    
    void enqueue(String data) {
        Node newNode = new Node(data);
        if (rear == null) {
            front = rear = newNode;
            return;
        }
        rear.next = newNode;
        rear = newNode;
    }

    void dequeue() {
        if (front == null) {
            System.out.println("Queue is empty.");
            return;
        }
        System.out.println(front.data + " has been served.");
        front = front.next;
        if (front == null)
            rear = null;
    }

    void display() {
        if (front == null) {
            System.out.println("Queue is empty.");
            return;
        }
        Node temp = front;
        System.out.print("Current Queue: ");
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }
}

public class TicketCounter {
    public static void main(String[] args) {
        Queue q = new Queue();
        q.enqueue("Alice");
        q.enqueue("Bob");
        q.enqueue("Charlie");
        q.enqueue("Diana");
        q.display();
        q.dequeue();
        q.display();
    }
}
```

## Output:

<img width="1245" height="842" alt="514899480-1e3f40a6-7f61-4ba7-85b7-34445df03ea7" src="https://github.com/user-attachments/assets/eba17626-ced4-48cc-9ccf-cdac40f4047d" />


## Result:
Thus, the program successfully simulates a ticket counter queue where customers are served in FIFO order using a linked list-based queue implementation.
