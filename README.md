# xmltodict.jl

Julia module that makes working with XML feel like you are working with JSON (inspired by the Python module `xmltodict`).

## Usage

```julia

xmltest = """
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
  <book category="COOKING" tag="first">
    <title lang="en">Everyday Italian</title>
    <author>Giada De Laurentiis</author>
  </book>
  <book category="CHILDREN">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
  </book>
  <newspaper category="news">
    <title lang="en">Harry Potter</title>
    <author>J K. Rowling</author>
  </newspaper>
</bookstore>
"""

xdict = xmlparse_string(xmltest)
```

```julia
xt1["bookstore"]["book"][1] 
```

Results in:

> OrderedDict{String,Any} with 6 entries:
>  "@category" => "COOKING"
>  "@tag"      => "first"
>  "title"     => ["@lang"=>"en","#text"=>"Everyday Italian"]
>  "author"    => ["#text"=>"Giada De Laurentiis"]
>  "year"      => ["#text"=>"2005"]
>  "price"     => ["#text"=>"30.00"]

## Macro Extensions


```julia
xt1["bookstore"][x2d"book"] 
```

```julia
xt1["bookstore"][x2d"newspaper"] => {"@category" => "news", "title" => { ... }, ... }
xt1["bookstore"][x2d"newspaper+"] => [ {"@category" => "news", "title" => { ... }, ... }, ]
```


```julia
xt1["bookstore"][x2d"magazine"] => key error
xt1["bookstore"][x2d"newspaper*"] => [ ] 
```

