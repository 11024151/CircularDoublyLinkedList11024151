# CircularDoublyLinkedList 11024151
---

## 題目二: Python實作的單向循環鏈錶功能範例
### 一、概述：
单向循环链表是指在单链表的基础上，表的最后一个元素指向链表头结点，不再是为空。
![執行結果](hww001.png)
由图可知，单向循环链表的判断条件不再是表为空了，而变成了是否到表头。

### 二、操作
is_empty() 判断链表是否为空
length() 返回链表的长度
travel() 遍历
add(item) 在头部添加一个节点
append(item) 在尾部添加一个节点
insert(pos, item) 在指定位置pos添加节点
remove(item) 删除一个节点
search(item) 查找节点是否存在

### 三、具体代码
class Node(object):
    """節點"""
    def __init__(self, item):
        self.item = item
        self.next = None


class SinCycLinkedlist(object):
    """單向循環鏈錶"""
    def __init__(self):
        self._head = None

    def is_empty(self):
        """判斷鍊錶是否為空"""
        return self._head is None

    def length(self):
        """返回鍊錶的長度"""
        if self.is_empty():
            return 0
        count = 1
        cur = self._head
        while cur.next != self._head:
            count += 1
            cur = cur.next
        return count

    def travel(self):
        """遍歷鍊錶"""
        if self.is_empty():
            return
        cur = self._head
        print(cur.item, end=' ')
        while cur.next != self._head:
            cur = cur.next
            print(cur.item, end=' ')
        print()

    def add(self, item):
        """頭部新增節點"""
        node = Node(item)
        if self.is_empty():
            self._head = node
            node.next = self._head
        else:
            node.next = self._head
            cur = self._head
            while cur.next != self._head:
                cur = cur.next
            cur.next = node
            self._head = node

    def append(self, item):
        """尾部新增節點"""
        node = Node(item)
        if self.is_empty():
            self._head = node
            node.next = self._head
        else:
            cur = self._head
            while cur.next != self._head:
                cur = cur.next
            cur.next = node
            node.next = self._head

    def insert(self, pos, item):
        """在指定位置新增節點"""
        if pos <= 0:
            self.add(item)
        elif pos > (self.length() - 1):
            self.append(item)
        else:
            node = Node(item)
            cur = self._head
            count = 0
            while count < (pos - 1):
                count += 1
                cur = cur.next
            node.next = cur.next
            cur.next = node

    def remove(self, item):
        """刪除一個節點"""
        if self.is_empty():
            return
        cur = self._head
        pre = None
        if cur.item == item:
            if cur.next != self._head:
                while cur.next != self._head:
                    cur = cur.next
                cur.next = self._head.next
                self._head = self._head.next
            else:
                self._head = None
        else:
            pre = self._head
            cur = self._head.next
            while cur != self._head:
                if cur.item == item:
                    pre.next = cur.next
                    return
                else:
                    pre = cur
                    cur = cur.next
            if cur.item == item:
                pre.next = cur.next

    def search(self, item):
        """查找節點是否存在"""
        if self.is_empty():
            return False
        cur = self._head
        if cur.item == item:
            return True
        while cur.next != self._head:
            cur = cur.next
            if cur.item == item:
                return True
        return False


if __name__ == "__main__":
    ll = SinCycLinkedlist()
    ll.add(1)
    ll.add(2)
    ll.append(3)
    ll.insert(2, 4)
    ll.insert(4, 5)
    ll.insert(0, 6)

    print("length:", ll.length())
    ll.travel()
    print(ll.search(3))
    print(ll.search(7))

    ll.remove(1)
    print("length:", ll.length())
    ll.travel()

### 四、執行結果截圖  
![執行結果](執行結果.png)


---
