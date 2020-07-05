Installing the default `MySQL` package always gives me an error. (This is extremely not user-friendly and had previously discouraged me from learning Julia.)

```julia
> Pkg.add("MySQL")
> using MySQL
ERROR: LoadError: UndefVarError: Printf not defined
...
# You can find some more meaning error message below complaining about DecPF ...
```

To resolve this, install `DecPF` from github directly. Here's a working example:

```julia
# mysql_demo_1.jl
using Pkg

Pkg.add("DataFrames")
Pkg.add(PackageSpec(url="git://github.com/JuliaMath/DecFP.jl"))
Pkg.add(PackageSpec(url="https://github.com/JuliaComputing/MySQL.jl"))

conn = DBInterface.connect(MySQL.Connection, "localhost", "root", "my_very_strong_password")

res = DBInterface.execute(conn, "SELECT * FROM test.Toy LIMIT 10") |> DataFrame
show(res)
```
