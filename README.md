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

##UIViewController
###Constructor with storyboard
```swift
...
// Constants for Storyboard/ViewControllers.
static let storyboardName = "Main"
static let viewControllerIdentifier = "DetailViewController"
...

class func detailViewControllerForProduct(_ product: Product) -> DetailViewController {
	let storyboard = UIStoryboard(name: DetailViewController.storyboardName, bundle: nil)

	let viewController = storyboard.instantiateViewController(withIdentifier: DetailViewController.viewControllerIdentifier) as! DetailViewController

	viewController.product = product

	return viewController
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
###Filter with Predicate
```swift
var customer = ["firstName":"karthi", "LastName":"alagu", "MiddleName":"prabhu"]
var client = ["firstName":"Selva", "LastName":"kumar", "MiddleName":"m"]
var employee = ["firstName":"karthi", "LastName":"prabhu", "MiddleName":"kp"]
var arrNames: Array = [customer, client, employee]

var attributeValue = "karthi"
var predicate = NSPredicate(format: "firstName like %@", attributeValue);

let filtered = arrNames.filter { predicate.evaluate(with: $0) };
```

##Array
###Swap values
```swift
swap(&s[0], &s[1])
```
