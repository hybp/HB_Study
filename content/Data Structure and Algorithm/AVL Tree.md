*Binary Search의 이론적 속도를 보장하기 위한 BST + 회전 Rebalancing Mechanism*


코드 임플멘테이션은 안나올듯

그래도 딱 하나 기억하고 싶다면
```python
def _update_height(self, node):
	if node:
		node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))
```

Rotation은 그냥 주변 노드들 확인해서 connection 바꿔주는거
연결 바꿔주고 update_height 돌려주면 됨


```python
class TreeNode:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None
        self.height = 1

class AVLTree:
    def __init__(self):
        self.root = None

    def _get_height(self, node):
        if not node:
            return 0
        return node.height

    def _get_balance(self, node):
        if not node:
            return 0
        return self._get_height(node.left) - self._get_height(node.right)

    def _update_height(self, node):
        if node:
            node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))

    def _rotate_left(self, z):
        y = z.right
        T2 = y.left

        # Perform rotation
        y.left = z
        z.right = T2

        # Update heights
        self._update_height(z)
        self._update_height(y)

        return y

    def _rotate_right(self, y):
        x = y.left
        T2 = x.right

        # Perform rotation
        x.right = y
        y.left = T2

        # Update heights
        self._update_height(y)
        self._update_height(x)

        return x

    def insert(self, root, key):
        # 1. Perform standard BST insert
        if not root:
            return TreeNode(key)
        elif key < root.key:
            root.left = self.insert(root.left, key)
        else:
            root.right = self.insert(root.right, key)

        # 2. Update height of current node
        self._update_height(root)

        # 3. Get the balance factor
        balance = self._get_balance(root)

        # 4. If the node is unbalanced, then try out the 4 cases
        # Left Left Case
        if balance > 1 and key < root.left.key:
            return self._rotate_right(root)

        # Right Right Case
        if balance < -1 and key > root.right.key:
            return self._rotate_left(root)

        # Left Right Case
        if balance > 1 and key > root.left.key:
            root.left = self._rotate_left(root.left)
            return self._rotate_right(root)

        # Right Left Case
        if balance < -1 and key < root.right.key:
            root.right = self._rotate_right(root.right)
            return self._rotate_left(root)

        return root

    def delete(self, root, key):
        if not root:
            return root

        elif key < root.key:
            root.left = self.delete(root.left, key)

        elif key > root.key:
            root.right = self.delete(root.right, key)

        else:
            if root.left is None:
                temp = root.right
                root = None
                return temp
            elif root.right is None:
                temp = root.left
                root = None
                return temp

            temp = self._get_min_value_node(root.right)
            root.key = temp.key
            root.right = self.delete(root.right, temp.key)

        if root is None:
            return root

        # Update height of current node
        self._update_height(root)

        # Get the balance factor
        balance = self._get_balance(root)

        # Left Left Case
        if balance > 1 and self._get_balance(root.left) >= 0:
            return self._rotate_right(root)

        # Left Right Case
        if balance > 1 and self._get_balance(root.left) < 0:
            root.left = self._rotate_left(root.left)
            return self._rotate_right(root)

        # Right Right Case
        if balance < -1 and self._get_balance(root.right) <= 0:
            return self._rotate_left(root)

        # Right Left Case
        if balance < -1 and self._get_balance(root.right) > 0:
            root.right = self._rotate_right(root.right)
            return self._rotate_left(root)

        return root

    def _get_min_value_node(self, node):
        current = node
        while current.left is not None:
            current = current.left
        return current

    def search(self, root, key):
        if not root:
            return None
        elif key < root.key:
            return self.search(root.left, key)
        elif key > root.key:
            return self.search(root.right, key)
        else:
            return root

    def inorder_traversal(self, root):
        result = []
        if root:
            result.extend(self.inorder_traversal(root.left))
            result.append(root.key)
            result.extend(self.inorder_traversal(root.right))
        return result

# Example Usage
if __name__ == "__main__":
    avl_tree = AVLTree()
    root = None

    keys_to_insert = [10, 20, 30, 40, 50, 25]
    for key in keys_to_insert:
        root = avl_tree.insert(root, key)

    print("Inorder traversal after insertion:", avl_tree.inorder_traversal(root))

    root = avl_tree.delete(root, 30)
    print("Inorder traversal after deleting 30:", avl_tree.inorder_traversal(root))

    search_result = avl_tree.search(root, 25)
    if search_result:
        print(f"Found node with key: {search_result.key}")
    else:
        print("Node not found")

    search_result = avl_tree.search(root, 30)
    if search_result:
        print(f"Found node with key: {search_result.key}")
    else:
        print("Node not found")
```