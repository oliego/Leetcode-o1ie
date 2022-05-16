## No.141 Linked List Cycle
1. 第一想法：双指针，一个指针每次移动一个node，另一个每次移动两个node，如果有环，两个node一定会遇上
```GO
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }
    var n1, n2 *ListNode = head, head
    for n1.Next != nil && n2.Next != nil && n2.Next.Next != nil {
        n1 = n1.Next
        n2 = n2.Next.Next
        if n2 == n1 {
            return true
        }
    }
    return false
}
```
2. solution: 思路一样，但for的判断语句可以改进
    + 因为是n1，n2，n2.Next要获取Next，所以只要确保这三个!=nil即可
```GO
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }
    var n1, n2 *ListNode = head, head
    for n1 != nil && n2 != nil && n2.Next != nil { // 只要保证n1,n2, n2.next != nil即可
        n1 = n1.Next
        n2 = n2.Next.Next
        if n2 == n1 {
            return true
        }
    }
    return false
}
```