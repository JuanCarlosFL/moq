# moq

- Martin Fowler defines a test double as a generic term for any case where you replace a production object for testing purposes, so, for example, replacing a real API call with a test version. Let's take a look at these terms in more detail. First up, we've got fakes. Fakes provide a working implementation of the dependency. The working implementation, however, is not suitable for production use. It's purely for testing purposes. So, for example, the Entity Framework Core in‑memory provider is an example of a fake. Dummies, on the other hand, are passed around like real implementations, but they're never accessed or used. We use dummies to satisfy parameters, for example the parameter of a method where we can't provide null. Stubs, on the other hand, can provide answers to calls. So the production code we're testing can call into a stubbed dependency, and this stub will provide answers to the code we're testing. These answers could come in the form of property gets and method return values. Next up, we've got mocks. Mocks allow us to expect and verify that specific calls were made by the production code. For example, we can test that the production code accessed a mock property or called a mock method. Moq allows us to create test doubles that act as dummies, stubs, and mocks. In this course, we're going to be using the general term mock object. We're not going to be differentiating between dummies, stubs, and mocks.

- test double -->  término genérico para cualquier caso en el que se sustituye un objeto de producción con fines de prueba, así, por ejemplo, la sustitución de una llamada a la API real con una versión de prueba.

- Fake --> roporcionan una implementación funcional de la dependencia. La implementación de trabajo, sin embargo, no es adecuada para su uso en producción. Es puramente para propósitos de prueba. Así, por ejemplo, the Entity Framework Core in‑memory provider es un ejemplo de fake.

- Dummies --> se pasan como implementaciones reales, pero nunca se accede a ellos ni se utilizan. Utilizamos los dummies para satisfacer parámetros, por ejemplo el parámetro de un método donde no podemos proporcionar null. 

- Stubs --> pueden proporcionar respuestas a las llamadas. Así que el código de producción que estamos probando puede llamar a una dependencia stubbed, y este stub proporcionará respuestas al código que estamos probando. Estas respuestas podrían venir en forma de propiedades y valores de retorno de métodos.

- Mocks --> nos permiten esperar y verificar que el código de producción realice determinadas llamadas. Por ejemplo, podemos probar que el código de producción accedió a una propiedad mock o llamó a un método mock. Moq nos permite crear test doubles que actúan como dummies, stubs y mocks.

Sintax of Moq:

```C#
var mockValidator = new Mock<IInterface>();

var sut = new ClassToTest(mockValidator.Object);
```

If we need to configure a Mock Object Method to return a value

```C#
mockValidator.Setup(x => x.Method("value").Returns("We want to return");
```

- We want to accept any value, range, etc.

```C#
mockValidator.Setup(x => x.Method(it.IsAny<string>())).Returns(true)

mockValidator.Setup(x => x.Method(it.Is<string>(number => number.StartsWith("y"))).Returns(true)

mockValidator.Setup(x => x.Method(it.IsRange("a", "z", Moq.Range.Inclusive))).Returns(true)

mockValidator.Setup(x => x.Method(it.IsIn("z", "y", "x"))).Returns(true)

mockValidator.Setup(x => x.Method(it.IsRegex("[a-z]"))).Returns(true)
```

Strict and Loose mode

- With strict mocking behavior, if a method has not been explicitly set up and it's called, it will throw an exception. Whereas with a loose mark, it will never throw an exception even if a mocked method called, but has not been explicitly set up. 

- Con un comportamiento de mock estricto, si un método no ha sido configurado explícitamente y es llamado, lanzará una excepción. Mientras que con una loose mark, nunca lanzará una excepción aunque se llame a un mocked method, pero que no ha sido configurado explícitamente. 

With ref params

```C#
mockRepository.Setup(x => x.Method(ref It.Ref<SearchParams>.IsAny)).Returns(-1);
```





