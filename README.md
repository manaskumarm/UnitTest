# UnitTest
Unit testing is a software testing method where individual units or components of a software are tested independently to ensure they function correctly. This involves testing small pieces of code, typically individual functions or methods.

![image](https://github.com/manaskumarm/UnitTest/assets/14363425/7b96476b-bc5e-4464-8e39-4373dbe11857)

# Advantages
Early Bug Detection: Helps in finding bugs early in the development cycle, making them easier and cheaper to fix.
Improved Code Quality: Enhances code quality by identifying issues early and promoting modular programming.
Better Team Communication: Provides a clear and concise way for team members to discuss code, thereby enhancing team communication.

# Disadvantages
Increased Development Time: Unit testing can increase the initial development time due to the need to write tests alongside the code.
Potential Overhead: Requires additional effort to set up and maintain test suites, which can add overhead to the development process.

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

# Best Practices
* TestContext.WriteLine('');
* Use constants instead of hardcode
* create .runsettings to hold test params
* Log unittest using trx and html file for future analysyis(using Logger in .runsettings file)
* Use TestBase class for common func
* DataRow, DataDynamic for data driven
* Use StringAssert for more string operation like Regex, Use StringAssert.Contains("test", "te");

# Conclusion
Unit testing plays a vital role in ensuring the reliability and quality of software applications. While it offers numerous advantages such as early bug detection and improved code quality, developers must also be mindful of potential drawbacks like increased development time and overhead. By incorporating unit testing into the development workflow, teams can build robust and maintainable software products that meet the highest standards of quality and reliability.
