# Dart OOP Assignment: Kigali Bus Card

**Name:** Ikirezi drocas  
**Student ID:** 26932

## My numbers
- D = 32, L = 2
- Starting balance = 1320 RWF
- Bus fare = 232 RWF
- Student discount = 12%

## Output of main.dart
```
Owner: Ikirezi drocas | Balance: 1320 RWF
Error: name too short
Owner: Ikirezi drocas | Balance: 1320 RWF
Owner: Ikirezi drocas | Balance: 1320 RWF
Error: top-up must be 500 to 50000 RWF
Topped up 2000 RWF
Paid 232 RWF
Paid 232 RWF
Owner: Ikirezi drocas | Balance: 856 RWF
Student discount: 27 RWF
Paid 205 RWF
Owner: Ikirezi drocas | Balance: 1093 RWF
Student card: 12% off
```

## Part 1: Why no setter for balance?
A balance setter would let anyone change the card balance directly without checking the rules. By keeping balance private with only a getter, the balance can only change through `topUp` and `pay`, which enforce the top-up limits (500 to 50000 RWF) and make sure you cannot pay more than you have. This protects the card from invalid or cheating changes.

## Part 2: What does ~/ do?
`~/` is integer division. It divides and throws away the remainder, returning an `int`.
- `print(237 * 17 / 100);` prints `40.29` (a double, keeps the decimal).
- `print(237 * 17 ~/ 100);` prints `40` (an integer, the remainder is dropped).

## Part 4: Bug table

| Bug | The line | Why it is wrong (your words) | Your fix |
|-----|----------|------------------------------|----------|
| 1 | `String _brand;` and `int _battery;` | The fields have no starting value, so Dart complains they are not initialized. | Give them defaults: `_brand = '';` and `_battery = 0;` |
| 2 | `SmartPhone(String brand, int battery, String system) {` | The child constructor never calls the parent constructor, so `Phone`'s fields are never set up. | Add `: super(brand, battery)` after the parameter list. |
| 3 | `@override void restart()` in `SmartPhone` | `Phone` has no `restart()` method, so `@override` is invalid — there is nothing to override. | Add a `void restart()` method to `Phone`. |
| 4 | `p.battery = 100;` | There is no setter for `battery`, so you cannot assign to it. | Add a `set battery(int value)` that only accepts 0 to 100. |
| 5 | `print(p.battery());` | `battery` is a getter, not a method, so calling it with `()` is wrong. | Change to `print(p.battery);` |
| Not a bug | `new Phone('Tecno', 50)` | `new` is optional in modern Dart, but writing it is still valid and not an error. | None — keep it as is. |

## Part 5

My prediction:
```
1
5
```

Reasoning:
- Bag `a` starts at 0, `a.add()` makes it 1. `a.items = -5` is rejected by the setter (negative not allowed), so it stays 1. First print: 1.
- BigBag `b` starts at 0. Each `b.add()` calls `super.add()` twice, so one call adds 2. Two calls make it 4. Then `b.items = b.items + 1` makes it 5. Second print: 5.

Real output:
```
1
5
```

Was I right? Yes.

Output verified: prediction matches real output.
