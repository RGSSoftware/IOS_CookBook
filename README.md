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
####Add separator between each element
```swift
let cast = ["Vivien", "Marlon", "Kim", "Karl"]
let list = cast.joined(separator: ", ")
print(list)
// Prints "Vivien, Marlon, Kim, Karl"
```
###Replacing Occurrences
```swift
let s = "Hello World"
let w = s.replacingOccurrences(of: " ", with: "_")
```

##Collection
###Remove object
```swift
if let index = contacts.index(of: contact){
	contacts.remove(at:index)
}
```
###Enumerate Array with index and value
```swift
for (i, contact) in contacts.enumerated(){
	print("\(i): '\(contact)'")
}
```

###Enumerate Dictionary and Set with key and value
```swift
for (key, contact) in zip(contacts.keys, contacts.values){
    print("\(key): '\(contact)'")
}
```

##Array
###Swap values
```swift
swap(&s[0], &s[1])
```






