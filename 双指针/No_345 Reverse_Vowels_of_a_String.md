## No.345 Reverse Vowels of a String
1. 第一想法：第一个指针从string的第一位开始，第二个指针从string的最后一位开始，如果两个指针都是元音就交换
```GO
var arr = []string{"a", "e", "i", "o", "u", "A", "E", "I", "O", "U"}

func in_list(s string) bool {
	for _, value := range arr {
		if value == s {
			return true
		}
	}
	return false
}

func reverseVowels(s string) string {
    r := []rune(s)
	i, j := 0, len(s)-1
	for i < j {
		if !in_list(string(r[i])) {
			i++
		}
		if !in_list(string(r[j])) {
			j--
		}
		if in_list(string(r[i])) && in_list(string(r[j])) {
			r[i], r[j] = r[j], r[i]
			i++
			j--
		}
	}
    return string(r)
}
```
2. better solution
```GO
func in_list(c byte) bool {
    // A = 65, a = 97
    if c < 'a' {
        c += 32
    }
    return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u'
}

func reverseVowels(s string) string {
    r := []byte(s)
	i, j := 0, len(s)-1
	for i < j {
        // 使用continue，取消第三个if，提高速度
		if !in_list(r[i]) {
			i++
            continue
		}
		if !in_list(r[j]) {
			j--
            continue
		}
        r[i], r[j] = r[j], r[i]
        i++
        j--
	}
    return string(r)
}
```