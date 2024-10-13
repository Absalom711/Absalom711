import java.util.Scanner;

class Node {
    String name;
    String phoneNumber;
    Node left, right;

    public Node(String name, String phoneNumber) {
        this.name = name;
        this.phoneNumber = phoneNumber;
        left = right = null;
    }
}

public class PhonebookBST {
    Node root;

    public PhonebookBST() {
        root = null;
    }

    // Insert contact
    public void insert(String name, String phoneNumber) {
        root = insertRec(root, name, phoneNumber);
    }

    private Node insertRec(Node root, String name, String phoneNumber) {
        if (root == null) {
            root = new Node(name, phoneNumber);
            return root;
        }
        if (name.compareTo(root.name) < 0) {
            root.left = insertRec(root.left, name, phoneNumber);
        } else if (name.compareTo(root.name) > 0) {
            root.right = insertRec(root.right, name, phoneNumber);
        }
        return root;
    }

    // Search contact
    public String search(String name) {
        return searchRec(root, name);
    }

    private String searchRec(Node root, String name) {
        if (root == null) {
            return "Contact not found.";
        }
        if (name.equals(root.name)) {
            return "Name: " + root.name + ", Phone: " + root.phoneNumber;
        }
        if (name.compareTo(root.name) < 0) {
            return searchRec(root.left, name);
        }
        return searchRec(root.right, name);
    }

    // Display all contacts
    public void display() {
        displayRec(root);
    }

    private void displayRec(Node root) {
        if (root != null) {
            displayRec(root.left);
            System.out.println("Name: " + root.name + ", Phone: " + root.phoneNumber);
            displayRec(root.right);
        }
    }

    // Delete contact
    public void delete(String name) {
        root = deleteRec(root, name);
    }

    private Node deleteRec(Node root, String name) {
        if (root == null) {
            return root;
        }
        if (name.compareTo(root.name) < 0) {
            root.left = deleteRec(root.left, name);
        } else if (name.compareTo(root.name) > 0) {
            root.right = deleteRec(root.right, name);
        } else {
            // Node with one child or no child
            if (root.left == null) return root.right;
            else if (root.right == null) return root.left;

            // Node with two children: Get the inorder successor
            root.name = minValue(root.right);
            root.phoneNumber = search(root.name).split(", ")[1].split(": ")[1]; // Update phone number
            root.right = deleteRec(root.right, root.name);
        }
        return root;
    }

    private String minValue(Node root) {
        String minValue = root.name;
        while (root.left != null) {
            minValue = root.left.name;
            root = root.left;
        }
        return minValue;
    }

    public static void main(String[] args) {
        PhonebookBST phonebook = new PhonebookBST();
        Scanner scanner = new Scanner(System.in);
        int choice;

        do {
            System.out.println("\nPhonebook Menu:");
            System.out.println("1. Add Contact");
            System.out.println("2. Search Contact");
            System.out.println("3. Display All Contacts");
            System.out.println("4. Delete Contact");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
            choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.print("Enter name: ");
                    String name = scanner.nextLine();
                    System.out.print("Enter phone number: ");
                    String phoneNumber = scanner.nextLine();
                    phonebook.insert(name, phoneNumber);
                    break;
                case 2:
                    System.out.print("Enter name to search: ");
                    name = scanner.nextLine();
                    System.out.println(phonebook.search(name));
                    break;
                case 3:
                    System.out.println("All Contacts:");
                    phonebook.display();
                



<!---
Absalom711/Absalom711 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
