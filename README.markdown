Browse : [C#](https://github.com/michel-leonard/ciede2000-csharp) · [C++](https://github.com/michel-leonard/ciede2000-cpp) · [C99](https://github.com/michel-leonard/ciede2000-c) · [Dart](https://github.com/michel-leonard/ciede2000-dart) · [Go](https://github.com/michel-leonard/ciede2000-go) · **JavaScript** · [Java](https://github.com/michel-leonard/ciede2000-java) · [Julia](https://github.com/michel-leonard/ciede2000-julia) · [Kotlin](https://github.com/michel-leonard/ciede2000-kotlin) · [Lua](https://github.com/michel-leonard/ciede2000-lua) · [MATLAB](https://github.com/michel-leonard/ciede2000-matlab)

# CIEDE2000 color difference formula in JavaScript

This page presents the CIEDE2000 color difference, implemented in the JavaScript programming language.

![Logo](https://raw.githubusercontent.com/michel-leonard/ciede2000-color-matching/refs/heads/main/docs/assets/images/logo.jpg)

## About

Here you’ll find the first rigorously correct implementation of CIEDE2000 that doesn’t use any conversion between degrees and radians. Set parameter `canonical` to obtain results in line with your existing pipeline.

`canonical`|The algorithm operates...|
|:--:|-|
`false`|in accordance with the CIEDE2000 values currently used by many industry players|
`true`|in accordance with the CIEDE2000 values provided by [this](https://hajim.rochester.edu/ece/sites/gsharma/ciede2000/) academic MATLAB function|

## Our CIEDE2000 offer

These 2 production-ready files, released in 2026, contain the CIEDE2000 algorithm.

Source File|Type|Bits|Purpose|Advantage|
|:--:|:--:|:--:|:--:|:--:|
[ciede2000.js](./ciede2000.js)|`Number`|64|General|Interoperability|
[ciede2000-arbitrary-precision.js](./ciede2000-arbitrary-precision.js)|`Decimal`|Unlimited|Metrology|–|

### Software Versions

- Decimal.js 10.6 (only for arbitrary precision)

### Example Usage

We calculate the CIEDE2000 distance between two colors, first without and then with parametric factors.

```javascript
// Example of two L*a*b* colors
var l1 = 76.8, a1 = 103.9, b1 = 6.6
var l2 = 73.6, a2 = 116.1, b2 = -3.9

var delta_e = ciede2000(l1, a1, b1, l2, a2, b2)
console.log("CIEDE2000 = ", delta_e) // ΔE2000 = 4.575648907164364

// Example of parametric factors used in the textile industry
var kl = 2.0, kc = 1.0, kh = 1.0

// Perform a CIEDE2000 calculation compliant with that of Gaurav Sharma
var canonical = true

delta_e = ciede2000(l1, a1, b1, l2, a2, b2, kl, kc, kh, canonical)
console.log("CIEDE2000 = ", delta_e) // ΔE2000 = 4.1058032084100855
```

These CIEDE2000 calculations in JavaScript are fast, typically allowing millions of color comparisons per second.

### Test Results

LEONARD’s tests are based on well-chosen L\*a\*b\* colors, with various parametric factors `kL`, `kC` and `kH`.

<details>
<summary>Display test results for 12 correct decimal places in 64-bits</summary>

```
CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.83453294874678
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 1187.14 seconds
     Average Delta E : 67.12
   Average Deviation : 6.8e-15
   Maximum Deviation : 3.3e-13
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : 50.0,128.0,-124.0,50.0,33.0,32.0,1.0,1.0,1.0,44.8343428812861
           Precision : 12 decimal digits
           Successes : 100000000
               Error : 0
            Duration : 1208.73 seconds
     Average Delta E : 67.12
   Average Deviation : 7e-15
   Maximum Deviation : 3.3e-13
```

</details>

<details>
<summary>Display test results for 50 correct decimal places in arbitrary precision</summary>

```
CIEDE2000 Verification Summary :
          Compliance : [ ] CANONICAL [X] SIMPLIFIED
  First Checked Line : -0.0,8.0,32.0,0.0,32.00003,-128.0,1.0,1.0,1.0,52.95758888475620024850387...
           Precision : 50 decimal digits
           Successes : 10000000
               Error : 0
            Duration : 16075.37 seconds
     Average Delta E : 67.12
   Average Deviation : 3.4e-53
   Maximum Deviation : 6.6e-52
```

```
CIEDE2000 Verification Summary :
          Compliance : [X] CANONICAL [ ] SIMPLIFIED
  First Checked Line : -0.0,8.0,32.0,0.0,32.00003,-128.0,1.0,1.0,1.0,52.95739626510368628922817...
           Precision : 50 decimal digits
           Successes : 10000000
               Error : 0
            Duration : 15963.18 seconds
     Average Delta E : 67.12
   Average Deviation : 3.1e-53
   Maximum Deviation : 6.6e-52
```

</details>

## Public Domain Licence

You are free to use these files, even for commercial purposes.
