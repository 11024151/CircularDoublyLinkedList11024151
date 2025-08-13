# CircularDoublyLinkedList 11024151
---

## 題目二: Python實作的單向循環鏈表功能範例
### 一、概述：
單向循環鏈表是指在單鏈表的基礎上，表的最後一個元素指向鏈表頭結點，不再是為空。
![執行結果](hww001.png)

由圖可知，單向循環鏈表的判斷條件不再是表為空了，而變成了是否到表頭。

### 二、操作
is_empty() 判斷鏈表是否為空

length() 傳回鏈表的長度

Travel() 遊覽

add(item) 在頭部新增一個節點

append(item) 在尾部增加一個節點

insert(pos, item) 在指定位置 pos 新增節點

remove(item) 刪除一個節點

search(item) 查找節點是否存在

### 三、具體代碼
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

### 主程式執行區塊

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
