# .NET/.NET Core Clean Code concepts adapted

If you liked `dotnet-cleancode` project or if it helped you, please give a star :star: for this repository. That will not only help strengthen our .NET community but also improve skills about the clean code for .NET developers in around the world. Thank you very much :+1:

Say hi on [Twitter](https://twitter.com/ajaysingh853)!

# Table of Contents

- [.NET/.NET Core Clean Code concepts adapted](#netnet-core-clean-code-concepts-adapted)
- [Table of Contents](#table-of-contents)
- [Introduction](#introduction)
- [.NET Clean Code](#net-clean-code)
  - [Naming](#naming)
  - [Variables](#variables)
  - [Functions](#functions)
  - [Objects and Data Structures](#objects-and-data-structures)
  - [Formatting](#formatting)
  - [Comments](#comments)
- [Other Resources](#other-resources)
- [License](#license)

# Introduction

![Humorous image of software quality estimation as a count of how many expletives you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book [_Clean Code_](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), adapted for .NET/.NET Core. This is not a style guide. It's a guide to producing readable, reusable, and refactorable software in .NET/.NET Core.

Not every principle herein has to be strictly followed, and even fewer will be universally agreed upon. These are guidelines and nothing more, but they are ones codified over many years of collective experience by the authors of _Clean Code_.

# .NET Clean Code

## Naming

<details>
  <summary><b>Avoid using bad names</b></summary>
A good name allows the code to be used by many developers. The name should reflect what it does and give context.

❌ **Bad:**

```csharp
int cd;
```

:white_check_mark: **Good:**

```csharp
int currentDateTime;
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid Misleading Names</b></summary>

Name the variable to reflect what it is used for.

❌ **Bad:**

```csharp
var dataFromDb = db.GetFromService().ToList();
```

:white_check_mark: **Good:**

```csharp
var listOfUsers = _usersService.GetUsers().ToList();
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid Hungarian notation</b></summary>

Hungarian Notation restates the type which is already present in the declaration. This is pointless since modern IDEs will identify the type.

❌ **Bad:**

```csharp
int iCounter;
string strFullName;
DateTime dModifiedDate;
```

:white_check_mark: **Good:**

```csharp
int counter;
string fullName;
DateTime modifiedDate;
```

Hungarian Notation should also not be used in paramaters.

❌ **Bad:**

```csharp
public bool IsProduct(string pProduct, int pAmount)
{
    // some logic
}
```

:white_check_mark: **Good:**

```csharp
public bool IsProduct(string product, int amount)
{
    // some logic
}
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use consistent capitalization</b></summary>

Capitalization tells you a lot about your variables,
functions, etc. These rules are subjective, so your team can choose whatever
they want. The point is, no matter what you all choose, just be consistent.

❌ **Bad:**

```csharp
const int DAYS_IN_WEEK = 7;
const int daysInMonth = 30;

var songs = new List<string> { 'Beautiful', 'See You', 'Dim' };
var Artists = new List<string> { 'Akon', 'Nosus', 'Skyharbor' };

bool EraseDatabase() {}
bool Restore_database() {}

class animal {}
class Alpaca {}
```

:white_check_mark: **Good:**

```csharp
const int DaysInWeek = 7;
const int DaysInMonth = 30;

var songs = new List<string> { 'Beautiful', 'See You', 'Dim' };
var artists = new List<string> { 'Akon', 'Nosus', 'Skyharbor' };

bool EraseDatabase() {}
bool RestoreDatabase() {}

class Animal {}
class Alpaca {}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use pronounceable names</b></summary>

It will take time to investigate the meaning of the variables and functions when they are not pronounceable.

❌ **Bad:**

```csharp
public class Employee
{
    public Datetime sWorkDate { get; set; } // what the heck is this
    public Datetime modTime { get; set; } // same here
}
```

:white_check_mark: **Good:**

```csharp
public class Employee
{
    public Datetime StartWorkingDate { get; set; }
    public Datetime ModificationTime { get; set; }
}
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use Camelcase notation</b></summary>

Use [Camelcase Notation](https://en.wikipedia.org/wiki/Camel_case) for variable and method paramaters.

❌ **Bad:**

```csharp
var employeephone;

public double CalculateSalary(int workingdays, int workinghours)
{
    // some logic
}
```

:white_check_mark: **Good:**

```csharp
var employeePhone;

public double CalculateSalary(int workingDays, int workingHours)
{
    // some logic
}
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use domain name</b></summary>

People who read your code are also programmers. Naming things right will help everyone be on the same page. We don't want to take time to explain to everyone what a variable or function is for.

**Good**

```csharp
public class SingleObject
{
    // create an object of SingleObject
    private static SingleObject _instance = new SingleObject();

    // make the constructor private so that this class cannot be instantiated
    private SingleObject() {}

    // get the only object available
    public static SingleObject GetInstance()
    {
        return _instance;
    }

    public string ShowMessage()
    {
        return "Hello World!";
    }
}

public static void main(String[] args)
{
    // illegal construct
    // var object = new SingleObject();

    // Get the only object available
    var singletonObject = SingleObject.GetInstance();

    // show the message
    singletonObject.ShowMessage();
}
```

**[⬆ Back to top](#table-of-contents)**

</details>

## Variables

<details>
  <summary><b>Avoid nesting too deeply and return early</b></summary>

Too many if else statements can make the code hard to follow. **Explicit is better than implicit**.

❌ **Bad:**

```csharp
public bool IsShopOpen(string day)
{
    if (!string.IsNullOrEmpty(day))
    {
        day = day.ToLower();
        if (day == "friday")
        {
            return true;
        }
        else if (day == "saturday")
        {
            return true;
        }
        else if (day == "sunday")
        {
            return true;
        }
        else
        {
            return false;
        }
    }
    else
    {
        return false;
    }

}
```

:white_check_mark: **Good:**

```csharp
public bool IsShopOpen(string day)
{
    if (string.IsNullOrEmpty(day))
    {
        return false;
    }

    var openingDays = new[] { "friday", "saturday", "sunday" };
    return openingDays.Any(d => d == day.ToLower());
}
```

❌ **Bad:**

```csharp
public long Fibonacci(int n)
{
    if (n < 50)
    {
        if (n != 0)
        {
            if (n != 1)
            {
                return Fibonacci(n - 1) + Fibonacci(n - 2);
            }
            else
            {
                return 1;
            }
        }
        else
        {
            return 0;
        }
    }
    else
    {
        throw new System.Exception("Not supported");
    }
}
```

:white_check_mark: **Good:**

```csharp
public long Fibonacci(int n)
{
    if (n == 0)
    {
        return 0;
    }

    if (n == 1)
    {
        return 1;
    }

    if (n > 50)
    {
        throw new System.Exception("Not supported");
    }

    return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid mental mapping</b></summary>

Don’t force the reader of your code to translate what the variable means. **Explicit is better than implicit**.

❌ **Bad:**

```csharp
var l = new[] { "India", "New York", "Canada" };

for (var i = 0; i < l.Count(); i++)
{
    var lo = l[i];
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    // Wait, what is `lo` for again?
    Dispatch(lo);
}
```

:white_check_mark: **Good:**

```csharp
var locations = new[] { "India", "New York", "Canada" };

foreach (var location in locations)
{
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    Dispatch(location);
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid magic string</b></summary>

Magic strings are string values that are specified directly within application code that have an impact on the application’s behavior. Frequently, such strings will end up being duplicated within the system, and since they cannot automatically be updated using refactoring tools, they become a common source of bugs when changes are made to some strings but not others.

**Bad**

```csharp
if (userRole == "Admin")
{
    // logic in here
}
```

**Good**

```csharp
const string ADMIN_ROLE = "Admin"
if (userRole == ADMIN_ROLE)
{
    // logic in here
}
```

Using this we only have to change in centralize place and others will adapt it.

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Don't add unneeded context</b></summary>

If your class/object name tells you something, don't repeat that in your variable name.

❌ **Bad:**

```csharp
public class Car
{
    public string CarMake { get; set; }
    public string CarModel { get; set; }
    public string CarColor { get; set; }

    //...
}
```

:white_check_mark: **Good:**

```csharp
public class Car
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Color { get; set; }

    //...
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use meaningful and pronounceable variable names</b></summary>

❌ **Bad:**

```csharp
var ymdstr = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

:white_check_mark: **Good:**

```csharp
var currentDate = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use the same vocabulary for the same type of variable</b></summary>

❌ **Bad:**

```csharp
GetUserInfo();
GetUserData();
GetUserRecord();
GetUserProfile();
```

:white_check_mark: **Good:**

```csharp
GetUser();
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use searchable names (part 1)</b></summary>

We will read more code than we will ever write. It's important that the code we do write is readable and searchable. By _not_ naming variables that end up being meaningful for understanding our program, we hurt our readers. Make your names searchable.

❌ **Bad:**

```csharp
// What the heck is data for?
var data = new { Name = "John", Age = 42 };

var stream1 = new MemoryStream();
var ser1 = new DataContractJsonSerializer(typeof(object));
ser1.WriteObject(stream1, data);

stream1.Position = 0;
var sr1 = new StreamReader(stream1);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr1.ReadToEnd());
```

:white_check_mark: **Good:**

```csharp
var person = new Person
{
    Name = "John",
    Age = 42
};

var stream2 = new MemoryStream();
var ser2 = new DataContractJsonSerializer(typeof(Person));
ser2.WriteObject(stream2, data);

stream2.Position = 0;
var sr2 = new StreamReader(stream2);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr2.ReadToEnd());
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use searchable names (part 2)</b></summary>

❌ **Bad:**

```csharp
var data = new { Name = "Singh", Age = 42, PersonAccess = 4};

// What the heck is 4 for?
if (data.PersonAccess == 4)
{
    // do edit ...
}
```

:white_check_mark: **Good:**

```csharp
public enum PersonAccess : int
{
    ACCESS_READ = 1,
    ACCESS_CREATE = 2,
    ACCESS_UPDATE = 4,
    ACCESS_DELETE = 8
}

var person = new Person
{
    Name = "Singh",
    Age = 42,
    PersonAccess= PersonAccess.ACCESS_CREATE
};

if (person.PersonAccess == PersonAccess.ACCESS_UPDATE)
{
    // do edit ...
}
```

**[⬆ Back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use explanatory variables</b></summary>

❌ **Bad:**

```csharp
const string Address = "One Infinite Loop, Delhi 110101";
var cityZipCodeRegex = @"/^[^,\]+[,\\s]+(.+?)\s*(\d{5})?$/";
var matches = Regex.Matches(Address, cityZipCodeRegex);
if (matches[0].Success == true && matches[1].Success == true)
{
    SaveCityZipCode(matches[0].Value, matches[1].Value);
}
```

:white_check_mark: **Good:**

Decrease dependence on regex by naming subpatterns.

```csharp
const string Address = "One Infinite Loop, Delhi 110101";
var cityZipCodeWithGroupRegex = @"/^[^,\]+[,\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/";
var matchesWithGroup = Regex.Match(Address, cityZipCodeWithGroupRegex);
var cityGroup = matchesWithGroup.Groups["city"];
var zipCodeGroup = matchesWithGroup.Groups["zipCode"];
if(cityGroup.Success == true && zipCodeGroup.Success == true)
{
    SaveCityZipCode(cityGroup.Value, zipCodeGroup.Value);
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Use default arguments instead of short circuiting or conditionals</b></summary>

**Not good:**

This is not good because `breweryName` can be `NULL`.

This opinion is more understandable than the previous version, but it better controls the value of the variable.

```csharp
public void CreateMicrobrewery(string name = null)
{
    var breweryName = !string.IsNullOrEmpty(name) ? name : "XYZ Tech Co.";
    // ...
}
```

:white_check_mark: **Good:**

```csharp
public void CreateMicrobrewery(string breweryName = "XYZ Tech Co.")
{
    // ...
}
```

**[⬆ back to top](#table-of-contents)**

</details>

## Functions

<details>
  <summary><b>Avoid side effects</b></summary>

A function produces a side effect if it does anything other than take a value in and return another value or values. A side effect could be writing to a file, modifying some global variable, or accidentally wiring all your money to a stranger.

Now, you do need to have side effects in a program on occasion. Like the previous example, you might need to write to a file. What you want to do is to centralize where you are doing this. Don't have several functions and classes that write to a particular file. Have one service that does it. One and only one.

The main point is to avoid common pitfalls like sharing state between objects without any structure, using mutable data types that can be written to by anything, and not centralizing where your side effects occur. If you can do this, you will be happier
than the vast majority of other programmers.

❌ **Bad:**

```csharp
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
var name = "Tonny Stark";

public void SplitAndEnrichFullName()
{
    var temp = name.Split(" ");
    name = $"His first name is {temp[0]}, and his last name is {temp[1]}"; // side effect
}

SplitAndEnrichFullName();

Console.WriteLine(name); // His first name is Tonny, and his last name is Stark
```

:white_check_mark: **Good:**

```csharp
public string SplitAndEnrichFullName(string name)
{
    var temp = name.Split(" ");
    return $"His first name is {temp[0]}, and his last name is {temp[1]}";
}

var name = "Tonny Stark";
var fullName = SplitAndEnrichFullName(name);

Console.WriteLine(name); // Tonny Stark
Console.WriteLine(fullName); // His first name is Tonny, and his last name is Stark
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid negative conditionals</b></summary>

❌ **Bad:**

```csharp
public bool IsDOMNodeNotPresent(string node)
{
    // ...
}

if (!IsDOMNodeNotPresent(node))
{
    // ...
}
```

:white_check_mark: **Good:**

```csharp
public bool IsDOMNodePresent(string node)
{
    // ...
}

if (IsDOMNodePresent(node))
{
    // ...
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid conditionals</b></summary>

This seems like an impossible task. Upon first hearing this, most people say, "how am I supposed to do anything without an `if` statement?" The answer is that you can use polymorphism to achieve the same task in many cases. The second question is usually, "well that's great but why would I want to do that?" The answer is a previous clean code concept we learned: a function should only do
one thing. When you have classes and functions that have `if` statements, you are telling your user that your function does more than one thing. Remember, just do one thing.

❌ **Bad:**

```csharp
class Airplane
{
    // ...

    public double GetCruisingAltitude()
    {
        switch (_type)
        {
            case '777':
                return GetMaxAltitude() - GetPassengerCount();
            case 'Air Force One':
                return GetMaxAltitude();
            case 'Cessna':
                return GetMaxAltitude() - GetFuelExpenditure();
        }
    }
}
```

:white_check_mark: **Good:**

```csharp
interface IAirplane
{
    // ...

    double GetCruisingAltitude();
}

class Boeing777 : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetPassengerCount();
    }
}

class AirForceOne : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude();
    }
}

class Cessna : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetFuelExpenditure();
    }
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid type-checking (part 1)</b></summary>

❌ **Bad:**

```csharp
public Path TravelToDelhi(object vehicle)
{
    if (vehicle.GetType() == typeof(Bicycle))
    {
        (vehicle as Bicycle).PeddleTo(new Location("delhi"));
    }
    else if (vehicle.GetType() == typeof(Car))
    {
        (vehicle as Car).DriveTo(new Location("delhi"));
    }
}
```

:white_check_mark: **Good:**

```csharp
public Path TravelToDelhi(Traveler vehicle)
{
    vehicle.TravelTo(new Location("delhi"));
}
```

or

```csharp
// pattern matching
public Path TravelToDelhi(object vehicle)
{
    if (vehicle is Bicycle bicycle)
    {
        bicycle.PeddleTo(new Location("delhi"));
    }
    else if (vehicle is Car car)
    {
        car.DriveTo(new Location("delhi"));
    }
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid type-checking (part 2)</b></summary>

❌ **Bad:**

```csharp
public int Combine(dynamic val1, dynamic val2)
{
    int value;
    if (!int.TryParse(val1, out value) || !int.TryParse(val2, out value))
    {
        throw new Exception('Must be of type Number');
    }

    return val1 + val2;
}
```

:white_check_mark: **Good:**

```csharp
public int Combine(int val1, int val2)
{
    return val1 + val2;
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Avoid flags in method parameters</b></summary>

A flag indicates that the method has more than one responsibility. It is best if the method only has a single responsibility. Split the method into two if a boolean parameter adds multiple responsibilities to the method.

❌ **Bad:**

```csharp
public void CreateFile(string name, bool temp = false)
{
    if (temp)
    {
        Touch("./temp/" + name);
    }
    else
    {
        Touch(name);
    }
}
```

:white_check_mark: **Good:**

```csharp
public void CreateFile(string name)
{
    Touch(name);
}

public void CreateTempFile(string name)
{
    Touch("./temp/"  + name);
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Don't write to global functions</b></summary>

Polluting globals is a bad practice in many languages because you could clash with another library and the user of your API would be none-the-wiser until they get an exception in production. Let's think about an example: what if you wanted to have configuration array.
You could write global function like `Config()`, but it could clash with another library that tried to do the same thing.

❌ **Bad:**

```csharp
public Dictionary<string, string> Config()
{
    return new Dictionary<string,string>(){
        ["foo"] = "bar"
    };
}
```

:white_check_mark: **Good:**

```csharp
class Configuration
{
    private Dictionary<string, string> _configuration;

    public Configuration(Dictionary<string, string> configuration)
    {
        _configuration = configuration;
    }

    public string[] Get(string key)
    {
        return _configuration.ContainsKey(key) ? _configuration[key] : null;
    }
}
```

Load configuration and create instance of `Configuration` class

```csharp
var configuration = new Configuration(new Dictionary<string, string>() {
    ["foo"] = "bar"
});
```

And now you must use instance of `Configuration` in your application.

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Don't use a Singleton pattern</b></summary>

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:

1. They are generally used as a **global instance**, why is that so bad? Because **you hide the dependencies** of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a [code smell](https://en.wikipedia.org/wiki/Code_smell).
2. They violate the [single responsibility principle](#single-responsibility-principle-srp): by virtue of the fact that **they control their own creation and lifecycle**.
3. They inherently cause code to be tightly [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). This makes faking them out under **test rather difficult** in many cases.
4. They carry state around for the lifetime of the application. Another hit to testing since **you can end up with a situation where tests need to be ordered** which is a big no for unit tests. Why? Because each unit test should be independent from the other.

There is also very good thoughts by [Misko Hevery](http://misko.hevery.com/about/) about the [root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

❌ **Bad:**

```csharp
class DBConnection
{
    private static DBConnection _instance;

    private DBConnection()
    {
        // ...
    }

    public static GetInstance()
    {
        if (_instance == null)
        {
            _instance = new DBConnection();
        }

        return _instance;
    }

    // ...
}

var singleton = DBConnection.GetInstance();
```

:white_check_mark: **Good:**

```csharp
class DBConnection
{
    public DBConnection(IOptions<DbConnectionOption> options)
    {
        // ...
    }

    // ...
}
```

Create instance of `DBConnection` class and configure it with [Option pattern](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1).

```csharp
var options = <resolve from IOC>;
var connection = new DBConnection(options);
```

And now you must use instance of `DBConnection` in your application.

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Function arguments (2 or fewer ideally)</b></summary>

Limiting the amount of function parameters is incredibly important because it makes testing your function easier. Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument.

Zero arguments is the ideal case. One or two arguments is ok, and three should be avoided. Anything more than that should be consolidated. Usually, if you have more than two arguments then your function is trying to do too much. In cases where it's not, most of the time a higher-level object will suffice as an argument.

❌ **Bad:**

```csharp
public void CreateMenu(string title, string body, string buttonText, bool cancellable)
{
    // ...
}
```

:white_check_mark: **Good:**

```csharp
public class MenuConfig
{
    public string Title { get; set; }
    public string Body { get; set; }
    public string ButtonText { get; set; }
    public bool Cancellable { get; set; }
}

var config = new MenuConfig
{
    Title = "Foo",
    Body = "Bar",
    ButtonText = "Baz",
    Cancellable = true
};

public void CreateMenu(MenuConfig config)
{
    // ...
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Functions should do one thing</b></summary>

This is by far the most important rule in software engineering. When functions do more than one thing, they are harder to compose, test, and reason about. When you can isolate a function to just one action, they can be refactored easily and your code will read much
cleaner. If you take nothing else away from this guide other than this, you'll be ahead of many developers.

❌ **Bad:**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    foreach (var client in clients)
    {
        var clientRecord = db.Find(client);
        if (clientRecord.IsActive())
        {
            Email(client);
        }
    }
}
```

:white_check_mark: **Good:**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    var activeClients = GetActiveClients(clients);
    // Do some logic
}

public List<Client> GetActiveClients(string[] clients)
{
    return db.Find(clients).Where(s => s.Status == "Active");
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Function names should say what they do</b></summary>

❌ **Bad:**

```csharp
public class Email
{
    //...

    public void Handle()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
message.Handle();
```

:white_check_mark: **Good:**

```csharp
public class Email
{
    //...

    public void Send()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// Clear and obvious
message.Send();
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Functions should only be one level of abstraction</b></summary>

> Not finished yet

When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

❌ **Bad:**

```csharp
public string ParseBetterJSAlternative(string code)
{
    var regexes = [
        // ...
    ];

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            // ...
        }
    }

    var ast = new string[] {};
    foreach (var token in tokens)
    {
        // lex...
    }

    foreach (var node in ast)
    {
        // parse...
    }
}
```

**Bad too:**

We have carried out some of the functionality, but the `ParseBetterJSAlternative()` function is still very complex and not testable.

```csharp
public string Tokenize(string code)
{
    var regexes = new string[]
    {
        // ...
    };

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            tokens[] = /* ... */;
        }
    }

    return tokens;
}

public string Lexer(string[] tokens)
{
    var ast = new string[] {};
    foreach (var token in tokens)
    {
        ast[] = /* ... */;
    }

    return ast;
}

public string ParseBetterJSAlternative(string code)
{
    var tokens = Tokenize(code);
    var ast = Lexer(tokens);
    foreach (var node in ast)
    {
        // parse...
    }
}
```

:white_check_mark: **Good:**

The best solution is move out the dependencies of `ParseBetterJSAlternative()` function.

```csharp
class Tokenizer
{
    public string Tokenize(string code)
    {
        var regexes = new string[] {
            // ...
        };

        var statements = explode(" ", code);
        var tokens = new string[] {};
        foreach (var regex in regexes)
        {
            foreach (var statement in statements)
            {
                tokens[] = /* ... */;
            }
        }

        return tokens;
    }
}

class Lexer
{
    public string Lexify(string[] tokens)
    {
        var ast = new[] {};
        foreach (var token in tokens)
        {
            ast[] = /* ... */;
        }

        return ast;
    }
}

class BetterJSAlternative
{
    private string _tokenizer;
    private string _lexer;

    public BetterJSAlternative(Tokenizer tokenizer, Lexer lexer)
    {
        _tokenizer = tokenizer;
        _lexer = lexer;
    }

    public string Parse(string code)
    {
        var tokens = _tokenizer.Tokenize(code);
        var ast = _lexer.Lexify(tokens);
        foreach (var node in ast)
        {
            // parse...
        }
    }
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Function callers and callees should be close</b></summary>

If a function calls another, keep those functions vertically close in the source file. Ideally, keep the caller right above the callee. We tend to read code from top-to-bottom, like a newspaper. Because of this, make your code read that way.

❌ **Bad:**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    public ManagerData GetManagerReview()
    {
        var manager = LookupManager();
    }

    public EmployeeData GetSelfReview()
    {
        // ...
    }
}

var  review = new PerformanceReview(employee);
review.PerfReview();
```

:white_check_mark: **Good:**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData GetManagerReview()
    {
        var manager = LookupManager();
        return manager;
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private EmployeeData GetSelfReview()
    {
        // ...
    }
}

var review = new PerformanceReview(employee);
review.PerfReview();
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Encapsulate conditionals</b></summary>

❌ **Bad:**

```csharp
if (article.state == "published")
{
    // ...
}
```

:white_check_mark: **Good:**

```csharp
if (article.IsPublished())
{
    // ...
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Remove dead code</b></summary>

Dead code is just as bad as duplicate code. There's no reason to keep it in your codebase. If it's not being called, get rid of it! It will still be safe in your version history if you still need it.

❌ **Bad:**

```csharp
public void OldRequestModule(string url)
{
    // ...
}

public void NewRequestModule(string url)
{
    // ...
}

var request = NewRequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

:white_check_mark: **Good:**

```csharp
public void RequestModule(string url)
{
    // ...
}

var request = RequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

**[⬆ back to top](#table-of-contents)**

</details>

## Objects and Data Structures

<details>
  <summary><b>Use getters and setters</b></summary>

In C# / VB.NET you can set `public`, `protected` and `private` keywords for methods.
Using it, you can control properties modification on an object.

- When you want to do more beyond getting an object property, you don't have to look up and change every accessor in your codebase.
- Makes adding validation simple when doing a `set`.
- Encapsulates the internal representation.
- Easy to add logging and error handling when getting and setting.
- Inheriting this class, you can override default functionality.
- You can lazy load your object's properties, let's say getting it from a server.

Additionally, this is part of Open/Closed principle, from object-oriented design principles.

❌ **Bad:**

```csharp
class BankAccount
{
    public double Balance = 1000;
}

var bankAccount = new BankAccount();

// Fake buy shoes...
bankAccount.Balance -= 100;
```

:white_check_mark: **Good:**

```csharp
class BankAccount
{
    private double _balance = 0.0D;

    pubic double Balance {
        get {
            return _balance;
        }
    }

    public BankAccount(balance = 1000)
    {
       _balance = balance;
    }

    public void WithdrawBalance(int amount)
    {
        if (amount > _balance)
        {
            throw new Exception('Amount greater than available balance.');
        }

        _balance -= amount;
    }

    public void DepositBalance(int amount)
    {
        _balance += amount;
    }
}

var bankAccount = new BankAccount();

// Buy shoes...
bankAccount.WithdrawBalance(price);

// Get balance
balance = bankAccount.Balance;
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Make objects have private/protected members</b></summary>

❌ **Bad:**

```csharp
class Employee
{
    public string Name { get; set; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("Dr. Strange");
Console.WriteLine(employee.Name); // Employee name: Dr. Strange
```

:white_check_mark: **Good:**

```csharp
class Employee
{
    public string Name { get; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("Dr. Strange");
Console.WriteLine(employee.Name); // Employee name: Dr. Strange
```

**[⬆ back to top](#table-of-contents)**

</details>

## Formatting

<details>
  <summary><b>Uses <i>.editorconfig</i> file</b></summary>

❌ **Bad:**

Has many code formatting styles in the project. For example, indent style is `space` and `tab` mixed in the project.

:white_check_mark: **Good:**

Define and maintain consistent code style in your codebase with the use of an `.editorconfig` file

```csharp
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# C# files
[*.cs]
indent_size = 4
# New line preferences
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_within_query_expression_clauses = true

# Code files
[*.{cs,csx,vb,vbx}]
indent_size = 4

# Indentation preferences
csharp_indent_block_contents = true
csharp_indent_braces = false
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = one_less_than_current

# avoid this. unless absolutely necessary
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion

# only use var when it's obvious what the variable type is
# csharp_style_var_for_built_in_types = false:none
# csharp_style_var_when_type_is_apparent = false:none
# csharp_style_var_elsewhere = false:suggestion

# use language keywords instead of BCL types
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion

# name all constant fields using PascalCase
dotnet_naming_rule.constant_fields_should_be_pascal_case.severity = suggestion
dotnet_naming_rule.constant_fields_should_be_pascal_case.symbols  = constant_fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.style    = pascal_case_style

dotnet_naming_symbols.constant_fields.applicable_kinds   = field
dotnet_naming_symbols.constant_fields.required_modifiers = const

dotnet_naming_style.pascal_case_style.capitalization = pascal_case

# static fields should have s_ prefix
dotnet_naming_rule.static_fields_should_have_prefix.severity = suggestion
dotnet_naming_rule.static_fields_should_have_prefix.symbols  = static_fields
dotnet_naming_rule.static_fields_should_have_prefix.style    = static_prefix_style

dotnet_naming_symbols.static_fields.applicable_kinds   = field
dotnet_naming_symbols.static_fields.required_modifiers = static

dotnet_naming_style.static_prefix_style.required_prefix = s_
dotnet_naming_style.static_prefix_style.capitalization = camel_case

# internal and private fields should be _camelCase
dotnet_naming_rule.camel_case_for_private_internal_fields.severity = suggestion
dotnet_naming_rule.camel_case_for_private_internal_fields.symbols  = private_internal_fields
dotnet_naming_rule.camel_case_for_private_internal_fields.style    = camel_case_underscore_style

dotnet_naming_symbols.private_internal_fields.applicable_kinds = field
dotnet_naming_symbols.private_internal_fields.applicable_accessibilities = private, internal

dotnet_naming_style.camel_case_underscore_style.required_prefix = _
dotnet_naming_style.camel_case_underscore_style.capitalization = camel_case

# Code style defaults
dotnet_sort_system_directives_first = true
csharp_preserve_single_line_blocks = true
csharp_preserve_single_line_statements = false

# Expression-level preferences
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion

# Expression-bodied members
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:none
csharp_style_expression_bodied_indexers = true:none
csharp_style_expression_bodied_accessors = true:none

# Pattern matching
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
csharp_style_inlined_variable_declaration = true:suggestion

# Null checking preferences
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = true:suggestion

# Space preferences
csharp_space_after_cast = false
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_after_comma = true
csharp_space_after_dot = false
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_after_semicolon_in_for_statement = true
csharp_space_around_binary_operators = before_and_after
csharp_space_around_declaration_statements = do_not_ignore
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_before_comma = false
csharp_space_before_dot = false
csharp_space_before_open_square_brackets = false
csharp_space_before_semicolon_in_for_statement = false
csharp_space_between_empty_square_brackets = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_parameter_list_parentheses = false
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_declaration_name_and_open_parenthesis = false
csharp_space_between_method_declaration_parameter_list_parentheses = false
csharp_space_between_parentheses = false
csharp_space_between_square_brackets = false

[*.{asm,inc}]
indent_size = 8

# Xml project files
[*.{csproj,vcxproj,vcxproj.filters,proj,nativeproj,locproj}]
indent_size = 2

# Xml config files
[*.{props,targets,config,nuspec}]
indent_size = 2

[CMakeLists.txt]
indent_size = 2

[*.cmd]
indent_size = 2

```

**[⬆ back to top](#table-of-contents)**

</details>

## Comments

<details>
  <summary><b>Avoid positional markers</b></summary>

They usually just add noise. Let the functions and variable names along with the proper indentation and formatting give the visual structure to your code.

❌ **Bad:**

```csharp
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
void Actions()
{
    // ...
};
```

❌ **Bad:**

```csharp

#region Scope Model Instantiation

var model = {
    menu: 'foo',
    nav: 'bar'
};

#endregion

#region Action setup

void Actions() {
    // ...
};

#endregion
```

:white_check_mark: **Good:**

```csharp
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

void Actions()
{
    // ...
};
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Don't leave commented out code in your codebase</b></summary>

Version control exists for a reason. Leave old code in your history.

❌ **Bad:**

```csharp
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

:white_check_mark: **Good:**

```csharp
doStuff();
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Don't have journal comments</b></summary>

Remember, use version control! There's no need for dead code, commented code, and especially journal comments. Use `git log` to get history!

❌ **Bad:**

```csharp
/**
 * 2018-12-20: Removed monads, didn't understand them (RM)
 * 2017-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
public int Combine(int a,int b)
{
    return a + b;
}
```

:white_check_mark: **Good:**

```csharp
public int Combine(int a,int b)
{
    return a + b;
}
```

**[⬆ back to top](#table-of-contents)**

</details>

<details>
  <summary><b>Only comment things that have business logic complexity</b></summary>

Comments are an apology, not a requirement. Good code _mostly_ documents itself.

❌ **Bad:**

```csharp
public int HashIt(string data)
{
    // The hash
    var hash = 0;

    // Length of string
    var length = data.length;

    // Loop through every character in data
    for (var i = 0; i < length; i++)
    {
        // Get character code.
        const char = data.charCodeAt(i);
        // Make the hash
        hash = ((hash << 5) - hash) + char;
        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

❌ **Better but still Bad:**

```csharp
public int HashIt(string data)
{
    var hash = 0;
    var length = data.length;
    for (var i = 0; i < length; i++)
    {
        const char = data.charCodeAt(i);
        hash = ((hash << 5) - hash) + char;

        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

If a comment explains WHAT the code is doing, it is probably a useless comment and can be implemented with a well named variable or function. The comment in the previous code could be replaced with a function named `ConvertTo32bitInt` so this comment is still useless.
However it would be hard to express by code WHY the developer chose djb2 hash algorithm instead of sha-1 or another hash function. In that case a comment is acceptable.

:white_check_mark: **Good:**

```csharp
public int Hash(string data)
{
    var hash = 0;
    var length = data.length;

    for (var i = 0; i < length; i++)
    {
        var character = data[i];
        // use of djb2 hash algorithm as it has a good compromise
        // between speed and low collision with a very simple implementation
        hash = ((hash << 5) - hash) + character;

        hash = ConvertTo32BitInt(hash);
    }
    return hash;
}

private int ConvertTo32BitInt(int value)
{
    return value & value;
}
```

**[⬆ back to top](#table-of-contents)**

</details>

# License

To the extent possible under law, [ajaysingh](https://github.com/ajaysingh853) has waived all copyright and related or neighboring rights to this work.
