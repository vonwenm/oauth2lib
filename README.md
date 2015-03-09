# oauth2lib

Pre-baked library for using golang.org/x/oauth2 with facebook, github, google, etc.  Compatible with any framework that uses the standard golang http.HandlerFunc

## Simple Example

```
func main() {
	config := &oauth2.Config{
		ClientID:     "your-facebook-app-id",
		ClientSecret: "your-facebook-app-secret",
		RedirectURL:  "your-oauth2-callback-endpoint",
	}

	handler := oauth2lib.Facebook(config, authorize)
	http.Handle("/oauth2/facebook", handler)

	http.ListenAndServe(":8000", nil)
}

func authorize(c *oauth2lib.Context) {
	fmt.Println("access token is", c.Token.AccessToken)
	http.Redirect(c, c.Request, "/blah", http.StatusTemporaryRedirect)
}
```