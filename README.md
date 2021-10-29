# trap
Go package for returning a root context for graceful exits

## Example

This should typically be used in main. Its context method can be used to return a context that is cancelled when an OS signal is received.

```go
func main() {
	ctx := trap.Context()

	db, err := open(ctx, "...")
	if err != nil {
		log.Fatalf("open: %s", err)
	}

	go work(db)
	<-ctx.Done()
	db.Close()

	log.Println("done :)")
}
```
