# pool
a pool that make goroutine limit


example :

package main

import (
	"fmt"
	"github.com/zutim/pool"
	"sync"
)

func main() {
	do()
}

func do() {
	res := 0
	pool2 := pool.NewFixedGoroutinePool()
	wg := sync.WaitGroup{}
	for i := 0; i < 10; i++ {
		a := i
		wg.Add(1)
		pool2.Schedule(func() {
			defer wg.Done()
			res += a
		})
	}

	pool2.Stop()
	
	wg.Wait()
	fmt.Println(res)
}

