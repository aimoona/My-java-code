# My-java-code

class BST<T extends Comparable<T>> {
    private class Node {
        T data;
        Node left, right;

        Node(T data) {
            this.data = data;
            left = right = null;
        }
    }

    private Node root;

    public void add(T data) {
        root = insert(root, data);
    }

    private Node insert(Node node, T data) {
       if(node==null) return new Node(data);

       int cmp=data.compareTo(node.data);
       if(cmp<0) node.left=insert(node.left,data);
       if(cmp>0) node.right=insert(node.right,data);

       return node;
    }

    public boolean contains(T data) {
        return search(root, data);
    }

    private boolean search(Node node, T data) {
       if(node==null) return false;

       int cmp=data.compareTo(node.data);
       if(cmp==0) return true;
       return cmp<0 ? search(node.left,data) : search(node.right,data);
    }

    public void delete(T data) {
        root = delete(root, data);
    }

    private Node delete(Node node, T data) {
        if(node==null) return null;

        int cmp=data.compareTo(node.data);
        if(cmp<0){
            node.left=delete(node.left,data);
        } else if(cmp>0){
            node.right=delete(node.right,data);
        } else{
            if(node.left==null) return node.right;
            if(node.right==null) return node.left;

            Node min=findMin(node.right);
            node.data=min.data;
            node.right=delete(node.right,data);
        }
        return node;
    }

    private Node findMin(Node node) {
      while(node.left!=null) node=node.left;
      return node;
    }

    public void inorder() {
        inorder(root);
        System.out.println();
    }

    private void inorder(Node node) {
        if (node == null) return;
        inorder(node.left);
        System.out.print(node.data + " ");
        inorder(node.right);
    }

    public void preorder() {
        preorder(root);
        System.out.println();
    }

    public void preorder(Node node) {
        if (node == null) return;
        System.out.println(node.data);
        preorder(node.left);
        preorder(node.right);
    }

    public void postorder() {
        postorder(root);
        System.out.println();
    }

    public void postorder(Node node) {
        if (node == null) return;
        postorder(node.left);
        postorder(node.right);
        System.out.println(node.data);
    }
}

public class Main {
    public static void main(String[] args) {
        BST<Integer> tree = new BST<>();

        int[] values = {5, 3, 1, 10, 7, 12, 5};

        for (int v : values) tree.add(v);
        System.out.println("Tree before deletion (inorder):");
        tree.inorder();
        System.out.println("Preorder:");
        tree.preorder();
        System.out.println("Postorder:");
        tree.postorder();
        tree.delete(12);
        System.out.println("\nTree after deletion (inorder):");
        tree.inorder();
        System.out.println("Preorder:");
        tree.preorder();
        System.out.println("Postorder:");
        tree.postorder();
        System.out.println("\nContains 12: " + tree.contains(12));
    }
}
