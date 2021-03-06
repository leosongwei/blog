Arma3 Note
========================

tags: script; Arma3; Game;

Notes of Arma3.

* Ammunition initial speed:
  - "airFriction" https://community.bistudio.com/wiki/CfgAmmo_Config_Reference

* log: `systemChat "Hello world!";`

* Compile:

```
_string = "a = a + 1";
_code = compile _string;
call _code;
```

* execVM:

```
_handle = player execVM "test.sqf";
waitUntil {scriptDone _handle};
```

* Read file: `_contents = loadFile "myFunction.sqf";`

Op
--

```
+, -, *, /, %==mod, ^(power)
&&==and, ||==or
>, <, >=, <=, !=, ==
```

Variables
---------

**Private** variables starts with underscore: `_myvar = 0;`

In functions, private variables should be marked as private:

* `private "_myprivatevar";_myprivatevar = 0;`
* `private _myvar = 0;`

Or: `private ["_p1", "_p2"]`

**Global** variables are not started with underscore. `Myvar = 0;`

**Public** Variables: the global variables broadcasts over the computers:

`myPubvar = 123; publicVariable "myPubvar";`

While trying to initialize a variable, if the form didn't returns a value, the variable will not be established. Referencing this variable will cause variable not bound error.

Function
--------

```
my_func = {
  params ["_a", "_b"];
  ...
};

[1, 2] call my_func;
```

Array & String
--------------
* copy array: `_a = + _array`

```
_a = [1] + [2]
_count = count _a; // Output: 2
_s = "a" + " b" // "a b"
```

* Invalid: `[1,2,] // Error: Unexpected ","`

```
_myMultiArray = [["Array1Elem1","Array1Elem2"],["Array2Elem1","Array2Elem2"]];
_selectFirst = _myMultiArray select 0; // Output: ["Array1Elem1","Array1Elem2"] (Array)
```

* append: concatenate array without creating new
	- `_arrayThree = _arrayOne append _arrayTwo; // Output: ["One","Two"];`

```
_a = [[1,1,1],[1,1,1]];
_b = +_a;
(_b select 0) set [0, 4]; // Now _b is an array [[4,1,1],[1,1,1]], while _a is still [[1,1,1],[1,1,1]]
```

```
_array = [];
_element = (_array select 0) // out of bounds
```

Control flow
------------

Return Values: Control structures always return the last expression evaluated within the structure.

* IF:

```
// What about "else if"
if (CONDITION) then {
	STATEMENT1;
} else { // optional
	STATEMENT2;
};
```

* IF returns:

```
// IF has value
_living = if (alive player) then {true} else {false};
```

```
switch (VARIABLE) do {
    case VALUE1: {
        STATEMENT;
    };
    case VALUE2: {
        STATEMENT;
        ...
    };
	default { // optional
        STATEMENT;
        ...
    };
};
```

* while

```
while {CONDITION} do {
    STATEMENT;
};
```

* for

```
// Is the {} in [] real statements?
for [{_i=0}, {_i<10}, {_i=_i+1}] do {
    player globalChat format["%1",_i];
};

for "_i" from 0 to 9 step 2 do {
    player globalChat format["%1",_i];
};

{ _x setDamage 1; } forEach _array;
```

Disable AI:

```
{_x disableAI "ALL";} forEach units group t1;
```

Create Unit:

```group _unit createUnit ["O_Soldier_VR_F", position _unit, [], 0, "NONE"]; ```

Install Workshop Mod on Dedicated Server
----------------------------------------

* `./steamcmd.sh +login username passwd +workshop_download_item 107410 853743366`
	- `107410`: Arma3 appid (use the client one, not the server one)
	- `853743366`: Mod id ( https://steamcommunity.com/sharedfiles/filedetails/?id=853743366 )
