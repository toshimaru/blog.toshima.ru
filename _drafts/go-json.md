```go
package main

import (
	"encoding/json"
	"fmt"
)

type Country struct {
	Name        string     `json:"name"`
	Prefectures Prefecture `json:"prefectures"`
}

type Prefecture struct {
	Name       string `json:"name"`
	Capital    string `json:"capital"`
	Population int    `json:"population"`
}

func main() {
	jsonStr := `
{
  "name": "日本",
  "prefectures": {
      "name": "東京都",
      "capital": "東京",
      "population": 13482040
  }
}
`
	jsonBytes := ([]byte)(jsonStr)
	data := new(Country)

	if err := json.Unmarshal(jsonBytes, data); err != nil {
		fmt.Println("JSON Unmarshal error:", err)
		return
	}
	fmt.Println(data)
}

```
