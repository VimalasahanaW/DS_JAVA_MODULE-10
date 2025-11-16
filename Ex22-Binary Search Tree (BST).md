# Ex22 Searching for a Book ID in a Binary Search Tree (BST)
## DATE: 17-11-25
## AIM:
To design and implement java program that constructs a Binary Search Tree (BST) using given Book IDs and checks whether a specific Book ID exists in the BST.
## Algorithm
1.Read the number of Book IDs and the Book ID values from the user.

2.Insert each Book ID into the BST according to BST rules.

3.Ask the user for the Book ID to search in the BST.

4.Recursively search the BST for the given Book ID.

5.Display whether the Book ID exists or does not exist in the BST. 
  

## Program:
```
/*
Program to constructs a Binary Search Tree (BST) using given Book IDs 
Developed by: VIMALA SAHANA W
RegisterNumber: 212223040241  
*/
import java.util.Scanner;

public class BSTBookID {

    // Node class (helper)
    static class Node {
        int data;
        Node left, right;
        Node(int data) { this.data = data; }
    }

    // Insert Book ID into BST
    public static Node insert(Node root, int data) {
        if (root == null) return new Node(data);
        if (data < root.data) root.left = insert(root.left, data);
        else if (data > root.data) root.right = insert(root.right, data);
        return root; // duplicates ignored
    }

    // Search for Book ID
    public static boolean search(Node root, int key) {
        if (root == null) return false;
        if (root.data == key) return true;
        return key < root.data ? search(root.left, key) : search(root.right, key);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Node root = null;

        System.out.print("Enter number of Book IDs: ");
        int n = sc.nextInt();

        System.out.println("Enter Book IDs:");
        for (int i = 0; i < n; i++) {
            int id = sc.nextInt();
            root = insert(root, id);
        }

        System.out.print("Enter Book ID to search: ");
        int searchID = sc.nextInt();

        if (search(root, searchID)) {
            System.out.println("Book ID " + searchID + " exists in the BST.");
        } else {
            System.out.println("Book ID " + searchID + " does NOT exist in the BST.");
        }

        sc.close();
    }
}

```

## Output:

<img width="481" height="229" alt="image" src="https://github.com/user-attachments/assets/78298910-7a59-415b-a84f-70017f532afe" />


## Result:
The program has been successfully implemented and executed.
It constructs a Binary Search Tree from the given Book IDs and accurately determines whether a queried Book ID exists in the library system.
