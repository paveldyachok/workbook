### Уточнение типа

Для проверки передачи массива в функцию

```php
function foo(array $var) {} // Ожидается только массив
```

С PHP 5.4 можно указать уточнение **callable **

```php
function bar(callable $var, $arg) {
    return $var($arg);
}
```

С PHP 7 можно уточнять скалярные типы

```php
function foo(int $i, string $s, bool $b, int ...$nums):bool {}

// int ...$nums - означает что все последующие переменные должны быть типом int
// :bool - тип возвращаемого значения.
```



