# Tribute

```swift
let string = NSMutableAttributedString().add("Hello ") {
    $0.font = .systemFontOfSize(20)
    $0.color = .redColor()
    $0.underline = .StyleSingle
}.add("world ") {
    $0.stroke = .Filled(width: 2)
    $0.strokeColor = .orangeColor()
}.add("of Swift "){
    $0.font = .systemFontOfSize(12)
    $0.underline = nil
}.add(UIImage(named: "swift")!)
```

Not bad comparing to

```swift
let string2 = NSMutableAttributedString()
string2.appendAttributedString(NSAttributedString(string: "Hello ", attributes: [
    NSFontAttributeName: UIFont.systemFontOfSize(20),
    NSUnderlineStyleAttributeName: NSUnderlineStyle.StyleSingle.rawValue,
    NSForegroundColorAttributeName: UIColor.redColor()
]))
string2.appendAttributedString(NSAttributedString(string: "world ", attributes: [
    NSFontAttributeName: UIFont.systemFontOfSize(20),
    NSUnderlineStyleAttributeName: NSUnderlineStyle.StyleSingle.rawValue,
    NSForegroundColorAttributeName: UIColor.redColor(),
    NSStrokeColorAttributeName: UIColor.orangeColor(),
    NSStrokeWidthAttributeName: -2
]))
string2.appendAttributedString(NSAttributedString(string: "of Swift ", attributes: [
    NSFontAttributeName: UIFont.systemFontOfSize(12),
    NSForegroundColorAttributeName: UIColor.redColor(),
    NSStrokeColorAttributeName: UIColor.orangeColor(),
    NSStrokeWidthAttributeName: -2
]))
let attachment = NSTextAttachment()
attachment.image = UIImage(named: "swift")
string2.appendAttributedString(NSAttributedString(attachment: attachment))
```

# Design Goals

1. Word processor logic: appending a string should inherit last attributes.
1. Allow for easy customization of common properties, including toggle bold or change the font size.
1. Flatten paragraph style and attrbiutes, no more 5 lines of code if all you wanted is to change text alignment.
1. Minimal overhead: produce only required attributes.
1. Have an attributed string ready to use every time you leave the configuration block.
1. Replace string constants with strongly typed enums where possible.

# Notes

1. Keep in mind that playground doesn't always render `NSAttributesString` correctly (font variations and attachments are few of the problematic I noticed). Use a `UILabel` as a live view instead: `XCPlaygroundPage.currentPage.liveView = label`.
2. Not all fonts have both italic and bold variations, you can use `obliqueness` property as a poor man italic



*This is just a tribute*
