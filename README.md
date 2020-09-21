# Documentation theme for the packages of JuliaDynamics

*(requires at least documenter `v0.24.6`)*

Add the following before the `makedocs` command:

```julia
using DocumenterTools: Themes
# download the themes
for file in ("juliaclimate-lightdefs.scss", "juliaclimate-darkdefs.scss", "juliaclimate-style.scss")
    download("https://raw.githubusercontent.com/JuliaClimate/doctheme/master/$file", joinpath(@__DIR__, file))
end
# create the themes
for w in ("light", "dark")
    header = read(joinpath(@__DIR__, "juliaclimate-style.scss"), String)
    theme = read(joinpath(@__DIR__, "juliaclimate-$(w)defs.scss"), String)
    write(joinpath(@__DIR__, "juliaclimate-$(w).scss"), header*"\n"*theme)
end
# compile the themes
Themes.compile(joinpath(@__DIR__, "juliaclimate-light.scss"), joinpath(@__DIR__, "src/assets/themes/documenter-light.css"))
Themes.compile(joinpath(@__DIR__, "juliaclimate-dark.scss"), joinpath(@__DIR__, "src/assets/themes/documenter-dark.css"))
```

Lastly, because we are using Google fonts, use
```julia
format = Documenter.HTML(
    assets = [
        asset("https://fonts.googleapis.com/css?family=Montserrat|Source+Code+Pro&display=swap", class=:css),
        ],
    ),
```
as argument to `makedocs`.
