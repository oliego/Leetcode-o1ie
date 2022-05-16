## No.524 Longest Word Through Deleting
1. 第一想法：
2. solution：
    + isSubstring：给定input和dictionary里的一个词，使用双指针判断dictionary里的这个词是否是input的substring
    + 遍历dictionary，过滤掉长度比retString短或首字母比retString大的词，然后使用isSubstring判断
```GO
func findLongestWord(s string, dictionary []string) string {
    retString := ""
    for _, value := range dictionary {
        l1 := len(retString)
        l2 := len(value)
        if l2 < l1 || (l2 == l1 && value[:1] > retString[:1]) { // 如果长度一样但dictionary里的词长度较大，则不考虑
            continue
        }
        if isSubstring(s, value) {
            retString = value
        }
    }
    return retString
}

func isSubstring(tS string, dS string) bool {
    tR, dR := []rune(tS), []rune(dS)
    i, j := 0, 0
    for ; i < len(tR) && j < len(dR); {
        if tR[i] == dR[j] {
            j++
        }
        i++
    }
    return j == len(dR)
}
```