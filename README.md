# IOS_CookBook

##Share Styles
1) Create UI placement in storyboard or nib  
2) Style UI element programmatically
```swift
extension UIButton {
    public static func greenButtonStyle(_ button: UIButton) {
        button.setTitleColor(.white, for: .normal)
        button.setBackgroundColor(.ksr_green_500, forState: .normal)
        
        button.setTitleColor(.white, for: .highlighted)
        button.setBackgroundColor(.blue, forState: .highlighted)
        
        button.setTitleColor(.white, for: .disabled)
        button.setBackgroundColor(.blue, forState: .disabled)
        
        button.layer.borderColor = UIColor.green.cgColor
        button.layer.borderWidth = 1.0
        
        button.titleLabel?.text = .All_Art_Projects()
    }
}

@IBOutlet fileprivate weak var viewMessagesButton: UIButton!
UIButton.greenButtonStyle(viewMessagesButton)
```

##Share Color
```swift
extension UIColor {
  /// 0x25CB68
  public static var ksr_green_500: UIColor {
    return .hex(0x25CB68)
  }
}

import class UIKit.UIColor
import CoreGraphics
import func Darwin.round

public extension UIColor {
  @nonobjc public static func hexa(_ value: UInt32) -> UIColor {
    let a = CGFloat((value & 0xFF000000) >> 24) / 255.0
    let r = CGFloat((value & 0xFF0000) >> 16) / 255.0
    let g = CGFloat((value & 0xFF00) >> 8) / 255.0
    let b = CGFloat((value & 0xFF)) / 255.0

    return UIColor(red: r, green: g, blue: b, alpha: a)
  }

  @nonobjc public static func hex(_ value: UInt32) -> UIColor {
    let r = CGFloat((value & 0xFF0000) >> 16) / 255.0
    let g = CGFloat((value & 0xFF00) >> 8) / 255.0
    let b = CGFloat((value & 0xFF)) / 255.0

    return UIColor(red: r, green: g, blue: b, alpha: 1.0)
  }

  public var hexString: String {
    guard let components = self.cgColor.components else { return "000000" }
    let r = components[0]
    let g = components[1]
    let b = components[2]
    return String(format: "%02X%02X%02X", Int(r * 255), Int(g * 255), Int(b * 255))
  }
}
```
##Share Font
```swift
import UIKit

extension UIFont {
  /// Returns a bolded version of `self`.
  public var bolded: UIFont {
    return self.fontDescriptor.withSymbolicTraits(.traitBold)
      .map { UIFont(descriptor: $0, size: 0.0) } ?? self
  }

  /// Returns a italicized version of `self`.
  public var italicized: UIFont {
    return self.fontDescriptor.withSymbolicTraits(.traitItalic)
      .map { UIFont(descriptor: $0, size: 0.0) } ?? self
  }
  
  /// regular, 17pt font, 22pt leading, -24pt tracking
  public static func ksr_body(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .body, size: size)
  }

  /// regular, 16pt font, 21pt leading, -20pt tracking
  public static func ksr_callout(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .callout, size: size)
  }

  /// regular, 12pt font, 16pt leading, 0pt tracking
  public static func ksr_caption1(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .caption1, size: size)
  }

  /// regular, 11pt font, 13pt leading, 6pt tracking
  public static func ksr_caption2(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .caption2, size: size)
  }

  /// regular, 13pt font, 18pt leading, -6pt tracking
  public static func ksr_footnote(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .footnote, size: size)
  }

  /// semi-bold, 17pt font, 22pt leading, -24pt tracking
  public static func ksr_headline(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .headline, size: size)
  }

  /// regular, 15pt font, 20pt leading, -16pt tracking
  public static func ksr_subhead(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .subheadline, size: size)
  }

  /// light, 28pt font, 34pt leading, 13pt tracking
  public static func ksr_title1(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .title1, size: size)
  }

  /// regular, 22pt font, 28pt leading, 16pt tracking
  public static func ksr_title2(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .title2, size: size)
  }

  /// regular, 20pt font, 24pt leading, 19pt tracking
  public static func ksr_title3(size: CGFloat? = nil) -> UIFont {
    return .preferredFont(style: .title3, size: size)
  }

  fileprivate static func preferredFont(style: UIFontTextStyle, size: CGFloat? = nil) -> UIFont {

    let defaultSize: CGFloat
    switch style {
    case UIFontTextStyle.body:         defaultSize = 17
    case UIFontTextStyle.callout:      defaultSize = 16
    case UIFontTextStyle.caption1:     defaultSize = 12
    case UIFontTextStyle.caption2:     defaultSize = 11
    case UIFontTextStyle.footnote:     defaultSize = 13
    case UIFontTextStyle.headline:     defaultSize = 17
    case UIFontTextStyle.subheadline:  defaultSize = 15
    case UIFontTextStyle.title1:       defaultSize = 28
    case UIFontTextStyle.title2:       defaultSize = 22
    case UIFontTextStyle.title3:       defaultSize = 20
    default:                           defaultSize = 17
    }

    let font = UIFont.preferredFont(forTextStyle: style)
    let descriptor = font.fontDescriptor
    return UIFont(descriptor: descriptor,
                  size: ceil(font.pointSize / defaultSize * (size ?? defaultSize)))
  }
}

button.titleLabel?.font = .ksr_body()
label.font = .ksr_title1(size: 22)
```

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
###Constructor with Main storyboard
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

