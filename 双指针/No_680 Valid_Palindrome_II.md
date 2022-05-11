## No. 680 Valid Palindrome II
1. 第一想法：
    + 第一个指针从头开始，第二个指针从尾开始
    + 若arr[i] != arr[j]，删除一个字母，即i++/j--
    + 若删除完之后是palindrome，accept，反之reject
        + second_run(s, i+1, j) || second_run(s, i, j-1)
        + 在左边删一个字符 || 在右边删一个字符
``` GO
func validPalindrome(s string) bool {
    b := []byte(s)
    for i, j := 0, len(s) - 1; i <= j; i, j = i + 1, j - 1 {
        if b[i] != b[j] {
            return second_run(b, i+1, j) || second_run(b, i, j-1)
        }
    }
    return true
}

func second_run(b []byte, i int, j int) bool {
    for ; i <= j; i, j = i + 1, j - 1 {
        if b[i] != b[j] {
            return false
        }
    }
    return true
}
```