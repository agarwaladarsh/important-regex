# ALL THESE REQUIRE THE WHOLE STRING TO BE A NUMBER
# For numbers embedded in sentences, see discussion below

## NUMBERS AND DECIMALS ONLY ####

*No commas allowed
  * Pass: (1000.0), (001), (.001)
  * Fail: (1,000.0)
  * ^\d*\.?\d+$

*No commas allowed + Can't start with "."
  * Pass: (0.01)
  * Fail: (.01)
  * ^(\d+\.)?\d+$

## CURRENCY ####
*No commas allowed + Can't start with "."
*"$" optional
*Either 0 or 2 decimal digits
  * Pass: ($1000), (1.00), ($0.11)
  * Fail: ($1.0), (1.), ($1.000), ($.11)
  * ^\$?\d+(\.\d{2})?$

## COMMA-GROUPED ####
*Commas required between powers of 1,000 + Can't start with "."
  * Pass: (1,000,000), (0.001)
  * Fail: (1000000), (1,00,00,00), (.001)
  * ^\d{1,3}(,\d{3})*(\.\d+)?$

*Commas required + Cannot be empty
  * Pass: (1,000.100), (.001)
  * Fail: (1000), ()
  * ^(?=.)(\d{1,3}(,\d{3})*)?(\.\d+)?$

*Commas optional as long as they're consistent + Can't start with "."
  * Pass: (1,000,000), (1000000)
  * Fail: (10000,000), (1,00,00)
  * ^(\d+|\d{1,3}(,\d{3})*)(\.\d+)?$

## LEADING AND TRAILING ZEROES ####
*No commas allowed + Can't start with "."


*No leading zeroes in integer part
  * Pass: (1.00), (0.00)
  * Fail: (001)
  * ^([1-9]\d*|0)(\.\d+)?$

*No trailing zeroes in decimal part
  * Pass: (1), (0.1)
  * Fail: (1.00), (0.1000)
  * ^\d+(\.\d*[1-9])?$
