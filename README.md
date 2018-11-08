# Swift-Design-Pattern

MVC Login Example in Swift 4.0, 
First we build our View :
```swift
protocol LoginView {
    func onLoginSuccess()
    func onLoginFail()
}
```

Then we should build the model :
```swift
class LoginModel {
    private var view:LoginView? = nil
    
    init(view:LoginView) {
        self.view = view
    }
    
    func login(username:String,password:String) {
        if username == "John" && password == "12345" {
            self.view?.onLoginSuccess()
        } else {
            self.view?.onLoginFail()
        }
    }

}
```
finally we build the Controller :
```swift
class LoginController {
    private var view:LoginView? = nil
    private var model:LoginModel!
    
    init(view:LoginView) {
        self.view = view
        model = LoginModel(view: view)
    }
    
    func login(username: String, password: String) {
        model.login(username: username, password: password)
    }
    
}
```

Now let take a test :

```swift 
class Test:LoginView {
    
    init() {
        let controller = LoginController(view: self)
        
        // failed login
        controller.login(username: "aaa", password: "123")
        // failed login
        controller.login(username: "John", password: "123")
        // success
        controller.login(username: "John", password: "12345")
    }
    
    func onLoginSuccess() {
        print("success")
    }
    
    func onLoginFail() {
        print("login failed")
    }
    
}
```
