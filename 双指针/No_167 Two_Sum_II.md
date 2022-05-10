## No.167 Two Sum II - Input Array is Sorted
1. 第一想法：双指针遍历，O(n^2)
2. 第二想法：一个指针从第一个数开始遍历，在每个iteration中，第二个指针每次循环*=2
```java
// time limit exceed
public int[] twoSum(int[] numbers, int target) {
        int[] ret = new int[2];
        for (int i = 0; i < numbers.length; i++) {
            int j = i + 1;
            for (int k = 1; ; k*=2) {
                j+=k;
                if (j >= numbers.length) {
                    j = numbers.length - 1;
                    break;
                }
                if (numbers[i] + numbers[j] > target) {
                    break;
                } else if (numbers[i] + numbers[j] == target) {
                    ret[0] = i+1;
                    ret[1] = j+1;
                    return ret;
                }
            }
            for (; j >= i; j--) {
                if (numbers[i] + numbers[j] == target) {
                    ret[0] = i+1;
                    ret[1] = j+1;
                    return ret;
                }
            }
        }
        return ret;
    }
```
3. 第三想法：第一个指针从第一个数开始遍历， 第二个指针做二分查找
```java
public int[] twoSum(int[] numbers, int target) {
        int[] ret = new int[2];
        for (int i = 0; i < numbers.length; i++) {
            int l = i + 1;
            int r = numbers.length - 1;
            if (l == r) {
                if (numbers[i] + numbers[l] == target) {
                    ret[0] = i + 1;
                    ret[1] = l + 1;
                    return ret;
                }
            }
            while (l < r) {
                int m = (l + r) / 2;
                if (numbers[i] + numbers[m] < target) {
                    l = m;
                } else if (numbers[i] + numbers[m] > target) {
                    r = m;
                } else {
                    ret[0] = i + 1;
                    ret[1] = m + 1;
                    return ret;
                }
                if (l == r - 1) {
                    ret[0] = i + 1;
                    if (numbers[i] + numbers[l] == target) {
                        ret[1] = l + 1;
                        return ret;
                    } else if (numbers[i] + numbers[r] == target) {
                        ret[1] = r + 1;
                        return ret;
                    } else {
                        break;
                    }
                }
            }
        }
        return ret;
    }
```
4. 答案
    + 一个指针指向array head，另一个指针指向array tail，sum = 两个指针指向元素之和
    + 若sum > target，将第二个指针向左移动使sum变小；反之把第一个指针向右移动使sum变大
    + O(n)
```java
public int[] twoSum(int[] numbers, int target) {
        int[] ret = new int[2];
        int l = 0;
        int r = numbers.length - 1;
        while (l < r) {
            int sum = numbers[l] + numbers[r];
            if (sum < target) {
                l++;
            } else if (sum > target) {
                r--;
            } else {
                ret[0] = l + 1;
                ret[1] = r + 1;
                return ret;
            }
        }
        return ret;
    }
```