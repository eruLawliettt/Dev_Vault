#DeepCSharp 
[[Deep C Sharp]]

Необработанный строковый литерал начинается и заканчивается как минимум тремя двойными кавычками (`"`) символами:

`var str = """`
        `<element attr="content">`
            `<body>`
            `</body>`
        `</element>`
       ` """;`

`var str = $"""`
        `<element attr="content">`
        `{1 + 2}`
            `<body>`
            `</body>`
        `</element>`
        `""";`