![image](https://user-images.githubusercontent.com/54390204/232182083-911c46c1-84d8-45ba-ac6b-bc672f5f3a15.png)
```go
func reverseKGroup( head *ListNode ,  k int ) *ListNode {
    // write code here
    dummyNode := &ListNode{}
    pre := dummyNode
    pre.Next = head

    for pre != nil {
        start := pre.Next
        end := start
        for i := 0; i < k-1; i++ {
            if end == nil {
                break
            }
            end = end.Next
        }
        if end != nil {
            // nex := end.Next
            end, start = reverse(start, end)
            pre.Next = end

            pre = start

        } 
        // else {
        //     break
        // }
    }
    return dummyNode.Next
}

func reverse(start, end *ListNode) (*ListNode, *ListNode) {
    prev := end.Next
    p := start
    for prev != end {
        next := p.Next
        p.Next = prev
        prev = p
        p = next
    }
    return end, start
}
```

思路：

1. 使用虚拟头节点
2. 记录pre，以便指向反转后的下一部分
3. 先循环k次，找到start和end的段，然后再去调用reverse函数去反转
4. 在reverse函数中，已经实现了指向这一段的下一个节点，所以不用单独处理

注意：如果end为nil，应该及时break跳出，不然会报错
