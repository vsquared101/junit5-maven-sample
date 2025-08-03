# Getting Started

### Reference Documentation
https://assertj.github.io/doc/

### String assertions with AssertJ
```java
@Test
void shouldShowStringRelatedAssertionsAvailableInAssertJ() {
    Employee emp1 = new Employee("John Doe", "john@gmail.com", 23);
    assertThat(emp1.getName()).isNotNull();
    assertThat(emp1.getName()).isNotBlank();
    assertThat(emp1.getName()).isEqualTo("John Doe");
    assertThat(emp1.getName()).startsWith("John");
    assertThat(emp1.getName()).startsWithIgnoringCase("john");
    assertThat(emp1.getName()).endsWithIgnoringCase("Doe");
    assertThat(emp1.getName()).startsWithIgnoringCase("john").endsWithIgnoringCase("doe");

    assertThat(emp1.getEmail()).startsWith("john");
    assertThat(emp1.getEmail()).endsWith("gmail.com");
    assertThat(emp1.getEmail()).startsWith("john").endsWith("gmail.com");
}
```

### Numeric assertions with AssertJ
```java
@Test
void shouldShowNumericAssertionsAvailableInAssertJ() {
    Employee emp1 = new Employee("Jane Doe", "jane.doe@gmail.com", 27);
    assertThat(emp1.getAge()).isEqualTo(27);
    assertThat(emp1.getAge()).isGreaterThanOrEqualTo(25);
    assertThat(emp1.getAge()).isLessThan(30);
    assertThat(emp1.getAge()).isGreaterThan(25).isLessThan(30);
}
```

### AssertJ assertions for exception use-case
```java
@Test
void shouldThrowExceptionForNegativeAge() {
    assertThatThrownBy(() -> new Employee("Jack Doe", "jack.doe@gmail.com", -10))
            .isInstanceOf(RuntimeException.class)
            .hasMessageContaining("Invalid age")
            .hasMessage("Invalid age!");
}
```

### AssertJ assertions for object comparisons
```java
@Test
void shouldBeAbleToCompareItemsOfSameType() {
    Employee emp1 = new Employee("Jill", "jill@gmail.com", 30);
    Employee emp2 = new Employee("Jill", "jill@gmail.com", 25);
    Employee emp3 = new Employee("Jill", "jill@gmail.com", 30);

    assertThat(emp1)
            .usingRecursiveComparison()
            .ignoringFields("age")
            .isEqualTo(emp2);

    assertThat(emp1)
            .usingRecursiveComparison()
            .comparingOnlyFields("name", "email")
            .isEqualTo(emp2);

    assertThat(emp1)
            .usingRecursiveComparison()
            .isEqualTo(emp3);
}
```

### AssertJ object and list comparison examples
```java
@Test
void shouldBeAbleToCompareIndividualItemAgainstListOfItems() throws Exception {
    List<Employee> employees = List.of(new Employee("Jill", "jill@gmail.com", 31),
            new Employee("Jane", "jane@gmail.com", 25),
            new Employee("Jack", "jack@gmail.com", 27));

    Employee emp1 = new Employee("Jack", "jack@gmail.com", 30);
    Employee emp2 = new Employee("Jane", "jane@gmail.com", 25);

    assertThat(employees).doesNotContain(emp1);
    assertThat(employees).contains(emp2);

    assertThat(emp1)
            .usingRecursiveComparison()
            .ignoringFields("age")
            .isIn(employees);

    assertThat(emp1)
            .usingRecursiveComparison()
            .comparingOnlyFields("name","email")
            .isIn(employees);

    assertThat(employees).hasSize(3).contains(emp2).doesNotContain(emp1);
}
```

