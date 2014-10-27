# Mandrill Emails via Golang

Stripped down package for sending emails through the Mandrill API. Inspired by [https://github.com/mostafah/mandrill](@mostafah's implementation).

### Installation

    go get -u github.com/keighl/mandrill

### Documentation

http://godoc.org/github.com/keighl/mandrill

### Regular Message

https://mandrillapp.com/api/docs/messages.JSON.html#method=send

    client := ClientWithKey("y2cQvBBfdFoZNByVaKsJsA")

    message := &Message{}
    message.AddRecipient("bob@example.com", "Bob Johnson", "to")
    message.FromEmail = "kyle@example.com"
    message.FromName = "Kyle Truscott"
    message.Subject = "You won the prize!"
    message.HTML = "<h1>You won!!</h1>"
    message.Text = "You won!!"

    responses, mandrillError, err := client.MessagesSend(message)

### Send Template

You can also register a template

https://mandrillapp.com/api/docs/messages.JSON.html#method=send-template

http://help.mandrill.com/entries/21694286-How-do-I-add-dynamic-content-using-editable-regions-in-my-template-

    templateContent := map[string]string{"header": "Bob! You won the prize!"}
    responses, mandrillError, err := client.MessagesSendTemplate(message, "you-won", templateContent)

### Including Merge Tags

http://help.mandrill.com/entries/21678522-How-do-I-use-merge-tags-to-add-dynamic-content-

    message.GlobalMergeVars := mandrill.ConvertMapToVariables(map[string]string{"name": "Bob"})
    message.MergeVars := mandrill.ConvertMapToVariablesForRecipient("bob@example.com", map[string]string{"name": "Bob"})
