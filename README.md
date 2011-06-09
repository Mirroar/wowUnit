wowUnit is a [unit testing](http://en.wikipedia.org/wiki/Unit_testing "see Wikipedia")
framework intended to be used for AddOn development in World of Warcraft.

Example
=======

Say you have an AddOn called *addAddOn* that simply has a function for adding two
numbers. You could write tests to make sure the function performs as expected
like so:

	addAddOn.tests = {
		["Check addition of numbers"] = {
			["See if results are correct"] = function()
				wowUnit:assertEquals(addAddOn:add(1, 1), 2, "1 and 1 is 2");
				wowUnit:assertEquals(addAddOn:add(-3, 5), 2, "-3 + 5 = 2");
				wowUnit:assertEquals(addAddOn:add(1997, -1995), 2, "1997 + (-1995) = 2");
			end,
			["make sure it behaves as expected for strange input"] = function()
				wowUnit:isNil(addAddOn:add(), "nil when no parameters are given");
				wowUnit:isNil(addAddOn:add(1), "nil when only on parameter is given");
				wowUnit:isNil(addAddOn:add(nil, 1), "nil when only one parameter is given");
				wowUnit:assertEquals(addAddOn:add(-3, 5, 10), 2, "any parameters past the first 2 are ignored");
				wowUnit:isNil(addAddOn:add(1, "1"), "nil when a parameter is not a number");
			end
		}
	}

Once tests are written and loaded, you could run these tests in game by typing
*/test addAddOn*.