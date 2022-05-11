## No.88 Merge Sorted Array
1. 第一想法：两个指针指向两个array的头，创建一个长度为m+n的数组，插入两个指针中小的值
    + problem：GO不支持以变量为长度的数组
2. solution：三指针
    + i1、i2分别指向nums1和nums2的有效长度的尾，i3指向nums1的尾
        + i1 = m - 1， i2 = n - 1, i3 = m + n - 1
    + 将i1和i2指向的较大的值写入i3的位置，若i1或i2 < 0，即nums1或nums2已经读取完，那么只读取另一个数组的数
```GO
func merge(nums1 []int, m int, nums2 []int, n int)  {
    if len(nums2) == 0 {
        return
    }
    i1, i2, i3 := m - 1, n - 1, m + n - 1
    for i3 >= 0 {
        if i1 < 0{ // nums1已读完
            nums1[i3] = nums2[i2]
            i3--
            i2--
        } else if i2 < 0 { // nums2已读完
            nums1[i3] = nums1[i1]
            i3--
            i1--
        }else if nums1[i1] > nums2[i2] {
            nums1[i3] = nums1[i1]
            i3--
            i1--
        } else if nums1[i1] <= nums2[i2] {
            nums1[i3] = nums2[i2]
            i3--
            i2--
        }
    }
}
```