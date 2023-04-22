

![Pipeline](https://github.com/pb33f/libopenapi-validator/workflows/Build/badge.svg)
[![GoReportCard](https://goreportcard.com/badge/github.com/pb33f/libopenapi-validator)](https://goreportcard.com/report/github.com/pb33f/libopenapi-validator)
[![codecov](https://codecov.io/gh/pb33f/libopenapi-validator/branch/main/graph/badge.svg?)](https://codecov.io/gh/pb33f/libopenapi-validator)
[![discord](https://img.shields.io/discord/923258363540815912)](https://discord.gg/x7VACVuEGP)
[![Docs](https://img.shields.io/badge/godoc-reference-5fafd7)](https://pkg.go.dev/github.com/pb33f/libopenapi)


# libopenapi-validator

Full Documentation coming shortly, now ready for early testing.

Example use: 

```go
// 1. Load the OpenAPI 3+ spec into a byte array
petstore, err := os.ReadFile("test_specs/invalid_31.yaml")

if err != nil {
    panic(err)
}

// 2. Create a new OpenAPI document using libopenapi
document, docErrs := libopenapi.NewDocument(petstore)

if docErrs != nil {
    panic(docErrs)
}

// 3. Create a new validator
docValidator, validatorErrs := NewValidator(document)

if validatorErrs != nil {
    panic(validatorErrs)
}

// 4. Validate!
valid, validationErrs := docValidator.ValidateDocument()

if !valid {
    for i, e := range validationErrs {
        // 5. Handle the error
        fmt.Printf("%d: Type: %s, Failure: %s\n", i, e.ValidationType, e.Message)
        fmt.Printf("Fix: %s\n\n", e.HowToFix)
    }
}
// Output: 0: Type: schema, Failure: Document does not pass validation
//Fix: Ensure that the object being submitted, matches the schema correctly
```