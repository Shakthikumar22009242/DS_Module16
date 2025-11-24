# Ex16 Check for Balanced Parentheses Using Stack
## DATE: 01-11-25
## AIM:
To write a Java program that verifies whether the parentheses (brackets) in an input string are balanced — meaning each opening bracket (, {, [ has a corresponding and correctly ordered closing bracket ), }, ].

## Algorithm
Start the program.

Create an empty stack.

Traverse each character in the string.

Push opening brackets onto the stack.

When a closing bracket is encountered, check if it matches the top of the stack.

If any mismatch or leftover element exists, the parentheses are not balanced.

If the stack is empty at the end, the parentheses are balanced. 

## Program:
```
/*
Program to verify whether the parentheses (brackets) in an input string are balanced
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/

import java.util.Scanner;

public class ParenChecker {
    static class ArrayStack
    {
        private char[] data;
        private int top;
        public ArrayStack(int capacity)
        {
            data=new char[capacity];
            top=-1;
        }
        public boolean isEmpty()
        {
            return top==-1;
        }
        
        public boolean isFull()
        {
            return top==data.length-1;
        }
        public void push(char c)
        {
            if(isFull())
            {
                System.out.println("Stack overflow");
            }
            data[++top]=c;
        }
        public char pop()
        {
            if(isEmpty())
            {
                System.out.println("Stack underflow");
            }
            return data[top--];
            
            
        }
        public char peek()
        {
            if(isEmpty())
            {
                System.out.println("Stack underflow");
            }
            return data[top];
        }
    }


    public static boolean isBalanced(String expr) {
        ArrayStack st = new ArrayStack(expr.length());
        for (char ch : expr.toCharArray()) {
            if (ch == '(' || ch == '{' || ch == '[') {
                st.push(ch);
            } else if (ch == ')' || ch == '}' || ch == ']') {
                if (st.isEmpty()) return false;
                char top = st.pop();
                if ((ch == ')' && top != '(') ||
                    (ch == '}' && top != '{') ||
                    (ch == ']' && top != '[')) {
                    return false;
                }
            }
        }
        return st.isEmpty();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String expr = sc.nextLine();
        boolean ok = isBalanced(expr);
        System.out.println(ok);
        sc.close();
    }
}
```

## Output:

<img width="443" height="361" alt="514896471-d8a974a9-2caa-46b2-8f1c-5854a59bf1b2" src="https://github.com/user-attachments/assets/4dade23e-43ad-43d3-9e3c-24e48cb049b6" />


## Result:
Thus,the program correctly checks whether an input string has balanced parentheses using a stack.
