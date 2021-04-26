If you run this code, it'll tell you where to find a form to fill out. 

Unfortunately I forgot what language this is.

Also, it might be broken? Sorry

Anyway, good luck.

    package main

    import (
      "crypto/sha1"
      "fmt"
      "net/http"
      "log"
      "io/ioutil"
    )

    func main() {
      api_url := "https://intern21.ww.dev.hstream.net"
      fmt.Printf("API_URL: %s\n", api_url)

      h := sha1.New()

      h.Write([]byte(api_url))

      value := h.Sum(nil)

      valuestr := fmt.Sprintf("%x", value)

      fmt.Printf("API Value: %s\n", valuestr)

      url_to_get := api_url + "/" + valuestr

      fmt.Printf("url_to_get: %s\n", url_to_get)

      fmt.Printf("getting...")

      resp, err := http.Get(url_to_get)
      if err != nil {
         log.Fatalln(err)
      }

      body, err := ioutil.ReadAll(resp.Body)
      if err != nil {
         log.Fatalln(err)

      form_url := string(body)
      fmt.Printf("\n**************\nSuccess! To finish this task, please visit the follow url and fill in the form:\n%s\n**************\n", form_url)
    }
