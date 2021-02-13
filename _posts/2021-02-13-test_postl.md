---
title:  test post
tags:
  - TEST
  - Markdown
  - golang
---

# test post
## test post
### test post
#### test post

---

{% highlight golang %}
package main

import (
"bufio"
"fmt"
"os"
"strconv"
)

var sc = bufio.NewScanner(os.Stdin)

func nextInt() int {
    sc.Scan()
    i, e := strconv.Atoi(sc.Text())
    if e != nil {
    panic(e)
    }
    return i
}

func matrix(num int) [][]int {
    var t, x, y int
    matrix := make([][]int, num)
    for i := 0; i < num; i++ {
        t = nextInt()
        x = nextInt()
        y = nextInt()
        matrix[i] = []int{t, x, y}
    }
    return matrix
}

func check(matrix [][]int, n int) bool {
    //位置情報
    position := []int{0, 0}
    
    var status = false
    var workCount int
    for i := 0; i < n; i++ {
        //移動回数
        if i > 0 {
            workCount = matrix[i][0] - matrix[i-1][0]
        } else {
            workCount = matrix[i][0]
        }

        for j := 0; j < workCount; j++ {
            if position[0] < matrix[i][1] {
                position[0]++
            } else if position[1] < matrix[i][2] {
                position[1]++
            } else if position[0] > matrix[i][1] {
                position[0]--
            } else if position[1] > matrix[i][2] {
                position[1]--
            } else {
                position[0]++
            }
        }

        if position[0] == matrix[i][1] && position[1] == matrix[i][2] {
            status = true
            continue
        } else {
            status = false
            break
        }
    }
    return status
}

func main() {
    sc.Split(bufio.ScanWords)
    n := nextInt()
    matrix := matrix(n)
    status := check(matrix, n)

    if status {
        fmt.Println("Yes")
    } else {
        fmt.Println("No")
    }
}

{% endhighlight %}