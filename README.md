https://disk.yandex.ru/i/jTXSsvJIdSTtfA        
https://disk.yandex.ru/i/xPW7bLhGaOHbSw        18лаб
https://disk.yandex.ru/i/UbBNagFUhYTkcg        16лаб

18лаб
[TestClass]
public class UnitTest1
{
    public string noException="no expected exception";

    //тестирование первого if функции Calculate с корректными числами x < 1 && c != 0
    [TestMethod]
    public void CalculateTestCorrectNumbersIf1()
    {
        // Аргументы для первого случая
        double a = 2;
        double b = 4;
        double c = 2;
        double x = 0.5;
        double expectedResult = 2.5;

        // Вызов функции и проверка результата
        double result = Calc.Calculate(a, b, c, x);
        Assert.AreEqual(expectedResult, result, "Function F result is incorrect for case 1.");
    }

    //тестирование второго if функции Calculate с корректными числами x > 1.5 && c == 0
    [TestMethod]
    public void CalculateTestCorrectNumbersIf2()
    {
        // Аргументы для второго случая
        double a = 2;
        double b = 4;
        double c = 0;
        double x = 2.5;
        double expectedResult = 0.08;

        // Вызов функции, который должен вызвать исключение
        double result = Calc.Calculate(a, b, c, x);
        Assert.AreEqual(expectedResult, result, "Function F result is incorrect for case 2.");
    }

    //тестирование третьго if функции Calculate с корректными числами при с!=0
    [TestMethod]
    public void CalculateTestCorrectNumbersIf3()
    {
        // Аргументы для третьего случая
        double a = 2;
        double b = 4;
        double c = 2;
        double x = 2;
        double expectedResult = 1;

        // Вызов функции и проверка результата
        double result = Calc.Calculate(a, b, c, x);
        Assert.AreEqual(expectedResult, result, "Function F result is incorrect for case 3.");
    }

    //тестирование выброса исключения при с=0 и x<1.5
    [TestMethod]
    public void CalculateExceptionDivideByZeroTest()
    {
        //arrange
        bool isException = false;
    
        double a = 2;
        double b = 4;
        double c = 0;
        double x = 1.3;
        
        //act and assert
        try
        {
            // Вызов функции, который должен вызвать исключение
            double result = Calc.Calculate(a, b, c, x);
        }
        catch (DivideByZeroException)
        {
            isException = true;
        }
        Assert.IsTrue(isException,noException);         
    }

    //второй вариант тестирование выброса исключения при с=0 и x<1.5
    [TestMethod]
    public void ThrowsExceptionDivideByZeroTest()
    {
        // Аргументы для теста
        double a = 1.0;
        double b = 2.0;
        double c = 0.0;
        double x = 1.2;

        // Проверка ожидаемого исключения
        Assert.ThrowsException<DivideByZeroException>(() => Calc.Calculate(a, b, c, x));
    }
       
