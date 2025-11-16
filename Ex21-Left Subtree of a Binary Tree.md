# Ex21 Count the Number of Nodes in the Left Subtree of a Binary Tree
## DATE: 17-11-25
## AIM:
To design and implement a java program that constructs a binary tree from given level order input and counts the number of nodes present in the left subtree of the root node.

## Algorithm
1.Read level-order input from the user and store it in an array (use -1 to represent NULL).

2.Create the root node using the first value of the array.

3.Use a queue to iteratively construct left and right children while reading the array.

4.After building the tree, traverse the left subtree (using DFS or BFS) and count the number of nodes.

5.Display the count of nodes present in the left subtree of the root. 


## Program:
```
/*
Program to constructs a binary tree from given level order input and counts the number of nodes 
Developed by: VIMALA SAHANA W
RegisterNumber: 212223040241  
*/
import java.util.*;

public class BinaryTreeLeftCount {

    // Node class
    static class Node {
        int data;
        Node left, right;
        Node(int data) { this.data = data; }
    }

    // Build tree from level-order array
    public static Node buildTree(int[] arr) {
        if (arr.length == 0 || arr[0] == -1) return null;

        Node root = new Node(arr[0]);
        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        int i = 1;
        while (!queue.isEmpty() && i < arr.length) {
            Node current = queue.poll();

            if (i < arr.length && arr[i] != -1) {
                current.left = new Node(arr[i]);
                queue.add(current.left);
            }
            i++;

            if (i < arr.length && arr[i] != -1) {
                current.right = new Node(arr[i]);
                queue.add(current.right);
            }
            i++;
        }

        return root;
    }

    // Count nodes in a subtree
    public static int countNodes(Node root) {
        if (root == null) return 0;
        return 1 + countNodes(root.left) + countNodes(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.println("Enter level order values (-1 for null):");
        String[] input = sc.nextLine().split(" ");

        int[] arr = new int[input.length];
        for (int i = 0; i < input.length; i++) {
            arr[i] = Integer.parseInt(input[i]);
        }

        Node root = buildTree(arr);

        if (root == null) {
            System.out.println("Tree is empty!");
        } else {
            int countLeft = countNodes(root.left);
            System.out.println("Number of nodes in left subtree: " + countLeft);
        }

        sc.close();
    }
}

```

## Output:

<img width="518" height="213" alt="image" src="https://github.com/user-attachments/assets/4dcefa2b-d388-4c64-b120-e30eeee0b09e" />


## Result:
The program has been successfully implemented and executed.
It correctly constructs the binary tree from level order input and counts the number of nodes in the left subtree of the root node.