###Constructor with multiple storyboards
```swift
public enum Storyboard: String {
//storyboards
  case Activity
  case Backing
  
  public func instantiate<VC: UIViewController>(_ viewController: VC.Type,
                                                inBundle bundle: Bundle = Bundle.main) -> VC {
    guard
      let vc = UIStoryboard(name: self.rawValue, bundle: Bundle(identifier: bundle.identifier))
        .instantiateViewController(withIdentifier: VC.storyboardIdentifier) as? VC
      else { fatalError("Couldn't instantiate \(VC.storyboardIdentifier) from \(self.rawValue)") }

    return vc
  }
}

extension UIViewController {
	public static var storyboardIdentifier: String {
		return String(describing: type(of: self))
	}
}

let controller = Storyboard.Activity.instantiate(SignupViewController.self)
```

##Error Handling Try Catch
```swift
public enum LoginError: LocalizedError {
    case genericFailure
    case invalidUsername
    case invalidPassword
    
    public var errorDescription: String? {
        switch self {
        case .genericFailure:
            return .Generic_Failure()
        case .invalidUsername:
            return .Login_Invalid_Username_Error()
        case .invalidPassword:
            return .Login_Invalid_Password_Error()
        }
    }
}

func loginWith(password: String, username: String) throws -> String {
    throw LoginError.genericFailure
}

do {
		_ = try loginWith(password: "", username: "")
	} catch let error where error is LoginError {
		switch error {
		case LoginError.invalidUsername:
		print("username")
		case LoginError.invalidPassword:
		print("password")
		default:()  
		}
		print(error.localizedDescription)
	} catch let error {
		print("base")
		print(error.localizedDescription)
	}
```

##Check verson
```swift
if #available(iOS 10.0. *) {
	print("iOS > 10.0")
}
```

##Localized String
```swift
extension String {
    public static func All_Art_Projects() -> String {
        return NSLocalizedString("All_Art_Projects", comment: "All_Art_Projects")
    }
}

button.titleLabel?.text = .All_Art_Projects()
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
for (key, contact) in contacts {
    print("\(key): '\(contact)'")
}
```
###Filter with Predicate
```swift
let customer = ["firstName": "karthi", "LastName": "alagu", "MiddleName": "prabhu"]
let client = ["firstName": "Selva", "LastName": "kumar", "MiddleName": "m"]
let employee = ["firstName": "karthi", "LastName": "prabhu", "MiddleName": "kp"]
let contacts = [customer, client, employee]

let attributeValue = "karthi"
let predicate = NSPredicate(format: "firstName like %@", attributeValue)

let filtered = contacts.filter { predicate.evaluate(with: $0) }
```

##Array
###Swap values
```swift
swap(&s[0], &s[1])
```
