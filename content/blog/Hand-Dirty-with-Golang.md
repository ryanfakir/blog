+++
date = "2016-12-24T18:37:06-05:00"
draft = false
title = "Hand Dirty with Golang"

+++

#### Task: web crawler with go

```Golang
func main() {
	for _, v := range os.Args[1:] {
		resp, err := http.Get(v)
		if err != nil {
			fmt.Fprintf(os.Stderr, "err with: %v\n", err)
			os.Exit(1)
		}
		defer resp.Body.Close()
		_, err = io.Copy(os.Stdout, resp.Body)
		if err != nil {
			fmt.Fprintf(os.Stderr, "can't copy from body: %v\n", err)
		}
	}
}
```