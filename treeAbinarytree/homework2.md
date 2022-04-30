## 1

假设一棵二叉树的前序序列是：EBADCFHGIKJ，中序序列是：ABCDEFGHIJK，（1）画出此二叉树，（2）写出后序序列，（3）画出中序线索树。

![3.jpg](https://cdn.acwing.com/media/article/image/2022/04/30/186034_f9749b2bc8-3.jpg) 

## 2

假设用于通信的电文仅为a,b,c,d,e,f,g,h等8个字母组成，字母在电文中出现的频率分别为0.07, 0.19, 0.02, 0.06, 0.32, 0,03, 0.21, 0.1。试为这8个字母设计哈夫曼树及哈夫曼编码，并计算带权路径长度WPL。

![4.jpg](https://cdn.acwing.com/media/article/image/2022/04/30/186034_07af542fc8-4.jpg) 

## 3

编写算法：设二叉树的数据域是正整数，求二叉树中结点数据域的最大值。int FindMax(BiTree BT)

```c++
int treemax = -1;  // 设置一个全局变量

struct BiTreeNode {
    int data;
    BiTreeNode* left;
    BiTreeNode* right;
};

int FindMax(BiTreeNode* root)
{
    if (root == NULL)
        return 0;
    if (root != NULL)
    {
        if (root->data > treemax) treemax = root->data;
        FindMax(root->left);
        FingMax(root->right);
    }
    
    return treemax;
}
```



## 4

画出下列森林转换成的二叉树。并写出森林的先序遍历和中序遍历序列。

![2.png](https://cdn.acwing.com/media/article/image/2022/04/30/186034_88b31a60c8-2.png) 

![5.jpg](https://cdn.acwing.com/media/article/image/2022/04/30/186034_2fdc1e55c8-5.jpg) 