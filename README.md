# The Buildbox iOS Style Guide

Welcome to the Buildbox! 

Now as a developer that will be responsible to make other people's dream come true, you should always strive for quality in our projects. Due to the increased amount of projects that you're going to work with, this guide was created to make sure that anyone in our team can hop between projects without problems to understand what is being done.

# Table of Contents



# 1 Coding Style
This section contains parts of the following Swift Style-Guides.
* [Google Swift Style Guide](https://google.github.io/swift/)
* [RayWenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)
* [Linkedin Swift Style Guide](https://github.com/linkedin/swift-style-guide) 
*  [Apple's official Swift naming and API Design Guidelines](https://swift.org/documentation/api-design-guidelines/).

They are a great source of knowledge, and you should read them all if you have the time.  However the one you should focus is the one from Apple, since we adopt it in its entirety.

## 1.1 Naming
 We know that naming is hard, and that we will not always find the best names. When you can't come up with a 
 good option for naming just ask a coworker. He probably had a similar issue and will be able to help you. Below are some highlight points to pay attention:
 
 * **1.1.1** Do not abbreviate names, prioritize clarity over brevit.
 * **1.1.2** Use **camelCase**.
 * **1.1.3** Use descriptive and unambiguous names.
   ```swift
   // PREFERED
   class RoundAnimatingButton { }

   //  NOT PREFERED
   class MyButton {  }
   ```
 * **1.1.4** Use names based on roles not types.
 * **1.1.5** In general, there should be a comma following a space.  
 * **1.1.6** Begin factory methods with make.
 * **1.1.7** There is no need for prefixing in Swift.
 
    e.g. No need to use *BXLoginViewController*, just use *LoginViewController*.
 
 * **1.1.8** When dealing with an acronym or other name that is written in all caps, like CPF, if it is on the start of a name use all lowercase letters, if not use uppercase instead. 
   ```swift
   var cpf: String = ""

   var userCPF: String = ""
   ```
   
* **1.1.9** When dealing with a protocol that describes a capability, it should end in -able or -ible.
  ```swift
      protocol Flyable { 
          func fly()
      }
  ``` 
* **1.1.10** Protocols that describe what something is doing should be named as nouns. (e.g. Collection, Sequence) 

* **1.1.11** Boolean types should read like assertions. 
   ```swift
    var isReading: Bool
   ```
* **1.1.12** Avoid obscure terms if a common word will do.
   
* **1.1.13** Include type information in constant or variable when its not obvious. 

    ```swift 
    //PREFERED
    var personImageView: UIImageView
    
    //NOT PREFERED
    var personImage: UIImageView
    ```
* **1.1.14** Prefer methods and properties to free functions. 

* **1.1.15** Label closure and tuple parameters. 

* **1.1.16** Boolean types should read like assertions. 
   ```swift
   var isReading: Bool
   ```

## 1.2 Horizontal Alignment

Horizontal alignment is forbidden except when writing tabular data in which readability would be seriously prejudiced if such alignment is not used. 
    
```swift
    // PREFERED
    struct Car {
        var licensePlate: String 
        var model: String
        var color: String
    }
    //
    // NOT PREFERED
    struct Car {
        var licensePlate: String
        var model:        String
        var color:        String
    }
```
    
## 1.3 Vertical Whitespace
All our projects have Swift Lint activated. Therefore it's whitespace rule should never be disabled or ignored.

## 1.4 General

* **1.4.1** - Prefer `let` to `var` whenever possible. 

* **1.4.2** - Avoid writing an enum type when inference allows the use of shorthand access. 

* **1.4.3** - Prefer not writing self unless it is required.(e.g. Inside a closure, block, init).  

* **1.4.4** - If a class or method is not going to be overridden, use the final keyword on its definition.

* **1.4.5** - When using a statement such as else, catch etc. Use the [1TBS](https://en.m.wikipedia.org/wiki/Indentation_style#1TBS) style. 

* **1.4.6** - If you have a function that takes no arguments, do not change the context, and returns some value or object, prefer a computed property instead.

* **1.4.7** - Prefer the use of `map`, `filter` and `reduce` over common iteration. 

* **1.4.8** - When returning multiple values, prefer using a tuple instead of inout arguments. 
* **1.4.9** - Be careful with retain cycles when creating delegates/protocols for classes. Remember to declare the properties weak. 
* **1.4.9** - Be careful with retain cycles when passing self to an escaping closure. Use capture list when this might be the case. 
* **1.4.10** - Switch statements should be indented at the same level as the switch statement to which they belong. 
    ```swift
    // PREFERED
    switch order {
    case .ascending:
        print("Up")
    case .descending:
        print("Down")
    default:
        break
    }
    //
    // NOT PREFERED
    switch order {
        case .ascending:
            print("Up")
        case .descending:
            print("Down")
        default:
            break
    }
    ```

## 1.5 Optionals

Always avoid force unwrap! Also try not to use implicitly unwrapped optionals. Except when you are sure that there will be a value to unwrap, like user-interface objects whose lifetimes are based on the UI lifecycle instead of being strictly based on the lifetime of the owning object.

Use optional binding when it's more convenient to unwrap once and perform multiple operations:

if let textContainer = self.textContainer {
  // do many things with textContainer
}

If you don't need to use the value stored in an optional, but need to know whether or not this values is nil, check this value against nil instead of use if let sintax.

## 1.6 Using `Guard` Statements

Guard is a statement control to make early exits and used to improve code readability.
Prefer guard statements to unwrap multiple optionals.
```swift
    // PREFERED
    func printSum(a: Int?, b: Int?, c: Int?) {
        guard let a = a, let b = b, let c = c else {
         return
        }
        let sum = a + b + c
        print(sum)
    }
    
    //
    // NOT PREFERED
    func printSum(a: Int?, b: Int?, c: Int?) {
        if let a = a {
            if let b = b {
                if let c = c {
                    let sum = a + b + c
                    print(sum)
                } else {
                      fatalError("impossible")
                  }
            } else {
                fatalError("impossible")
            }
        } else {
              fatalError("impossible")
        }
    }
```
## 1.7 Documentation

Documentation comments are written using the format where each line is preceded by a triple slash (///).
Document the parameters, return value, and thrown errors of functions using the Parameter(s), Returns, and Throws tags.
An easy way to write documentation comments in Xcode is to place the text cursor on the declaration and press 
Command + Option + /.

## 1.8 Code organization

* **1.8.1** Use the tag // MARK: - comment to keep things well-organized.

* **1.8.2** When implementing a protocol, use extensions in order to separate your code into logical blocks of functionality.

* **1.8.3** Remove unused code, like Xcode templates.

* **1.8.4** Keep imports minimal



 
