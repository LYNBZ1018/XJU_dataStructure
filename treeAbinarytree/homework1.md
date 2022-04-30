## 1. 编写二叉树的中序遍历递归算法。

```c++
struct BiTreeNode {
    int data;
    BiTreeNode* left;
    BiTreeNode* right;
};

void inOrder(BiTreeNode* root)
{
    if (root)
    {
        inOrder(root->left);
        printf("%d", root->data);
        inOrder(root->right);
    }
}
```

​     

## 2.  统计二叉树中叶子结点个数。

```c++
struct BiTreeNode {
    int data;
    BiTreeNode* left;
    BiTreeNode* right;
};

int cntLeafNode(BiTreeNode* root)
{
    if (root == NULL) return 0;
    else if (root->left == NULL && root->right == NULL) return 1;
    else return cntLeafNode(root->left) + cntLeafNode(root->right);
}
```

​    

## 3. 求二叉树的高度。

```c++
struct BiTreeNode {
    int data;
    BiTreeNode* left;
    BiTreeNode* right;
};

int getBiTreeHeight(BiTreeNode* root)
{
    if (root == NULL) return 0;
    else
    {
		int a = getBiTreeHeight(root->left);
        int b = getBiTreeHeight(root->right);
        if (a > b) return a + 1;
        else return b + 1;
    }
}
```

