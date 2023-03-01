# Navigation

- [Comments conventions](#comments-conventions)
- [Code style](#code-style)
	- [Rules](#rules)
		- [Classes](#classes)
		- [Fields, Properties](#fields,-properties)
		- [Methods](#methods)
- [Rouvy coding conventions](#rouvy-coding-conventions)
	- [UI](#ui)
		- [Naming conventions](#naming-conventions)
		- [Platform specifics](#platform-specific-screens-and-views)
		- [Screens and Views](#creating-screens-and-views)
		- [Controllers](#screen-and-view-controllers)
		- [Views and controllers interaction](#views-and-controllers-interaction-rules)
		- [Unity specific handling](#unity-specific-handling)
	- [Backend](#backend)
		- [API communication](#api-communication)
		- [Data containers](#models-and-data-container-classes)
		- [Other](#other-backend)
	- [Tests](#tests)
	- [Other](#other)
- [Other agreements](#other-agreements)

# Code policy

This readme should contain all important information about code policy including style and other useful tips how to write Rouvy App code.

<a name="comments-conventions"></a>
## Comments conventions

Every developer should (of course) make sure their code is readable and well documented.

* All classes (enums etc.) should be documented about their purpose, usage and responsibilities. Exceptions can be classes which name or content is perfectly self-describing.
* Developer should add doc-comments to every interface or public methods, to define the propper contract between the creating entity and clients that are going to use it.
	* Use triple slashes (`///`) for documentation comments, which will automatically generate XML documentation.
	* Do not hesitate to use XML tags to increase readability and comprehensibility of the comment.
	* Recommended tags in [Microsoft doc](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-specification/documentation-comments).
	* Some tags can be optional like return (maybe param) as the tag's content does not give any new information and it just bloats the code (see the bad example below).
	* The doc comment should always contain the `Exception` line(s) with all relevant exception that may be thrown (probably no system exceptions that can be thrown anywhere - like `NRE`).

*Incorrect DOC example:*

```
/// <summary>
/// Provides the calculation and returns the result.
/// </summary>
/// <returns>The result of the calculation.</returns>
int Calculate(double input);
```

* Code inline comments are also welcomed. These comments should be written in a way they increase the readability and not just increases the lines of code.
	* We should try to respect the official Microsoft commenting [rules](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions#commenting-conventions):
		* Use double slashes (`//`) for single-line comments.
		* Put space behind slashes.
		* The first letter has to be capital.
		* Put period at the end.
		* Place comments above the line of code they pertain to.
		* In case the comment is too long, it is ok to split it into mupliple lines.
		* In case of not sentence comments the period at the end or capital letter is not required. However think whether the comment is really needed.
	* Use the `//TODO:` prefix for comments that indicate a task that needs to be completed or a problem that needs to be fixed.
	* Use the `//HACK:` prefix for comments that indicate a quick, temporary solution to a problem.
	* Always comment any non-obvious code, such as complex algorithms or tricky logic.
	* Keep comments up-to-date and remove any that are no longer relevant.

See the example of correctly used doc and inline comments:

```
/// <summary>
/// The method takes the given input, and if the value is greater than zero,
/// then the double the value 2 is returned.
/// </summary>
/// <param name="input">The input should be integer in kilograms as user's weight.</param>
/// <returns>Doubled the user's weight given in input param. Be aware the value is in grams!</returns>
public int Calculate(double input)
{
	//HACK: The server should send integer, not double.
	var fixed = (int) input.

    // Check if the input is valid.
    if (fixed <= 0)
    {
        //TODO: Add error handling for invalid input.
        return 0;
    }

    // Perform bitwise shift left by 1 bit (i.e. multiplication by 2).
    int result = fixed << 1;
    // Return the value converted to grams.
    return result * 1000;
}
```

Here the `// Genders` comment is probably redundant as the property names already indicates everything.

```
// Genders
public const string GenderMale = "male";
public const string GenderFemale = "female";
```

<a name="code-style"></a>
## Code style

First of all, the main source of truth of code style is `.editorconfig` in the project root. Please turn on auto formatting based on this config. It will also provides you suggestions how to improve the code.

The `.editorconfig` should more or less reflect the official Microsoft [conventions](https://learn.microsoft.com/en-us/dotnet/csharp/fundamentals/coding-style/coding-conventions).

<a name="rules"></a>
### Rules

* Use descriptive and meaningful names for identifiers. Avoid using single-letter or abbreviated names.

Note: *Do not reorganize (or fix the style of) tones of legacy code in your feature commit. Otherwise, it's hard to check the changes in the Git history. Rather use separate commit.*

* And yes, if you see any violation of these rules, do not hesitate to fix it.

<a name="classes"></a>
#### Classes

See the [MS Names of Classes, Structs, and Interfaces](https://learn.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-classes-structs-and-interfaces).

* Use PascalCase for class, struct, enum, and interface names.
* Use an `I` prefix for interface names, such as `IMyInterface`.
* For base classes use `Base` suffix. Such a class should be `abstract` and usually cannot be used as-is.
	* When a base class has some more logic and can be used as-is, use `Basic` suffix.
* Inside the classes use the appropriate accessors:
	* Apply *Information hiding*. Mark every not public fields and methods as `private` (or `protected` - depends on specific case).
	* The `internal` keyword should be avoided (at least until the project will not be split into different assemblies.)

**Only one public class per file**

* Keep max. one public class, enum, interface, struct in one file only. The file has the same name as the class.

There may be some exceptions:

* `public static class FooExtension` (Helper) which is dedicated to the XXX class, enum, interface, struct only may be in the same file with `Foo` class (enum, struct, interface).7
* Nested classes/structs/enums where it makes logical sense (and are relativelly small, so they do not increase the line count too much). Like `Dictionary.KeyCollection`, not new class `DictionaryKeyCollection`.

<a name="fields,-properties"></a>
#### Fields, Properties
* Do NOT use an underscore prefix (`_someField`) for private field names.
* Use PascalCase for constant field names (even though they are private).
	* Same for `private static readonly`.

* Use PascalCase for property names.
* Do not use expression bodied members in case of properties. If not defined body, the property should be one lined.

```
public bool IsCorrect => false;

public bool IsCorrect
{
	get => true;
}

public bool OneLine { get; set; }
```

* Names of fields used in properties has the same name as the property and are lowercase. E.g.:

```
private int value;

public int Value
{
	get => value;
}
```

<a name="methods"></a>
#### Methods

* Use camelCase for variable and parameter names.
* Use the `base` keyword to refer to the base class, such as `base.MyMethod()`.
* Use the `this` keyword to refer to the current instance of a class, such as `this.myField`, only in case the name collides with name of local variable.
* Use `var` type declaration, when the type is clear from the right hand side or the surrounding code:

```
var a = "string";
var a = new MyClass();
var a = obj as MyClass;
var a = (MyClass) obj;
var a = ButtonFactory.Create();

// It is clear the orders are some IEnumerable of Order from the line bellow.
var orders = service.GetOrders();
for (var o in orders)
{
	...
}
```

*	But do not use:

```
// What is the retVal? Is it the speed? double, float or bool as success value?
var retVal = service.CalcSpeed(int power);
```

<a name="rouvy-coding-conventions"></a>
## Rouvy coding conventions

Specific conventions of Rouvy APP team.

<a name="ui"></a>
### UI
The UI in Unity App is created from code so Unity UI designer should not be used. For this purpose there are base UI elements implemented in the RouvyLib.

<a name="naming-conventions"></a>
#### Naming conventions
* Always use UI element name as suffix for fields and properties:

```
private UILabel titleLabel;
private UIButton startButton;
private UIListView racersListView;
```

* Always use UI element name as suffix for derived classes. In most cases use `View` suffix for classes derived from `UIImage` or `UIRect` (most UI subclasses in Unity App will have View suffix):

```
public class DashboardScreen : UIScreen { }
public class UserInfoView : UIImage { }
```

* Use full view (screen) name with Controller suffix for view (screen) controllers:

```
// Correct.
public class DashboardScreenController : ScreenController
public class UserInfoViewController : ViewController

// Wrong.
public class DashboardController : ScreenController
public class UserInfoController : ViewController
```

* Do not name Actions (events or delegates) with On prefix.
* Do not name public methods in view (screen) controller with On prefix.

<a name="platform-specific-screens-and-views"></a>
#### Platform specific screens and views

Some screens and views have different design and functionality on the specific platform (Desktop, Mobile, TV). Consider originally platform independent view `UserInfoView` should be platform specific. To do this make `UserInfoView` class abstract, rename it to `UserInfoViewBase` and create subclasses for all (currently supported) platforms as follows:

 * `UserInfoViewBase`
 * `UserInfoViewDesktop`
 * `UserInfoViewMobile`
 * `UserInfoViewTV`

![UI platform specific classes](./img/ui_platform_specific_classes.png "UI platform specific classes")

Actually the AppleTV implementation is very similar to desktop implementations, thus in many cases it looks like in the diagram below.

![UI platform specific classes actual](./img/ui_platform_specific_classes_real.png "UI platform specific classes actual")

`UserInfoViewBase` should:

* contain as much as possible common child views and code for each platform,
* contain only common child views and code for each platform,
* layout only these child views that have the same position (absolute or relative) in parent for each platform,
* define abstract methods with specific behaviour for each platform.

<a name="creating-screens-and-views"></a>
#### Creating screens and views

Every screen or view must be an `UIRect` subclass. These rules should be respected for every screen or view class (try to keep the same order in code as the order of items):

1. public fields with actions (events or delegates, user actions on view or screen, usually buttonClicked actions etc.),
2. public, protected or private property with screen or view controller,
3. protected or private fields with child views,
4. protected override Awake method:
	* view controller addition using `AddComponent<>` method.
5. protected override Initialize method:
	* child views initialization:
		* set every aspect that is constant (or default) for the view (color, text, size, etc.),
		* bind events (usually to methods defined in the controller),
		* assign view controller to screen view controller (only if view content is dependent on actions performed outside the view),
6. protected override LayoutChildren method:
	* child views layout,
	* do nothing else here.

If passing data into the created screen is needed, do it as follows:

```
var myScreen = UIScreen.Create<ScreenmyScreenBase, myScreenDesktop, myScreenMobile, myScreenAppleTV>();

myScreen.Controller.SetSomething(123);
ScreensController.Push(myScreen);
```

<a name="screen-and-view-controllers"></a>
#### Screen and view controllers

**Screen controllers** are controllers in the sense as defined by the MVC pattern - they should present data from model (managers in our case) and handle user actions on views.

**View controllers** are helper controllers for screen controllers that are created because:

* moving code from screen controller to respective view controller keeping screen controller thiner and more readable,

* making view components encapsulated.

There is no need to create view controller for each view. View controllers should be created if:

* The view would contain more logic than just presenting the information (e.g. some interaction with IoC container, backend managers etc.). See the examples:


*Wrong view example*

```
// What not to do in the View.
public class BadExampleView : UIView
{
	private UIButton button;
    protected override void Initialize()
    {
        base.Initialize();
        button = ButtonFactory.CreateOrange(transform, "Example button");
        button.OnClick.AddListener(() =>
        {
			// This evokes that a controller should be created.
            IoC.Get<RouteManager>().RemoveFromFavourites(0);
        });
    }
}
```

*Correctly implemented the example above*

```
// How to do it properly in View.
public class FixedBadExampleView : UIView
{
    private UIButton button;

    private FixedBadExampleViewController controller;

    protected override void Awake()
    {
        base.Awake();
        controller = AddComponent<FixedBadExampleViewController>();
    }

    protected override void Initialize()
    {
        base.Initialize();
        button = ButtonFactory.CreateGreen(transform, "Example button");
        button.OnClick.AddListener(() => controller.RemoveFromFavourites(0));
    }
}

// Simple controller for the view.
public class FixedBadExampleViewController : ViewController
{
    private RouteManager routeManager;
    protected override void Awake()
    {
        base.Awake();
        routeManager = IoC.Get<RouteManager>();
    }

    public void RemoveFromFavourites(int routeId)
        => routeManager.RemoveFromFavourites(routeId);
}
```

*Correct simple view*

```
// What you can do straight in the view.
public class CorrectExampleView : UIView
{
    private UIButton button;
    protected override void Initialize()
    {
        base.Initialize();
        button = ButtonFactory.CreateGreen(transform, "Example button");
        button.OnClick.AddListener(() => UIUtils.OpenUrl(MyRouvyUris.TermsUrl));
    }
}
```


**Creating screen and view controllers**

Every screen controller must be a `ScreenController` subclass, every view controller must be a `ViewController` subclass. These rules should be respected for every screen or view controller class (try to keep the same order in code as the order of items):

1. public properties with view controllers (controllers for views whose content is dependent on actions performed outside the view),
2. private or protected fields with data managers,
3. private or protected field with controlled view,
4. protected override Awake method
	* managers assignment using `IoC.Get<>` method,
	* view assignment using `GetComponent<>` method.
5. protected override Start method:
	* Update view according data from manager.
6. public methods used for manipulating controlled view (these methods are usually bind to actions during view initialization).

<a name="views-and-controllers-interaction-rules"></a>
#### Views and controllers interaction rules
Every presented view must be a part of the screen.

View controller A is allowed to have a reference to view controller B only if view controlled by B is a child of view controlled by A. It follows:

* View controller must not have a reference to screen controller, screen controller may have a reference to all view controllers.
* If some view on the screen is dependent on the state or action from other view on the screen, this dependency should be solved through screen controller.

<a name="unity-specific-handling"></a>
#### Unity specific handling
* There is a need to check game object is destroyed after awaited call or in other methods that may be called from other context, eg. `Handle<>`.

* Do not use other then `==` and `!=` operators to check if MonoBehaviour object is null. Operators are overloaded and checks the underlying gameobject is destroyed. Do not use `?!` , `??=` and simmilar.

<a name="backend"></a>
### Backend

<a name="api-communication"></a>
#### API communication

* For calling API (that could be called directly from controllers and does not have its own layer) use `MiscApiManager`.
	* Do not use API calls directly from view controllers.

* ApiOperation should throw an exception when the non-success status code is returned. The upper layer (usually some managers) can translate this exception into some valid response object.
	* Do not try to parse the error response to a valid response object inside ApiOperation. Throw exception instead. The exception can contain detailed information about API errors if provided (HTTP static code, ApiError object, string, etc).

<a name="models-and-data-container-classes"></a>
#### Models and Data container classes
* For data classes (data containers) used for communication with API or for local storage, use `Data` suffix and keep only properties that are serialized. Place extra methods, properties, etc. into separate extension or helper class.
* In case new data container classes do not use fields but properties. In the case of existing ones, replace fields with properties only in case u touch the class.

* Be careful when changing container data classes (classes with `Data` suffix). These classes are used to persist data in local storage. Dao classes use the persisted data to initialize Data Containers (we use JSON for serialization in-app). This can cause problems when updating the app to a new version. If there is a backward incompatible change in the data container class then after the update  “old“ data serialized in JSON on disk will fail to load → can cause problems in the app (`StorageManager` tries to handle this case correctly, but it can still lead to loss of data).
	* Steps to properly handle changes in container data classes:
		- Be careful when changing fields/properties of container data classes!
		- Try not to delete existing files/properties, instead, introduce a new one and mark the old one as deprecated (ideally with the version when it was deprecated -> can be removed once support for this version will be dropped).
		- Use `UdateHelper` class that run during application start before Dao classes and Managers are initialized. This class is intended to handle required data changes during an application update.

<a name="other-backend"></a>
#### Other
* We should use the builder pattern to creating some complex instances in backend code. The builder pattern allows to write fluent and readable code.
	* Use the `With` prefix of special build methods e.g. `public Builder WithColor(Color color)`.
	* See [more](https://refactoring.guru/design-patterns/builder).

<a name="tests"></a>
### Tests

* Use the AAA pattern.
* Use `NSubstitute` library to create mocks.
* Use `FluentAssertions` library while creating unit tests. The code is much more readable. While adding unit test into test class where the `FluentAssertions` are not used, please, rfc the tests to use it.
* In Unit tests, we have custom attributes, eg. `[StorageCategory]`. Although attributes are inherited, mark all test classes with all applicable attributes for better orientation.

<a name="other"></a>
### Other
* Do not use regions, see [are-regions-an-antipattern-or-code-smell](https://softwareengineering.stackexchange.com/questions/53086/are-regions-an-antipattern-or-code-smell). If the file is too large, rather think about splitting it.
* Use float in Unity code and for performance optimization, eg. MP Server. Otherwise use double.

<a name="other-agreements"></a>
## Other Agreements
* If the developer sees some potential change in the `.editorconfig`, he should discuss it with the team and change the editor config to meet one programming style convention.
