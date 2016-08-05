---
title:          iOS Shared Web Credentials
date:           2016-08-05 14:00:00
summary:        Simplify authentication for your users
categories:     code reference
---

1. Add entitlement and stuff
1. Get file on server
1. Simulator: Settings > General > Safari > Passwords (1234)
1. Add password
1. Code


```swift
SecRequestSharedWebCredential(nil, nil) { credentials, error in
    dispatch_async(dispatch_get_main_queue()) {
        guard error == nil else {
            self.store.dispatch(SharedPasswordError(error: error!))
            return
        }
        guard let unwrappedCredentials = credentials else {
            self.store.dispatch(SharedPasswordError(error: Error.nilCredentials))
            return
        }
        let arrayCredentials = unwrappedCredentials as [AnyObject]
        guard let typedCredentials = arrayCredentials as? [[String: AnyObject]] else {
            self.store.dispatch(SharedPasswordError(error: Error.malformedCredentials))
            return
        }
        guard let credential = typedCredentials.first else {
            self.store.dispatch(SharedPasswordError(error: Error.missingCredentials))
            return
        }
        do {
            let username: String = try credential <| String(kSecAttrAccount)
            let password: String = try credential <| String(kSecSharedPassword)
            self.store.dispatch(SharedPasswordRetrieved(username: username, password: password))
        } catch {
            self.store.dispatch(SharedPasswordError(error: Error.missingCredentials))
        }
    }
}
```
