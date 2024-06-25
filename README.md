# UnitTest
Unit testing is a software testing method where individual units or components of a software are tested independently to ensure they function correctly. This involves testing small pieces of code, typically individual functions or methods. Following are few characteristics:

* **Isolation**: Units are tested independently to ensure that they work correctly in isolation. Dependencies are often mocked or stubbed to simulate interactions.
* **Automation**: Unit tests are typically automated, allowing them to be run frequently and consistently without manual intervention.
* **Repeatability**: Unit tests can be executed repeatedly with the same input data to verify that the software behaves consistently.
* **Speed**: Unit tests are generally fast to execute, providing quick feedback to developers about the correctness of the code.
* **Granularity**: Tests focus on small, specific parts of the code, allowing developers to pinpoint issues precisely.

![image](https://github.com/manaskumarm/UnitTest/assets/14363425/7b96476b-bc5e-4464-8e39-4373dbe11857)

# Advantages
* Early Bug Detection: Helps in finding bugs early in the development cycle, making them easier and cheaper to fix.
* Improved Code Quality: Enhances code quality by identifying issues early and promoting modular programming.
* Better Team Communication: Provides a clear and concise way for team members to discuss code, thereby enhancing team communication.

# Disadvantages
* Increased Development Time: Unit testing can increase the initial development time due to the need to write tests alongside the code.
* Potential Overhead: Requires additional effort to set up and maintain test suites, which can add overhead to the development process.

There are different types of Unit test frameworks available like NUnit, XUnit and MSTest. You can choose one of them based on your requirement(we discuss about MSTest and NUnit).

# Framework 1: MSTest
 Here are the few attributes of MSTest framework:
* [TestInitialize]	Marks a method that should be called before each test method. One such method should be present before each test class.
* [TestCleanup]	Marks a method that should be called after each test method. One such method should be present before each test class.
* [TestClass]	Marks a class that contains tests.
* [TestMethod]	Marks the method, i.e., the actual test case in the test class.
* [DataRow]	Allows setting the values of the parameters of the tests. Multiple [DataRow] annotations can be present in the code.
* [DataTestMethod]	It has the same functionality as the [TestMethod] attribute except that it is used when the [DataRow] attribute is used.
* [AssemblyInitialize]	Marks the method that should be called once before the execution of any method in the assembly code.
* [AssemblyCleanup]	Marks the method that should be called once after the execution of any method in the assembly code.
* [Ignore]	Marks a test method or test class that should be considered for execution, i.e., it is ignored.
* [TestCategory]	Specify the category for the test.
* [ClassInitialize]	Methods that will be called only once before executing any of the test methods present in that class.
* [ClassCleanup]	Methods that will be called only once after executing the test methods present in that class.

# Code
```
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace MyProject.Tests
{
    [TestClass]
    public class MyMathTests
    {
        [TestMethod]
        public void TestAddition()
        {
            // Arrange
            int a = 5;
            int b = 7;
            int expected = 12;

            // Act
            int result = MyMath.Add(a, b);

            // Assert
            Assert.AreEqual(expected, result);
        }
    }
}
```
# Moq
In software testing terms, involves creating dummy objects based upon your application's real objects and then using those dummy objects to simulate the behavior of your real objects in various conditions. It allows you to mimic dependencies that your code may have, allowing you to control their behavior in order to better test the functionality of the object you are testing. **Moq** is a popular mocking framework in C# which allows developers to create mock objects for dependencies in their unit tests. Moq can be used to mock both classes and interfaces. Here's why Moq is needed and its significance:

**Mocking Dependencies**: Moq enables developers to create mock implementations of dependencies, such as databases, external services, or other components, without needing to rely on their actual implementations.

**Improved Test Readability and Maintainability**: By using Moq, developers can write unit tests that are more readable and maintainable(expressive and concise test code).

**Verification of Method Calls**: Moq provides capabilities for verifying whether specific methods or properties of mocked objects were called during the test execution. This ensures that the code under test interacts correctly with its dependencies

To use Moq, you need to install it. Go to "Tools" -> "Nuget Package Manager" -> "Package Manager Console" -> "Install-Package Moq".
```
using Moq;
using NUnit.Framework;

[TestFixture]
public class MyServiceTests
{
    [Test]
    public void MyService_GetData_Success()
    {
        // Arrange
        var mockRepository = new Mock<IRepository>();
        mockRepository.Setup(repo => repo.GetData()).Returns("Mocked data");
        
        var myService = new MyService(mockRepository.Object);

        // Act
        var result = myService.GetData();

        // Assert
        Assert.AreEqual("Mocked data", result);
    }
}

public interface IRepository
{
    string GetData();
}

public class MyService
{
    private readonly IRepository _repository;

    public MyService(IRepository repository)
    {
        _repository = repository;
    }

    public string GetData()
    {
        return _repository.GetData();
    }
}
```
# Best Practices
* TestContext.WriteLine('');
* Use constants instead of hardcode
* create .runsettings to hold test params
* Log unittest using trx and html file for future analysyis(using Logger in .runsettings file)
* Use TestBase class for common func
* DataRow, DataDynamic for data driven
* Use StringAssert for more string operation like Regex, Use StringAssert.Contains("test", "te");
# Framework 2: NUnit
**NUnit** is a popular open-source unit testing framework for C#. It is ported from the JUnit framework and is used for the development and execution of tests with the .NET language. NUnit facilitates batch execution of tests through the console runner (nunit-console.exe). It’s widely used in the .NET ecosystem to ensure code quality and reliability by writing and running automated tests. You can run test parallely using following options in NUnit:

* _ParallelScope.Self_: The test itself may run in parallel with other tests.
* _ParallelScope.Children_: Child tests may run in parallel with one another.
* _ParallelScope.Fixtures_: Fixtures (test classes) may run in parallel with one another.
* _ParallelScope.All_: The test and its descendants may run in parallel with others at the same level.

```
[Parallelizable(ParallelScope.Self)]
[TestFixture]
public class MyService_IsPrimeShould
{
    private MyService _myService;

    [SetUp]
    public void SetUp()
    {
        _myService = new MyService();
    }

    [Test]
    public void IsPrime_InputIs1_ReturnFalse()
    {
        var result = _myService.IsPrime(1);

        Assert.That(result, Is.False, "1 should not be prime");
    }
    
    // For different inputs
    [TestCase(2)]
    [TestCase(9)]
    [TestCase(1)]
    public void IsPrime_ValuesLessThan_ReturnFalse(int value)
    {
        var result = _myService?.IsPrime(value);

        Assert.That(result, Is.False, $"{value} should not be prime");
    }
    
    [Test]
    public void MethodThatThrowsArgumentException_ShouldThrowArgumentException()
    {
        // Arrange
        var sample = new SampleClass();

        // Act & Assert
        var ex = Assert.Throws<ArgumentException>(() => sample.MethodThatThrowsArgumentException());

        // Additional asserts on the exception if needed
        Assert.AreEqual("Invalid argument.", ex.Message);
    }
}
```
# Assertions
* _Assert.AreEqual()_ - Contains same objects in same order.
* _Assert.AreEquivalent()_ - Contains same objects in any order.

**Fluent Assertions** is a powerful library for enhancing unit tests in C# with expressive and concise assertions.
```
IEnumerable<int> numbers = new[] { 1, 2, 3 };
numbers.Should().OnlyContain(n => n > 0);
numbers.Should().HaveCount(4, "because we thought we put four items in the collection");
```
# Code Coverage
**Coverlet** is a cross-platform code coverage tool for .NET, and coverlet.collector is a data collector extension for the Visual Studio Test Platform. It integrates with dotnet test and allows you to collect code coverage data during test execution.

Installation (coverlet.collector)
dotnet add package coverlet.collector

Coverlet is integrated into the Visual Studio Test Platform as a data collector. To get coverage simply run the following command:
dotnet test --collect:"XPlat Code Coverage"

dotnet tool install -g dotnet-reportgenerator-globaltool

reportgenerator -reports:./TestResults/**/*.xml -targetdir:./coverage-report -reporttypes:Html

or 

dotnet tool install -g dotnet-coverage
dotnet tool install -g dotnet-reportgenerator-globaltool

# Conclusion
Unit testing plays a vital role in ensuring the reliability and quality of software applications. While it offers numerous advantages such as early bug detection and improved code quality, developers must also be mindful of potential drawbacks like increased development time and overhead. By incorporating unit testing into the development workflow, teams can build robust and maintainable software products that meet the highest standards of quality and reliability.
