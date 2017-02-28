# IOS_CookBook

##UITableViewController
###Sharing UITableViewCells across multiple UITableViewControllers
1) Create cell UI in a nib file  
2) Link UI to UITableViewCell subclass  
3) Add cell's identifier as static let
```swift
class BasicCell: UITableViewCell {
	...
	static let Identifier: String = "BasicCell"   
	...
}
```
4) Register nib with tableView
```swift
override func viewDidLoad() {
	super.viewDidLoad()
	...
	tableView.register(UINib(nibName: BasicCell.Identifier, bundle: nil), forCellReuseIdentifier: BasicCell.Identifier)
	...
}

```

##String
###Concatenation
```swift
var s = "Hello"
s += " World"

let s = "Hello"
let w = s + " World"

let s = "World"
let w = "Hello \(s)"
```
###Replacing Occurrences
```swift
let s = "Hello World"
let w = s.replacingOccurrences(of: " ", with: "_")
```





