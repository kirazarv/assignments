https://disk.yandex.ru/i/jTXSsvJIdSTtfA        
https://disk.yandex.ru/i/xPW7bLhGaOHbSw        18лаб
https://disk.yandex.ru/i/UbBNagFUhYTkcg        16лаб


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



    ________
    namespace UnitTestProjectBankTests2
{
    [TestClass]
    public class UnitTest1
    {
        //тестирование метода Debit при вводе корректного значения параметра debitAmount
        [TestMethod]
        public void Debit_WithValidAmount_UpdatesBalance()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = 4.55;
            double expected = 7.44;
            BankAccount account = new BankAccount("Mr Bryan Walton", beginningBalance, "12345678");
            // Act
            account.Debit(debitAmount, account);
            // Assert
            double actual = account.Balance;
            Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");

        }

        //Тестирование корректности обработки исключения "amount<0" в методе Debit
        [TestMethod]
        public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = -100.00;
            BankAccount account = new BankAccount("Mr Bryan Walton", beginningBalance, "12345678");
            // Act and assert
            //            Используем метод ThrowsException для подтверждения правильности созданного
            //исключения.Этот метод приводит к тому, что тест не будет пройден, если не возникнет
            //исключения ArgumentOutOfRangeException. при debitAmount=-100 возникает исключение=> тест будет пройден
            Assert.ThrowsException<System.ArgumentOutOfRangeException>(() =>
            account.Debit(debitAmount, account ));
        }

        //Тестирование корректности обработки исключения "amount>balance" в методе Debit
        [TestMethod]
        public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
        {
            // Arrange
            double beginningBalance = 11.99;
            double debitAmount = 20.00;
            BankAccount account = new BankAccount("Mr Bryan Walton", beginningBalance, "12345678");
            // Act 
            try
            {
                account.Debit(debitAmount,account);
            }
            catch (System.ArgumentOutOfRangeException e)
            {
                //assert
                StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
                return;
            }
            Assert.Fail("The expected exception was not thrown");
        }

        //custom test №1
        //Тестирование корректности обработки исключения "invalid chars in name" при создании экземпляра класса BankAccount 
        [TestMethod]
        public void NameWithInValidChars()
        {
            // Arrange
            string name = "Ian 1@ Jake McNaughton";
            //act
           try 
           {
                BankAccount account = new BankAccount(name, 11, "12345678");
                
           }
            catch(Exception e)
           {
                //assert
                StringAssert.Contains(e.Message, BankAccount.InvalidCharactersMessage);
                return;
           }
            Assert.Fail("The expected exception was not thrown");

        }

        //custom test №2
        //Тестирование метода нахождения минимального значения на балансе
        [TestMethod]
        public void FindMin()
        {
            // Arrange
            List<double> values = new List<double> { 11.99, 1.99, 8.99, 5.99 };
            double expected = 1.99;
            BankAccount account = new BankAccount("Mr Bryan Walton", 11.99, "12345678");
            // Act
            account.Debit(10.00, account);
            account.Credit(7.00, account);
            account.Debit(3.00, account);
            account.FindMinBalance(account.balanceHistory);

            // Assert
            double actual= account.MinBalance;
            Assert.AreEqual(expected, actual, 0.001, "min balance is not found correctly");
        }

        //custom test №3
        //Тестирование метода проверки пароля на соответствие требованиям isPassValid 
        [TestMethod]
        public void PassAtLeart8CharsIsValid()
        {
            // Arrange
            string pass1 = "1234567y";
            BankAccount account=new BankAccount("Jacob Johnson",11, pass1);

            // Act
            account.isPassValid(pass1);
            bool isValid= account.IsValid;
            // Assert
            Assert.IsTrue(isValid);
        }
    }
}
