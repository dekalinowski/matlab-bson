Matlab BSON
===========

Matlab BSON encoder based on [libbson](https://github.com/mongodb/libbson).

[BSON](http://bsonspec.org/) is a bin­ary-en­coded seri­al­iz­a­tion of
JSON-like doc­u­ments. This package contains API to convert Matlab variables
to and from BSON binary. It is useful for exchanging data with Matlab and
other programs written in different language.

Build
-----

A Windows Msys2 environment is required to build the package. Get necessary
Msys2 packages to build libbson (base-devel, gcc, mingw-w64-x86_64-toolchain).
If you don't have libbson installed in the system, you need the Internet
connection.

Create a Windows environment variable MSYSROOT, set to the root directory of
Msys2, e.g. MSYSROOT is C:\msys64

Add the %MSYSROOT%\usr\bin directory to the Windows environment PATH,
e.g. <current PATH setting>;C:\msys64\usr\bin

Adjust environment PATH priority based on your needs.

Also `mex -setup` if you have never used `mex` command in Matlab. Special
mexopts have been provided in this repository, to select the Msys2 MinGW
toolchain with mex -setup. See directory mexopts/.

Once all the requirements are met, type the following in Matlab to build. This
will automatically download and compile the libbson package to build the Matlab
API.

```Matlab
mex -setup:mexopts\mex_C_msys-w64.xml C
mex -setup:mexopts\mex_C++_msys-w64.xml C++
addpath /path/to/matlab-bson;
bson.make;
```

Check `help bson.make` for the detailed instruction.

Example
-------

```Matlab
parrot = struct( ...
  'name', 'Grenny', ...
  'type', 'African Grey', ...
  'male', true, ...
  'age', 1, ...
  'birthdate', {bson.datetime(now)}, ...
  'likes', {{'green color', 'night', 'toys'}}, ...
  'extra1', [] ...
  );
bson_value = bson.encode(parrot);
assert(bson.validate(bson_value));
parrot = bson.decode(bson_value);
disp(bson.asJSON(bson_value));
```

API
---

    asJSON    Convert BSON to JSON.
    datetime  Datetime type in BSON format.
    decode    Deserialize value from BSON format.
    encode    Serialize value in BSON format.
    fromJSON  Convert JSON to BSON.
    make      Build a driver mex file.
    read      Read bson from file.
    validate  Validates BSON format.
    write     Write variable to a BSON file.

Check `help bson` for detail.
