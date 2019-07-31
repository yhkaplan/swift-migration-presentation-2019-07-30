slidenumbers: true slide-transition: true

# [fit] The Great Swift Migration

---

# [fit] Self Intro

---

- Name: Josh Kaplan
- Company: GMO Pepabo
- App: minne
- Strengths: English
- Hobbies: Collecting Xcode versions

^ From the US
^ Pepabo's just down the street
^ minne, Japan's largest handmade marketplace

---

# [fit] 30,000 lines of Obj-C

^ 1.5 years
^ 3-4 people

---

# [fit] Why?

---

- Future proofing
- Safety
- Productivity with features like generics, etc
- Security

^ And until what point: just enough to be useful, 92% in our case
^ Security: being able to use latest version of libraries
^ SwiftUI, etc

---

# [fit] How?

---

# [fit] Modernize Objective-C

^ Models in particular
^ You're using ARC, right?
^ Nullability Annotations and Lightweight Generics
^ Why, how

---

```objectivec
@property (nonatomic, nonnull) NSArray<MICreator *> *creators;
@property (nonatomic, nonnull) MICartPayment *payment;
@property (nonatomic, nonnull) MIAPIClient *client;
@property (nonatomic, nullable) MICoupon *coupon;
```

^ Review of lightweight generics
^ No compiler checks w/o annotations

---

# Check nullability in current Swift code

![80%](images/call_hierarchy.png)

```swift
let num: Int? = nil
"\(num)" // String interpolation produces a debug description for an optional value
```

^ The dreaded "Optional()"

---

# Choosing which areas to migrate

- First, modernize models
- Then, ViewControllers and ViewModels/Presenters
    - Work on feature/module basis
- Avoid converting code that is then used in obj-c
- Cells and smaller views can wait

^ Convert your business logic
^ Calling Swift from obj-c is painful because of feature differences like enums, generics, structs, etc
^ Calling modern obj-c is much less painful

---

# [fit] Details

---

# [fit] Steps

---

1. Move properties in m file to header and add annotations
2. Make Swift file and make extension
3. Migrate non-lifecyle methods and commit for each method
4. Make temporary method for lifecycle and IBAction method contents
5. Migrate lifecycle methods and properties
6. Update storyboard

^ Separate commits for each method is great for when there's a bug
^ Being able to compile and run your app w/ each commit is best practice

---

# [fit] Points

---

- Only *minor* refactoring
- Writing tests first helps
- Communicate with team to prevent conflicts
- Things like major renaming should be in separate PRs to make review easier
- Set goals and monitor progress with tools like *tokei*

^ Trying to make the logic significantly different while migrating makes reviews harder and makes it difficult to prevent bugs from entering
^ Running relevant tests on each commit allows for peace of mind
^ "brew install tokei", faster than cloc

---

# [fit] Bonus: Migrating to SwiftUI

---

- Small components
- Use Xcode Preview now
- Fewer dependencies
- Swift 😉

^ Talked w/ Apple engineers about this
^ Xcode Preview works with UIKit too, just need to make views/VCs conform to a protocol
^ Dependencies aren't bad, but unmaintained ones are a burden
