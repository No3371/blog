---
layout: post
title: "Learning C#: Bit-Twiddling-Abs"
tags: csharp
published: true
language: en
---

NOTE: C# numbers are stored in 2's complement.

We'll use int (32bit) P = 17 (`0000 0000 0000 0000 0000 0000 0001 0001`) and N = -17 (`1111 1111 1111 1111 1111 1111 1110 1111`) to demonstrate.

### Extract the sign bit

We shift 32 bits right to get the sign bit:

```csharp
int step1N = -17 >> 31; // = -1, 1111 1111 1111 1111 1111 1111 1111 1111
int step1P =  17 >> 31; // = 0,  0000 0000 0000 0000 0000 0000 0000 0000
```

### XOR the original value and the mask

XOR means output 1 if the bits are different.
```csharp
int step2N = -17 ^ step1N;
// The leftmost bit of -17 is 1, the the one of step1N is also 1, they are the same, so the XOR result bit would be 0, which makes the value positive.
// After XOR, step2N is now `0000 0000 0000 0000 0000 0000 0001 0000`, which is 16

int step2P =  17 ^ step1P;
// The leftmost bit of 17 is 0, the the one of step1P is also 0, they are the same, so the XOR result bit would be 0, which is not changed (17 is positive too).
// After XOR, step2P is now `0000 0000 0000 0000 0000 0000 0001 0001`, which is 17
```

###  Subtact the step2 values

We need to adjust the value for N to makes the abs result correct.
```csharp
int absN = step2N - step1N; // = 17, 16 - -1
int absP = step2P - step1P; // = 17, 17 - 0
// As you can see, this step does not modify the result if the original value is positive.
```

### Not Safe: int.MinValue

Let's perform the above technique for `int.MinValue`, -2147483648, which is `1000 0000 0000 0000 0000 0000 0000 0000`.

```csharp
int x = -2147483648 >> 31; // -1, 1111 1111 1111 1111 1111 1111 1111 1111
x = -2147483648 ^ x;
// The leftmost bit of -17 is 1, the the one of step1N is also 1, they are the same, so the XOR result bit would be 0, which makes the value positive.
// After XOR, x is now 0111 1111 1111 1111 1111 1111 1111 1111, which is 2147483647, the `int.MaxValue`
x = x - -1; // it's supposed to be 2147483647+1, but 2147483647 is already `int.MaxValue`, this will results in a overflow, makes it again -2147483648.
```

So if the value is possibliy `int.MinValue`, we have to avoid using this trick.

Also, this does not necessarily makes your program faster because modern compiler is good at optimization, it's often faster then manual optimization.
