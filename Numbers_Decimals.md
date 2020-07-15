# ALL THESE REQUIRE THE WHOLE STRING TO BE A NUMBER
# For numbers embedded in sentences, see discussion below

## NUMBERS AND DECIMALS ONLY ####

* No commas allowed
  * Pass: (1000.0), (001), (.001)
  * Fail: (1,000.0)
  * **_ ^\d*\.?\d+$ _**

* No commas allowed + Can't start with "."
  * Pass: (0.01)
  * Fail: (.01)
  * **_ ^(\d+\.)?\d+$ _**

## CURRENCY ####
* No commas allowed + Can't start with "."
* "$" optional
* Either 0 or 2 decimal digits
  * Pass: ($1000), (1.00), ($0.11)
  * Fail: ($1.0), (1.), ($1.000), ($.11)
  * **_ ^\$?\d+(\.\d{2})?$ _**

## COMMA-GROUPED ####
* Commas required between powers of 1,000 + Can't start with "."
  * Pass: (1,000,000), (0.001)
  * Fail: (1000000), (1,00,00,00), (.001)
  * **_ ^\d{1,3}(,\d{3})*(\.\d+)?$ _**

* Commas required + Cannot be empty
  * Pass: (1,000.100), (.001)
  * Fail: (1000), ()
  * **_ ^(?=.)(\d{1,3}(,\d{3})*)?(\.\d+)?$ _**

* Commas optional as long as they're consistent + Can't start with "."
  * Pass: (1,000,000), (1000000)
  * Fail: (10000,000), (1,00,00)
  * **_ ^(\d+|\d{1,3}(,\d{3})*)(\.\d+)?$ _**

## LEADING AND TRAILING ZEROES ####
* No commas allowed + Can't start with "."


* No leading zeroes in integer part
  * Pass: (1.00), (0.00)
  * Fail: (001)
  * **_ ^([1-9]\d*|0)(\.\d+)?$ _**

* No trailing zeroes in decimal part
  * Pass: (1), (0.1)
  * Fail: (1.00), (0.1000)
  * **_ ^\d+(\.\d*[1-9])?$ _**
